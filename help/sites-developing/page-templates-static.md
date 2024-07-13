---
title: Sidmallar - statiska
description: En mall används för att skapa en sida och definierar vilka komponenter som kan användas i det valda omfånget
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 0%

---

# Sidmallar - statiska{#page-templates-static}

En mall används för att skapa en sida och definierar vilka komponenter som kan användas i det valda omfånget. En mall är en hierarki med noder som har samma struktur som den sida som ska skapas, men utan något verkligt innehåll.

Varje mall innehåller ett urval av komponenter som är tillgängliga för användning.

* Mallar består av [komponenter](/help/sites-developing/components.md);
* Komponenterna använder, och tillåter åtkomst till, widgetar och dessa används för att återge innehållet.

>[!NOTE]
>
>[Redigerbara mallar](/help/sites-developing/page-templates-editable.md) är också tillgängliga och är den rekommenderade typen av mallar för större flexibilitet och de senaste funktionerna.

## Egenskaper och underordnade noder för en mall {#properties-and-child-nodes-of-a-template}

En mall är en nod av typen cq:Template och har följande egenskaper och underordnade noder:

<table>
 <tbody>
  <tr>
   <td><strong>Namn <br /> </strong></td>
   <td><strong>Typ <br /> </strong></td>
   <td><strong>Beskrivning <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>Aktuell mall. En mall är av nodtypen cq:Template.<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> Sträng[]</td>
   <td>Sökväg till en mall som kan vara underordnad den här mallen.<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> Sträng[]</td>
   <td>Sökväg till en mall som tillåts vara överordnad den här mallen.<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> Sträng[]</td>
   <td>Sökväg till en sida som kan baseras på den här mallen.<br /> </td>
  </tr>
  <tr>
   <td> jcr:skapad</td>
   <td> Datum</td>
   <td>Skapad av mallen.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> Sträng</td>
   <td>Beskrivning av mallen.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> Sträng</td>
   <td>Mallens namn.<br /> </td>
  </tr>
  <tr>
   <td> rankning</td>
   <td> Lång</td>
   <td>Mallens rangordning. Används för att visa mallen i användargränssnittet.<br /> </td>
  </tr>
  <tr>
   <td> jcr:innehåll</td>
   <td> cq:PageContent</td>
   <td>Nod som innehåller mallens innehåll.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:fil</td>
   <td>Mallens miniatyrbild.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:fil</td>
   <td>Ikon för mallen.<br /> </td>
  </tr>
 </tbody>
</table>

En mall är grunden för en sida.

Om du vill skapa en sida måste mallen kopieras (nodträd `/apps/<myapp>/template/<mytemplate>`) till motsvarande position i platsträdet: detta händer om en sida skapas med fliken **Webbplatser** .

Den här kopieringsåtgärden ger även sidan dess ursprungliga innehåll (vanligtvis innehåll på översta nivån) och egenskapen sling:resourceType, sökvägen till sidkomponenten som används för att återge sidan (allt i den underordnade noden jcr:content).

## Hur mallar är strukturerade {#how-templates-are-structured}

Det finns två aspekter att tänka på:

* mallens struktur
* strukturen för det innehåll som skapas när en mall används

### Strukturen i en mall {#the-structure-of-a-template}

En mall skapas under en nod av typen **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

Du kan ange olika egenskaper, särskilt:

* **jcr:title** - mallens rubrik visas i dialogrutan när du skapar en sida.
* **jcr:description** - beskrivning av mallen; visas i dialogrutan när du skapar en sida.

Den här noden innehåller en jcr:content-nod (cq:PageContent) som används som bas för innehållsnoden på de resulterande sidorna. Den här referensen använder sling:resourceType, den komponent som ska användas för återgivning av det faktiska innehållet på en ny sida.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Den här komponenten används för att definiera innehållets struktur och design när en ny sida skapas.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### Innehållet som skapas av en mall {#the-content-produced-by-a-template}

Mallar används för att skapa sidor av typen `cq:Page` (som tidigare nämnts är en sida en särskild typ av komponent). Varje AEM har en strukturerad nod `jcr:content`. Det:

* är av typen cq:PageContent
* är en strukturerad nodtyp som innehåller en definierad innehållsdefinition
* har egenskapen `sling:resourceType` som refererar till komponenten som innehåller de snedskriftsskript som används för återgivning av innehållet

### Standardmallar {#default-templates}

AEM levereras med olika standardmallar som är tillgängliga direkt. Ibland kanske du vill använda mallarna som de är. I så fall måste du se till att mallen är tillgänglig för din webbplats.

AEM innehåller till exempel flera mallar, inklusive en innehållssida och en hemsida.

| **Titel** | **Komponent** | **Plats** | **Syfte** |
|---|---|---|---|
| Hemsida | hemsida | geometrixx | Geometrixx hemsidmall. |
| Innehållssida | innehållsida | geometrixx | Innehållssidmallen för Geometrixx. |

#### Visa standardmallar {#displaying-default-templates}

Om du vill se en lista över alla mallar i databasen gör du så här:

1. Öppna menyn **Verktyg** i CRXDE Lite och klicka på **Fråga**.

1. På fliken Fråga
1. Som **typ** väljer du **XPath**.

1. Ange följande sträng i indatafältet **Fråga**:
//element(&#42;, cq:Template)

1. Klicka på **Kör**. Listan visas i resultatrutan.

Oftast skapar du en befintlig mall och skapar en ny för eget bruk. Mer information finns i [Utveckla sidmallar](#developing-page-templates).

Om du vill aktivera en befintlig mall för webbplatsen och du vill att den ska visas i dialogrutan **Skapa sida** när du skapar en sida direkt under **Webbplatser** från konsolen **Webbplatser** anger du egenskapen allowedPaths för mallnoden till: **/content(/).&#42;)?**

## Hur malldesigner används {#how-template-designs-are-applied}

När format definieras i användargränssnittet med [designläget](/help/sites-authoring/default-components-designmode.md), behålls designen med den exakta sökvägen för den innehållsnod som formatet definieras för.

>[!CAUTION]
>
>Adobe rekommenderar att du bara använder designer via [designläget](/help/sites-authoring/default-components-designmode.md).
>
>Det är till exempel inte bra att ändra design i CRXDE Lite och tillämpningen av sådana designer kan variera från förväntat beteende.

Om designer endast används i designläge gäller inte följande avsnitt, [Design Path Resolution](/help/sites-developing/page-templates-static.md#design-path-resolution), [Decision Tree](/help/sites-developing/page-templates-static.md#decision-tree) och [Example](/help/sites-developing/page-templates-static.md#example).

### Design Path-upplösning {#design-path-resolution}

När du återger innehåll baserat på en statisk mall försöker AEM tillämpa den mest relevanta designen och formaten på innehållet baserat på en genomgång i innehållshierarkin.

AEM avgör vilket format som är mest relevant för en innehållsnod i följande ordning:

* Om det finns en design för den fullständiga och exakta sökvägen för innehållsnoden (som när designen definieras i designläge) använder du den designen.
* Om det finns en design för den överordnade noden ska du använda den designen.
* Om det finns en design för en nod på innehållsnodens sökväg använder du den designen.

Om det finns mer än en tillämplig design i de två sista fallen använder du den som ligger närmast noden content.

### Beslutsträd {#decision-tree}

Detta är en grafisk representation av logiken för [Design Path Resolution](/help/sites-developing/page-templates-static.md#design-path-resolution) .

![design_path_resolution](assets/design_path_resolution.png)

### Exempel {#example}

Här följer en enkel innehållsstruktur där en design kan användas på alla noder:

`/root/branch/leaf`

I följande tabell beskrivs hur AEM väljer en design.

<table>
 <tbody>
  <tr>
   <td><strong>Hitta design för<br /> </strong></td>
   <td><strong>Det finns design för<br /> </strong></td>
   <td><strong>Design vald<br /> </strong></td>
   <td><strong>Kommentar</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>Den mest exakta matchningen används alltid.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>Gå tillbaka till den närmaste matchningen som är lägre i trädet.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>Om inget annat fungerar tar du det som återstår.<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>Om det inte finns någon exakt matchning tar du den längre ned i trädet.</p> <p>Förutsättningen är att detta alltid kommer att gälla, men ytterligare trädet kan vara för specifikt.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Utveckla sidmallar {#developing-page-templates}

AEM är helt enkelt modeller som används för att skapa sidor. De kan innehålla så lite, eller så mycket, initialt innehåll som behövs, och deras roll är att skapa rätt initiala nodstrukturer, med de nödvändiga egenskaperna (främst sling:resourceType) inställda för redigering och återgivning.

### Skapa en mall (baserad på en befintlig mall) {#creating-a-new-template-based-on-an-existing-template}

En ny mall kan skapas helt från början, men ofta kopieras en befintlig mall i stället och uppdateras för att spara tid och arbete. Mallarna i Geometrixx kan till exempel användas för att hjälpa dig komma igång.

Så här skapar du en mall baserad på en befintlig mall:

1. Kopiera en befintlig mall (helst med en definition som ligger så nära den du vill uppnå) till en ny nod.

   Mallar lagras i **/appar/**.

   >[!NOTE]
   >
   >Listan med tillgängliga mallar beror på den nya sidans plats och de placeringsbegränsningar som anges i respektive mall. Se [Malltillgänglighet](#templateavailibility).

1. Ändra **jcr:title** för den nya mallnoden så att den återspeglar dess nya roll. Du kan även uppdatera **jcr:description** om det behövs. Var noga med att ändra malltillgängligheten för sidan efter behov.

   >[!NOTE]
   >
   >Om du vill att mallen ska visas i dialogrutan **Skapa sida** när du skapar en sida direkt under **Webbplatser** från konsolen **Webbplatser** anger du egenskapen `allowedPaths` för mallnoden till: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Kopiera komponenten som mallen baseras på (detta anges av egenskapen **sling:resourceType** för noden **jcr:content** i mallen) för att skapa en instans.

   Komponenter lagras i **/apps/&lt;webbplatsnamn>/components/&lt;komponentnamn>**.

1. Uppdatera den nya komponentens **jcr:title** och **jcr:description**.
1. Ersätt thumbnail.png om du vill att en ny miniatyrbild ska visas i mallurvalslistan (storlek 128 x 98 px).
1. Uppdatera noden **sling:resourceType** för mallens **jcr:content** så att den refererar till den nya komponenten.
1. Gör ytterligare ändringar av mallens funktionalitet eller design, eller av dess underliggande komponent, eller både och.

   >[!NOTE]
   >
   >Ändringar som görs i noden **/apps/&lt;webbplats>/templates/** påverkar mallinstansen (som i urvalslistan).
   >
   >
   Ändringar som görs i noden **/apps/&lt;webbplats>/components/&lt;komponentnamn>** påverkar innehållssidan som skapas när mallen används.

   Nu kan du skapa en sida på webbplatsen med den nya mallen.

>[!NOTE]
>
Redigeringsklientbiblioteket förutsätter att namnområdet `cq.shared` finns på innehållssidorna, och om det saknas returneras JavaScript-felet `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
Alla exempelinnehållssidor innehåller `cq.shared`, så allt innehåll som baseras på dem inkluderar automatiskt `cq.shared`. Om du vill skapa egna innehållssidor från grunden utan att basera dem på exempelinnehåll måste du se till att inkludera namnutrymmet `cq.shared`.
>
Mer information finns i [Använda bibliotek på klientsidan](/help/sites-developing/clientlibs.md).

## Göra en befintlig mall tillgänglig {#making-an-existing-template-available}

I det här exemplet visas hur du tillåter att en mall används för vissa innehållssökvägar. Mallarna som är tillgängliga för sidförfattaren när sidor skapas avgörs av logiken som definieras i [Malltillgänglighet](/help/sites-developing/templates.md#template-availability).

1. I CRXDE Lite går du till den mall som du vill använda för sidan, till exempel mallen Nyhetsbrev.
1. Ändra egenskapen `allowedPaths` och andra egenskaper som används för [malltillgänglighet](/help/sites-developing/templates.md#template-availability). `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` betyder till exempel att den här mallen tillåts i alla sökvägar under `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
