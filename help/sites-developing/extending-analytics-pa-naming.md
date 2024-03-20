---
title: Implementera sidnamngivning på serversidan för analys
description: Adobe Analytics använder egenskapen s.pageName för att unikt identifiera sidor och för att associera data som samlas in för sidorna
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Implementera sidnamngivning på serversidan för analys{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics använder `s.pageName` för att unikt identifiera sidor och för att koppla data som samlas in för sidorna. Vanligtvis utför du följande uppgifter i AEM för att tilldela ett värde till den här egenskapen som AEM skickar till Analytics:

* Använd molntjänstramverket för Analytics för att mappa en CQ-variabel till Analytics `s.pageName` -egenskap. (Se [Mappa komponentdata med Adobe Analytics-egenskaper](/help/sites-administering/adobeanalytics-mapping.md).)

* Utforma sidkomponenten så att den innehåller CQ-variabeln som du mappar till `s.pageName` -egenskap. (Se [Implementera Adobe Analytics Tracking för anpassade komponenter](/help/sites-developing/extending-analytics-components.md).)

För att kunna visa analysrapportdata i Sites-konsolen och i Content Insight måste AEM ha värdet för `s.pageName` för varje sida. Java-API:t för AEM Analytics definierar `AnalyticsPageNameProvider` det gränssnitt som du implementerar för att tillhandahålla Sites-konsolen och Content Insights med värdet i `s.pageName` -egenskap. Dina `AnaltyicsPageNameProvider` -tjänsten löser egenskapen pageName på servern för rapportering, eftersom den kan ställas in dynamiskt med JavaScript på klienten för spårning.

## Sidnamnsprovidertjänsten för standardanalys {#the-default-analytics-page-name-provider-service}

The `DefaultPageNameProvider` är standardtjänsten som avgör värdet på `s.pageName` -egenskap som används för att hämta Analytics-data för en sida. Tjänsten fungerar tillsammans med AEM på grundsidan ( `/libs/foundation/components/page`). Den här sidkomponenten definierar följande CQ-variabler som ska mappas till `s.pageName` egenskap:

* `pagedata.path`: Värdet ställs in på sidans sökväg.
* `pagedata.title`: Värdet ställs in på sidrubriken.
* `pagedata.navTitle`: Värdet ställs in på sidnavigeringsrubriken.

The `DefaultPageNameProvider` avgör vilken av dessa CQ-variabler som mappas till `s.pageName` i molntjänstramverket för Analytics. Tjänsten avgör sedan vilken sidegenskap som ska användas för att hämta analysrapportdata:

* `pagedata.path`: Tjänsten använder `page.getPath()`

* `pagedata.title`: Tjänsten använder `page.getTitle()`

* `pagedata.navTitle`: Tjänsten använder `page.getNavigationTitle()`

The `page` objektet är [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java-objekt för sidan.

Om du inte kopplar en CQ-variabel till `s.pageName` i ramverket, värdet för `s.pageName` genereras från sidsökvägen. Till exempel sidan med banan `/content/geometrixx/en` använder värdet `content:geometrixx:en` for `s.pageName`.

>[!NOTE]
>
>Tjänsten DefaultPageNameProvider använder en rankning på 100.

## Bevara kontinuitet i analysrapporter {#maintaining-continuity-in-analytics-reporting}

För att upprätthålla en komplett historik med analysdata för en sida måste värdet för egenskapen s.pageName som används för en sida aldrig ändras. Det är dock enkelt att ändra de analysegenskaper som definieras av bassidans komponent. Om du till exempel flyttar en sida ändras värdet för `pagedata.path` och bryter kontinuiteten i rapporthistoriken:

* Data som samlades in för föregående sökväg är inte längre kopplade till sidan.
* Om en annan sida använder sökvägen som en annan sida använde, ärver den andra sidan informationen för den sökvägen.

För att säkerställa kontinuiteten i rapporteringen bör värdet av `s.pageName` ska ha följande egenskaper:

* Unik.
* Stabil.
* Kan läsas av människor.

En anpassad sidkomponent kan till exempel innehålla en sidegenskap som författare använder för att ange ett unikt ID för sidan som används som värde för `s.pageProperties` egenskap:

* Sidan innehåller en analysvariabel som är inställd på värdet för det unika ID som lagras i sidegenskapen.
* Analysvariabeln mappas till `s.pageProperties` i Analytics-ramverket.
* Din implementering av gränssnittet AnalyticsPageNameProvider hämtar värdet på sidegenskapen som ska användas för att fråga efter sidanalysdata.

>[!NOTE]
>
>Be er analyskonsult om hjälp med att utveckla en effektiv strategi för er `s.pageName` värde.

### Implementera en tjänst för leverantör av sidnamn för analyser {#implementing-an-analytics-page-name-provider-service}

Implementera `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` som en OSGi-tjänst för att anpassa logiken som hämtar `s.pageName` egenskapsvärde. Webbplatssidans analys och Content Insight använder tjänsten för att hämta rapportdata från Analytics.

Gränssnittet AnalyticsPageNameProvider definierar två metoder som du måste implementera:

* `getPageName`: Returnerar en `String` värdet som representerar värdet som ska användas som `s.pageName` -egenskap.

* `getResource`: Returnerar en `org.apache.sling.api.resource.Resource` objekt som representerar sidan som är associerad med `s.pageName` -egenskap.

Båda metoderna har en `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` -objekt som en parameter. The `AnalyticsPageNameContext` klassen ger information om kontexten för analysanropen:

* Sidresursens grundsökväg.
* The `Framework` -objekt för molntjänstkonfigurationen för Analytics.
* The `Resource` objekt för sidan.
* The `ResourceResolver` objekt för sidan.

Klassen innehåller också en set-metod för sidnamnet.

### Exempel på implementering av AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

Följande exempel `AnalyticsPageNameProvider` implementeringen stöder en anpassad sidkomponent:

* Komponenten utökar bassidans komponent.
* Dialogrutan innehåller ett fält som författare använder för att ange värdet för `s.pageName` -egenskap.
* Egenskapsvärdet lagras i egenskapen pageName för `jcr:content`noden för sidinstanser.
* Analysegenskapen som lagrar `s.pageName` egenskapen anropas `pagedata.pagename`. Den här egenskapen är mappad till `s.pageName` i Analytics-ramverket.

Följande implementering av `getPageName` metoden returnerar värdet för nodegenskapen pageName om ramverksmappningen är korrekt konfigurerad:

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

Följande implementering av metoden getResource returnerar resursobjektet för sidan:

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

Följande kod representerar hela klassen, inklusive SCR-anteckningar som konfigurerar tjänsten. Tjänstrankningen är 200 vilket åsidosätter standardtjänsten.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
