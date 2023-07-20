---
title: Konfigurera Android-&handeln; Studieprojekt och bygg Android&trade. app
description: Steg för att konfigurera Android&handeln; Studio-projekt och bygg installationsprogrammet för Forms-appen Adobe Experience Manager (AEM)
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Konfigurera Android™-studioprojektet och bygg Android™-appen {#set-up-the-android-studio-project-and-build-the-android-app}

Den här artikeln handlar om att skapa AEM Forms App 6.3.1.1 och senare versioner. Information om hur du skapar en app från källkoden för AEM Forms App 6.3 finns i [Konfigurera Eclipse-projektet och bygg Android™-appen](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms tillhandahåller den fullständiga källkoden för AEM Forms-appen. Källan innehåller alla komponenter som behövs för att skapa en anpassad AEM Forms-app. Källkodsarkivet `adobe-lc-mobileworkspace-src-<version>.zip` är en del av `adobe-aemfd-forms-app-src-pkg-<version>.zip` paket om programvarudistribution.

Så här hämtar du programkällan för AEM Forms:

1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Tryck **[!UICONTROL Adobe Experience Manager]** finns i rubrikmenyn.
1. I **[!UICONTROL Filters]** avsnitt:
   1. Välj **[!UICONTROL Forms]** från **[!UICONTROL Solution]** nedrullningsbar lista.
   2. Välj version och typ för paketet. Du kan också använda **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på det paketnamn som gäller för operativsystemet och välj **[!UICONTROL Accept EULA Terms]** och trycka **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  och klicka **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.

I följande bild visas det extraherade innehållet i `adobe-lc-mobileworkspace-src-<version>.zip`.

![Extraherat innehåll i den zippade Android™-källan](assets/mws-content-1.png)

Följande bild visar katalogstrukturen för `android`i `src`mapp.

![Katalogstruktur för android-mappen i src](assets/android-folder.png)

## Bygg AEM Forms standardapp {#set-up-the-xcode-project}

1. Utför följande steg för att konfigurera ett projekt i Android™ Studio och ange en signeringsidentitet:

   Logga in på en dator där Android™ Studio är installerat och konfigurerat.

1. Kopiera den hämtade filen `adobe-lc-mobileworkspace-src-<version>.zip` arkivera till:

   **För Mac**: `[User_Home]/Projects`

   **För Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >För Windows® rekommenderar vi att du behåller Android™-projektet i systemenheten.

1. Extrahera arkivet i följande katalog:

   **För Mac**: `[User_Home]/Projects/[your-project]`

   **För Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   Vi rekommenderar att du behåller det extraherade Android-projektet i systemenheten innan du importerar projektet till Android™ Studio.

1. Starta Android™ Studio.

   **För Mac**: Uppdatera `local.properties` filen finns i `[User_Home]/Projects/[your-project]/android` mapp och peka på `sdk.dir` variabel till `SDK` plats på datorn.

   **För Windows®**: Uppdatera `local.properties` filen finns i `%HOMEPATH%\Projects\[your-project]\android` mapp och peka på `sdk.dir` variabel till `SDK` plats på datorn.

1. Klicka **[!UICONTROL Finish]** för att bygga projektet.

   Projektet är tillgängligt i ADT Project Explorer.

   ![Förmörka projekt efter att appen har skapats](assets/eclipsebuildmws.png)

1. I Android™ Studio väljer du **[!UICONTROL Import Project (Eclipse ADT, Gradle, Etc.)]**.
1. I projektutforskaren väljer du rotkatalogen för projektet som du vill bygga i **Rotkatalog** textruta:

   **För Mac:** [User_Home]/Projects/MobileWorkspace/src/android

   **För Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. När projektet har importerats visas ett popup-fönster med alternativet att uppdatera Android™-pluginmodulen Gradle. Klicka på lämplig knapp beroende på dina behov.

   ![dontremindmeagainforisproject](assets/dontremindmeagainforthisproject.png)

1. När du har skapat en övertoning visas följande skärm. Anslut lämplig enhet eller emulator till systemet och klicka på **[!UICONTROL Run Android™]**.

   ![graderskonsol](assets/gradleconsole.png)

1. Android™ Studio visar anslutna enheter och tillgängliga emulatorer. Välj den enhet som du vill köra programmet på och klicka sedan på **OK**.

   ![ansluten enhet](assets/connecteddevice.png)

När du har skapat projektet kan du välja att installera programmet med Android™ Debug Bridge eller Android™ Studio.

### Använda Android™ Debug Bridge {#andriod-debug-bridge}

Du kan installera programmet på en Android™-enhet med [Android™ Debug Bridge](https://developer.android.com/tools/adb) med följande kommando:

**För Mac**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**För Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
