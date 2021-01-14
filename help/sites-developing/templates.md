---
title: Mallar
seo-title: Mallar
description: Mallar används när du skapar en sida som ska användas som bas för den nya sidan
seo-description: Mallar används när du skapar en sida som ska användas som bas för den nya sidan
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 27276945a0bdb20410f4c0e98868ea5ce1c09a47
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---


# Mallar{#templates}

Mallar används vid olika tillfällen i AEM:

* När du [skapar en sida måste du välja en mall](#templates-pages); det här används som bas för den nya sidan. Mallen definierar strukturen för den resulterande sidan, allt initialt innehåll och de [komponenter](/help/sites-authoring/default-components.md) som kan användas (designegenskaper).

* När [du skapar ett innehållsfragment måste du också välja en mall](#templates-content-fragments). Den här mallen definierar strukturen, initiala element och variationer.

Följande mallar beskrivs i detalj:

* [Sidmallar - redigerbara](/help/sites-developing/page-templates-editable.md)
* [Sidmallar - statiska](/help/sites-developing/page-templates-static.md)
* [Mallar för innehållsfragment](/help/sites-developing/content-fragment-templates.md)
* [Adaptiv mallåtergivning](/help/sites-developing/templates-adaptive-rendering.md)

## Mallar - Sidor {#templates-pages}

AEM har nu två grundläggande typer av mallar för att skapa sidor:

>[!NOTE]
>
>När du använder en mall för att [skapa en ny sida](/help/sites-authoring/managing-pages.md#creating-a-new-page) finns det ingen synlig skillnad (för sidförfattaren) och ingen indikation på vilken malltyp som används.

### Redigerbara mallar {#editable-templates}

Redigerbara mallar anses nu vara de bästa sätten att utveckla med AEM.

Fördelarna med redigerbara mallar:

* Kan vara [skapad](/help/sites-authoring/templates.md#creating-a-new-template-template-author) och [redigerad](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) av dina författare.

* Har introducerats för att du ska kunna definiera följande för alla sidor som skapas med mallen:

   * strukturen
   * det ursprungliga innehållet
   * innehållsprinciper

* När den nya sidan har skapats upprätthålls en dynamisk anslutning mellan sidan och mallen. Detta innebär att ändringar i mallstrukturen kommer att återspeglas på alla sidor som skapas med den mallen (ändringar av det ursprungliga innehållet kommer inte att återspeglas).
* Innehållsprinciper (redigerade från mallredigeraren) används för att bevara designegenskaperna (designläget används inte i sidredigeraren).
* lagras under `/conf`
* Mer information finns i [Redigerbara mallar](/help/sites-developing/page-templates-editable.md).

>[!NOTE]
>
>Det finns en artikel i AEM Community som förklarar hur du utvecklar en Experience Manager-webbplats med redigerbara mallar. Mer information finns i [Skapa en Adobe Experience Manager 6.5-webbplats med redigerbara mallar](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Statiska mallar {#static-templates}

Statiska mallar:

* Måste definieras och konfigureras av utvecklarna.
* Detta var det ursprungliga mallsystemet för AEM och har funnits i många versioner.
* En statisk mall är en hierarki med noder som har samma struktur som den sida som ska skapas, men utan något faktiskt innehåll.
* Kopieras för att skapa den nya sidan. Därefter finns ingen dynamisk anslutning.
* Använder [Designläge](/help/sites-authoring/default-components-designmode.md) för att behålla designegenskaper.
* lagras under `/apps`
* Mer information finns i [Statiska mallar](/help/sites-developing/page-templates-static.md).

>[!NOTE]
>
>Från och med AEM 6.5 anses användningen av statiska mallar inte vara en god praxis. Använd redigerbara mallar i stället.
>
>[AEM ](modernization-tools.md) modereringsverktyg kan hjälpa dig att migrera från statiska till redigerbara mallar.

### Malltillgänglighet {#template-availability}

>[!CAUTION]
>
>AEM erbjuder flera egenskaper för att styra mallarna som tillåts under **Platser**. En kombination av dem kan dock leda till mycket komplexa regler som är svåra att spåra och hantera.
>
>Därför rekommenderar Adobe att du börjar enkelt genom att definiera:
>
>* endast egenskapen `cq:allowedTemplates`
   >
   >
* endast i platsroten
>
>
Se till exempel We.Retail: `/content/we-retail/jcr:content`
>
>Egenskaperna `allowedPaths`, `allowedParents` och `allowedChildren` kan också placeras i mallarna för att definiera mer avancerade regler. När det är möjligt är det *mycket* enklare att definiera ytterligare `cq:allowedTemplates`-egenskaper för underavsnitt på platsen om det finns behov av att begränsa de tillåtna mallarna ytterligare.
>
>En ytterligare fördel är att `cq:allowedTemplates`-egenskaperna kan uppdateras av en författare på fliken **Avancerat** på **Sidegenskaper**. De andra mallegenskaperna kan inte uppdateras med (standard) användargränssnittet, så behöver en utvecklare för att behålla reglerna och en koddistribution för varje ändring.

När du skapar en ny sida i webbplatsens administratörsgränssnitt beror listan med tillgängliga mallar på platsen för den nya sidan och de placeringsbegränsningar som anges i varje mall.

Följande egenskaper avgör om en mall `T` får användas för en ny sida som ska placeras som underordnad till sidan `P`. Var och en av dessa egenskaper är en sträng med flera värden som innehåller noll eller flera reguljära uttryck som används för matchning med sökvägar:

* Egenskapen `cq:allowedTemplates` för undernoden `jcr:content` för `P` eller en överordnad till `P`.

* Egenskapen `allowedPaths` för `T`.

* Egenskapen `allowedParents` för `T`.

* Egenskapen `allowedChildren` för mallen `P`.

Utvärderingen fungerar enligt följande:

* Den första icke-tomma `cq:allowedTemplates`-egenskapen som påträffades när sidhierarkin som börjar med `P` ökades matchas mot sökvägen `T`. Om inget av värdena matchar avvisas `T`.

* Om `T` har en `allowedPaths`-egenskap som inte är tom, men inget av värdena matchar sökvägen `P`, avvisas `T`.

* Om båda ovanstående egenskaper är tomma eller inte finns, avvisas `T` om den inte tillhör samma program som `P`. `T` tillhör samma program som  `P` if och endast om namnet på den andra nivån i sökvägen  `T` är detsamma som namnet på den andra nivån i sökvägen  `P`. Mallen `/apps/geometrixx/templates/foo` tillhör till exempel samma program som sidan `/content/geometrixx`.

* Om `T` har en `allowedParents`-egenskap som inte är tom, men inget av värdena matchar sökvägen `P`, avvisas `T`.

* Om mallen för `P` har en `allowedChildren`-egenskap som inte är tom, men inget av värdena matchar sökvägen för `T`, avvisas `T`.

* I alla andra fall är `T` tillåtet.

I följande diagram visas mallutvärderingsprocessen:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Begränsa mallar som används på underordnade sidor {#limiting-templates-used-in-child-pages}

Om du vill begränsa vilka mallar som kan användas för att skapa underordnade sidor under en viss sida använder du egenskapen `cq:allowedTemplates` för noden `jcr:content` på sidan för att ange listan med mallar som ska tillåtas som underordnade sidor. Varje värde i listan måste vara en absolut sökväg till en mall för en tillåten underordnad sida, till exempel `/apps/geometrixx/templates/contentpage`.

Du kan använda egenskapen `cq:allowedTemplates` på mallens `jcr:content`-nod om du vill att den här konfigurationen ska tillämpas på alla nyskapade sidor som använder den här mallen.

Om du vill lägga till fler begränsningar, till exempel för mallhierarkin, kan du använda egenskaperna `allowedParents/allowedChildren` för mallen. Du kan sedan uttryckligen ange att sidor som skapats från en mall T måste vara överordnade/underordnade sidor till sidor som skapats från en mall T.

## Mallar - Innehållsfragment {#templates-content-fragments}

Mer information finns i [Mallar för innehållsfragment](/help/sites-developing/content-fragment-templates.md).
