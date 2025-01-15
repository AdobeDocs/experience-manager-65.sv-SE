---
title: Konfigurera din Adobe PhoneGap Build-Cloud Service
description: Följ den här sidan för att konfigurera molntjänsterna och skapa ditt program med PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# Konfigurera din Adobe PhoneGap Build-Cloud Service {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

Med **PhoneGap Build Tile** på programkontrollpanelen kan du skapa och distribuera ditt PhoneGap-mobilprogram via Adobe PhoneGap Build-tjänsten.

Alla plattformar som stöds som definieras i **Manage App** -plattan byggs med PhoneGap Build när en fjärrbyggnad skickas med **PhoneGap Build** -plattan.

Du kan skicka en fjärrversion till `https://build.phonegap.com` eller hämta källan för att bygga lokalt med PhoneGap CLI på `https://docs.phonegap.com/references/phonegap-cli/`.

![PhoneGap Build Tile](assets/chlimage_1-60.png)

## Konfigurera Cloud Servicen {#configuring-the-cloud-service}

För att kunna utnyttja PhoneGap Build måste du konfigurera Cloud Servicen AEM PhoneGap Build med PhoneGap Build-kontoinformationen.

Om du för närvarande inte har något konto går du till `https://build.phonegap.com` och registrerar dig! Om du har ett Adobe Creative Cloud-medlemskap kan du ha stöd för upp till 25 privata appar (appar utan öppen källkod).

När du har verifierat att ditt PhoneGap Build-konto är aktivt går du till AEM Cloud Management Console, särskilt [PhoneGap Build-Cloud Servicen](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Använd panelen **Hantera Cloud Service** om du vill konfigurera en ny molntjänstkonfiguration.

### Använda rutan Hantera Cloud Service {#using-manage-cloud-services-tile}

Innan du börjar bygga din app med panelen **PhoneGap Build** måste du konfigurera dina molntjänster med panelen **Hantera Cloud Service** från AEM Mobile instrumentpanel.

Följ stegen nedan för att konfigurera molntjänster för din app:

1. Klicka på det övre högra hörnet i rutan **Hantera Cloud Service**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Välj alternativet **PhoneGap Build** på skärmen **Lägg till eller redigera Cloud Service**.

   Klicka på **Nästa**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Ange dina autentiseringsuppgifter så att du kan skapa en molnkonfiguration.

   När den har verifierats klickar du på **Skicka**. Den här konfigurerade molnkonfigurationen visas nu i rutan **Hantera Cloud Service**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Bygga ditt program med PhoneGap Build {#building-your-application-with-phonegap-build}

När du har konfigurerat molntjänsterna kan du bygga ditt program med **PhoneGap Build**. Klicka på det övre högra hörnet så att du kan välja mellan alternativen **Skapa fjärrmapp** eller **Hämta Source**.

![chlimage_1-64](assets/chlimage_1-64.png)

Klicka på **Bygg fjärr** om du vill anropa en fjärrversion med Adobe PhoneGap Build.

>[!NOTE]
>
>Om bygget misslyckas av någon anledning (den röda iOS-ikonen nedan anger att plattformen misslyckades) kan du hovra över ikonen för att få felmeddelandet. Du kan också klicka på den trippelprickade punkten, &quot;..&quot; längst ned i rutan för att navigera direkt till `https://build.phonegap.com` (du måste autentisera) och titta på och hantera bygget direkt.

### Bygga ditt program med PhoneGap CLI {#building-your-application-with-phonegap-cli}

PhoneGap har ett kommandoradsgränssnitt som gör att du kan skapa programmet lokalt.

Kompilera PhoneGap-programmet på datorn med PhoneGap Command-Line Interface (CLI). Om du vill inkludera AEM innehåll i ditt program skapar AEM en ZIP-fil som innehåller innehållet i ditt mobilprogram, konfigurationer för innehållssynkronisering och andra nödvändiga resurser. Hämta ZIP-filen och inkludera den i bygget.

För att kunna utnyttja PhoneGaps CLI måste du konfigurera din lokala miljö så att den omfattar:

1. Platform SDK (iOS, Android™, WindowsPhone, ...) och
1. PhoneGap CLI

Du kan läsa mer här på `https://docs.phonegap.com/references/phonegap-cli/`.

När du har installerat de nödvändiga komponenterna kan du testa dem på ett enkelt sätt genom att skapa en enkel app och få den att köras antingen i simulatorn eller ännu bättre på enheten, från ett terminalförsök:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>Lägg till - emulera i slutet av den här raden om du inte vill köra den på den anslutna enheten.

När du har verifierat att ovanstående fungerar använder du **PhoneGap Build**-panelen för att **hämta Source**. Spara och zippa upp filen i det lokala systemet. När det är klart:

* navigera till den sparade filen (mapp)
* run &#39;phonegap run ios&#39; (eller android, osv.)

### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvarsområden för en författare och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Skapa för Adobe PhoneGap Enterprise i AEM](/help/mobile/phonegap.md)
