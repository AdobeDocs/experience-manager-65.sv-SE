---
title: AEM Taggningsramverk
description: Tagga innehåll och använda infrastrukturen för AEM taggar
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 8dafa901bc628ee5e4823e9f8811bf4d09b7e072
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# AEM Taggningsramverk {#aem-tagging-framework}

Taggning gör att innehållet kan kategoriseras och struktureras. Taggar kan klassificeras med ett namnutrymme och en taxonomi. Mer information om hur du använder taggar:

* Se dokumentet [Använda taggar](/help/sites-authoring/tags.md) om du vill ha information om hur du taggar innehåll som innehållsförfattare.
* Se dokumentet [Administrera taggar](/help/sites-administering/tags.md) för administratörens perspektiv på att skapa och hantera taggar och på vilka innehållstaggar har tillämpats.

Den här artikeln fokuserar på det underliggande ramverket som stöder taggning i AEM och hur det används som utvecklare.

## Introduktion {#introduction}

Så här taggar du innehåll och använder infrastrukturen för AEM taggar:

* Taggen måste finnas som en nod av typen `[cq:Tag](#tags-cq-tag-node-type)` under [taxonomirotnod.](#taxonomy-root-node)

* Taggad innehåll-nodens `NodeType` måste innehålla [`cq:Taggable`](#taggable-content-cq-taggable-mixin) blanda.
* The [`TagID`](#tagid) läggs till i innehållsnodens [`cq:tags`](#tagged-content-cq-tags-property) -egenskap och löses till en nod av typen ` [cq:Tag](#tags-cq-tag-node-type)`.

## Taggar: cq:Tag Node Type  {#tags-cq-tag-node-type}

Deklarationen för en tagg hämtas i databasen i en nod av typen `cq:Tag`.

En tagg kan vara ett enkelt ord (till exempel `sky`) eller representerar en hierarkisk taxonomi (t.ex. `fruit/apple`, vilket betyder både det generiska `fruit` och mer specifikt `apple`).

Taggar identifieras av ett unikt TagID.

En tagg har valfri metainformation, t.ex. en titel, lokaliserade titlar och en beskrivning. Titeln ska visas i användargränssnitt i stället för i TagID, om det finns.

Med taggningsramverket kan du även begränsa möjligheten för författare och besökare att endast använda specifika, fördefinierade taggar.

### Märkordsegenskaper {#tag-characteristics}

* Nodtypen är `cq:Tag`n
* Nodnamnet är en komponent i [TaggID](#tagid).
* The [TaggID](#tagid) innehåller alltid [namnutrymme.](#tag-namespace)
* The `jcr:title` -egenskapen (titeln som ska visas i användargränssnittet) är valfri.
* The `jcr:description` -egenskapen är valfri.
* När taggen innehåller underordnade noder kallas den för [behållartagg.](#container-tags)
* Taggen lagras i databasen under en bassökväg som kallas [taxonomirotnod.](#taxonomy-root-node)

Eftersom taggar bara är JCR-noder måste nodnamnen förstås följa de [JCR-namnkonvention.](naming-conventions.md)

### TaggID {#tagid}

Ett TagID identifierar en sökväg som löses till en taggnod i databasen.

TagID är vanligtvis ett kort TagID som börjar med namnutrymmet eller så kan det vara ett absolut TagID från [taxonomirotnod.](#taxonomy-root-node)

Om innehållet är taggat och inte finns än, `[cq:tags](#tagged-content-cq-tags-property)` -egenskapen läggs till i innehållsnoden och taggID läggs till i egenskapens `String` arrayvärde.

TagID består av en [namespace](#tag-namespace) följt av det lokala TagID:t. [Behållartaggar](#container-tags) har undertaggar som representerar en hierarkisk ordning i taxonomin. Undertaggar kan användas för att referera till taggar som är samma som alla lokala TagID. Du kan till exempel tagga innehåll med `fruit` tillåts, även om det är en behållartagg med undertaggar, som `fruit/apple` och `fruit/banana`.

### Taxonomirotnod {#taxonomy-root-node}

Taxonomirotnoden är grundsökvägen för alla taggar i databasen. Taxonomirotnoden får inte vara en nod av typen `cq:Tag`.

I AEM är bassökvägen `/content/cq:tags` och rotnoden är av typen `cq:Folder`.

### Namnutrymme för tagg {#tag-namespace}

Med namnutrymmen kan du gruppera saker. Det vanligaste användningsexemplet är ett namnutrymme per webbplats (t.ex. public, internal och portal) eller per större program (t.ex. WCM, Assets, Communities). Men namnutrymmen kan användas för olika behov. Namnutrymmen används i användargränssnittet för att endast visa deluppsättningen taggar (d.v.s. taggar för ett visst namnutrymme) som är tillämpliga för det aktuella innehållet.

Taggens namnutrymme är den första nivån i taxonomiunderträdet, som är noden direkt under [taxonomirotnod](#taxonomy-root-node). Ett namnutrymme är en nod av typen `cq:Tag` vars överordnade inte är en `cq:Tag` nodtyp.

Alla taggar har ett namnutrymme. Om inget namnutrymme anges tilldelas taggen standardnamnutrymmet, som är TagID `default` med rubriken `Standard Tags`, dvs. `/content/cq:tags/default`.

### Behållartaggar {#container-tags}

En behållartagg är en nod av typen `cq:Tag` som innehåller valfritt antal och valfri typ av underordnade noder, vilket gör det möjligt att förbättra taggmodellen med anpassade metadata.

Dessutom fungerar behållartaggar (eller supertaggar) i en taxonomi som undertaggar till alla undertaggar. Innehåll som du t.ex. taggat med `fruit/apple` anses vara taggad med `fruit` också. Det vill säga, söka efter innehåll taggat med `fruit` söker även efter innehåll som taggats med `fruit/apple`.

### Lösa tagg-ID:n {#resolving-tagids}

Om tagg-ID:t innehåller ett kolon (`:`) separerar kolon namnutrymmet från taggen eller undertaxonomin, som separeras ytterligare med snedstreck (`/`). Om TagID inte har ett kolon används standardnamnutrymmet.

Standardplatsen och den enda platsen för taggar är under `/content/cq:tags`.

Tagg som refererar till icke-befintliga banor eller banor som inte pekar på en `cq:Tag` noden betraktas som ogiltig och ignoreras.

I följande tabell visas några exempel på tagg-ID:n, deras element och hur tagg-ID:t tolkas till en absolut sökväg i databasen:

| TaggID | Namnutrymme | Lokalt ID | Behållartaggar | Lövtagg | Databassökväg för absolut tagg |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | Ingen | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | Ingen | Ingen | Inget, namnutrymmet | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### Lokalisering av taggtitel {#localization-of-tag-title}

När -taggen innehåller den valfria titelsträngen ( `jcr:title`) går det att lokalisera titeln för visning genom att lägga till egenskapen `jcr:title.<locale>`.

Mer information finns i följande dokument:

* [Taggar på olika språk](/help/sites-developing/building.md#tags-in-different-languages)som beskriver hur API:erna används
* [Hantera taggar på olika språk](/help/sites-administering/tags.md#managing-tags-in-different-languages)som beskriver hur taggningskonsolen används

### Åtkomstkontroll {#access-control}

Taggar finns som noder i databasen under [taxonomirotnod](#taxonomy-root-node). Du kan skapa taggar i ett givet namnutrymme genom att ange lämpliga åtkomstkontrollistor i databasen, så att författare och besökare kan neka eller neka åtkomst.

Om du dessutom nekar läsbehörighet för vissa taggar eller namnutrymmen kan du använda taggar för visst innehåll.

Ett typiskt exempel är:

* Tillåta `tag-administrators` skrivåtkomst för grupp/roll till alla namnutrymmen (lägg till/ändra under `/content/cq:tags`). Den här gruppen levereras med AEM.
* Ge användare/författare läsåtkomst till alla namnutrymmen som ska vara läsbara för dem (oftast alla).
* Ger användare/författare skrivåtkomst till de namnutrymmen där taggar ska kunna definieras fritt av användare/författare (lägg till en nod under `/content/cq:tags/some_namespace`)

## Taggbart innehåll: cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

För programutvecklare som vill bifoga taggning till en innehållstyp, nodens registrering ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) måste innehålla `cq:Taggable` blanda eller `cq:OwnerTaggable` blanda.

The `cq:OwnerTaggable` mixin, som ärver från `cq:Taggable`, är avsedd att indikera att innehållet kan klassificeras av ägaren/författaren. I AEM är det bara ett attribut för `cq:PageContent` nod. The `cq:OwnerTaggable` mixin krävs inte av taggningsramverket.

>[!NOTE]
>
>Du bör bara aktivera taggar på den översta noden i ett aggregerat innehållsobjekt (eller på dess `jcr:content` nod). Exempel:
>
>* Sidor (`cq:Page`) där `jcr:content`noden är av typen `cq:PageContent` som innehåller `cq:Taggable` blanda
>* Resurser ( `cq:Asset`) där `jcr:content/metadata` noden har alltid `cq:Taggable` blanda
>

### Nodtypsnotation (CND) {#node-type-notation-cnd}

Det finns nodtypsdefinitioner i databasen som CND-filer. CND-notation definieras som en del av JCR-dokumentationen [här](https://jackrabbit.apache.org/jcr/node-type-notation.html).

De viktigaste definitionerna för de nodtyper som ingår i AEM är följande:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## Taggat innehåll: cq:tagg, egenskap {#tagged-content-cq-tags-property}

The `cq:tags` egenskapen är en `String` -matris som används för att lagra ett eller flera tagg-ID när de tillämpas på innehåll av författare eller webbplatsbesökare. Egenskapen har bara betydelse när den läggs till i en nod som definieras med `[cq:Taggable](#taggable-content-cq-taggable-mixin)` blanda.

>[!NOTE]
>
>Om du vill använda AEM taggningsfunktioner bör anpassade utvecklade program inte definiera andra taggegenskaper än `cq:tags`.

## Flytta och sammanfoga taggar {#moving-and-merging-tags}

Nedan följer en beskrivning av effekterna i databasen när du flyttar eller sammanfogar taggar med [taggningskonsol](/help/sites-administering/tags.md):

* När en tagg A flyttas eller sammanfogas till tagg B under `/content/cq:tags`:

   * Tagg A tas inte bort och en `cq:movedTo` -egenskap.
   * Tagg B skapas (om det finns en flytt) och får en `cq:backlinks` -egenskap.

* `cq:movedTo` pekar på tagg B.

   * Den här egenskapen innebär att tagg A har flyttats eller sammanfogats till tagg B. Om du flyttar tagg B uppdateras den här egenskapen i enlighet med detta. Tagg A är alltså dold och sparas bara i databasen för att matcha tagg-ID:n i innehållsnoder som pekar på tagg A. Taggskräpinsamlaren tar bort taggar som tagg A en gång och inga fler innehållsnoder pekar på dem.

   * Ett specialvärde för `cq:movedTo` egenskapen är `nirvana`. Den används när taggen tas bort men inte kan tas bort från databasen eftersom det finns undertaggar med en `cq:movedTo` som måste behållas.

  >[!NOTE]
  >
  >The `cq:movedTo` egenskapen läggs bara till i den flyttade eller sammanfogade taggen om något av dessa villkor uppfylls:
  >
  >1. Taggen används i innehåll (vilket innebär att den har en referens) eller
  >1. Taggen har underordnade objekt som redan har flyttats.

* `cq:backlinks` behåller referenserna i den andra riktningen. Det innebär att det finns en lista med alla taggar som har flyttats till eller sammanfogats med tagg B. Detta krävs oftast för att behålla `cq:movedTo` egenskaperna är uppdaterade även när tagg B flyttas/sammanfogas/tas bort eller när tagg B aktiveras, och då måste även alla dess bakåttaggar aktiveras.

  >[!NOTE]
  >
  >The `cq:backlinks` egenskapen läggs bara till i den flyttade eller sammanfogade taggen om något av dessa villkor uppfylls:
  >
  >1. Taggen används i innehåll (vilket innebär att den har en referens) ELLER
  >1. Taggen har underordnade objekt som redan har flyttats.

* Läsa en `cq:tags` -egenskapen för en innehållsnod omfattar följande upplösning:

   1. Om det inte finns någon matchning under `/content/cq:tags`, returneras ingen tagg.

   1. Om taggen har en `cq:movedTo` egenskapsuppsättningen följs det refererade tagg-ID:t.

      * Det här steget upprepas så länge som den efterföljande taggen har en `cq:movedTo` -egenskap.

   1. Om den följande taggen inte har en `cq:movedTo` -egenskapen läses taggen.

* Om du vill publicera ändringen när en tagg har flyttats eller sammanfogats väljer du `cq:Tag` noden och alla dess bakgrunder måste replikeras. Detta görs automatiskt när taggen aktiveras i tagghanteringskonsolen.

* Senare uppdateringar av sidans `cq:tags` egenskapen rensar automatiskt de gamla referenserna. Detta utlöses eftersom en flyttad tagg som löses via API returnerar måltaggen och därmed anger måltaggens ID.

>[!NOTE]
>
>Förflyttning av taggar skiljer sig från migrering av taggar.

## Taggmigrering {#tags-migration}

Sedan Adobe Experience Manager 6.4 lagras taggar i `/content/cq:tags` Tidigare versioner lagrade taggar under `/etc/tags`.

När du uppgraderar ett AEM från en version som är tidigare än 6.4 måste taggar migreras till `/content/cq:tags`. Se dokumentet [Omstrukturering av de gemensamma tillgångarna i AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) för mer information.
