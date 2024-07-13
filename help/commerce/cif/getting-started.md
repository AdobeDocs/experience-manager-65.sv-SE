---
title: Komma igång med AEM innehåll och Commerce
description: Lär dig hur du distribuerar ett AEM och Commerce-projekt.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Komma igång med AEM innehåll och Commerce {#start}

För att komma igång med AEM och Commerce måste du installera AEM Content och Commerce Add-On för AEM 6.5.

## Lägsta programvarukrav

[AEM 6.5 Service Pack ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 eller senare krävs.

## Onboarding {#onboarding}

Introduktionen av AEM och Commerce är en tvåstegsprocess:

1. Installera AEM och Commerce Add-on för AEM 6.5

2. Koppla AEM till e-handelslösningen

### Installera AEM och Commerce Add-on för AEM 6.5 {#install-add-on}

Hämta och installera AEM Commerce Add-On för AEM 6.5 från portalen [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

Starta och installera AEM 6.5 Service Pack. Vi rekommenderar att du installerar det senaste tillgängliga Service Pack-paketet.

>[!NOTE]
>
>Detta görs av CSE för AEM kunder som har hanterade tjänster.

### Anslut AEM till ditt Commerce-system {#connect}

AEM kan anslutas till alla handelssystem som har en tillgänglig GraphQL-slutpunkt för AEM. Dessa slutpunkter är vanligtvis offentligt tillgängliga eller kan anslutas via privata VPN-anslutningar eller lokala anslutningar beroende på de enskilda projektinställningarna.

Autentiseringshuvudet kan också anges om du vill använda ytterligare CIF funktioner som kräver autentisering.

Projekt som har genererats av [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) och [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) som redan ingår i [standardkonfigurationen](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) måste justeras.

Ersätt värdet för `url` i `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` med slutpunkten för GraphQL i e-handelssystemet. Denna konfiguration kan göras via OSGI-konsolen eller genom att distribuera OSGI-konfigurationen via projektet. Olika konfigurationer för staging- och produktionssystem stöds med olika AEM körningslägen.

Komponenterna AEM Content och Commerce Add-On och CIF Core använder både anslutningar på serversidan och på klientsidan. Huvudkomponenter CIF klientsidan och redigeringsverktygen för CIF tillägg ansluter som standard till `/api/graphql`. Detta kan vid behov justeras via CIF Cloud Service-konfigurationen (se nedan).

CIF Add-On tillhandahåller en GraphQL-proxyserver på `/api/graphql` som kan användas för [lokal utveckling](develop.md). För produktionsdistributioner rekommenderar vi starkt att du skapar en omvänd proxy till e-handelsplatsen för GraphQL via AEM Dispatcher eller andra nätverkslager (som CDN).

## Konfigurera butiker och kataloger {#catalog}

Tillägget och [CIF Core Components](https://github.com/adobe/aem-core-cif-components) kan användas på flera AEM webbplatsstrukturer som är anslutna till olika e-handelsbutiker (eller butiksvyer osv.). Som standard distribueras CIF Add-On med en standardkonfiguration som ansluter till Adobe Commerce standardbutik och -katalog.

Den här konfigurationen kan justeras för projektet via konfigurationen för CIF Cloud Service enligt följande:

1. AEM går till Verktyg > Cloud Service > CIF Konfiguration

2. Välj den e-postkonfiguration som du vill ändra

3. Öppna konfigurationsegenskaperna via åtgärdsfältet

![Konfiguration CIF Cloud Service](/help/commerce/cif/assets/cif-cloud-service-config.png)

Följande egenskaper kan konfigureras:

- GraphQL Client - Välj den konfigurerade GraphQL-klienten för e-handelskommunikation. Detta bör normalt vara kvar som standard.
- Butiksvy - butiksvyns identifierare. Om den är tom används standardbutiksvyn.
- GraphQL Proxy Path - den URL-sökväg som GraphQL Proxy AEM använder för proxybegäranden till GraphQL-slutpunkt för e-handel.

  >[!NOTE]
  >
  >I de flesta inställningar får standardvärdet `/api/graphql` inte ändras. Endast avancerade inställningar som inte använder den angivna GraphQL-proxyn bör ändra den här inställningen.

- Aktivera stöd för katalog-UID - aktivera stöd för UID i stället för ID i e-handelsserverdelens GraphQL-anrop.

  >[!NOTE]
  >
  >Stöd för UID introducerades i Adobe Commerce 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.

- Katalogrotkategoriidentifierare - identifieraren (UID eller ID) för arkivkatalogroten

  >[!CAUTION]
  >
  >Från och med CIF Core Components version 2.0.0 har stödet för `id` tagits bort och ersatts med `uid`. Om ditt projekt använder CIF Core Components version 2.0.0 måste du aktivera stöd för katalog-UID och använda ett giltigt kategori-UID som&quot;Katalogens rotkategoriidentifierare&quot;.

Konfigurationen som visas ovan är för referens. Projekten ska ha egna konfigurationer.

Mer komplexa inställningar som använder flera AEM webbplatsstrukturer i kombination med olika e-handelskataloger finns i självstudiekursen [Commerce Multi-Store Setup](configuring/multi-store-setup.md).

## Ytterligare resurser {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia)
- [Installation av Commerce Multi-Store](configuring/multi-store-setup.md)
