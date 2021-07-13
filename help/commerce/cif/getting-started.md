---
title: Komma igång med AEM innehåll och handel
description: Lär dig hur du distribuerar ett AEM Content and Commerce-projekt.
topics: Commerce
feature: Commerce Integration Framework
source-git-commit: 1b200ea21709cd9234c92da8a8ef6145d2c2f635
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Komma igång med AEM innehåll och handel {#start}

För att komma igång med AEM innehåll och handel måste du installera AEM Content and Commerce Add-On för AEM 6.5.

## Lägsta programvarukrav

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 eller senare krävs.

## Onboarding {#onboarding}

Introduktionen AEM innehåll och handel är en tvåstegsprocess:

1. Installera AEM Content and Commerce Add-on för AEM 6.5

2. Koppla AEM till e-handelslösningen

### Installera AEM Content and Commerce Add-on för AEM 6.5 {#install-add-on}

Hämta och installera AEM Commerce Add-On för AEM 6.5 från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)-portalen.

Starta och installera AEM 6.5 Service Pack. Vi rekommenderar att du installerar det senaste tillgängliga Service Pack-paketet.

>[!NOTE]
>
>Detta görs av CSE för AEM kunder som har hanterade tjänster.

### Anslut AEM till ditt Commerce System {#connect}

AEM kan anslutas till alla handelssystem som har en tillgänglig GraphQL-slutpunkt för AEM. Dessa slutpunkter är vanligtvis offentligt tillgängliga eller kan anslutas via privata VPN-anslutningar eller lokala anslutningar beroende på de enskilda projektinställningarna.

Autentiseringshuvudet kan också anges för att använda ytterligare CIF-funktioner som kräver autentisering.

Projekt som skapats av [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) och [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) som redan ingår i [standardkonfigurationen](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) måste justeras.

Ersätt värdet för `url` i `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` med GraphQL-slutpunkten i e-handelssystemet. Denna konfiguration kan göras via OSGI-konsolen eller genom att distribuera OSGI-konfigurationen via projektet. Olika konfigurationer för staging- och produktionssystem stöds med olika AEM körningslägen.

AEM Content and Commerce Add-On och CIF Core Components använder både anslutningar på serversidan och på klientsidan. CIF-kärnkomponenter på klientsidan och CIF-tilläggsverktyg ansluter som standard till `/api/graphql`. Detta kan vid behov justeras via CIF-Cloud Servicens konfiguration (se nedan).

CIF Add-On tillhandahåller en GraphQL-proxyserver på `/api/graphql` som kan användas för [lokal utveckling](develop.md). För produktionsdistributioner rekommenderar vi starkt att du skapar en omvänd proxy till Commerce GraphQL-slutpunkten via AEM Dispatcher eller andra nätverkslager (som CDN).

## Konfigurera butiker och kataloger {#catalog}

Tillägget och [CIF Core-komponenterna](https://github.com/adobe/aem-core-cif-components) kan användas på flera AEM webbplatsstrukturer som är kopplade till olika e-handelsbutiker (eller butiksvyer osv.). Som standard distribueras CIF-tillägget med en standardkonfiguration som ansluter till Adobe Commerce standardbutik och -katalog (Magento).

Den här konfigurationen kan justeras för projektet via CIF-Cloud Servicens konfiguration enligt följande steg:

1. I AEM går du till Verktyg -> Cloud Services -> CIF-konfiguration

2. Välj den e-postkonfiguration som du vill ändra

3. Öppna konfigurationsegenskaperna via åtgärdsfältet

![Konfiguration av CIF-Cloud Services](/help/commerce/cif/assets/cif-cloud-service-config.png)

Följande egenskaper kan konfigureras:

- GraphQL-klient - Välj den konfigurerade GraphQL-klienten för e-handel med serverdelskommunikation. Detta bör normalt vara kvar som standard.
- Butiksvy - (Magento) butiksvyns identifierare. Om den är tom används standardbutiksvyn.
- Proxysökväg för GraphQL - URL-sökvägen för GraphQL-proxy som används AEM proxybegäranden till GraphQL-slutpunkten för handel.
   >[!NOTE]
   >
   > I de flesta inställningar får standardvärdet `/api/graphql` inte ändras. Endast avancerade inställningar som inte använder den angivna GraphQL-proxyn bör ändra den här inställningen.
- Aktivera stöd för katalog-UID - aktivera stöd för UID i stället för ID i e-handelsbackend-GraphQL-anropen.
   >[!NOTE]
   >
   > Stöd för UID introducerades i Adobe Commerce (Magento) 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.
- Katalogrotkategoriidentifierare - identifieraren (UID eller ID) för arkivkatalogroten
   >[!CAUTION]
   >
   > Från och med CIF Core Components version 2.0.0 togs stödet för `id` bort och ersattes med `uid`. Om ditt projekt använder CIF Core Components version 2.0.0 måste du aktivera stöd för katalog-UID och använda ett giltigt kategori-UID som &quot;Katalogens rotkategoriidentifierare&quot;.

Konfigurationen som visas ovan är för referens. Projekten ska ha egna konfigurationer.

Mer komplexa inställningar som använder flera AEM webbplatsstrukturer i kombination med olika e-handelskataloger finns i [Commerce Multi-Store Setup](configuring/multi-store-setup.md) självstudiekursen.

## Ytterligare resurser {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Inställningar för Commerce Multi-Store](configuring/multi-store-setup.md)
