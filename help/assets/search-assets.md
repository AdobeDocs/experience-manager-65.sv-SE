---
title: Söka efter digitala resurser och bilder i Adobe Experience Manager
description: Lär dig hur du hittar de resurser du behöver i Adobe Experience Manager genom att använda panelen Filter och hur du använder de resurser som visas i sökningen.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Söka efter resurser i Adobe Experience Manager {#search-assets-in-aem}

Adobe Experience Manager Assets erbjuder robusta metoder för resursidentifiering som hjälper er att uppnå högre innehållshastighet. Teamen minskar time to market med sömlös, intelligent sökupplevelse med hjälp av färdiga funktioner och anpassade metoder. Att söka resurser är centralt för användningen av ett digitalt resurshanteringssystem - oavsett om det är avsett för kreativa användare, för robust hantering av resurser av företagsanvändare och marknadsförare eller för administration av DAM-administratörer. Enkla, avancerade och anpassade sökningar som du kan utföra via användargränssnittet i Experience Manager Assets eller andra appar och ytor hjälper dig att uppfylla dessa användningsexempel.

Experience Manager Assets har stöd för följande användningsfall och i den här artikeln beskrivs användning, begrepp, konfigurationer, begränsningar och felsökning för dessa användningsfall.

| Söka efter resurser | Konfiguration och administration | Arbeta med sökresultat |
|---|---|---|
| [Grundläggande sökningar](#searchbasics) | [Sökindex](#searchindex) | [Sortera resultat](#sort) |
| [Förstå sökgränssnittet](#searchui) | [Visuell sökning eller likhetssökning](#configvisualsearch) | [Kontrollera egenskaper och metadata för en resurs](#checkinfo) |
| [Sökförslag](#searchsuggestions) | [Obligatoriska metadata](#mandatorymetadata) | [Hämta](#download) |
| [Förstå sökresultat och beteenden](#searchbehavior) | [Ändra sökfaktorer](#searchfacets) | [Massmetadatauppdateringar](#metadataupdates) |
| [Sökrankning och förstärkning](#searchrank) | [Textextrahering](#extracttextupload) | [Smarta samlingar](#collections) |
| [Avancerad sökning: filtrering och sökningens omfattning](#scope) | [Anpassade predikat](#custompredicates) | [Förstå oväntade resultat och felsökning](#troubleshoot-unexpected-search-results-and-issues) |
| [Sök bland andra lösningar och appar](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Varumärkesportal](#brandportal)</li><li>[Experience Manager-datorprogram](#desktopapp)</li><li>[Adobe Stock-bilder](#adobestock)</li><li>[Dynamiska medieresurser](#dynamicmedia)</li></ul> |  |  |
| [Resursväljaren](#assetselector) |  |  |
| [Begränsningar](#limitations) och [tips](#tips) |  |  |
| [Illustrerade exempel](#samples) |  |  |

Sök efter resurser med hjälp av omsökningsfältet högst upp i Experience Manager-webbgränssnittet. Gå till **[!UICONTROL Resurser]** > **[!UICONTROL Filer]** i Experience Manager, klicka på sökikonen i det övre fältet, ange söknyckelord och tryck på Retur. Du kan också använda kortkommandot / (snedstreck) för att öppna Omnissearch-fältet. Plats:Resurser är förmarkerade för att begränsa sökningarna till DAM-resurser. Experience Manager ger förslag när du börjar skriva ett söknyckelord.

Använd panelen **[!UICONTROL Filter]** om du vill begränsa sökningen genom att filtrera sökresultaten baserat på olika alternativ (prediktiv), t.ex. filtyp, filstorlek, senaste ändringsdatum, status för mediefilen, information om insikter och Adobe Stock-licensiering. Administratörerna kan anpassa filterpanelen och lägga till eller ta bort sökpredikt med hjälp av sökfaktorer. Filtret [!UICONTROL Filtyp] på panelen [!UICONTROL Filter] har kryssrutor för olika lägen. Om du inte markerar alla kapslade predikat (eller format) markeras därför kryssrutorna på första nivån delvis.

Sökfunktionen i Experience Manager stöder sökning efter samlingar och sökning efter resurser i en samling. Se [söksamlingar](/help/assets/managing-collections-touch-ui.md).

## Förstå sökgränssnittet {#searchui}

Bekanta dig med sökgränssnittet och de tillgängliga åtgärderna.

![Förstå gränssnittet för Experience Manager Assets-sökresultat](assets/aem_search_results.png)

*Bild: Förstå gränssnittet för Experience Manager Assets-sökresultat*

**S.** Spara sökningen som en smart samling. **B.** Filter eller predikat som begränsar sökresultaten. **C.** Visa filer, mappar eller båda. **D.** Klicka på Filter för att öppna eller stänga den vänstra rutan. **E.** Sökplatsen är DAM. **F.** Omsökningsfält med användardefinierat söknyckelord. **G.** Välj inlästa sökresultat. **H.** Antal visade sökresultat av totalt antal sökresultat. **Jag.** Stäng sökning **J.** Växla mellan kortvyn och listvyn.

### Dynamiska sökfaktorer {#dynamicfacets}

Du kan identifiera önskade resurser snabbare från sökresultatsidan med det dynamiskt uppdaterade antalet förväntade sökresultat i sökmetoderna. Det förväntade antalet resurser uppdateras även innan sökfiltret används. Genom att se det förväntade antalet mot filtret kan du snabbt och effektivt navigera bland sökresultaten. Mer information finns i [Söka efter resurser i Experience Manager](search-assets.md).

![Se det ungefärliga antalet resurser utan att filtrera sökresultaten i sökfaktorer.](assets/asset_search_results_in_facets_filters.png)

*Bild: Se det ungefärliga antalet resurser utan att filtrera sökresultaten i sökfaktorer*

## Förstå sökresultat och beteenden {#searchbehavior}

### Grundläggande söktermer och sökresultat {#searchbasics}

Du kan köra nyckelordssökningar från OmniSearch-fältet. Nyckelordssökningen är inte skiftlägeskänslig och är en fulltextsökning (i alla vanliga metadatafält). Om mer än ett nyckelord söks efter används standardoperatorn mellan nyckelorden `AND` för standardsökning och det är `OR` när resurserna är smarta taggade.

Resultatet sorteras efter relevans, med början med närmast matchande. För flera nyckelord är mer relevanta resultat de resurser som innehåller båda termerna i sina metadata. I metadata rangordnas nyckelord som visas som smarta taggar högre än nyckelord som visas i andra metadatafält. Med Experience Manager kan du ge en viss sökterm högre vikt. Det går också att [höja rankningen](#searchrank) för vissa målresurser för specifika söktermer.

För att snabbt hitta relevanta resurser innehåller det avancerade gränssnittet funktioner för filtrering, sortering och markering. Du kan filtrera resultat baserat på flera villkor och se antalet sökningar efter olika filter. Du kan också köra sökningen igen genom att ändra frågan i fältet Omnissearch. När du ändrar söktermer eller filter används de andra filtren för att bevara sökkontexten.

När resultatet är många resurser visas de första 100 i kortvyn och 200 i listvyn. När användare rullar läses fler resurser in. Detta för att förbättra prestandan.

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

Ibland kan du se oväntade resurser i sökresultaten. Mer information finns i [oväntade resultat](#troubleshoot-unexpected-search-results-and-issues).

Experience Manager kan söka i många filformat och sökfiltren kan anpassas efter företagets behov. Kontakta administratören för att få veta vilka sökalternativ som är tillgängliga för DAM-databasen och vilka begränsningar ditt konto har.

### Resultat med och utan förbättrade smarta taggar {#withsmarttags}

Som standard kombineras söktermerna i Experience Manager Search med en AND-sats. Du kan till exempel söka efter nyckelordskvinna som springer. Som standard visas endast resurser med både kvinna och nyckelord som körs i metadata i sökresultatet. Samma beteende bevaras när specialtecken (punkter, understreck eller streck) används med nyckelorden. Följande sökfrågor returnerar samma resultat:

* `woman running`
* `woman.running`
* `woman-running`

Frågan `woman -running` returnerar emellertid resurser utan `running` metadata.
Om du använder smarta taggar läggs en extra `OR` sats till för att hitta någon av söktermerna som de använda smarta taggarna. En resurs som är taggad med antingen `woman` eller `running` med smarta taggar visas också i en sådan sökfråga. Sökresultaten är en kombination av

* Resurser med `woman` och `running` nyckelord i metadata (standardbeteende).

* Resurser som är smarta och taggade med något av nyckelorden (beteendet Smarta taggar).

### Sök efter förslag medan du skriver {#searchsuggestions}

När du börjar skriva nyckelord föreslår Experience Manager möjliga söknyckelord eller fraser. Förslagen baseras på metadata för de befintliga resurserna. Experience Manager indexerar alla metadatafält som kan vara till hjälp vid sökningen. Systemet använder värdena från följande metadatafält för att ge sökförslag. Om du vill ge sökförslag bör du överväga att fylla i följande fält med lämpliga nyckelord:

* Resurstaggar. (kartor till `jcr:content/metadata/cq:tags`)
* Resursrubrik. (kartor till `jcr:content/metadata/dc:title`)
* Resursbeskrivning. (kartor till `jcr:content/metadata/dc:description`)
* Titel i JCR-databasen. Värdet kan mappas till Resursrubrik. (kartor till `jcr:content/jcr:title`)
* Beskrivning i JCR-databasen. Värdet kan mappas till tillgångsbeskrivningen. (kartor till `jcr:content/jcr:description`)

Om du vill få förslag på fler än ett söknyckelord fortsätter du att skriva alla nyckelord utan att markera något förslag för ett nyckelord.

![Skriv in flera nyckelord för att visa förslag som passar alla](assets/search_suggestionsmanykeywords.gif)

*Bild: Skriv in flera nyckelord för att visa förslag som passar alla*

### Sök efter rankning och förstärkning {#searchrank}

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. Matchningar av `woman running` i de olika metadatafälten.
1. Matchar `woman running` i smarta taggar.
1. Matchar `woman` eller matchar `running` i smarta taggar.

Du kan förbättra nyckelordens relevans för vissa resurser för att öka sökningen baserat på nyckelorden. Det innebär att de bilder som du befordrar särskilda nyckelord för visas högst upp i sökresultatet när du söker baserat på dessa nyckelord.

1. Öppna egenskapssidan för resursen i Assets-gränssnittet. Klicka på **[!UICONTROL Avancerat]** och klicka/tryck på **[!UICONTROL Lägg till]** under **[!UICONTROL Upphöjd för att söka efter nyckelord]**.
1. I rutan **[!UICONTROL Sök efter]** ökning anger du ett nyckelord som du vill öka sökningen efter bilden för och klickar/trycker sedan på **[!UICONTROL Lägg till]**. Du kan ange flera nyckelord på samma sätt.
1. Klicka/tryck på **[!UICONTROL Spara och stäng]**. Den resurs som du befordrade för det här nyckelordet visas bland de översta sökresultaten.

Du kan använda detta till din fördel genom att öka rankningen för vissa resurser i sökresultaten för nyckelordet target. Se exempelvideon nedan. Mer information finns i [Sök i Experience Manager](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Förstå hur sökresultaten rangordnas och hur rangordningen kan påverkas.*

## Avancerad sökning {#scope}

I Experience Manager finns olika metoder, till exempel filter, som används för de sökda resurserna, så att du snabbare kan hitta de önskade resurserna. Nedan beskrivs några vanliga metoder. Några [illustrerade exempel](#samples) visas nedan.

**Sök efter filer eller mappar**: Se antingen filer, mappar eller båda i sökresultaten. På **[!UICONTROL filterpanelen]** kan du välja lämpligt alternativ. Se [sökgränssnitt](#searchui).

**Sök efter resurser i en mapp**: Du kan begränsa sökningen till en viss mapp. Lägg till en mappsökväg på panelen **[!UICONTROL Filter]** . Du kan bara markera en mapp i taget.

![Begränsa sökresultaten till en mapp genom att lägga till en mappsökväg i panelen Filter](assets/search_folder_select.gif)

*Bild: Begränsa sökresultaten till en mapp genom att lägga till en mappsökväg i panelen Filter*

### Söka efter liknande bilder {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. Experience Manager visar de smarta taggade bilderna från DAM-databasen som liknar den bild som användaren har valt. Läs [Så här konfigurerar du likhetssökning](#configvisualsearch).

![Söka efter liknande bilder med hjälp av alternativet i kortvyn](assets/search_find_similar.png)

*Bild: Söka efter liknande bilder med hjälp av alternativet i kortvyn*

### Adobe Stock-bilder {#adobestock}

I Experience Managers användargränssnitt kan användare söka efter [Adobe Stock-mediefiler](/help/assets/aem-assets-adobe-stock.md) och licensiera de mediefiler som behövs. Lägg till `Location: Adobe Stock` i omsökningsfältet. Du kan också använda panelen Filter för att hitta alla licensierade eller olicensierade mediefiler eller söka efter en viss mediefil med hjälp av Adobe Stock-filnumret.

### Dynamiska medieresurser {#dmassets}

Du kan filtrera efter dynamiska mediabilder genom att välja **[!UICONTROL Dynamiska media]** > **[!UICONTROL Uppsättningar]** på panelen **[!UICONTROL Filter]** . Den filtrerar och visar resurser som bilduppsättningar, karuseller, blandade medieuppsättningar och rotationsuppsättningar.

### Söka med specifika värden i metadatafält {#gqlsearch}

Du kan söka efter resurser baserat på exakta värden för specifika metadatafält, som titel, beskrivning och författare. Funktionen för fulltextsökning i GQL hämtar endast resurser vars metadatavärde exakt matchar din sökfråga. Namnen på egenskaperna (till exempel författare, titel och så vidare) och värdena är skiftlägeskänsliga.

| Metadatafält | Facet value and usage |
|---|---|
| Titel | title:John |
| Originalformat | skapare:John |
| Plats | plats:NA |
| Beskrivning | description:&quot;Sample Image&quot; |
| Skapare | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
| Copyright-ägare | copyrightowner:&quot;Adobe Systems&quot; |
| Medarbetare | medarbetare:John |
| Användningsvillkor | usageterms:&quot;CopyRights Reserved&quot; |
| Skapad | skapad:YYY-MM-DDTHH |
| Utgångsdatum | förfaller:ÅÅÅ-MM-DDTHH |
| I tid | ontime:YYYY-MM-DDTHH |
| Off time | offtime:YYYY-MM-DDTHH |
| Range of time(expires dateontime,offtime) | facet field : lowerbound..upperbound |
| Bana | /content/dam/&lt;folder name> |
| PDF Title | pdftitle:&quot;Adobe Document&quot; |
| Ämne | subject:&quot;Training&quot; |
| Tags | taggar:&quot;Plats och resa&quot; |
| Typ | type:&quot;image\png&quot; |
| Bildens bredd | width:lowerbound..upperbound |
| Bildens höjd | height:lowerbound..upperbound |
| Person | person:John |

Egenskapernas sökväg, gräns, storlek och sorteringsordning kan inte vara ORed med någon annan egenskap.

Nyckelordet för en användargenererad egenskap är dess fältetikett i egenskapsredigeraren i gemener, med borttagna blanksteg.

Here are some examples of search formats for complex queries:

* Så här visar du alla resurser med flera facets-fält (till exempel: title=John Doe and creator tool = Adobe Photoshop): `tiltle:"John Doe" creatortool : Adobe*`
* To display all assets when the facets value is not a single word but a sentence (for example: title=Scott Reynolds): `title:"Scott Reynolds"`
* To display assets with multiple values of a single property (for example: title=Scott Reynolds or John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Så här visar du resurser med egenskapsvärden som börjar med en viss sträng (till exempel: heter Scott Reynolds): `title:Scott*`
* To display assets with property values ending with a specific string (for example: title is Scott Reynolds): `title:*Reynolds`
* Så här visar du resurser med ett egenskapsvärde som innehåller en viss sträng (till exempel: title = Basel Meeting Room): `title:*Meeting*`
* To display assets that contain a particular string and have a specific property value (for example: search for string Adobe in assets having title=John Doe): `*Adobe* title:"John Doe"`

## Search assets from other Experience Manager offerings or interfaces {#beyondomnisearch}

Adobe Experience Manager connects DAM repository to various other Experience Manager solutions to provide faster access to digital assets and streamline the creative workflows. Any asset discovery starts with browse or search. The search behavior largely remains the same across the various surfaces and solutions. Some search methods change as the target audience, the use cases, and the user interface vary across the Experience Manager solutions. The specific methods are documented for the individual solutions at the links below. The universally applicable tips and behaviors are documented in this article.

### Search assets from Adobe Asset Link panel {#aal}

Using Adobe Asset Link, the creative professionals can now access content stored in Experience Manager Assets, without leaving the supported Adobe Creative Cloud apps. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in the Creative Cloud apps: Photoshop, Illustrator, and InDesign. Asset Link also allows users to search visually similar results. The visual search display results are powered by Adobe Sensei&#39;s machine learning algorithms and help users find aesthetically similar images. See [search and browse assets](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) using Adobe Asset Link.

### Search assets in Experience Manager desktop app {#desktopapp}

Creative professionals use the desktop app to make the Experience Manager Assets easily searchable and available on their local desktop (Win or Mac). Creatives can easily reveal the desired assets in Mac Finder or Windows Explorer, opened in desktop applications, and changed locally - the changes are saved back to Experience Manager with a new version created in the repository. The application supports basic searches using one or more keywords, * and ? wildcards, and AND operator. Se [Bläddra bland, söka efter och förhandsgranska resurser](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) i skrivbordsappen.

### Sök efter resurser i varumärkesportalen {#brandportal}

Affärsanvändare och marknadsförare använder Brand Portal för att effektivt och säkert dela godkänt digitalt material med interna team, partners och återförsäljare. Se [Sök resurser på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Sök efter Adobe Stock-bilder {#adobestock-1}

I Experience Managers användargränssnitt kan användarna söka efter Adobe Stock-mediefiler och licensiera de mediefiler som behövs. Lägg till `Location: Adobe Stock` i Omnissearch-fältet. Du kan också använda **[!UICONTROL filterpanelen]** för att hitta alla licensierade eller olicensierade mediefiler eller söka efter en viss mediefil med hjälp av Adobe Stock-filnumret. Se [Hantera Adobe Stock-bilder i Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Sök efter Dynamic Media-resurser {#dynamicmedia}

Du kan filtrera efter dynamiska mediabilder genom att välja **[!UICONTROL Dynamiska media]** > **[!UICONTROL Uppsättningar]** på panelen **[!UICONTROL Filter]** . Den filtrerar och visar resurser som bilduppsättningar, karuseller, blandade medieuppsättningar och rotationsuppsättningar. När författarna redigerar webbsidor kan de söka efter uppsättningar inifrån Content Finder. Det finns ett filter för uppsättningar på en snabbmeny.

### Söka efter resurser i Content Finder vid redigering av webbsidor {#contentfinder}

Authors can use Content Finder to search the DAM repository for the relevant assets and use the assets in the web pages they create. Upphovsmannen kan också använda funktionen Anslutna resurser för att söka efter resurser som är tillgängliga i en fjärrdistribution av Experience Manager. Authors can then use these assets in web pages on a local Experience Manager deployment. See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Search collections {#collections}

Experience Manager search capability supports searching for collections and searching for assets within a collection. See [search collections](/help/assets/managing-collections-touch-ui.md).

## Asset Picker {#assetselector}

Asset Picker lets you search, filter, and browse the DAM assets in a special way. Asset Picker is available at `https://[aem-server]:[port]/aem/assetpicker.html`. You can fetch the metadata of assets that you select using this functionality. You can launch it with supported request parameters, such as asset type (image, video, text) and selection mode (single or multiple selections). These parameters set the context of the asset Picker for a particular search instance and remains intact throughout the selection.

Resursväljaren använder HTML5- `Window.postMessage` meddelandet för att skicka data för den valda resursen till mottagaren. Resursväljaren fungerar bara i bläddringsläget och fungerar bara med omsökningsresultatsidan.

Du kan skicka följande frågeparametrar i en URL för att starta resursväljaren i ett visst sammanhang:

| Namn | Värden | Exempel | Syfte |
|---|---|---|---|
| resurssuffix (B) | Mappsökväg som resurssuffix i URL:[https://localhost:4502/aem/assetpicker.html/&lt;mappsökväg>](https://localhost:4502/aem/assetpicker.html) | Om du vill starta resursväljaren med en viss mapp markerad, t.ex. med mappen `/content/dam/we-retail/en/activities` markerad, ska URL:en ha formatet: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Om du vill att en viss mapp ska väljas när resursväljaren startas, skickar du den som ett resurssuffix. |
| läge | en, flera | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | In multiple mode, you can select several assets simultaneously using the asset selector. |
| mimeType | mimtyp(er) (`/jcr:content/metadata/dc:format`) av en resurs (jokertecken stöds också) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | Use it to filter assets based on MIME type(s) |
| dialog | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Använd de här parametrarna för att öppna resursväljaren som Granite-dialogrutan. This option is only applicable when you launch the asset selector through Granite Path Field, and configure it as pickerSrc URL. |
| assettype (S) | bilder, dokument, multimedia, arkiv | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Använd det här alternativet om du vill filtrera resurstyper baserat på det skickade värdet. |
| root | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | Use this option to specify the root folder for the asset selector. I det här fallet kan du bara välja underordnade resurser (direkt/indirekt) under rotmappen. |

Gå till `https://[aem_server]:[port]/aem/assetpicker`resursväljarens gränssnitt. Navigera till önskad mapp och markera en eller flera resurser. Du kan också söka efter den önskade resursen i rutan Sök, tillämpa det filter som behövs och sedan markera den.

![Bläddra och markera resurs i resursväljaren](assets/assetpicker.png)

*Bild: Bläddra och markera resurs i resursväljaren*

## Begränsningar {#limitations}

Sökfunktionen i Experience Manager Assets har följande begränsningar:

* Ange inget radavståndsutrymme i sökfrågan, annars fungerar inte sökningen.
* Experience Manager kan fortsätta att visa söktermen efter att du har valt egenskaper för en resurs bland sökresultaten och sedan avbrutit sökningen. <!-- (CQ-4273540) -->
* När du söker efter mappar, filer och mappar kan sökresultaten inte sorteras efter någon parameter.
* Om du trycker på retur utan att skriva något i omsökningsfältet returnerar Experience Manager bara en lista med filer och inte mappar. Om du söker specifikt efter mappar utan att använda ett nyckelord returneras inga resultat i Experience Manager.
* Använd alternativet **[!UICONTROL Markera alla]** i det övre högra hörnet av söksidan för att välja de sökbara resurserna. Experience Manager visar först 100 resurser i kortvyn och 200 resurser i listvyn. Fler resurser läses in när du bläddrar i sökresultaten. Du kan välja fler resurser än de inlästa resurserna. Antalet markerade resurser visas i det övre högra hörnet på sökresultatsidan. Du kan arbeta med markeringen, till exempel hämta de markerade resurserna, uppdatera metadataegenskaperna i grupp för de markerade resurserna eller lägga till de markerade resurserna i en samling. När fler resurser är markerade än vad som visas tillämpas en åtgärd antingen på alla markerade resurser eller så visas antalet resurser som åtgärden används på i en dialogruta. Om du vill tillämpa en åtgärd på de resurser som inte lästes in måste du se till att alla resurser är uttryckligen markerade.

Visuell sökning eller likhetssökning har följande begränsningar:

* Visuell sökning fungerar bäst med större databaser. While there is no minimum number of images required for good results, the quality of matches with a few images may not be as good as the matches from a large repository.
* Du kan inte ändra modell eller utbilda Experience Manager för att hitta liknande bilder. Modellen ändras inte om du till exempel lägger till eller tar bort smarta taggar för ett fåtal resurser. Resurserna tas inte med i de visuellt liknande sökresultaten.

Sökfunktionen kan ha prestandabegränsningar i följande scenarier:

* Kortvyn har en snabbare inläsningstid jämfört med listvyn för att visa sökresultaten.

## Söktips {#tips}

* När du övervakar granskningsstatusen för resurser ska du använda lämpligt alternativ för att hitta vilka resurser som är godkända eller vilka resurser som väntar på godkännande.
* Använd Insights-predikatet för att söka efter resurser som stöds baserat på användningsstatistik från olika Creative-program. Användningsdata grupperas under Användningspoäng, Impressions, Clicks och Media-kanaler där resurserna visas i kategorier.
* Använd kryssrutan **[!UICONTROL Markera alla]** för att välja de sökda resurserna. Experience Manager visar först 100 resurser i kortvyn och 200 resurser i listvyn. Fler resurser läses in när du bläddrar i sökresultaten. Du kan välja fler resurser än de inlästa resurserna. Antalet markerade resurser visas i det övre högra hörnet på sökresultatsidan. Du kan arbeta med markeringen, till exempel hämta de markerade resurserna, uppdatera metadataegenskaperna i grupp för de markerade resurserna eller lägga till de markerade resurserna i en samling. När fler resurser är markerade än vad som visas tillämpas en åtgärd antingen på alla markerade resurser eller så visas antalet resurser som åtgärden används på i en dialogruta. Om du vill tillämpa en åtgärd på de resurser som inte lästes in måste du se till att alla resurser är uttryckligen markerade.
* Mer information om hur du söker efter resurser som inte innehåller de obligatoriska metadata finns i [obligatoriska metadata](#mandatorymetadata).
* Alla metadatafält används för sökningen. En allmän sökning, som att söka efter 12, ger vanligtvis många resultat. For better results, use double (not single) quotes or ensure that the number is contiguous to a word without a special character (for example *shoe12*).
* Full text search supports operators such as -, ^, and so on. To search these letters as string literals, enclose the search expression in double quotes. For example, use &quot;Notebook - Beauty&quot; instead of Notebook - Beauty.
* If the search results are too many, limit the [scope of search](#scope) to zero-in on the desired assets. Det fungerar bäst om du har en aning om hur du ska söka efter de önskade resurserna, till exempel en viss filtyp, en viss plats, specifika metadata och så vidare.

* **Taggning**: Taggar hjälper dig att kategorisera resurser som du kan bläddra bland och söka efter mer effektivt. Tagging helps in propagating the appropriate taxonomy to other users and workflows. Experience Manager offers methods to automatically tag assets using Adobe Sensei&#39;s artificially intelligent services that keep getting better at tagging your assets with usage and training. When you search for assets, the smart tags are factored in if the feature is enabled on your account. It works alongside the in-built search functionality. Se [sökbeteende](#searchbehavior). To optimize the order in which the search results are displayed, you can [boost the search ranking](#searchrank) of a few select assets.

* **Indexering**: Endast indexerade metadata och resurser returneras i sökresultatet. For better coverage and performance, ensure proper indexing and follow the best practices. Se [indexering](#searchindex).

## Några exempel som illustrerar sökning {#samples}

Använd citattecken runt nyckelord för att hitta resurser som innehåller den exakta frasen i exakt den ordning som anges av användaren.

![Sökbeteende med och utan citattecken](assets/search_with_quotes.gif)

*Bild: Sökbeteende med och utan citattecken*

**Sök med asterisk som jokertecken**: Om du vill bredda sökningen använder du en asterisk före eller efter sökordet för att matcha ett valfritt antal tecken. Om du till exempel söker efter en körning utan asterisk returneras inga resurser som innehåller någon variant av ordet (inklusive i metadata). En asterisk ersätter ett valfritt antal tecken. Till exempel,

* `run` returnerar resurser med nyckelordet exakt run
* `run*` returnerar resurser som körs, körs, körs och så vidare.
* `*run` returnerar utfall, kör igen och så vidare.
* `*run*` returns all possible combinations.

![Illustrating use of asterisk wildcard in Asset search using an example](assets/search_with_asterisk_run.gif)

*Figure: Illustrating use of asterisk wildcard in Asset search using an example*

**Search with question mark wildcard**: To broaden the search, use one or more &#39;?&#39; tecken som matchar det exakta antalet tecken. I följande bild

* `run???` frågan matchar inte någon resurs.

* `run????` frågan matchar ordet `running` med fyra tecken efter `run`.

* `??run` frågan matchar ordet `rerun` med två tecken före `run`.

![Illustration use of question mark wildcard in Asset search using a example](assets/search_with_questionmark_run.gif)

*Bild: Illustration use of question mark wildcard in Asset search using a example*

**Exkludera ett nyckelord**: Använd streck för att söka efter resurser som inte innehåller något nyckelord. Frågan returnerar till exempel resurser som innehåller `running -shoe` men inte `running``shoe`. På samma sätt returnerar frågan resurser som innehåller `camp -night` men inte `camp` `night`. Observera att `camp-night` frågan returnerar resurser som innehåller både `camp` och `night`.

![Användning av bindestreck för att söka efter resurser som inte innehåller ett exkluderat nyckelord](assets/search_dash_exclude_keyword.gif)

*Bild: Användning av bindestreck för att söka efter resurser som inte innehåller ett exkluderat nyckelord*

## Konfigurations- och administrationsuppgifter som rör sökfunktioner {#configadmin}

### Sök i indexkonfigurationer {#searchindex}

Resursidentifiering bygger på indexering av DAM-innehåll, inklusive metadata. Snabbare och exaktare tillgångsidentifiering bygger på optimerad indexering och lämpliga konfigurationer. Se [sökindex](/help/assets/performance-tuning-guidelines.md#search-indexes), [frågor och indexering](/help/sites-deploying/queries-and-indexing.md)samt [metodtips](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Visuell sökning eller likhetssökning {#configvisualsearch}

Visuell sökning använder smart taggning och kräver Experience Manager 6.5.2.0 eller senare. Följ de här stegen när du har konfigurerat funktionen för smart taggning.

1. In Experience Manager CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

   * `costPerEntry` type-egenskap `Double` med värdet `10`.

   * `costPerExecution` type-egenskap `Double` med värdet `2`.

   * `refresh` property of type `Boolean` with the value `true`.
   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

   * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

   * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

   * Add `propertyIndex` property of type `Boolean` with the value of `true`.

   * Add `useInSimilarity` property of type `Boolean` with the value `true`.
   Spara ändringarna.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your Experience Manager repository. See [how to configure smart tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Spara ändringarna.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Spara alla ändringar.

For related information, see [understand smart tags in Experience Manager](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html) and [how to manage smart tags](/help/assets/managing-smart-tags.md).

### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, Experience Manager Assets offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administratörer kan anpassa filterpanelen för att ändra standardmetoderna med hjälp av inbyggda predikat. Experience Manager innehåller en bra samling inbyggda predikat och en redigerare som anpassar ansiktena. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure Experience Manager to extract the text from the assets when users upload assets, such as PSD or PDF files. Experience Manager indexerar den extraherade texten och hjälper användarna att söka efter dessa resurser baserat på den extraherade texten. Se [Överföra resurser](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### Anpassade predikat för att filtrera sökresultat {#custompredicates}

Predikat används för att skapa ansikten. Administratörer kan anpassa sökmetoderna på panelen Filter med förkonfigurerade predikat. Dessa predikat kan anpassas med hjälp av övertäckningar. Se [Skapa anpassade prediktiv](/help/assets/searchx.md).

Du kan söka efter digitala resurser baserat på en eller flera av följande egenskaper. Filter som gäller för vissa av dessa egenskaper är som standard tillgängliga och vissa andra filter kan skapas för att användas på andra egenskaper.

| Sökfält | Sök egenskapsvärden |
|---|---|
| MIME-typer | Images, Documents, Multimedia, Archives, or Other. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| Filstorlek | Small, Medium, or Large. |
| Publish Status | Published or Unpublished. |
| Approved Status | Approved or Rejected. |
| Orientering | Horizontal, Vertical, or Square. |
| Format | Color, or Black &amp; White. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Videobredd | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| Audio Bitrate | Anges som lägsta och högsta värde. Value is stored in the metadata of video renditions only. |

## Work with asset search results {#aftersearch}

Once you see some searched assets that match your criteria, you can do the following typical tasks with or take the following actions on these search results:

* View metadata properties and other information.
* Download one or more assets.
* Use Desktop Actions to open these assets in the desktop app.
* Skapa smarta samlingar.

### Sort searched results {#sort}

Om du sorterar sökresultatet hittar du snabbare den resurs du behöver. Sorting search results works in list view and only when you select **[!UICONTROL [Files](#searchui)]**from the**[!UICONTROL  Filters ]**panel. Experience Manager Assets använder sortering på serversidan för att snabbt sortera alla resurser (oavsett hur många) i en mapp eller resultaten av en sökfråga. Sortering på serversidan ger snabbare och exaktare resultat än sortering på klientsidan.

I listvyn kan du sortera sökresultaten på samma sätt som du kan sortera resurser i valfri mapp. Sorting works on these columns -- Name, Title, Status, Dimensions, Size, Rating, Usage, (Date) Created, (Date) Modified, (Date) Published, Workflow, and Checked out.

For limitations of sort functionality, see [limitations](#limitations).

### Check detailed information of an asset {#checkinfo}

Du kan kontrollera detaljerad information om en sökresurs från sökresultatsidan.

To see all metadata of an asset, select the asset and click **[!UICONTROL properties]** from the toolbar.

Om du vill kontrollera kommentarerna för en resurs eller versionshistoriken för en resurs klickar du på resursen för att öppna en stor förhandsvisning. Open timeline in the left rail and select **[!UICONTROL Comments]** or **[!UICONTROL Versions]**. Du kan också sortera tidslinjeaktiviteter, som kommentarer eller versioner, i kronologisk ordning.

![Sortera tidslinjeposter för en sökresurs](assets/sort_timeline_search_results.gif)

*Bild: Sortera tidslinjeposter för en sökresurs*

### Hämta sökbara resurser {#download}

You can download the searched assets and their renditions just as you download regular assets from folders. Select one or more assets from the search results and click **[!UICONTROL Download]** from the toolbar.

### Uppdatera metadataegenskaper gruppvis {#metadataupdates}

Det går att göra satsvisa uppdateringar av de gemensamma metadatafälten för flera resurser. Välj en eller flera resurser från sökresultaten. Click **[!UICONTROL Properties]** from the toolbar and update the metadata as required. Click **[!UICONTROL Save and Close]** when done. The previously existing metadata in the updated fields is overwritten.

För resurser som är tillgängliga i en enda mapp eller en samling är det enklare att [uppdatera metadata gruppvis](/help/assets/managing-multiple-assets.md) utan att använda sökfunktionen. För resurser som är tillgängliga i olika mappar eller matchar ett gemensamt villkor är det snabbare att uppdatera metadata i grupp via sökning.

### Smarta samlingar {#collections-1}

En samling är en ordnad uppsättning resurser som kan innehålla resurser från olika platser, eftersom samlingar bara innehåller referenser till dessa resurser. Samlingar är av följande två typer:

* En statisk referenslista med resurser, mappar och andra samlingar.
* En dynamisk lista (smart samling) som fyller i resurser i samlingen baserat på sökvillkor.

Du kan skapa smarta samlingar baserat på sökvillkoren. På **[!UICONTROL filterpanelen]** väljer du **[!UICONTROL Filer]** och klickar på **[!UICONTROL Spara smart samling]**. Läs mer i [Hantera samlingar](/help/assets/managing-collections-touch-ui.md).

## Felsöka oväntade sökresultat och problem {#troubleshoot-unexpected-search-results-and-issues}

| Fel, problem, symtom | Möjlig orsak | Möjlig korrigering eller förståelse för problemet |
|---|---|---|
| Felaktiga resultat vid sökning efter resurser som saknar metadata | När du söker efter resurser som saknar obligatoriska metadata kan Experience Manager visa resurser som har giltiga metadata. Resultatet baseras på indexerad metadataegenskap. | När metadata har uppdaterats krävs omindexering för att återspegla rätt status för resursens metadata. Se [obligatoriska metadata](metadata-schemas.md#define-mandatory-metadata). |
| För många sökresultat | En stor sökparameter. | Överväg att begränsa [sökningens](#scope)omfattning. Smarta taggar kan ge fler sökresultat än du förväntade dig. Se [sökbeteendet med smarta taggar](#withsmarttags). |
| Orelaterade eller delvis relaterade sökresultat | Sökbeteendet ändras med smart taggning. | Förstå [hur sökningen ändras efter smart taggning](#withsmarttags). |
| Inga förslag för resurser som fylls i automatiskt | Nyligen överförda resurser har ännu inte indexerats. Metadata är inte omedelbart tillgängliga som förslag när du börjar skriva ett söknyckelord i omsökningsfältet. | Experience Manager Assets väntar tills en timeout-period har gått ut (en timme som standard) innan ett bakgrundsjobb körs för att indexera metadata för alla nyligen överförda eller uppdaterade resurser och lägger sedan till metadata i listan med förslag. |
| Inga sökresultat | <ul><li>Det finns inga resurser som matchar din fråga.</li><li>Du lade till ett tomt utrymme före sökfrågan.</li><li>Ett metadatafält som inte stöds innehåller nyckelordet som du söker efter.</li><li>I tid och offline konfigureras resursen och sökningen gjordes när resursen var ledig.</li></ul> | <ul><li>Sök med ett annat nyckelord. Du kan även använda smart taggning för att förbättra sökresultaten.</li><li>Det är en [känd begränsning](#limitations).</li><li>Alla metadatafält beaktas inte vid sökningar. Se [omfång](#scope).</li><li>Sök senare eller ändra på- och avtidsinställningarna för de nödvändiga resurserna.</li></ul> |
| Sökfilter/ predikat är inte tillgängligt | <ul><li>Sökfiltret är inte konfigurerat.</li><li>Den är inte tillgänglig för din inloggning.</li><li>(Sannolikheten är mindre) Sökalternativen är inte anpassade efter den distribution du använder.</li></ul> | <ul><li>Kontakta administratören för att kontrollera om sökanpassningarna är tillgängliga eller inte.</li><li>Kontakta administratören för att kontrollera om ditt konto har behörighet att använda anpassningen.</li><li>Kontakta administratören och kontrollera tillgängliga anpassningar för den Experience Manager Assets-distribution som du använder.</li></ul> |
| När du söker efter visuellt liknande bilder saknas en förväntad bild | <ul><li>Bilden är inte tillgänglig i Experience Manager.</li><li>Bilden är inte indexerad. Vanligtvis när den nyligen har överförts.</li><li>Bilden är inte smart taggad.</li></ul> | <ul><li>Lägg till bilden i Experience Manager Assets.</li><li>Kontakta administratören om du vill indexera om databasen. Se även till att du använder rätt index.</li><li>Kontakta administratören om du vill tagga de relevanta resurserna på ett smart sätt.</li></ul> |
| När du söker efter visuellt liknande bilder visas en irrelevant bild | Visuell sökfunktion. | Experience Manager visar så många potentiellt relevanta resurser som möjligt. Mindre relevanta bilder, om sådana finns, läggs till i resultatet men med en lägre sökrankning. Kvaliteten på matchningarna och relevansen hos de sökda resurserna minskar när du bläddrar nedåt i sökresultaten. |
| När du väljer och arbetar med sökresultat används inte alla sökresurser | Med alternativet [!UICONTROL Markera alla] markeras endast de första 100 sökresultaten i kortvyn och de första 200 sökresultaten i listvyn. |  |

>[!MORELIKETHIS]
>
>* [Implementeringshandbok för Experience Manager-sökningar](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Avancerad konfiguration av predikat för sökning av flera värden och taggar](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [Konfigurera smart översättningssökning](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

