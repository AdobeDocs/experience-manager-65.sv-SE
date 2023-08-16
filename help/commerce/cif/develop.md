---
title: Utveckla AEM
description: Lär dig hur du skapar ett e-handelsaktiverat AEM med AEM projekttyp. Lär dig hur du bygger och distribuerar projektet till en lokal utvecklingsmiljö.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Utveckla AEM {#develop}

Utveckla AEM handelsprojekt som bygger på Commerce Integration Framework (CIF) för AEM följer samma regler och bästa praxis som andra AEM. Granska dessa först:

- [Användarhandbok om AEM 6.5-utveckling](/help/sites-developing/home.md)
- [AEM Core Concepts](/help/sites-developing/the-basics.md)
- [AEM - riktlinjer och bästa praxis](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Skapa AEM projekt med Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Lokal utveckling för AEM {#local}

En lokal utvecklingsmiljö rekommenderas för arbete med CIF-projekt.

>[!NOTE]
>
>Följande instruktioner hjälper dig att konfigurera en lokal AEM utvecklingsmiljö för AEM Commerce med CIF med fokus för AEM 6.5). Om du använder AEM as a Cloud Service kan du läsa [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html) dokumentation.

AEM Commerce Add-On för AEM 6.5 alias. CIF-tillägget finns även för lokal utveckling och tillhandahålls som ett AEM. Den kan laddas ned från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) som ett funktionspaket.

### Nödvändig programvara

Följande bör installeras lokalt:

- Lokal AEM 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 eller senare
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 eller senare)
- [Nod-LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Åtkomst till CIF-tillägget

CIF-tillägget kan hämtas från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html), söker du efter AEM Commerce add-on.

>[!TIP]
>
>Se till att du alltid använder den senaste CIF-tilläggsversionen.

### Lokal installation

För lokal CIF-projektutveckling med AEM och CIF-tillägget:

1. Hämta AEM 6.5 och installera AEM 6.5 Service Pack. AEM 6.5 Service Pack 7 krävs, men Adobe rekommenderar att du installerar det senaste tillgängliga Service Pack-paketet.

1. Packa upp AEM .jar för att skapa `crx-quickstart` mapp, kör:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Skapa en `crx-quickstart/install` mapp

1. Kopiera CIF-tillägget för alla paket som hämtats från portalen för distribution av programvara till `crx-quickstart/install` mapp.

>[!TIP]
>
>Ett alternativ är att CIF-tilläggspaketet också kan installeras via Package Manager.

1. Starta AEM snabbstart

Verifiera konfigurationen via OSGI-konsolen: `http://localhost:4502/system/console/osgi-installer`. Listan bör innehålla CIF-tilläggsrelaterade paket, innehållspaket och OSGI-konfigurationer. Se till att alla paket har startats.

## Projektinställningar {#project}

Det finns två sätt att starta AEM Commerce-projekt med CIF.

### Använd AEM projekttyp

The [AEM Project Archettype](https://github.com/adobe/aem-project-archetype) är huvudverktyget för att starta ett förkonfigurerat projekt för att komma igång med CIF. CIF Core Components och alla nödvändiga konfigurationer kan inkluderas i ett genererat projekt med ett extra alternativ.

>[!TIP]
>
>Använd [AEM Project Archetype 25 eller senare](https://github.com/adobe/aem-project-archetype/releases) för att generera projektet.

Se AEM Project Archetype [användningsinstruktioner](https://github.com/adobe/aem-project-archetype#usage) om hur du skapar ett AEM projekt. Om du vill inkludera CIF i projektet använder du `includeCommerce` alternativ.

Till exempel:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF Core Components kan användas i alla projekt, antingen med de medföljande `all` paket eller individ som använder CIF-innehållspaketet och tillhörande OSGI-paket. Om du vill lägga till CIF-kärnkomponenter manuellt i ett projekt använder du följande beroenden:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Använd AEM Venia Reference Store

Ett annat alternativ för att starta ett CIF-projekt är att klona och använda [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store är ett exempel på en butiksapplikation som demonstrerar användningen av CIF Core Components för AEM. Det är avsett som en uppsättning med metodtips och en potentiell utgångspunkt för att utveckla din egen funktionalitet.

Kom igång med Venia Reference Store genom att klona [Git-databas](https://github.com/adobe/aem-cif-guides-venia) och börja anpassa projektet efter dina behov.

>[!NOTE]
>
>Projektet Venia Reference Store innehåller två byggprofiler för AEM as a Cloud Service och AEM 6.5. Kontrollera [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) för att se hur de används. För AEM 6.5 använder du `classic` profil.

### Anslut AEM till Commerce System

För att ansluta ditt projekt till e-handelssystemet måste AEM konfigureras med GraphQL slutpunkt i e-handelssystemet.

Båda, ett projekt som genereras av [AEM Project Archettype](https://github.com/adobe/aem-project-archetype) eller [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia), innehåller redan [standardkonfiguration](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) som måste justeras.

Ersätt värdet för `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` med GraphQL slutpunkt i e-handelssystemet som används av projektet.

AEM Commerce Add-On och CIF Core Components ansluter till GraphQL-slutpunkten via AEM och direkt via webbläsaren. CIF-kärnkomponenter på klientsidan och CIF-tilläggsverktyg som standard ansluter till `/api/graphql`. Vid behov kan detta justeras via CIF-Cloud Servicens konfiguration (se nedan).

CIF-tillägget tillhandahåller en GraphQL-proxyserver på `/api/graphql`. Om du inte tänker använda en lokal AEM Dispatcher rekommenderar vi att du även konfigurerar GraphQL proxyserver.

Navigera till http://localhost:4502/system/console/configMgr och skapa en OSGI-konfiguration för `Adobe CIF GraphQL Proxy Configuration` service. Använd samma GraphQL-slutpunkt i e-handelssystemet som för GraphQL-klienten ovan.

## Ytterligare resurser

- [AEM Project Archettype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
