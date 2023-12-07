---
title: Redigering - miljö och verktyg
description: Med webbplatskonsolen kan du hantera och navigera på webbplatsen. Med två rutor kan strukturen på webbplatsen utökas och åtgärder vidtas för de element som behövs.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---

# Redigering - miljö och verktyg {#authoring-the-environment-and-tools}

I redigeringsmiljön i AEM finns olika sätt att ordna och redigera ditt innehåll. Verktygen som tillhandahålls är tillgängliga från olika konsoler och sidredigerare.

## Webbplatsadministration {#site-administration}

The **Webbplatser** konsolen gör att du kan hantera och navigera på webbplatsen. Med hjälp av de två rutorna kan webbplatsens struktur utökas och åtgärder vidtas för det element som krävs:

![chlimage_1-108](assets/chlimage_1-108.png)

## Redigera sidinnehåll {#editing-your-page-content}

Det finns en separat sidredigerare med det klassiska användargränssnittet som använder innehållssökaren och sidbrytaren:

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## Få hjälp {#accessing-help}

Olika **Hjälp** kan nås direkt från AEM:

Förutom att få tillgång till [hjälp från konsolens verktygsfält](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)kan du även komma åt hjälpen från sidan (med ? ikon) när du redigerar en sida:

![Sidekick, komprimerad](do-not-localize/sidekick-collapsed-2.png)

Eller genom att använda **Hjälp** i redigeringsdialogrutan för specifika komponenter. Då visas sammanhangsberoende hjälp.

## Sidekick {#sidekick}

The **Komponenter** kan du bläddra bland de komponenter som är tillgängliga för att läggas till på den aktuella sidan. Den önskade gruppen kan expanderas och sedan dras en komponent till önskad plats på sidan.

![chlimage_1-110](assets/chlimage_1-110.png)

## Innehållssökaren {#the-content-finder}

Innehållssökaren är ett snabbt och enkelt sätt att hitta resurser och/eller innehåll i databasen när du redigerar en sida.

Du kan använda innehållssökaren för att hitta en rad olika resurser. Om det behövs kan du dra ett objekt och släppa det i ett stycke på sidan:

* [Bilder](#finding-images)
* [Dokument](#finding-documents)
* [Filmer](#finding-movies)
* [Dynamic Media webbläsare](/help/sites-administering/scene7.md#scene7contentbrowser)
* [Sidor](#finding-pages)

* [Stycken](#referencing-paragraphs-from-other-pages)
* [Produkter](#products)
* Eller till [bläddra på webbplatsen efter databasstruktur](#the-content-finder)

Med alla alternativ kan du [söka efter specifika objekt](#the-content-finder).

### Hitta bilder {#finding-images}

På den här fliken visas alla bilder i databasen.

När du har skapat ett bildstycke på sidan kan du dra ett objekt och släppa det i stycket.

![chlimage_1-111](assets/chlimage_1-111.png)

### Söka efter dokument {#finding-documents}

På den här fliken visas alla dokument i databasen.

När du har skapat ett nedladdningsstycke på sidan kan du dra ett objekt och släppa det i stycket.

![chlimage_1-112](assets/chlimage_1-112.png)

### Söka efter filmer {#finding-movies}

På den här fliken visas alla filmer (till exempel Flashar) i databasen.

När du har skapat ett lämpligt stycke (till exempel Flash) på sidan kan du dra ett objekt och släppa det i stycket.

![chlimage_1-113](assets/chlimage_1-113.png)

### Produkter {#products}

På den här fliken visas alla produkter. När du har skapat ett lämpligt stycke (till exempel Produkt) på sidan kan du dra ett objekt och släppa det i stycket.

![chlimage_1-114](assets/chlimage_1-114.png)

### Hitta sidor {#finding-pages}

På den här fliken visas alla sidor. Dubbelklicka på en sida för att öppna den för redigering.

![chlimage_1-115](assets/chlimage_1-115.png)

### Referera stycken från andra sidor {#referencing-paragraphs-from-other-pages}

På den här fliken kan du söka efter en annan sida. Alla stycken från den sidan visas. Du kan sedan dra ett stycke till den aktuella sidan så skapas en referens till det ursprungliga stycket.

![chlimage_1-116](assets/chlimage_1-116.png)

### Använda den fullständiga databasvyn {#using-the-full-repository-view}

På den här fliken visas alla resurser i databasen.

![chlimage_1-117](assets/chlimage_1-117.png)

### Använda Söka med Innehållsläsaren {#using-search-with-the-content-browser}

På alla alternativ kan du söka efter specifika objekt. Alla taggar och resurser som matchar sökmönstret visas:

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

Du kan också använda jokertecken för sökning. Följande jokertecken stöds:

* `*`
matchar en sekvens med noll eller flera tecken.

* `?`
matchar ett enda tecken.

>[!NOTE]
>
>Det finns en pseudoegenskap, &quot;name&quot;, som måste användas för sökningar med jokertecken.

Om det till exempel finns en bild som heter:

`ad-nmvtis.jpg`

följande sökmönster hittar den (och alla andra bilder som matchar mönstret):

* `name:*nmv*`
* `name:AD*`
teckenmatchningen är *not* skiftlägeskänslig.

* `name:ad?nm??is.*`
Du kan använda valfritt antal jokertecken i en fråga.

>[!NOTE]
>
>Du kan också använda [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html) sökning.

## Visar referenser {#showing-references}

AEM låter dig se vilka sidor som är länkade till den sida du arbetar med just nu.

Så här visar du direkta sidreferenser:

1. I sidosparken väljer du **Sida** -tabbikonen.

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. Välj **Visa referenser...** AEM öppnar fönstret Referenser och visar vilka sidor som refererar till den markerade sidan, inklusive deras sökvägar.

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

I vissa situationer finns det ytterligare åtgärder att vidta från Sidekick, bland annat:

* [Launches](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live-kopior](/help/sites-administering/msm.md)

* [Blueprint](/help/sites-administering/msm-best-practices.md)

Övriga [Förbindelser mellan sidor kan visas i webbplatskonsolen](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## Granskningslogg {#audit-log}

The **Granskningslogg** kan nås via **Information** sidosparkens flik. Här listas de senaste åtgärderna som har utförts på den aktuella sidan, till exempel:

![chlimage_1-118](assets/chlimage_1-118.png)

## Sidinformation {#page-information}

Webbplatskonsolen [innehåller information om sidans aktuella status](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) som publicering, ändring, låst, livecopy och så vidare.

## Sidlägen {#page-modes}

När du redigerar en sida med det klassiska användargränssnittet finns det olika lägen som du kan komma åt med hjälp av ikonerna längst ned i sidosparken:

![Sidlägen](do-not-localize/chlimage_1-12.png)

Ikonerna längst ned på Sidekick används för att växla mellan olika lägen för att arbeta med sidorna:

* [Redigera](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
Det här är standardläget och du kan redigera sidan, lägga till eller ta bort komponenter och göra andra ändringar.

* [Förhandsgranska](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
I det här läget kan du förhandsgranska sidan som om den visades på webbplatsen i dess slutliga form.

* [Design](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
I det här läget kan du redigera sidans design genom att konfigurera de komponenter som är tillgängliga.

>[!NOTE]
>
>Andra alternativ är också tillgängliga:
>
>* [Ställning](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [Klientkontext](/help/sites-administering/client-context.md)
>* Webbplatser - öppnar webbplatskonsolen.
>* Läs in igen - uppdaterar sidan.

## Kortkommandon {#keyboard-shortcuts}

Olika [kortkommandon](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) är tillgängliga.
