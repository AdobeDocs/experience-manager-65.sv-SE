---
title: Felsök AEM Forms-appen
description: Lär dig mer om vanliga problem med AEM Forms-appen och hur du felsöker dem.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# Felsök AEM Forms-appen {#troubleshoot-aem-forms-app}

I den här artikeln beskrivs de felmeddelanden som kan visas när du skapar en AEM Forms-app och hur du löser dem.

Avsnitten i den här artikeln är:

* [Förlust av bifogade filer för iOS-användare](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [HTML 5-formulärutkast som skickas av arbetsyteanvändare visas inte på portalen](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5-formulär (inte cachelagrade) kan inte läsas in i AEM Forms-appen](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms synkroniseras inte i Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versionen av Gradle stöds inte](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Kompatibilitetsproblem med Gradle- och Android-insticksprogram](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Förlust av bifogade filer för iOS-användare {#attachment-loss-for-ios-users}

AEM Forms-app för iOS som är konfigurerad att synkroniseras med AEM Forms på OSGi stöder endast bilagor på fältnivå. Alla bilagor måste ha unika namn. Om flera bifogade filer har samma namn behålls bara en bifogad fil och alla andra med samma namn går förlorade. Utför följande steg för att förhindra dataförlust för användare på iOS-enheter:

1. På den anslutna servern går du till **Adobe Experience Manager > Verktyg > Åtgärder > Webbkonsol**.
1. Sök och klicka **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]**.
1. I [!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration] dialogruta, aktivera **Gör filnamn unika**.

   If **Gör filnamn unika** om inställningen är inaktiverad förlorar användaren data om de försöker skicka adaptiva formulär med flera bilagor.

1. Klicka **Spara**.

## HTML 5-formulärutkast som skickas av arbetsyteanvändare visas inte på portalen {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

För HTML5-formulär som aktiveras i AEM Forms-appen med **Spara som utkast** Återgivningsprofil i HTML är de sparade utkasten inte synliga för arbetsyteanvändare. Så här visar du sparade utkast av HTML 5-formulär som skickats in av arbetsyteanvändare på portalen:

1. Öppna CRXDE och logga in med administratörsautentiseringsuppgifter.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Klicka på i CRXDE-rotsökvägen i åtkomstkontrollistan under Åtkomstkontroll **+**.
1. I **Lägg till nytt inlägg** klickar du på gruppsökknappen i fältet Huvudnamn.
1. I fältet Namn i dialogrutan Välj huvudnamn skriver du `PERM_WORKSPACE_USER` och klicka **Sök**.
1. Välj `PERM_WORKSPACE_USER` i dialogrutan Välj huvudnamn och klicka på **OK**.
1. I dialogrutan Lägg till nytt inlägg `PERM_WORKSPACE_USER` gruppen är markerad i fältet Principal.

   Aktivera `jcr:read` behörigheter för användargruppen.

1. Klicka **OK**.

## HTML5-formulär (inte cachelagrade) kan inte läsas in i AEM Forms-appen {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

När AEM Forms-appen är ansluten till en äldre version av AEM Forms-servern går det inte att läsa in icke-cachelagrade HTML5-formulär i AEM Forms-appen.

Utför följande steg för att lösa problemet:

1. I författarinstansen går du till **Adobe Experience Manager > Verktyg > Konfigurera Workspace App Offline Service > Konfigurera nu**.
1. I **Offlinetjänst för Workspace-app** sida, klicka **Manuell resurscache**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. I **Manuell resurscache** klickar du på **+** för att lägga till en CRX-sökväg.
1. I **Lägg till en ny resurs** fält, typ: /etc.clientlibs/fd/xfaforms/I18N/en_US.js och klicka **Lägg till**.
1. Klicka **Spara**.

## AEM Forms synkroniseras inte i Windows {#aem-forms-do-not-sync-on-windows}

I AEM Forms App i Windows synkroniseras inte ett formulär med den anslutna servern om sökvägen till formuläret eller någon av dess resurser innehåller fler än eller lika med 256 tecken.

Ändra formulärets sökväg och dess resurser för att minska antalet tecken till färre än 256 tecken.

## Versionen av Gradle stöds inte {#unsupported-version-of-gradle}

**Felmeddelande:** Projektet använder en version av Gradle som inte stöds.

Felmeddelandet visas när du skapar en AEM Forms-app i Android Studio. Problemet inträffar på grund av att en version av Gradle som inte stöds i systemet inte stöds.

**Upplösning:** Klicka **Korrigera inkapsling och återimport av projekt** för att lösa problemet.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Kompatibilitetsproblem med Gradle- och Android-insticksprogram {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Felmeddelande:** Versionerna av plugin-programmet för Android Gradle och Gradle är inte kompatibla.

Felmeddelandet visas när du väljer **Bygg APK** från **Bygge** på Android Studio-användargränssnittet.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**Upplösning:** Öppna **Övertoningsskript** > **gradle-wrapper.properties** och redigera **distributionUrl** -egenskap.

Android Studio-konsolen rekommenderar till exempel att du nedgraderar Gradle-versionen till 3.5. Redigera versionen i **distributionUrl** av **gradle-wrapper.properties** -fil.

Välj **Bygge** > **Bygg APK** igen för att åtgärda felet och generera APK-filen.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
