---
title: Komponenter för innehållsfragment
description: Adobe Experience Manager (AEM) innehållsfragment skapas och hanteras som sidoberoende resurser
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Komponenter för innehållsfragment{#components-for-content-fragments}

## Komponenter för fragmentredigering {#components-for-fragment-authoring}

>[!CAUTION]
>
>Vi rekommenderar inte att du utökar eller ändrar de faktiska komponenterna som används i Fragment Editor eftersom de fortfarande kan ändras.

Se [API för hantering av innehållsfragment - klientsida](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Komponenter för sidredigering {#components-for-page-authoring}

>[!CAUTION]
>
>The [Kärnkomponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) rekommenderas nu. Se [Utveckla kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) för mer information.
>
>I det här avsnittet beskrivs den ursprungliga komponenten som levererats för användning med innehållsfragment (**Innehållsfragment** i **Allmänt** grupp).

>[!NOTE]
>
>Se även [Innehållsfragment Konfigurera komponenter för återgivning](/help/sites-developing/content-fragments-config-components-rendering.md) för ytterligare information.

Adobe Experience Manager (AEM) innehållsfragment är [skapat och hanterat som sidoberoende resurser](/help/assets/content-fragments/content-fragments.md). Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. [Du kan sedan använda dessa fragment och deras variationer när du redigerar innehållssidorna](/help/sites-authoring/content-fragments.md). Du kan också använda en befintlig innehållsfragmentresurs med [dra den från resursläsaren till sidan](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (som för andra tillgångsbaserade komponenter, t.ex. bildkomponenten). Komponenten för innehållsfragment som inte finns i kartongen visar bara en [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) av det refererade innehållsfragmentet. Med komponentdialogrutan kan du definiera [element, variation och intervall för fragmentstycken](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) som du vill visa på sidan.

>[!NOTE]
>
>Den här innehållskomponenten infördes i AEM 6.2 som en förbättrad version av artikelkomponenten, som har tagits bort.

>[!NOTE]
>
>Innehållsfragment stöds inte i det klassiska användargränssnittet.

### Definition {#definition}

The **Innehållsfragment** -komponenten används för att hålla en referens till ett innehålls fragmentresurs (effektivt förbättrade textresurser). Resurstypen för innehållsfragmentet är:

`dam/cfm/components/contentfragment/contentfragment`

Referensen definieras i egenskapen:

`fileReference`

Det är bara redigeraren av det beröringskänsliga användargränssnittet som helt stöder komponenter för innehållsfragment, som inkluderar klientbiblioteket:

`cq.authoring.editor.plugin.cfm`

Det här biblioteket lägger till funktioner som är specifika för innehållsfragment i redigeraren. Det finns till exempel stöd för att lägga till och konfigurera innehållsfragment på sidan, möjlighet att söka efter innehållsfragmentresurser i resursläsaren och efter associerat innehåll på sidopanelen.

### Mellan innehåll {#in-between-content}

The **Content Fragmen** Med den här komponenten kan du släppa ytterligare komponenter mellan de olika styckena i den visade [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). Elementet som visas består i själva verket av olika stycken (varje stycke markeras med en radmatning). Du kan infoga innehåll med andra komponenter mellan styckena.

Ur teknisk synvinkel finns varje stycke i det visade elementet i en egen parsys, och varje komponent som du lägger till mellan styckena infogas (under huven) i parsytan.

Om instansen av innehållsavsnittskomponenten består av tre stycken, har komponenten alltså tre olika parsyser i databasen. Allt mellanliggande innehåll som läggs till i innehållsfragmentet finns i dessa parsys.

I databasen lagras det mellanliggande innehållet i förhållande till dess position inuti den övergripande styckestrukturen, d.v.s. det är inte kopplat till det faktiska styckeinnehållet.

Tänk på följande för att illustrera detta:

* En instans av ett innehållsfragment bestående av tre stycken
* Och att en del innehåll redan har infogats efter det andra stycket

   * Det innebär att innehållet lagras i den andra parsysen.

Om styckestrukturen i den här instansen ändras (genom att ändra variationen, elementet eller styckeintervallet som visas) kan det påverka det mellanliggande innehållet som visas när innehållet i innehållsfragmentet:

* Redigeras och ett annat stycke läggs till före det andra stycket:

   * Det mellanliggande innehållet visas efter det nya stycket (den andra parsysen innehåller nu det nya stycket).

* Redigeras och det andra stycket tas bort:

   * Det mellanliggande innehållet visas efter det stycke som tidigare var det tredje (det andra stycket innehåller nu det föregående tredje stycket).

* Har konfigurerats så att endast det första stycket visas:

   * Det mellanliggande innehållet visas inte (den andra parametern återges inte längre på grund av den nya konfigurationen).

### Anpassa komponenten Innehållsfragment {#customizing-the-content-fragment-component}

Om du vill använda fragmentkomponenten som finns i kartongen som en plan för tillägg måste du följa följande kontrakt:

* Återanvänd HTML-återgivningsskriptet och tillhörande POJO så att du kan se hur funktionen för mellanliggande innehåll implementeras.
* Återanvänd noden för innehållsfragment: `cq:editConfig`

   * The `afterinsert`/ `afteredit`/ `afterdelete` avlyssnare används för att utlösa JS-händelser. Dessa händelser hanteras i `cq.authoring.editor.plugin.cfm` klientbibliotek för att visa det associerade innehållet på sidopanelen.
   * The `cq:dropTargets` har konfigurerats för att kunna dra innehållsfragmentresurser.
   * `cq:inplaceEditing` är konfigurerat för att stödja redigering av ett innehållsfragment i sidredigeraren. Fragmentets redigerare på plats definieras i `cq.authoring.editor.plugin.cfm` klientbiblioteket och tillåter en snabblänk att öppna den aktuella [element/variation](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) i [fragmentredigerare](/help/assets/content-fragments/content-fragments-variations.md).

### Återgivning av resurser före återgivning {#asset-rewriting-before-rendering}

I Content Fragment Management används en intern återgivningsprocess för att generera det slutliga HTML-resultatet för en sida. Detta används internt av komponenten Content Fragment, men också av bakgrundsprocessen som uppdaterar refererade fragment på refererande sidor.

Internt används Sling Rewriter för den återgivningen. Motsvarande konfiguration finns på `/libs/dam/config/rewriter/cfm` och kan vid behov justeras. Se [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) för mer information.

>[!CAUTION]
>
>Om du justerar/täcker över konfigurationen för omskrivaren:
>
>* `/libs/dam/config/rewriter/cfm`
>
>Sedan `serializerType` **måste** uppdateras till:
>
>* `serializerType="html5-serializer"`

I konfigurationen som är klar att användas används följande transformatorer:

* `transformer-cfm-payloadfilter` - för att hämta `body` part ( `<body>...</body>`) av endast fragmentets HTML

* `transformer-cfm-parfilter` - filtrerar bort oönskade stycken om ett styckeintervall anges (som kan göras med komponenten Innehållsfragment)
* `transformer-cfm-assetprocessor` - används internt för att hämta en lista över resurser som är inbäddade i fragmentet

Återgivningsprocessen visas genom [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) och kan användas (till exempel) av anpassade komponenter, om det behövs.
