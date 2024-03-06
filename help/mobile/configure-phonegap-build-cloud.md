---
title: Konfigurera din Adobe PhoneGap Build-Cloud Service
description: Följ den här sidan för att konfigurera molntjänsterna och skapa ditt program med PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# Konfigurera din Adobe PhoneGap Build-Cloud Service {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

The **PhoneGap Build Tile** på programkontrollpanelen kan du bygga och distribuera ditt PhoneGap-mobilprogram via Adobe PhoneGap Build Service.

Alla plattformar som stöds definieras i **Hantera program** plattan byggs med PhoneGap Build när man trycker på en fjärranslutning med **PhoneGap Build** Platt.

Du kan överföra en fjärrversion till `https://build.phonegap.com` eller hämta källan för att bygga lokalt med PhoneGap CLI på `https://docs.phonegap.com/references/phonegap-cli/`.

![PhoneGap Build Tile](assets/chlimage_1-60.png)

## Konfigurera Cloud Servicen {#configuring-the-cloud-service}

För att kunna utnyttja PhoneGap Build måste du konfigurera Cloud Servicen AEM PhoneGap Build med PhoneGap Build-kontoinformationen.

Om du inte har något konto går du till `https://build.phonegap.com` och registrera dig! Om du har ett Adobe Creative Cloud-medlemskap kan du ha stöd för upp till 25 privata appar (appar utan öppen källkod).

När du har verifierat att ditt PhoneGap Build-konto är aktivt navigerar du till din AEM Cloud Management Console, speciellt den [PhoneGap Build Cloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Använd **Hantera Cloud Service** panel för att konfigurera en ny molntjänstkonfiguration.

### Använda rutan Hantera Cloud Service {#using-manage-cloud-services-tile}

Innan du börjar bygga din app med **PhoneGap Build** måste du konfigurera dina molntjänster med **Hantera Cloud Service** från AEM Mobile Dashboard.

Följ stegen nedan för att konfigurera molntjänster för din app:

1. Klicka på det övre högra hörnet i **Hantera Cloud Service** platta.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Välj **PhoneGap Build** från **Lägg till eller redigera Cloud Service** skärm.

   Klicka på **Nästa**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Ange dina autentiseringsuppgifter så att du kan skapa en molnkonfiguration.

   När den har verifierats klickar du på **Skicka**. Den här konfigurerade molnkonfigurationen visas nu i **Hantera Cloud Service** platta.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Bygga ditt program med PhoneGap Build {#building-your-application-with-phonegap-build}

När du har konfigurerat molntjänsterna kan du bygga ditt program med **PhoneGap Build** platta. Klicka på det övre högra hörnet så att du kan välja från det övre högra hörnet **Skapa fjärrmapp** eller **Hämta källa** alternativ.

![chlimage_1-64](assets/chlimage_1-64.png)

Om du vill starta en fjärranslutning med Adobe PhoneGap Build klickar du på **Skapa fjärrmapp**.

>[!NOTE]
>
>Om bygget misslyckas av någon anledning (den röda iOS-ikonen nedan anger att plattformen misslyckades) kan du hovra över ikonen för att få felmeddelandet. Du kan också klicka på den trippelprickade punkten, &quot;..&quot; längst ned i rutan för att navigera direkt till `https://build.phonegap.com` (du måste autentisera) och se och hantera ditt bygge direkt.

### Bygga ditt program med PhoneGap CLI {#building-your-application-with-phonegap-cli}

PhoneGap har ett kommandoradsgränssnitt som gör att du kan skapa programmet lokalt.

Kompilera PhoneGap-programmet på datorn med PhoneGap Command-Line Interface (CLI). Om du vill inkludera AEM innehåll i ditt program skapar AEM en ZIP-fil som innehåller innehållet i ditt mobilprogram, konfigurationer för innehållssynkronisering och andra nödvändiga resurser. Hämta ZIP-filen och inkludera den i bygget.

För att kunna utnyttja PhoneGaps CLI måste du konfigurera din lokala miljö så att den omfattar:

1. Platform SDK (iOS, Android™, WindowsPhone, ...) och
1. PhoneGap CLI

Du kan läsa mer här: `https://docs.phonegap.com/references/phonegap-cli/`.

När du har installerat de nödvändiga komponenterna kan du testa dem på ett enkelt sätt genom att skapa en enkel app och få den att köras antingen i simulatorn eller ännu bättre på enheten, från ett terminalförsök:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>Lägg till - emulera i slutet av den här raden om du inte vill köra den på den anslutna enheten.

När du har kontrollerat att ovanstående fungerar använder du **PhoneGap Build** Överlappa till **Hämta källa**. Spara och zippa upp filen i det lokala systemet. När det är klart:

* navigera till den sparade filen (mapp)
* run &#39;phonegap run ios&#39; (eller android, osv.)

### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvarsområden för en författare och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Skapa för Adobe PhoneGap Enterprise i AEM](/help/mobile/phonegap.md)
