---
title: Mallar
description: Mallar används när du skapar en sida som används som bas för den nya sidan.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Mallar{#templates}

Mallar används vid olika tillfällen i AEM:

* [När du skapar en sida väljer du en mall](#templates-pages). Den här mallen används som bas för den nya sidan. Mallen definierar sidans struktur, allt ursprungligt innehåll och [komponenter](/help/sites-authoring/default-components.md) som kan användas (designegenskaper).

* [När du skapar ett innehållsfragment väljer du även en mall](#templates-content-fragments). Den här mallen definierar strukturen, initiala element och variationer.

Följande mallar beskrivs i detalj:

* [Sidmallar - redigerbara](/help/sites-developing/page-templates-editable.md)
* [Sidmallar - statiska](/help/sites-developing/page-templates-static.md)
* [Mallar för innehållsfragment](/help/sites-developing/content-fragment-templates.md)
* [Adaptiv mallåtergivning](/help/sites-developing/templates-adaptive-rendering.md)

## Mallar - Sidor {#templates-pages}

AEM har nu två grundläggande typer av mallar för att skapa sidor:

>[!NOTE]
>
>När en mall används för [skapa en sida](/help/sites-authoring/managing-pages.md#creating-a-new-page), det finns ingen synlig skillnad (för sidförfattaren) och ingen indikation på vilken typ av mall som används.

### Redigerbara mallar {#editable-templates}

Redigerbara mallar anses nu vara de bästa sätten att utveckla med AEM.

Fördelarna med redigerbara mallar:

* Kan [skapad](/help/sites-authoring/templates.md#creating-a-new-template-template-author) och [redigerad](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) av dina författare.

* Har introducerats för att du ska kunna definiera följande för alla sidor som skapas med mallen:

   * strukturen
   * det ursprungliga innehållet
   * innehållsprinciper

* När den nya sidan har skapats upprätthålls en dynamisk anslutning mellan sidan och mallen. Den här anslutningen innebär att ändringar i mallstrukturen återspeglas på alla sidor som skapas med den mallen. Ändringar av det ursprungliga innehållet återspeglas inte.
* Innehållsprinciper (redigerade från mallredigeraren) används för att bevara designegenskaperna (designläget används inte i sidredigeraren).
* lagras under `/conf`
* Se [Redigerbara mallar](/help/sites-developing/page-templates-editable.md) för ytterligare information.

>[!NOTE]
>
>Se [Använda redigerbara sidmallar för att utveckla en Experience Manager-webbplats](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html).

### Statiska mallar {#static-templates}

Statiska mallar:

* Måste definieras och konfigureras av utvecklarna.
* Det ursprungliga mallsystemet för AEM som har varit tillgängligt för många versioner.
* En statisk mall är en hierarki med noder som har samma struktur som den sida som ska skapas, men utan något faktiskt innehåll.
* Kopieras för att skapa sidan och det finns ingen dynamisk anslutning därefter.
* Användningsområden [Designläge](/help/sites-authoring/default-components-designmode.md) för att behålla designegenskaper.
* lagras under `/apps`
* Se [Statiska mallar](/help/sites-developing/page-templates-static.md) för ytterligare information.

>[!NOTE]
>
>Från och med AEM 6.5 anses användningen av statiska mallar inte vara en god praxis. Använd redigerbara mallar i stället.
>
>[AEM modernisering](modernization-tools.md) verktyg kan hjälpa dig att migrera från statiska till redigerbara mallar.

### Malltillgänglighet {#template-availability}

>[!CAUTION]
>
>AEM har flera egenskaper som styr mallarna under **Webbplatser**. Om du kombinerar dem kan det dock leda till komplexa regler som är svåra att spåra och hantera.
>
>Därför rekommenderar Adobe att du börjar enkelt genom att definiera:
>
>* endast `cq:allowedTemplates` property
>
>* endast i platsroten
>
>Se till exempel We.Retail: `/content/we-retail/jcr:content`
>
>Egenskaperna `allowedPaths`, `allowedParents`och `allowedChildren` kan också placeras i mallar för att definiera mer avancerade regler. Men om möjligt är det *mycket* enklare att definiera `cq:allowedTemplates` egenskaper på underavsnitt av platsen om det finns behov av att ytterligare begränsa de tillåtna mallarna.
>
>En extra fördel är att `cq:allowedTemplates` kan uppdateras av en författare i **Avancerat** -fliken i **Sidegenskaper**. De andra mallegenskaperna kan inte uppdateras med (standard) användargränssnittet, så behöver en utvecklare för att behålla reglerna och en koddistribution för varje ändring.

När du skapar en sida i webbplatsens administratörsgränssnitt beror listan med tillgängliga mallar på platsen för den nya sidan och de placeringsbegränsningar som anges i varje mall.

Följande egenskaper avgör om en mall `T` används för en ny sida som ska placeras som underordnad till sidan `P`. Var och en av dessa egenskaper är en sträng med flera värden som innehåller noll eller flera reguljära uttryck som används för matchning med sökvägar:

* The `cq:allowedTemplates` egenskapen för `jcr:content` undernod till `P` eller en överordnad till `P`.

* The `allowedPaths` egenskap för `T`.

* The `allowedParents` egenskap för `T`.

* The `allowedChildren` egenskap för mallen för `P`.

Utvärderingen fungerar enligt följande:

* Den första som inte är tom `cq:allowedTemplates` egenskap påträffades när sidhierarkin skulle ökas från `P` matchas mot sökvägen för `T`. Om inget av värdena matchar, `T` avvisas.

* If `T` har ett värde som inte är tomt `allowedPaths` -egenskapen, men inget av värdena matchar sökvägen för `P`, `T` avvisas.

* Om båda ovanstående egenskaper är tomma eller inte finns, `T` avvisas om det inte tillhör samma program som `P`. `T` tillhör samma program som `P` if och only if the name of the second level of the path of `T` är samma som namnet på den andra nivån i sökvägen för `P`. Mallen `/apps/geometrixx/templates/foo` tillhör samma program som sidan `/content/geometrixx`.

* If `T` har ett värde som inte är tomt `allowedParents` -egenskapen, men inget av värdena matchar sökvägen för `P`, `T` avvisas.

* Om mallen för `P` har ett värde som inte är tomt `allowedChildren` -egenskapen, men inget av värdena matchar sökvägen för `T`, `T` avvisas.

* I alla andra fall `T` är tillåtet.

I följande diagram visas mallutvärderingsprocessen:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Begränsa mallar som används på underordnade sidor {#limiting-templates-used-in-child-pages}

Om du vill begränsa vilka mallar som kan användas för att skapa underordnade sidor under en viss sida använder du `cq:allowedTemplates` egenskap för `jcr:content` nod på sidan för att ange listan med mallar som ska tillåtas som underordnade sidor. Varje värde i listan måste vara en absolut sökväg till en mall för en tillåten underordnad sida, till exempel `/apps/geometrixx/templates/contentpage`.

Du kan använda `cq:allowedTemplates` på mallens  `jcr:content` nod som den här konfigurationen ska tillämpas på alla nyskapade sidor som använder den här mallen.

Om du vill lägga till fler begränsningar för mallhierarkin kan du använda `allowedParents/allowedChildren` -egenskaper i mallen. Du kan sedan uttryckligen ange att sidor som skapats från en mall T måste vara överordnade/underordnade sidor till sidor som skapats från en mall T.

## Mallar - Innehållsfragment {#templates-content-fragments}

Se [Mallar för innehållsfragment](/help/sites-developing/content-fragment-templates.md).
