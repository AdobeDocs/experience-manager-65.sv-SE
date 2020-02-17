---
title: Konfigurera Android-studioprojektet och bygg Android-appen
seo-title: Konfigurera Android-studioprojektet och bygg Android-appen
description: Steg för att konfigurera Android Studio-projektet och skapa installationsprogrammet för AEM Forms-appen
seo-description: Steg för att konfigurera Android Studio-projektet och skapa installationsprogrammet för AEM Forms-appen
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# Konfigurera Android-studioprojektet och bygg Android-appen {#set-up-the-android-studio-project-and-build-the-android-app}

Den här artikeln handlar om att skapa AEM Forms App 6.3.1.1 och senare versioner. Information om hur du skapar en app från källkoden för källkoden i AEM Forms App 6.3 finns i [Konfigurera Eclipse-projektet och skapa Android™-appen](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms tillhandahåller den fullständiga källkoden för appen AEM Forms. Källan innehåller alla komponenter för att skapa en anpassad AEM Forms-app. Källkodsarkivet, `adobe-lc-mobileworkspace-src-<version>.zip` är en del av paketet för `adobe-aemfd-forms-app-src-pkg-<version>.zip` paketresursen.

Så här hämtar du AEM Forms-appkällan:

1. Navigera till paketresursen

   Webbadress: `https://<server>:<port>/crx/packageshare`.

1. Hämta källpaketet. När du hämtar paketet läggs det till i din AEM Forms-pakethanterare.
1. När nedladdningen är klar går du till: `https://<server>:<port>/crx/packmgr/index.jsp`, och installera `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Om du vill hämta källkodsarkivet öppnar du `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` i webbläsaren.

   Källpaketet hämtas till din enhet.

I följande bild visas det extraherade innehållet i `adobe-lc-mobileworkspace-src-<version>.zip`.

![Extraherat innehåll i den zippade Android™-källan](assets/mws-content-1.png)

Följande bild visar katalogstrukturen för `android`mappen i `src`mappen.

![Katalogstruktur för android-mappen i src](assets/android-folder.png)

## Bygg standardappen AEM Forms {#set-up-the-xcode-project}

1. Utför följande steg för att konfigurera ett projekt i Android™ Studio och ange en signeringsidentitet:

   Logga in på en dator där Android™ Studio är installerat och konfigurerat.

1. Kopiera det hämtade `adobe-lc-mobileworkspace-src-<version>.zip` arkivet till:

   **För MAC-användare**: `[User_Home]/Projects`

   **För Windows®-användare**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >För Windows® rekommenderar vi att du behåller android-projektet i systemenheten.

1. Extrahera arkivet i följande katalog:

   **För MAC-användare**: `[User_Home]/Projects/[your-project]`

   **För Windows®-användare**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Vi rekommenderar att du behåller det extraherade android-projektet i systemenheten innan du importerar projektet till Android Studio.

1. Starta Android™ Studio.

   **För MAC-användare**: Uppdatera `local.properties` filen som finns i `[User_Home]/Projects/[your-project]/android` mappen och peka på `sdk.dir` variabeln på `SDK` skrivbordet.

   **För Windows®-användare**: Uppdatera `local.properties` filen som finns i `%HOMEPATH%\Projects\[your-project]\android` mappen och peka på `sdk.dir` variabeln på `SDK` skrivbordet.

1. Klicka på **[!UICONTROL Slutför]** för att skapa projektet.

   Projektet är tillgängligt i ADT Project Explorer.

   ![Förmörka projekt efter att appen har skapats](assets/eclipsebuildmws.png)

1. I Android™ Studio väljer du **[!UICONTROL Importera projekt (Eclipse ADT, Gradle, etc.)]**.
1. I projektutforskaren väljer du rotkatalogen för projektet som du vill skapa i textrutan **Rotkatalog** :

   **** För Mac: [User_Home]/Projects/MobileWorkspace/src/android

   **** För Windows®: %HOMEPATH%\Projects\MobileWorkspace\src\android

1. När projektet har importerats visas ett popup-fönster med alternativet att uppdatera Android™-pluginmodulen Gradle. Klicka på lämplig knapp beroende på dina behov.

   ![dontremindmeagainforisproject](assets/dontremindmeagainforthisproject.png)

1. När du har skapat en övertoning visas följande skärm. Anslut lämplig enhet eller emulator till systemet och klicka på **[!UICONTROL Kör Android™]**.

   ![graderskonsol](assets/gradleconsole.png)

1. Android™ Studio visar anslutna enheter och tillgängliga emulatorer. Välj den enhet som du vill köra programmet på och klicka sedan på **OK**.

   ![ansluten enhet](assets/connecteddevice.png)

När du har skapat projektet kan du välja att installera programmet med Android™ Debug Bridge eller Android™ Studio.

### Använda Android™ Debug Bridge {#andriod-debug-bridge}

Du kan installera programmet på en Android™-enhet via [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) med följande kommando:

**För MAC-användare**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**För Windows®-användare**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
