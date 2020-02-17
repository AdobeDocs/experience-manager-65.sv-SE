---
title: Implementera en anpassad predikatutvärderare för Query Builder
seo-title: Implementera en anpassad predikatutvärderare för Query Builder
description: Med Query Builder kan du enkelt hämta frågor till innehållsdatabasen
seo-description: Med Query Builder kan du enkelt hämta frågor till innehållsdatabasen
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Implementera en anpassad predikatutvärderare för Query Builder{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

I det här avsnittet beskrivs hur du utökar [Query Builder](/help/sites-developing/querybuilder-api.md) genom att implementera en anpassad predikatutvärderare.

## Översikt {#overview}

Med [Query Builder](/help/sites-developing/querybuilder-api.md) kan du enkelt hämta frågor till innehållsdatabasen. CQ levereras med en uppsättning prediktiva utvärderare som hjälper dig att hantera dina data.

Men du kanske vill förenkla dina frågor genom att implementera en anpassad predikatutvärderare som döljer komplexiteten och ger ett bättre semantiskt resultat.

Ett anpassat predikat kan även utföra andra saker som inte är direkt möjliga med XPath, till exempel:

* söka efter vissa data från vissa tjänster
* anpassad filtrering baserad på beräkning

>[!NOTE]
>
>Prestandafrågor måste beaktas när du implementerar ett anpassat predikat.

>[!NOTE]
>
>Exempel på frågor finns i avsnittet [Frågebyggaren](/help/sites-developing/querybuilder-api.md) .

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-search-custom-prediate-valuator-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### Förutse utvärderaren i detalj {#predicate-evaluator-in-detail}

En predikatutvärderare hanterar utvärderingen av vissa predikat, vilket är definieringsbegränsningarna för en fråga.

Det mappar en sökbegränsning på högre nivå (t.ex. &quot;width > 200&quot;) till en specifik JCR-fråga som passar den faktiska innehållsmodellen (t.ex. metadata/@width > 200). Det kan också filtrera noder manuellt och kontrollera deras begränsningar.

>[!NOTE]
>
>Mer information om paketet `PredicateEvaluator` och `com.day.cq.search` paketet finns i [Java-dokumentationen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementera en anpassad predikatutvärderare för replikeringsmetadata {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

I det här avsnittet beskrivs hur du skapar en anpassad predikatutvärderare som kan användas för data baserat på replikeringens metadata:

* `cq:lastReplicated` som lagrar datumet för den senaste replikeringsåtgärden

* `cq:lastReplicatedBy` som lagrar ID för den användare som utlöste den senaste replikeringsåtgärden

* `cq:lastReplicationAction` som lagrar den senaste replikeringsåtgärden (t.ex. aktivering, inaktivering)

#### Frågar efter replikeringsmetadata med standardpredikatutvärderare {#querying-replication-metadata-with-default-predicate-evaluators}

Följande fråga hämtar listan med noder i `/content` grenen som har aktiverats `admin` sedan årets början.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Frågan är giltig men svårläst och visar inte relationen mellan de tre replikeringsegenskaperna. Implementering av en anpassad predikatutvärderare minskar komplexiteten och förbättrar semantiken i frågan.

#### Mål {#objectives}

Målet för sökningen `ReplicationPredicateEvaluator` är att ge stöd för ovanstående fråga med följande syntax.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Genom att gruppera metadata för replikering med en anpassad predikatutvärderare kan du skapa en meningsfull fråga.

#### Uppdaterar Maven Dependencies {#updating-maven-dependencies}

>[!NOTE]
>
>Hur man skapar nya AEM-projekt med Maven beskrivs i [Så här skapar man AEM-projekt med Apache Maven](/help/sites-developing/ht-projects-maven.md).

Först måste du uppdatera Maven-beroendena för ditt projekt. Den `PredicateEvaluator` är en del av `cq-search` artefakten, så den måste läggas till i din Maven-pom-fil.

>[!NOTE]
>
>Beroendets omfång `cq-search` anges till `provided` eftersom `cq-search` kommer att anges av `OSGi` behållaren.

pom.xml

Följande utdrag visar skillnaderna i [enhetligt format](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-predikate-valuator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### Skriver ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

Projektet innehåller `cq-search` den `AbstractPredicateEvaluator` abstrakta klassen. Detta kan utvidgas med några få steg för att implementera en egen predikatutvärderare `(PredicateEvaluator`).

>[!NOTE]
>
>I proceduren nedan beskrivs hur du skapar ett `Xpath` uttryck för att filtrera data. Ett annat alternativ är att implementera den `includes` metod som markerar data på radbasis. Mer information finns i [Java-dokumentationen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) .

1. Skapa en ny Java-klass som utökar `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Anteckna din klass med en `@Component` liknande följande

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   Följande utdrag visar skillnaderna i [enhetligt format](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-prediate-valuator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>Värdet `factory`måste vara en unik sträng som börjar med `com.day.cq.search.eval.PredicateEvaluator/`och slutar med namnet på din anpassade sträng `PredicateEvaluator`.

>[!NOTE]
>
>Namnet på predikatet `PredicateEvaluator` är namnet som används när frågor skapas.

1. Åsidosätt:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   I åsidosättningsmetoden skapar du ett `Xpath` uttryck baserat på det `Predicate` angivna argumentet.

### Exempel på en anpassad predikatutvärderare för replikeringsmetadata {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

Den fullständiga implementeringen av denna `PredicateEvaluator` kan likna följande klass.

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-prediate-valuator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
