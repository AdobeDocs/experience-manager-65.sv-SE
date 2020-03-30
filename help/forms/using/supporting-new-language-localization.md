---
title: Stöd för nya språk för lokalisering av adaptiva formulär
seo-title: Stöd för nya språk för lokalisering av adaptiva formulär
description: Med AEM Forms kan du lägga till nya språk för lokalisering av anpassningsbara formulär. De språkområden som stöds är som standard engelska, franska, tyska och japanska.
seo-description: Med AEM Forms kan du lägga till nya språk för lokalisering av anpassningsbara formulär. De språkområden som stöds är som standard engelska, franska, tyska och japanska.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Stöd för nya språk för lokalisering av adaptiva formulär{#supporting-new-locales-for-adaptive-forms-localization}

## Om språkordlistor {#about-locale-dictionaries}

Lokaliseringen av anpassningsbara formulär bygger på två typer av språkordlistor:

**Formulärspecifik ordlista** innehåller strängar som används i anpassningsbara formulär. Till exempel etiketter, fältnamn, felmeddelanden, hjälpbeskrivningar och så vidare. Den hanteras som en uppsättning XLIFF-filer för varje språkområde och du kan komma åt den på `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Globala ordlistor** Det finns två globala ordlistor, som hanteras som JSON-objekt, i AEM-klientbiblioteket. De här ordlistorna innehåller standardfelmeddelanden, namn på månader, valutasymboler, datum- och tidsmönster osv. Dessa ordlistor finns i CRXDe Lite på /libs/fd/xfaforms/clientlibs/I18N. Dessa platser innehåller separata mappar för varje språkområde. Eftersom globala ordlistor vanligtvis inte uppdateras så ofta, kan webbläsare cachelagra olika JavaScript-filer för varje språkinställning och minska användningen av nätverksbandbredd när olika adaptiva formulär används på samma server.

### Hur lokalisering av anpassningsbara formulär fungerar {#how-localization-of-adaptive-form-works}

När ett anpassat formulär återges identifierar det det begärda språkområdet genom att titta på följande parametrar i den angivna ordningen:

* Begäranparameter `afAcceptLang`Om du vill åsidosätta webbläsarens språkområde för användare kan du skicka parametern request så att språkområdet tvingas att `afAcceptLang` . Följande URL kommer till exempel att tvinga formuläret att återges på japanska språk:
   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Webbläsarens språkområdesuppsättning för användaren, som anges i begäran med hjälp av `Accept-Language` rubriken.

* Språkinställning för användaren som anges i AEM.

När språkområdet har identifierats väljs den formulärspecifika ordlistan i de adaptiva formulären. Om det inte går att hitta den formulärspecifika ordlistan för den begärda språkversionen används den engelska ordlistan (en).

Om det inte finns något klientbibliotek för det begärda språket söker programmet efter språkkoden i klientbiblioteket. Om den begärda språkversionen till exempel är `en_ZA` (sydafrikansk engelska) och klientbiblioteket för `en_ZA` inte finns, kommer den adaptiva formen att använda klientbiblioteket för `en` (engelska), om det finns. Om det inte finns någon av dem används lexikonet för nationella inställningar i det adaptiva formuläret. `en`

## Lägg till lokaliseringsstöd för språk som inte stöds {#add-localization-support-for-non-supported-locales}

AEM Forms har för närvarande stöd för lokalisering av innehåll i adaptiva formulär på engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska (Brasilien), kinesiska (zh-CN), kinesiska (zh-TW) och koreanska (ko-KR).

Så här lägger du till stöd för en ny språkinställning vid körning av adaptiva formulär:

1. [Lägg till en språkinställning i tjänsten GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Lägg till XFA-klientbibliotek för en språkinställning](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Lägg till anpassat formulärklientbibliotek för en språkinställning](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Lägg till språkstöd för ordlistan](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Starta om servern](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Lägga till en språkinställning i tjänsten för guidelokalisering {#add-a-locale-to-the-guide-localization-service-br}

1. Gå till `https://'[server]:[port]'/system/console/configMgr`.
1. Klicka för att redigera **komponenten för guidelokaliseringstjänsten** .
1. Lägg till det språkområde som du vill lägga till i listan över språkområden som stöds.

![GuideLocalizationService](assets/configservice.png)

### Lägg till XFA-klientbibliotek för en språkinställning {#add-xfa-client-library-for-a-locale-br}

Skapa en nod av typen `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, med kategori `xfaforms.I18N.<locale>`och lägg till följande filer i klientbiblioteket:

* **I18N.js** definierar `xfalib.locale.Strings` för `<locale>` enligt definitionen i `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** som innehåller följande:

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Lägg till anpassat formulärklientbibliotek för en språkinställning {#add-adaptive-form-client-library-for-a-locale-br}

Skapa en nod av typen `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, med kategorin `guides.I18N.<locale>` och beroenden som `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` och `guide.common`. &quot;

Lägg till följande filer i klientbiblioteket:

* **i18n.js** defining `guidelib.i18n`, having patterns of &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`for the `typefaces` `<locale>` [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)as Enligt XFA-specifikationerna som beskrivs i¥Locale Set Specification¥. Du kan också se hur den definieras för andra språkområden som stöds i `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definierar `guidelib.i18n.strings` och `guidelib.i18n.LogMessages` för `<locale>` enligt `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** som innehåller följande:

```
i18n.js
LogMessages.js
```

### Lägg till språkstöd för ordlistan {#add-locale-support-for-the-dictionary-br}

Utför bara det här steget om `<locale>` du lägger till inte finns bland `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja``ko-kr`¥.

1. Skapa en `nt:unstructured` nod `languages` under `etc`, om den inte redan finns.

1. Lägg till en strängegenskap med flera värden `languages` till noden, om den inte redan finns.
1. Lägg till `<locale>` standardvärden för nationella inställningar `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`om sådana inte finns.

1. Lägg till egenskapen `<locale>` i värdena för `languages` egenskapen `/etc/languages`.

Fältet `<locale>` visas på `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Starta om servern {#restart-the-server}

Starta om AEM-servern så att de nya språkinställningarna börjar gälla.

## Exempelbibliotek för att lägga till stöd för spanska {#sample-libraries-for-adding-support-for-spanish}

Exempel på klientbibliotek för att lägga till stöd för spanska

[Hämta fil](assets/sample.zip)
