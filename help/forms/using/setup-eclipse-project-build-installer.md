---
title: Bygg appen AEM Forms Android
seo-title: Build the AEM Forms Android app
description: Steg för att konfigurera Android Studio-projektet och skapa APK-filen för AEM Forms-appen för Android
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Bygg appen AEM Forms Android {#build-the-aem-forms-android-app}

Utför följande steg i den rekommenderade sekvensen för att skapa Android-appen för AEM Forms.

1. [Ladda ned källkodspaketet för AEM Forms App](#download-android-zip)
1. [Ange miljövariabler](#set-environment-variable-android)
1. [Bygg AEM Forms standardapp](#set-up-the-xcode-project)

## Ladda ned källkodspaketet för AEM Forms App {#download-android-zip}

Källkodspaketet för AEM Forms App refererar till `adobe-lc-mobileworkspace-src-<version>.zip` arkiv. Detta arkiv innehåller den källkod som krävs för att skapa en anpassad AEM Forms-app. Arkivet ingår i `adobe-aemfd-forms-app-src-pkg-<version>.zip`som finns på Software Distribution.

Utför följande steg för att hämta `adobe-aemfd-forms-app-src-pkg-<version>.zip` fil:

1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Tryck **[!UICONTROL Adobe Experience Manager]** finns i rubrikmenyn.
1. I **[!UICONTROL Filters]** avsnitt:
   1. Välj **[!UICONTROL Forms]** från **[!UICONTROL Solution]** nedrullningsbar lista.
   2. Välj version och typ för paketet. Du kan också använda **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på det paketnamn som gäller för operativsystemet och välj **[!UICONTROL Accept EULA Terms]** och trycka **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  och klicka **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.
1. Öppna om du vill hämta källkodsarkivet **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** i webbläsaren. ZIP-filen för Android-appen hämtas till din enhet.
1. Extrahera innehållet i ZIP-filen till en mapp i det lokala filsystemet. Till exempel: *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

I följande bild visas strukturen för `adobe-lc-mobileworkspace-src-<version>.zip\android`mapp.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Ange miljövariabler {#set-environment-variable-android}

Ange följande miljövariabler innan du startar byggprocessen för AEM Forms-programmet:

* Ställ in miljövariabeln JAVA_HOME på JDK-programvarans plats i det lokala filsystemet. Exempel: C:\Program Files\Java\jdk1.8.0_181
* Ange `ANDROID_SDK_ROOT` systemmiljövariabel till SDK-plats för Android. Till exempel C:\Users\&amp;lt;användarnamn>\AppData\Local\Android\Sdk
* Ange `Path` systemmiljövariabel som inkluderar mapplatserna för plattformsverktyg och verktyg för Android. Till exempel C:\Users\&amp;lt;användarnamn>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;användarnamn>\AppData\Local\Android\Sdk\tools.

## Bygg AEM Forms standardapp {#set-up-the-xcode-project}

När du har sparat adobe-lc-mobileworkspace-src-&lt;version>ZIP-fil i det lokala filsystemet och ange systemvariabler. Bygg en AEM Forms Android-standardapp med något av följande alternativ:

* [Bygg AEM Forms-app med Android Studio](#using-android-studio)
* [Generera APK-fil med Android Studio](#generate-apk-android-studio)

### Bygg AEM Forms-app med Android Studio {#using-android-studio}

Utför följande steg för att skapa AEM Forms-program med Android Studio:

1. Starta Android Studio-programmet på datorn.
1. Klicka **Öppna ett befintligt Android Studio-projekt**. Om dialogrutan för att öppna ett befintligt projekt inte visas automatiskt väljer du **Fil** > **Öppna**.
1. Navigera till *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* på det lokala filsystemet och klicka på **OK**.

   The **android** visas i den vänstra rutan.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Välj **android** från den vänstra rutan och klicka på **Kör** > **Kör android**.
1. Välj Android-enheten under Anslutna enheter i dialogrutan Välj distributionsmål och klicka på OK.

   När du har skapat utvecklingsmiljön kan du nu använda anpassningar i appen. Använd följande artiklar för att anpassa appen:

   * [Anpassning av varumärkesprofilering](/help/forms/using/branding-customization.md)
   * [Temaanpassning](/help/forms/using/theme-customization.md)
   * [Gestanpassning](/help/forms/using/gesture-customization.md)

   När du har anpassat programmet kan du generera APK-filen för distribution.

### Generera APK-fil med Android Studio {#generate-apk-android-studio}

Så här genererar du APK-filen med Android Studio:

1. Starta Android Studio-programmet på datorn.
1. Välj **Öppna ett befintligt Android Studio-projekt**. Om dialogrutan för att öppna ett befintligt projekt inte visas automatiskt väljer du **Fil** > **Öppna**.
1. Navigera till *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* på det lokala filsystemet och klicka på **OK**.

   Android-alternativet visas i den vänstra rutan.

1. Välj **Bygge** > **Bygg APK** för att generera APK-filen.

   Valfritt, välj **Bygge** > **Generera signerad APK** för att generera [undertecknad version](https://developer.android.com/studio/publish/app-signing) av APK-filen.

## Använd Android Debug Bridge {#build-android-debug-bridge}

När APK-filen har skapats kör du följande kommando för att installera programmet på en Android-enhet med [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Windowsanvändare:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Användare av Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
