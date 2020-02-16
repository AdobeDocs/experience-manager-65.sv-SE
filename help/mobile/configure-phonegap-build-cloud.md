---
title: Konfigurera din Adobe PhoneGap Build-molntjänst
seo-title: Konfigurera din Adobe PhoneGap Build-molntjänst
description: Följ den här sidan för att konfigurera molntjänsterna och bygga ditt program med PhoneGap Build.
seo-description: Följ den här sidan för att konfigurera molntjänsterna och bygga ditt program med PhoneGap Build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera din Adobe PhoneGap Build-molntjänst {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

PhoneGap Build-panelen **för** PhoneGap på programkontrollpanelen ger möjlighet att skapa och distribuera ditt PhoneGap-mobilprogram via Adobe PhoneGap Build-tjänsten.

Alla plattformar som stöds som definieras i **Manage App** tile byggs med PhoneGap Build när du trycker på en fjärrversion med **PhoneGap Build** Tile.

Du kan överföra en fjärrversion till [https://build.phonegap.com](https://build.phonegap.com) eller hämta källan för att bygga lokalt med [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build Tile](assets/chlimage_1-60.png)

## Konfigurera molntjänsten {#configuring-the-cloud-service}

För att kunna utnyttja PhoneGap Build måste du konfigurera AEM PhoneGap Build Cloud-tjänsten med din PhoneGap Build-kontoinformation.

Om du inte har något konto går du till [https://build.phonegap.com](https://build.phonegap.com) och registrerar dig! Om du har ett Adobe Creative Cloud-medlemskap kan du ha stöd för upp till 25 privata program (program utan öppen källkod).

När du har verifierat att ditt PhoneGap Build-konto är aktivt går du till din AEM Cloud Management Console, närmare bestämt [PhoneGap Build-molntjänsten](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Använd panelen **Hantera molntjänster** för att konfigurera en ny molntjänstkonfiguration.

### Använda panelen Hantera molntjänster {#using-manage-cloud-services-tile}

Innan du börjar bygga din app med **PhoneGap Build** -panelen måste du konfigurera dina molntjänster med panelen **Hantera molntjänster** från AEM Mobile-instrumentpanelen.

Följ stegen nedan för att konfigurera molntjänster för din app:

1. Klicka på det övre högra hörnet i rutan **Hantera molntjänster** .

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Välj alternativet **PhoneGap Build** på skärmen **Lägg till eller redigera molntjänst** .

   Click **Next**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Ange dina autentiseringsuppgifter för att skapa en ny molnkonfiguration.

   När den har verifierats klickar du på **Skicka**. Den här konfigurerade molnkonfigurationen visas nu på panelen **Hantera molntjänster** .

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Bygga ditt program med PhoneGap Build {#building-your-application-with-phonegap-build}

När du har konfigurerat molntjänsterna kan du bygga ditt program med **PhoneGap Build** . Klicka på det övre högra hörnet för att välja bland alternativen **Skapa fjärrmapp** eller **Hämta källa** .

![chlimage_1-64](assets/chlimage_1-64.png)

Klicka på **Skapa fjärr** för att anropa en fjärrversion med Adobe PhoneGap Build.

>[!NOTE]
>
>Om bygget misslyckas av någon anledning (röd iOS-ikon nedan anger att plattformen misslyckades) kan du hovra över ikonen för att få felmeddelandet. Du kan också klicka på den trippelprickade punkten, &quot;..&quot; längst ned på panelen för att navigera direkt till https://build.phonegap.com (du måste autentisera) och titta på och hantera bygget direkt.

### Bygga ditt program med PhoneGap CLI {#building-your-application-with-phonegap-cli}

PhoneGap har ett kommandoradsgränssnitt som gör att du kan skapa programmet lokalt.

Kompilera PhoneGap-programmet på datorn med PhoneGap Command Line Interface (CLI). För att inkludera AEM-innehållet i programmet skapar AEM en ZIP-fil som innehåller innehållet i ditt mobilprogram, konfigurationer för innehållssynkronisering och andra nödvändiga resurser. Hämta ZIP-filen och inkludera den i bygget.

För att du ska kunna utnyttja kommandoradsgränssnittet i PhoneGap måste du konfigurera den lokala miljön så att den omfattar:

1. Platform SDK (iOS, Android, WindowsPhone, ...) och
1. PhoneGap CLI

Du kan läsa mer [här](https://docs.phonegap.com/references/phonegap-cli/).

När du har installerat de nödvändiga komponenterna kan du testa dem på ett enkelt sätt genom att skapa en enkel app och få den att köras antingen i simulatorn eller ännu bättre på enheten, från ett terminalförsök:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add - emulera i slutet av den här raden om du inte vill köra den på den anslutna enheten.

När du har verifierat att ovanstående fungerar använder du **PhoneGap Build** Tile för att **hämta källan**. Spara och zippa upp filen på din dator. När det är klart:

* navigera till den sparade filen (mapp)
* run &#39;phonegap run ios&#39; (or android, etc.)

### Additional Resources {#additional-resources}

Mer information om roller och ansvarsområden för en författare och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Om du skriver för Adobe PhoneGap Enterprise i AEM](/help/mobile/phonegap.md)
