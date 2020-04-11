---
title: Anpassning av varumärkesprofilering
seo-title: Anpassning av varumärkesprofilering
description: Anpassa programikonen, programnamnet, startbilderna och inloggningssidan för att ge AEM Forms-appen ett distinkt organisationsspecifikt utseende.
seo-description: Anpassa programikonen, programnamnet, startbilderna och inloggningssidan för att ge AEM Forms-appen ett distinkt organisationsspecifikt utseende.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Anpassning av varumärkesprofilering {#branding-customization}

Du kan anpassa programikonen, programnamnet, startbilderna och inloggningssidan för att ge AEM Forms-appen ett tydligt organisationsspecifikt utseende. Du kan till exempel ändra bilderna så att de använder logotyper från din organisation. Appen AEM Forms stöder följande anpassningar:

* Anpassa programikoner och starta bilder
* Anpassa appnamn
* Anpassa bilder på inloggningssidan
* Anpassa logotypen på appmenyn

## Anpassa ikoner och starta bilder {#customizing-icon-and-launch-images}

Följ de här stegen för att anpassa standardprogramikonen och startbilden för AEM Forms-appen:

>[!NOTE]
>
>Använd icke-sammanflätade PNG-format för alla ikoner och bilder.

### Anpassa ikoner och starta bilder {#to-customize-icon-and-launch-images}

#### För iOS {#for-ios}

1. Öppna `Capture.xcodeproj` projektet i Xcode.
1. (***Om du vill anpassa ikonen***) I navigeringsvyn i Capture går du till **[!UICONTROL Capture > Capture > Supporting Files > Capture-info.plist]**. Klicka på listrutan bredvid ikonfilerna. Ange namnet på ikonfilen (.png) och överför filen på **[!UICONTROL Capture > Capture > Resources > icons]**. De dimensioner som stöds för närvarande är: 29x29, 50x50, 58x58, 72x72, 100x100 och 144x144.
1. (***För anpassning av startbilder***) Kontrollera att filnamnen för bilderna är:

   * För stående: `Default-Portrait~ipad.png` och `Default-Portrait@2x~ipad.png`
   * För liggande: `Default-Landscape~ipad.png` och `Default-Landscape@2x~ipad.png`
   Överför dem till Capture-projektet för att ersätta befintliga filer i projektet.

   >[!NOTE]
   >
   >Kontrollera att namnet och upplösningen på bilden matchar den bild du ersätter i projektet.

1. Bygg och kör appen AEM Forms på iOS-enheter eller iOS-simulatorer.

#### För Android {#for-android}

1. Namnge programikonfilerna som:

   `ic_launcher.png`

1. Placera motsvarande ikonfiler i följande kataloger:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`
   >[!NOTE]
   >
   >Kontrollera att namnet och upplösningen på bilden matchar den bild du ersätter i projektet.

1. Återskapa appen AEM Forms.

### För Windows {#for-windows}

1. Ersätt ikonerna i sökvägen:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Ersätt startbilden i sökvägen:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Kontrollera att namnet och upplösningen på bilden matchar den bild du ersätter i projektet.

1. Återskapa appen AEM Forms.

## Anpassa appnamnet {#customize-the-app-name}

### För iOS {#for-ios-1}

1. Öppna `Capture.xcodeproj` projektet i Xcode.
1. I navigeringsvyn i Capture går du till **[!UICONTROL Capture > Capture > Supporting Files > InfoPlist.strings]**.

   Uppdatera värdet för `CFBundleDisplayName` attributet till ett namn som du vill visa för programmet.

1. Bygg och kör appen AEM Forms på iOS-enheter eller iOS-simulatorer.

   Mer information om hur du skapar appen för iOS finns i [Konfigurera Xcode-projektet och skapa iOS-appen](/help/forms/using/setup-xcode-project-build-installer.md).

### För Android {#for-android-1}

1. Öppna följande XML i en text- eller XML-redigerare:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Uppdatera värdet för nyckeln `app_name`.
1. Återskapa appen AEM Forms.

   Mer information om hur du skapar appen för Android finns i [Konfigurera Eclipse-projektet och skapa Android-appen](/help/forms/using/setup-eclipse-project-build-installer.md).

### För Windows {#for-windows-1}

1. Öppna följande XML i en textredigerare:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Uppdatera värdet i `<name>...</name>` -taggen.
1. Återskapa appen AEM Forms.

   Mer information om hur du skapar en app för Windows finns i [Konfigurera Visual Studio-projektet och bygg Windows-appen](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Anpassa bilder på inloggningssidan {#customizing-images-on-the-login-page}

Inloggningssidan för AEM Forms-appen innehåller logotyper och bakgrundsbilder. Logotypen finns ovanför inloggningsdialogrutan och bakgrundsbilden finns under inloggningsdialogrutan. Följ de här stegen för att anpassa standardbilden på inloggningssidan:

**Innan du startar**

Kontrollera att du har följande bilder:

<table>
 <tbody>
  <tr>
   <th><p>Beskrivning</p> </th>
   <th><p>Storlek</p> </th>
   <th><p>Filnamn</p> </th>
  </tr>
  <tr>
   <td><p>Logotyp</p> </td>
   <td><p>72 x 72 pixlar</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>Bakgrundsbild (stående)</p> </td>
   <td><p>1 280 x 989 pixlar</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Anpassa bilder på inloggningssidan med Xcode**

1. Öppna `Capture.xcodeproj` projektet i Xcode.

1. Navigate to the `www/wsmobile/images`folder.
1. Om du vill ändra logotyp ersätter du standardfilen `LC-logo.png` med den anpassade `LC-logo.png` filen.
1. Om du vill ändra bakgrund ersätter du standardfilen `Landing_bg.jpeg` med den anpassade `Landing_bg.jpeg`filen.
1. Bygg och kör appen AEM Forms på iOS-enheter eller iOS-simulatorer.

### Anpassa bilder på inloggningssidorna med Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Öppna Android-projektet i Eclipse.

1. Navigate to the `assets/www/wsmobile/images`folder.
1. Om du vill ändra logotyp ersätter du standardfilen `LC-logo.png` med den anpassade `LC-logo.png` filen.
1. Om du vill ändra bakgrund ersätter du standardfilen `Landing_bg.jpeg` med den anpassade `Landing_bg.jpeg`filen.
1. Bygg och kör appen AEM Forms på en Android-enhet.

### Anpassa bilder på inloggningssidorna med Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Öppna `MWSWindows.sln` projektet i Visual Studio.

1. Navigate to the `MWSWindows\www\wsmobile\images`folder.
1. Om du vill ändra logotyp ersätter du standardfilen `LC-logo.png` med den anpassade `LC-logo.png` filen.
1. Om du vill ändra bakgrund ersätter du standardfilen `Landing_bg.jpeg` med den anpassade `Landing_bg.jpeg`filen.
1. Bygg och kör appen AEM Forms på en Windows-enhet.

## Anpassa logotypen på appmenyn {#customizing_images_on_the_login_page-1}

När du har loggat in på appen AEM Forms och tryckt på menyknappen visas logotypen ovanför menyn. Följ de här stegen för att anpassa standardlogotypen:

**Innan du startar**

Kontrollera att du har följande bild:

<table>
 <tbody>
  <tr>
   <th><p>Beskrivning</p> </th>
   <th><p>Storlek</p> </th>
   <th><p>Filnamn</p> </th>
  </tr>
  <tr>
   <td><p>Logotyp</p> </td>
   <td><p>72 x 72 pixlar</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Anpassa bilder på inloggningssidan med Xcode**

1. Öppna `Capture.xcodeproj` projektet i Xcode.

1. Navigate to the `www/wsmobile/images`folder.
1. Om du vill ändra logotypen ersätter du standardfilen `aem_icon.png` med den anpassade `aem_icon.png` filen.
1. Bygg och kör appen AEM Forms på iOS-enheter eller iOS-simulatorer.

### Anpassa bilder på inloggningssidorna med Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Öppna Android-projektet i Eclipse.

1. Navigate to the `assets/www/wsmobile/images`folder.
1. Om du vill ändra logotypen ersätter du standardfilen `aem_icon.png` med den anpassade `aem_icon.png` filen.
1. Bygg och kör appen AEM Forms på en Android-enhet.

### Anpassa bilder på inloggningssidorna med Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Öppna `MWSWindows.sln` projektet i Visual Studio.

1. Navigate to the `MWSWindows\www\wsmobile\images`folder.
1. Om du vill ändra logotypen ersätter du standardfilen `aem_icon.png` med den anpassade `aem_icon.png` filen.
1. Bygg och kör appen AEM Forms på en Windows-enhet.
