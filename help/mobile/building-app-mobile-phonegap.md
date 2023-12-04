---
title: Bygger mobilprogram
description: På den här sidan finns en komplett, stegvis artikel om hur du skapar ett mobilprogram med hjälp av kod från GitHub. Bygg applikationen för installation på en enhet eller simulator för testning eller publicering i appbutiker. Du kan skapa program lokalt med PhoneGap Command Line Interface eller i molnet med PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# Bygger mobilprogram{#building-mobile-applications}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Bygg applikationen för installation på en enhet eller simulator för testning eller publicering i appbutiker. Du kan skapa program lokalt med PhoneGap Command Line Interface eller i molnet med PhoneGap Build.

Det finns en komplett, stegvis artikel om hur du bygger ett mobilprogram med hjälp av kod från GitHub [här](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Flytta programmet till publiceringsinstansen {#moving-the-application-to-the-publish-instance}

Flytta programfiler till publiceringsinstansen så att du kan tillhandahålla innehållsuppdateringar till de installerade instanserna av mobilprogrammet och skapa programmet med det publicerade innehållet. Programmen består av två nodgrenar i databasen:

* `/content/phonegap/apps/<application name>`: Webbsidorna som författare skapar och aktiverar.
* `/content/phonegap/content/<application name>`: Programkonfigurationsfiler och konfigurationer för innehållssynkronisering.

>[!NOTE]
>
>Om du inte flyttar programfilerna till publiceringsinstansen kan innehållsförfattarna inte uppdatera cachen för innehållssynkronisering.

Du behöver bara flytta filerna i `/content/phonegap/content/<application name>` till publiceringsinstansen. Filerna i `/content/phonegap/apps/<application name>` grenen flyttas när författaren aktiverar sidorna.

I AEM finns två metoder för att flytta massinnehåll till publiceringsinstansen:

* [Använda kommandot Aktivera träd](/help/sites-authoring/publishing-pages.md) på replikeringskonsolen.
* [Skapa ett paket](/help/sites-administering/package-manager.md) som innehåller innehållet och replikera paketet.

Ett mobilprogram med namnet phonegapapp skapas till exempel. Följande nod måste flyttas till publiceringsinstansen: /content/phonegap/content/phonegapapp.

**Tips:** Om du vill flytta ett paket från författarinstansen till publiceringsinstansen använder du kommandot Replikera i paketet.

![chlimage_1-16](assets/chlimage_1-16.png)

## Bygga med kommandoradsgränssnittet PhoneGap {#building-using-the-phonegap-command-line-interface}

Kompilera PhoneGap-programmet på datorn med PhoneGap Command-line Interface (CLI). Om du vill inkludera AEM innehåll i ditt program skapar AEM en ZIP-fil som innehåller innehållet i ditt mobilprogram, konfigurationer för innehållssynkronisering och andra nödvändiga resurser. Hämta ZIP-filen och inkludera den i bygget.

### Förbereder din byggmiljö {#preparing-your-build-environment}

Om du vill bygga med PhoneGap CLI måste du installera Node.js och PhoneGap-klientverktyget. Du måste ha en internetanslutning för att kunna utföra följande procedur.

1. Hämta och installera [Node.js](https://nodejs.org/en).
1. Öppna en terminal eller kommandotolk och ange följande nodkommando för att installera PhoneGap-verktyget:

   ```shell
   npm install -g phonegap
   ```

   I ett UNIX®- eller Linux®-system kan du behöva prefix till kommandot med `sudo`.

   Terminalen visar resultatet av en serie HTTP GET-kommandon. När installationen är klar visar terminalen var biblioteken är installerade, som i följande exempel:

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. (Valfritt) Skaffa SDK för den mobila plattform som ni riktar er mot:

   * Installera den senaste versionen av iOS för att skapa appar för [Xcode](https://developer.apple.com/xcode/).
   * Installera [Android™ SDK](https://developer.android.com/).

### Laddar ned innehålls-ZIP-filen {#downloading-the-content-zip-file}

Flytta innehållet i mobilprogrammet till filsystemet.

1. Välj ditt program på sidan Mobilprogram.
1. (Valfritt) Klicka på ikonen Rensa cache i verktygsfältet för att skapa programmet för fullständiga installationer.

   ![Ikonen Rensa cache indikeras av en bruten länksymbol.](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >Cachen innehåller innehållsuppdateringar för installerade program. Om du rensar cachen försvinner alla cachelagrade uppdateringar.

1. Klicka på ikonen Hämta CLI-resurser i verktygsfältet.

   ![Ikonen Hämta CLI-resurser indikeras av en överlappande tablet-symbol.](do-not-localize/chlimage_1-1.png)

1. När du har sparat ZIP-filen klickar du på Stäng i dialogrutan Slutfört.
1. Extrahera innehållet i ZIP-filen.

### Använda PhoneGap CLI för att bygga {#using-the-phonegap-cli-to-build}

Använd PhoneGap CLI för att kompilera och installera programmet. Mer information om hur du använder PhoneGap CLI finns i PhoneGap-kommandoradsgränssnittet (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`).

1. Öppna en terminal eller kommandotolk och ändra den aktuella katalogen till den hämtade ZIP-programfilen. Följande ändrar till exempel katalogen till filen ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Ange kommandot phonegap för plattformen som du riktar dig mot. Följande kommando skapar till exempel programmet för Android™:

   ```shell
   phonegap build android
   ```

## Bygger med PhoneGap Build {#building-using-phonegap-build}

Använd PhoneGap-molntjänsten för att bygga din app. För att kunna utföra den här proceduren måste du först skapa en PhoneGap Build-konfiguration.

### Ansluter till PhoneGap Build {#connecting-to-phonegap-build}

Skapa en PhoneGap Build-konfiguration så att du kan använda PhoneGap Build-tjänsterna inifrån AEM. Ange användarnamn och lösenord för det PhoneGap Build-konto som du ska använda för att skapa dina mobilprogram.

1. Öppna sidan Verktyg. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Klicka på Cloud Service i området CQ-åtgärder.
1. Klicka på länken Konfigurera nu för PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. I dialogrutan Skapa konfiguration anger du ett värde för egenskapen Titel. Som standard hämtas värdet för egenskapen Namn från titeln, men du kan ange ett namn. Klicka på Skapa.
1. I dialogrutan PhoneGap Build Configuration skriver du ditt användarnamn och lösenord för PhoneGap Build och klickar sedan på OK.

### Använda PhoneGap Build {#using-phonegap-build}

Skicka programresurserna till PhoneGap Build för kompilering för olika mobilplattformar.

1. Öppna ditt mobilprogram på sidan Mobilprogram. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Valfritt) Om du vill skapa programmet för fullständiga installationer markerar du programmet och klickar på ikonen Rensa cache.

   ![Ikonen Rensa cache indikeras av en bruten länksymbol.](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >Cachen innehåller innehållsuppdateringar för installerade program. Om du rensar cachen försvinner alla cachelagrade uppdateringar.

1. Markera välkomstsidan och klicka sedan på ikonen Skapa fjärrmapp.

   ![Ikonen för att skapa en fjärrkontroll visas med två runda växlar.](do-not-localize/chlimage_1-3.png)

   **Obs!** Betaversionen av AEM Beta skapar inte något inkorgsmeddelande när bygget är klart.

1. I dialogrutan Slutfört klickar du på PhoneGap Build för att öppna Adobe PhoneGap Build-sidan på `https://build.phonegap.com/apps`. Om du väntar på att appen ska visas kan du kontrollera PhoneGapet Build-statusen på `https://status.build.phonegap.com/`.

   Mer information om hur du installerar bygget finns i [PhoneGap Build Documentation](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Kostnadsfria PhoneGap Build-konton kan användas med ett privat program. PhoneGap-byggen misslyckas om du skapar ytterligare ett privat program.

### Nästa steg {#the-next-steps}

Nästa steg efter byggprocessen är att lära sig om [Struktur för ett program](/help/mobile/phonegap-structure-an-app.md).
