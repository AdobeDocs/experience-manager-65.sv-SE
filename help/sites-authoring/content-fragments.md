---
title: Sidredigering med innehållsfragment
seo-title: Sidredigering med innehållsfragment
description: Med AEM Content Fragments kan du utforma, skapa, strukturera och använda sidoberoende innehåll
seo-description: Med AEM Content Fragments kan du utforma, skapa, strukturera och använda sidoberoende innehåll
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: 74f259d579bcf8d7a9198f93ef667288787a4493
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---


# Sidredigering med innehållsfragment{#page-authoring-with-content-fragments}

Innehållsfragment i Adobe Experience Manager (AEM) [skapas och hanteras som sidoberoende resurser](/help/assets/content-fragments/content-fragments.md).

Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. Du kan sedan använda dessa fragment och deras variationer när du redigerar innehållssidorna.

Tillsammans med den uppdaterade JSON-exporteraren kan strukturerade innehållsfragment även användas för att leverera AEM innehåll via Content Services till andra kanaler än AEM.

>[!NOTE]
>
>**Innehållsfragment** och  **[Upplevelsefragment](/help/sites-authoring/experience-fragments.md)** är olika funktioner i AEM:
>
>* **Innehållsfragmenterarär** redaktionellt innehåll, främst text och relaterade bilder. De är rent innehåll, utan design och layout.
>* **Upplevelsefragment** är helt utformat. ett fragment av en webbsida.

>
>
Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.

>[!CAUTION]
>
>Den här sidan måste läsas tillsammans med [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md) (och relaterade sidor) eftersom den innehåller grundläggande terminologi och koncept samt skapar och hanterar fragment.

Innehållsfragmenten aktiverar:

* **Marknadsförings- och kampanjstrategi**

   * Granska innehåll via centralt hanterade innehållsfragment.

* **Creative Pro**

   * Spåra kreativa resurser via samlingar som är kopplade till innehållsfragment.

* **Kopiera författare**

   * Skriv i AEM innehållsfragmentredigerare.
   * Kan skapa innehållsvariationer.
   * Kan associera relevant innehåll med innehållsfragmentet.
   * Kan använda versionshantering/arbetsflöde.
   * Kan dela innehållsfragment.
   * Kan hantera översättningar centralt.

* **Producenter och reseansvariga**

   * Välj bland fördefinierade fragment och variationer med redigering i AEM.
   * Kan förlita sig på att fragment och tillhörande innehåll alltid är uppdaterade när kopieringsförfattare och kreatörer uppdaterar centralt hanterade fragment och resurser.
   * Kan lita på att tillhörande medieinnehåll kurateras för relevans.
   * Kan skapa tillfälliga innehållsvariationer direkt samtidigt som dessa variationer förblir centralt hanterade i fragmentet.

## Lägga till ett innehållsfragment på sidan {#adding-a-content-fragment-to-your-page}

1. Öppna sidan för redigering.

1. Lägg till **innehållsfragment**-komponenten; från antingen webbläsaren **Komponenter** eller **Infoga ny komponent**.

1. Du kan antingen:

   * Öppna webbläsaren **Resurser** och filtrera efter **Innehållsfragment** (standardvärdet är Bilder). Dra sedan det önskade fragmentet till komponentinstansen.

   * Markera innehållskomponenten och **Konfigurera** i verktygsfältet. I dialogrutan kan du öppna urvalsdialogrutan för att bläddra och välja önskat **innehållsfragment**.
   >[!NOTE]
   >
   >Ett annat sätt är att dra ett visst innehållsfragment direkt till sidan. Då skapas automatiskt den associerade komponenten (innehållsfragment).

1. Inledningsvis visas innehållet från **Main**-elementet och **Överordnad** (variation). Du kan [välja andra element och/eller variationer](#selecting-the-element-or-variation) efter behov.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Mer information om ytterligare redigeringsfunktioner finns även i:
   >
   >
   >
   >    * [Responsiv layout](/help/sites-authoring/responsive-layout.md)
   >    * [Redigera sidinnehåll](/help/sites-authoring/editing-content.md)


### Markera elementet eller variationen {#selecting-the-element-or-variation}

Öppna dialogrutan **Konfiguration** för fragmentet och konfigurera det för användning på den aktuella sidan. Dialogrutan kan vara beroende av vilken komponent som används.

I rätt konfigurationsdialogruta kan du välja tillgängliga parametrar, bland annat:

* **Innehållsfragment**

   Ange det fragment som ska användas.

* **Visningsläge**:

   * **Enkelt textelement**

   * **Flera element**

* **Element**

   * Standardvärdet **Main** är alltid tillgängligt.
   * En markering blir tillgänglig om fragmentet skapades med en lämplig mall.

   >[!NOTE]
   >
   >Vilka element som är tillgängliga beror på vilken mall som används.

* **Variant**

   * **Standardmastern** är alltid tillgänglig.
   * En markering blir tillgänglig om variationer har skapats för fragmentet.

* **Stycken**: ange det eller de stycken som ska ingå:

   * **Alla**
   * **Intervall**: t.ex.  `1`,  `3-5`,  `9-*`

      * **Hantera rubriker som egna stycken**

* **Hantera rubriker som egna stycken**

### Snabb anslutning till Fragment Editor {#quick-connection-to-fragment-editor}

Du kan öppna fragmentkällan för redigering (resursen) med ikonen **Redigera** i komponentverktygsfältet. Detta gör att du kan [redigera och hantera innehållsfragmentet](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Som alltid kommer redigering av fragmentkällan att påverka alla sidor som refererar till det innehållsfragmentet.

### Lägger till mellaninnehåll {#adding-in-between-content}

När ett visst innehållsfragment läggs till på sidan finns det en **Dra komponenter här** platshållare mellan varje HTML-stycke (och längst upp/längst ned) i fragmentet.

Detta gör att du kan lägga till extra innehåll [mellan (dvs. mellanliggande innehåll)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) fragmentinnehållet (vid någon av de tillgängliga punkterna) utan att behöva ändra rotfragmentet.

För mellanliggande innehåll kan du:

* Lägg till komponenter från [komponentwebbläsaren](/help/sites-authoring/author-environment-tools.md#components-browser).
* Lägg till resurser från [Resursläsaren](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Använd [Associerat innehåll](#using-associated-content) som källa för mellanliggande innehåll.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>Du kan även [infoga visuella resurser (bilder) i själva fragmentet](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Visuella resurser som infogats i själva fragmentet kopplas till föregående stycke i fragmentet. Det innebär att du inte kan placera innehåll mellan en visuell resurs och föregående stycke.

>[!CAUTION]
>
>När du har lagt till mellanliggande innehåll i ett innehållsfragment på sidan kan ändringar av strukturen för det underliggande innehållsfragmentet (dvs. i innehållsfragmentredigeraren) leda till felaktiga/oväntade resultat.
>
>När detta inträffar behålls det mellanliggande innehållet som det är:
>
>* Mellanliggande komponenter har en absolut position inom komponentsekvensen i fragmentflödet. Den här positionen ändras inte, även när innehållet i styckena i fragmentet ändras.
>
>  
Detta kan få det att se ut som om den relativa placeringen har ändrats, eftersom mellanliggande stycken inte har någon kontextuell relation till (fragmentet) stycken som de är placerade bredvid.
>* Om inte de två styckestrukturerna står i konflikt med varandra. I så fall visas inte det mellanliggande innehållet (även om det fortfarande finns internt).

>



### Använda associerat innehåll {#using-associated-content}

Om du har [associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med [innehållsfragmentet](/help/assets/content-fragments/content-fragments.md) är dessa resurser tillgängliga från sidopanelen (när du har placerat fragmentet på innehållssidan). Associerat innehåll är i själva verket en särskild innehållskälla för [mellanliggande innehåll](#adding-in-between-content).

>[!NOTE]
>
>Det finns olika metoder för att lägga till [visuella resurser (t.ex. bilder)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till avsnittet och/eller sidan.

>[!NOTE]
>
>Om du har flera innehållsfragment på en sida visar fliken **Associerat innehåll** resurser som passar alla fragment.

När du har lagt till ett fragment med associerat innehåll på sidan öppnas en ny flik (**Associerat innehåll**) på sidopanelen.

Här kan du dra resurserna till önskad plats (antingen till en befintlig komponent eller till önskad plats där rätt komponent skapas):

![cfm-6420-03](assets/cfm-6420-03.png)

### Resurser infogade i fragmentet {#assets-inserted-into-the-fragment}

Om resurser (t.ex. bilder) har infogats i själva fragmentet är alternativen för att redigera dessa resurser i sidredigeraren begränsade. <!-- Removed link as it was a 404 on helpx -->

För en bild kan du till exempel

* Beskär, rotera eller vänd bilden.
* Lägg till en titel eller alternativ text.
* Ange en storlek.
* Du kan också konfigurera layouten.

Andra ändringar, till exempel move, copy, delete, måste göras i fragmentredigeraren.

### Publicerar {#publishing}

Fragment måste publiceras så att de kan användas på dina publicerade webbsidor:

* Ett fragment kan publiceras när [fragmentet har skapats i resurskonsolen](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* Om ett *opublicerat fragment* används på en sida som publiceras, kan fragmentet även publiceras just nu.

