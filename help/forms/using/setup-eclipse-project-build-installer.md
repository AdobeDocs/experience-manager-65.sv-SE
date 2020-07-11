---
title: Bygg Android-appen för AEM Forms
seo-title: Bygg Android-appen för AEM Forms
description: Steg för att konfigurera Android Studio-projektet och skapa APK-filen för AEM Forms-appen för Android
seo-description: Steg för att konfigurera Android Studio-projektet och skapa APK-filen för AEM Forms-appen för Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# Bygg Android-appen för AEM Forms {#build-the-aem-forms-android-app}

Utför följande steg i den rekommenderade sekvensen för att skapa Android-appen för AEM Forms.

1. [Hämta AEM Forms App Source Code Package](#download-android-zip)
1. [Ange miljövariabler](#set-environment-variable-android)
1. [Bygg standardappen AEM Forms](#set-up-the-xcode-project)

## Hämta AEM Forms App Source Code Package {#download-android-zip}

AEM Forms App Source Code Package refererar till `adobe-lc-mobileworkspace-src-<version>.zip` arkivet. Detta arkiv innehåller den källkod som krävs för att skapa en anpassad AEM Forms-app. Arkivet ingår i det `adobe-aemfd-forms-app-src-pkg-<version>.zip`paket som finns på Software Distribution.

Så här hämtar du `adobe-aemfd-forms-app-src-pkg-<version>.zip` filen:

1. Öppna [programvarudistribution](https://experience.adobe.com/downloads). Du måste ha ett Adobe ID för att kunna logga in på Software Distribution.
1. Tryck **[!UICONTROL Adobe Experience Manager]** på rubrikmenyn.
1. I **[!UICONTROL Filters]** avsnittet:
   1. Välj **[!UICONTROL Forms]** i **[!UICONTROL Solution]** listrutan.
   2. Välj version och typ för paketet. Du kan också använda alternativet **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på det paketnamn som gäller för ditt operativsystem, markera **[!UICONTROL Accept EULA Terms]** och tryck **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) och klicka **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.
1. Om du vill hämta källkodsarkivet öppnar du **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** i webbläsaren. ZIP-filen för Android-appen hämtas till din enhet.
1. Extrahera innehållet i ZIP-filen till en mapp i det lokala filsystemet. Exempel: *C:\&lt;Mappstruktur>\adobe-lc-mobileworkspace-src-2.4.20*

I följande bild visas `adobe-lc-mobileworkspace-src-<version>.zip\android`mappens struktur.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Ange miljövariabler {#set-environment-variable-android}

Ange följande miljövariabler innan du startar byggprocessen för AEM Forms-appen:

* Ställ in miljövariabeln JAVA_HOME på JDK-programvarans plats i det lokala filsystemet. Exempel: C:\Program Files\Java\jdk1.8.0_181
* Ställ in systemmiljövariabeln på SDK- `ANDROID_SDK_ROOT` platsen för Android. Till exempel C:\Users\&amp;lt;användarnamn>\AppData\Local\Android\Sdk
* Ställ in systemmiljövariabeln så att den omfattar mapplatserna för plattformsverktyg och verktyg för Android. `Path` Till exempel C:\Users\&amp;lt;användarnamn>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;användarnamn>\AppData\Local\Android\Sdk\tools.

## Bygg standardappen AEM Forms {#set-up-the-xcode-project}

När du har sparat filen adobe-lc-mobileworkspace-src-&lt;version>.zip i det lokala filsystemet och angett systemvariabler kan du skapa en AEM Forms Android-standardapp med något av följande alternativ:

* [Bygg appen AEM Forms med Android Studio](#using-android-studio)
* [Generera APK-fil med Android Studio](#generate-apk-android-studio)

### Bygg appen AEM Forms med Android Studio {#using-android-studio}

Utför följande steg för att skapa AEM Forms-appen med Android Studio:

1. Starta Android Studio-programmet på datorn.
1. Klicka på **Öppna ett befintligt Android Studio-projekt**. Om dialogrutan för att öppna ett befintligt projekt inte visas automatiskt väljer du **Arkiv** > **Öppna**.
1. Navigera till *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* i det lokala filsystemet och klicka på **OK**.

   Alternativet **android** visas i den vänstra rutan.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Välj **android** i den vänstra rutan och klicka på **Kör** > **Kör android**.
1. Välj Android-enheten under Anslutna enheter i dialogrutan Välj distribuerings-Target och klicka på OK.

   När du har skapat utvecklingsmiljön kan du nu använda anpassningar i appen. Använd följande artiklar för att anpassa appen:

   * [Anpassning av varumärkesprofilering](/help/forms/using/branding-customization.md)
   * [Temaanpassning](/help/forms/using/theme-customization.md)
   * [Gestanpassning](/help/forms/using/gesture-customization.md)

   När du har anpassat programmet kan du generera APK-filen för distribution.

### Generera APK-fil med Android Studio {#generate-apk-android-studio}

Så här genererar du APK-filen med Android Studio:

1. Starta Android Studio-programmet på datorn.
1. Välj **Öppna ett befintligt Android Studio-projekt**. Om dialogrutan för att öppna ett befintligt projekt inte visas automatiskt väljer du **Arkiv** > **Öppna**.
1. Navigera till *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* i det lokala filsystemet och klicka på **OK**.

   Android-alternativet visas i den vänstra rutan.

1. Välj **Skapa** > **Skapa APK** för att generera .apk-filen.

   Du kan också välja **Skapa** > **Generera signerad APK** för att generera en [signerad version](https://developer.android.com/studio/publish/app-signing) av .apk-filen.

## Använd Android Debug Bridge {#build-android-debug-bridge}

När APK-filen har skapats kör du följande kommando för att installera programmet på en Android-enhet med [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Windowsanvändare:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MAC-användare:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
