---
title: Uppgradera till AEM 6.5 Communities
description: Hur man uppgraderar från en tidigare version till AEM 6.5 Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Uppgradera till AEM 6.5 Communities {#upgrading-to-aem-communities}

Beroende på de olika platsernas topologi och funktioner kan följande åtgärder vara nödvändiga när du uppgraderar till AEM Communities 6.5 eller installerar det senaste funktionspaketet.

Det här avsnittet är specifikt för Communities och kompletterar informationen i [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md) (plattform).

## Uppgradera från AEM 6.1 eller senare {#upgrading-from-aem-or-later}

### Indexera om Solr {#reindex-solr}

När du installerar ett nytt funktionspaket för Communities på en distribution som konfigurerats med MSRP måste du:

1. Installera det [senaste funktionspaketet](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installera de [senaste Solr-konfigurationsfilerna](/help/communities/msrp.md#upgrading).
1. Indexera om MSRP
se avsnittet [MSRP Reindex Tool](/help/communities/msrp.md#msrp-reindex-tool).

## Uppgradera från AEM 6.0 {#upgrading-from-aem}

Om befintlig UGC måste behållas beror det på om distributionen lagrade UGC [lokalt](#on-premise-storage) eller i molnet [Adobe](#adobe-cloud-storage).

### Adobe Cloud-lagring {#adobe-cloud-storage}

Om den uppgraderade webbplatsen har konfigurerats för att använda molnlagring i Adobe kan den visas (felaktigt) som om all UGC har förlorats eftersom SRP-metoderna inte kan hitta den befintliga UGC:n på den gamla platsen.

Det går alltså att instruera ASRP att använda `AEM 6.0 compatability-mode` för att få åtkomst till UGC.

För alla AEM 6.3-instanser:

* Logga in med administratörsbehörighet.
* Konfigurera [ASRP](/help/communities/asrp.md).
* Följ de här stegen för att göra befintlig UGC synlig:

   * Bläddra till webbkonsolen:

      * Till exempel [https://&lt;värd>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Leta reda på konfigurationen för **AEM Communities Utilities**.
      * Markera för att expandera konfigurationspanelen:

         * *Avmarkera* `Cloud Storage`

         * Välj **Spara**

     ![verktyg](assets/utilities.png)

### Lokal lagring {#on-premise-storage}

Om den uppgraderade webbplatsen inte använde molnlagring måste eventuell befintlig UGC konverteras så att den överensstämmer med den nya struktur som introducerades i AEM 6.1 Communities till stöd för den gemensamma butiken.

Ett migreringsverktyg med öppen källkod är tillgängligt på GitHub:
[AEM Communities UGC-migreringsverktyg](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java-API:er {#java-apis}

Vid uppgradering från AEM 6.0 sociala communityn till AEM 6.3 Communities har många API:er omorganiserats till olika paket. De flesta bör vara lätta att lösa när man använder en integrerad utvecklingsmiljö för anpassning av communityfunktioner.

Mer information om det borttagna paketet SocialUtils finns på [SocialUtils Refactoring](/help/communities/socialutils.md).

Se även [Använda Maven för Communities](/help/communities/maven.md).

### Inga JSP-komponentmallar {#no-jsp-component-templates}

I det [sociala komponentramverket](/help/communities/scf.md) (SCF) används mallspråket [HandlebarsJS](https://handlebarsjs.com/) (HBS) i stället för Java Server Pages (JSP) som användes före AEM 6.0.

I AEM 6.0 låg JSP-komponenterna kvar tillsammans med de nya HBS-ramverkskomponenterna på samma plats, och HBS-komponenterna fanns vanligtvis i undermappar med namnet&quot;hbs&quot;.

Från och med AEM 6.1 togs JSP-komponenterna bort helt. För Communities rekommenderas att all användning av JSP-komponenter ersätts med SCF-komponenter.

## AEM Communities UGC-migreringsverktyg {#aem-communities-ugc-migration-tool}

[AEM Communities UGC-migreringsverktyg](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) är ett migreringsverktyg med öppen källkod, som finns på GitHub, som kan anpassas för att exportera UGC från tidigare versioner AEM sociala communities och importera till AEM Communities 6.1 eller senare.

Förutom att flytta UGC från tidigare versioner går det också att använda verktyget för att flytta UGC från en [SRP](/help/communities/working-with-srp.md) till en annan, till exempel från MSRP till DSRP.

## Uppgradera från AEM 5.6.1 eller tidigare {#upgrading-from-aem-or-earlier}

Det finns tre generationer av communitykomponenter:

**Gen 1**: CQ 5.4 till AEM 5.6.0 är de här **collab** -komponenterna som lagrade UGC i den lokala databasen med replikering som ett sätt att synkronisera UGC mellan plattformar. Andra skillnader är implementeringen med Java Server Pages (JSP) och bloggfunktionen som bara består av redigering i författarmiljön.

**Gen 2**: Från AEM 5.6.1 till AEM 6.1 är detta en blandning av komponenterna **collab** och **social**. AEM 6.0 introducerade det nya ramverket [för sociala komponenter](/help/communities/scf.md) (SCF) och AEM 6.2 introducerade ett [vanligt UGC-arkiv](/help/communities/working-with-srp.md) där UGC används med en [lagringsresursleverantör](/help/communities/srp.md) (SRP).

**Gen 3**: Från och med AEM 6.2 finns det bara **sociala** komponenter som implementerats i SCF som HBS-komponenter som kräver att du väljer SRP för UGC.
