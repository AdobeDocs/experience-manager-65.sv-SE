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

Detta avsnitt är specifikt för Communities och kompletterar informationen i [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md) (plattform).

## Uppgradera från AEM 6.1 eller senare {#upgrading-from-aem-or-later}

### Indexera om Solr {#reindex-solr}

När du installerar ett nytt funktionspaket för Communities på en distribution som konfigurerats med MSRP måste du:

1. Installera [senaste funktionspaketet](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installera [senaste Solr-konfigurationsfiler](/help/communities/msrp.md#upgrading).
1. Indexera om avsnittet MSRP [MSRP Reindex Tool](/help/communities/msrp.md#msrp-reindex-tool).

## Uppgradera från AEM 6.0 {#upgrading-from-aem}

Om befintlig UGC måste behållas beror metoden för att göra det på om den lagrade UGC-distributionen är lagrad [lokal](#on-premise-storage) eller i [Adobe cloud](#adobe-cloud-storage).

### Adobe Cloud-lagring {#adobe-cloud-storage}

Om den uppgraderade webbplatsen har konfigurerats för att använda molnlagring i Adobe kan den visas (felaktigt) som om all UGC har förlorats eftersom SRP-metoderna inte kan hitta den befintliga UGC:n på den gamla platsen.

Därför finns det möjlighet att instruera ASRP att använda `AEM 6.0 compatability-mode` för att få tillgång till UGC.

För alla AEM 6.3-instanser:

* Logga in med administratörsbehörighet.
* Konfigurera [ASRP](/help/communities/asrp.md).
* Följ de här stegen för att göra befintlig UGC synlig:

   * Bläddra till webbkonsolen:

      * Till exempel: [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Sök **AEM Communities Utilities** konfiguration.
      * Markera för att expandera konfigurationspanelen:

         * *Avmarkera* `Cloud Storage`

         * Välj **Spara**

     ![utilities](assets/utilities.png)

### Lokal lagring {#on-premise-storage}

Om den uppgraderade webbplatsen inte använde molnlagring måste eventuell befintlig UGC konverteras så att den överensstämmer med den nya struktur som introducerades i AEM 6.1 Communities till stöd för den gemensamma butiken.

Ett migreringsverktyg med öppen källkod är tillgängligt på GitHub:
[AEM Communities UGC-migreringsverktyg](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java-API:er {#java-apis}

Vid uppgradering från AEM 6.0 sociala communityn till AEM 6.3 Communities har många API:er omorganiserats till olika paket. De flesta bör vara lätta att lösa när man använder en integrerad utvecklingsmiljö för anpassning av communityfunktioner.

Mer information om paketet SocialUtils finns på [Omfaktorisering för SocialUtils](/help/communities/socialutils.md).

Se även [Använda Maven for Communities](/help/communities/maven.md).

### Inga JSP-komponentmallar {#no-jsp-component-templates}

The [ramverk för sociala komponenter](/help/communities/scf.md) (SCF) använder [HandtagBarJS](https://handlebarsjs.com/) (HBS) mallspråk i stället för Java Server Pages (JSP) som användes före AEM 6.0.

I AEM 6.0 låg JSP-komponenterna kvar tillsammans med de nya HBS-ramverkskomponenterna på samma plats, och HBS-komponenterna fanns vanligtvis i undermappar med namnet&quot;hbs&quot;.

Från och med AEM 6.1 togs JSP-komponenterna bort helt. För Communities rekommenderas att all användning av JSP-komponenter ersätts med SCF-komponenter.

## AEM Communities UGC-migreringsverktyg {#aem-communities-ugc-migration-tool}

The [AEM Communities UGC-migreringsverktyg](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) är ett migreringsverktyg med öppen källkod, som finns på GitHub, som kan anpassas för att exportera UGC från tidigare versioner av AEM sociala communities och importera till AEM Communities 6.1 eller senare.

Förutom att flytta användargenererat innehåll från tidigare versioner går det även att använda verktyget för att flytta användargenererat innehåll från en [SRP](/help/communities/working-with-srp.md) till en annan, till exempel från MSRP till DSRP.

## Uppgradera från AEM 5.6.1 eller tidigare {#upgrading-from-aem-or-earlier}

Det finns tre generationer av communitykomponenter:

**Gen 1**: CQ 5.4 till AEM 5.6.0 är de **kollab** -komponenter som lagrade UGC i den lokala databasen med replikering som ett sätt att synkronisera UGC över olika plattformar. Andra skillnader är implementeringen med Java Server Pages (JSP) och bloggfunktionen som bara består av redigering i författarmiljön.

**Gen 2**: Från AEM 5.6.1 till och med AEM 6.1 är detta en blandning av **kollab** och **social** -komponenter. AEM 6.0 introducerade [ramverk för sociala komponenter](/help/communities/scf.md) (SCF) och AEM 6.2 införde ett [gemensam UGC-butik](/help/communities/working-with-srp.md) där UGC används med en [lagringsresursprovider](/help/communities/srp.md) (SRP).

**Gen 3**: Från AEM 6.2 och framåt finns det bara **social** -komponenter, implementerade i SCF som HBS-komponenter (Handlebars) som kräver val av SRP för UGC.
