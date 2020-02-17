---
title: Felsöka appen AEM Forms
seo-title: Felsöka appen AEM Forms
description: Lär dig mer om vanliga problem med appen AEM Forms och hur du felsöker dem.
seo-description: Lär dig mer om vanliga problem med appen AEM Forms och hur du felsöker dem.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Felsöka appen AEM Forms {#troubleshoot-aem-forms-app}

I den här artikeln beskrivs de felmeddelanden som kan visas när du skapar en AEM Forms-app och hur du löser dem.

Avsnitten i den här artikeln är:

* [Förlust av bifogade filer för iOS-användare](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [HTML5-formulärutkast som skickas av arbetsyteanvändare visas inte på portalen](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5-formulär (inte cachelagrade) kan inte läsas in i appen AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms synkroniseras inte i Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versionen av Gradle stöds inte](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Kompatibilitetsproblem med Gradle- och Android-insticksprogram](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Förlust av bifogade filer för iOS-användare {#attachment-loss-for-ios-users}

Appen AEM Forms för iOS som är konfigurerad att synkroniseras med AEM Forms i OSGi stöder endast bilagor på fältnivå. Alla bilagor måste ha unika namn. Om flera bifogade filer har samma namn behålls bara en bifogad fil och alla andra med samma namn går förlorade. Utför följande steg för att förhindra att användare på iOS-enheter drabbas av dataförlust:

1. På den anslutna servern går du till **Adobe Experience Manager > Verktyg > Åtgärder > Webbkonsol**.
1. Sök efter och klicka på **tjänsten** Adaptiv formulärkonfiguration.
1. Aktivera **Gör filnamn unika** i dialogrutan Adaptiv formulärkonfigurationstjänst.

   Om inställningen **Gör filnamn unika** är inaktiverad, kommer användarna att förlora data om de försöker skicka adaptiva formulär med flera bilagor.

1. Click **Save**.

## HTML5-formulärutkast som skickas av arbetsyteanvändare visas inte på portalen {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

För HTML5-formulär som är aktiverade i AEM Forms-appen med **Spara som utkast** -HTML-återgivningsprofil är de sparade utkasten inte synliga för arbetsyteanvändare. Så här visar du sparade utkast av HTML5-formulär som skickats av arbetsyteanvändare på portalen:

1. Öppna CRXDE och logga in med administratörsautentiseringsuppgifter.

   Webbadress: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Klicka på **+** i CRXDE-rotsökvägen i åtkomstkontrollistan under Åtkomstkontroll.
1. I dialogrutan **Lägg till nytt inlägg** klickar du på gruppsökningsknappen i fältet Principal.
1. I fältet Namn i dialogrutan Välj huvudnamn skriver du `PERM_WORKSPACE_USER` och klickar på **Sök**.
1. Markera `PERM_WORKSPACE_USER` gruppen i dialogrutan Välj huvudnamn och klicka på **OK**.
1. I dialogrutan Lägg till nytt inlägg är `PERM_WORKSPACE_USER` gruppen markerad i fältet Huvudnamn.

   Aktivera `jcr:read` behörigheter för användargruppen.

1. Click **OK**.

## HTML5-formulär (inte cachelagrade) kan inte läsas in i appen AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

När appen AEM Forms är ansluten till en äldre version av AEM Forms-servern går det inte att läsa in icke-cachelagrade HTML5-formulär i appen AEM Forms.

Utför följande steg för att lösa problemet:

1. Gå till **Adobe Experience Manager > Verktyg > Konfigurera Workspace App Offline Service > Konfigurera nu**.
1. Klicka på **Manuell resurscache** på sidan Offlinetjänst **** för Workspace-app.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. Klicka på knappen **+** på fliken **Manuell resurscache** för att lägga till en CRX-sökväg.
1. I fältet **Lägg till en ny resurs** skriver du: /etc.clientlibs/fd/xfaforms/I18N/en_US.js och klicka på **Lägg till**.
1. Click **Save**.

## AEM Forms synkroniseras inte i Windows {#aem-forms-do-not-sync-on-windows}

I appen AEM Forms i Windows synkroniseras inte ett formulär med den anslutna servern om sökvägen till formuläret eller någon av dess resurser innehåller fler än eller lika med 256 tecken.

Ändra formulärets sökväg och dess resurser för att minska antalet tecken till färre än 256 tecken.

## Versionen av Gradle stöds inte {#unsupported-version-of-gradle}

**** Felmeddelande: Projektet använder en version av Gradle som inte stöds.

Felmeddelandet visas när du skapar en AEM Forms-app i Android Studio. Problemet inträffar på grund av att en version av Gradle som inte stöds i systemet inte stöds.

**** Upplösning: Klicka på **Korrigera inkapsling och importera projektet** igen för att lösa problemet.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Kompatibilitetsproblem med Gradle- och Android-insticksprogram {#gradle-and-android-gradle-plug-in-compatibility-issues}

**** Felmeddelande: Versionerna av plugin-programmet för Android Gradle och Gradle är inte kompatibla.

Felmeddelandet visas när du väljer alternativet **Skapa APK** på menyn **Skapa** i användargränssnittet i Android Studio.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**** Upplösning: Öppna **filen Gradle Scripts** > **gradle-wrapper.properties** och redigera **egenskapen distributionUrl** .

Android Studio-konsolen rekommenderar till exempel att du nedgraderar Gradle-versionen till 3.5. Redigera versionen i **distributionUrl** för **filen gradle-wrapper.properties** .

Välj **Skapa** > **Skapa APK** igen för att lösa felet och generera APK-filen.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

