---
title: AEM Taggningsramverk
seo-title: AEM Taggningsramverk
description: Tagga innehåll och utnyttja infrastrukturen för AEM taggar
seo-description: Tagga innehåll och utnyttja infrastrukturen för AEM taggar
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# AEM Taggningsramverk {#aem-tagging-framework}

Så här taggar du innehåll och använder infrastrukturen för AEM taggar:

* Taggen måste finnas som en nod av typen ` [cq:Tag](#tags-cq-tag-node-type)` under [taxonomirotnoden](#taxonomy-root-node)

* NodeType för tagged content-noden måste innehålla [ `cq:Taggable`](#taggable-content-cq-taggable-mixin)-mixin
* [TagID](#tagid) läggs till i innehållsnodens [ `cq:tags`](#tagged-content-cq-tags-property)-egenskap och löses till en nod av typen ` [cq:Tag](#tags-cq-tag-node-type)`

## Taggar: cq:Tag Node Type {#tags-cq-tag-node-type}

Deklarationen för en tagg hämtas i databasen i en nod av typen `cq:Tag.`

En tagg kan vara ett enkelt ord (t.ex. himmel) eller motsvara en hierarkisk taxonomi (t.ex. frukt/äpple, vilket betyder både den generiska frukten och det mer specifika äpplet).

Taggar identifieras av ett unikt TagID.

En tagg har valfri metainformation, t.ex. en titel, lokaliserade titlar och en beskrivning. Titeln ska visas i användargränssnitt i stället för i TagID, om det finns.

Med taggningsramverket kan du även begränsa möjligheten för författare och besökare att endast använda specifika, fördefinierade taggar.

### Taggegenskaper {#tag-characteristics}

* nodtypen är `cq:Tag`
* nodnamnet är en komponent i ` [TagID](#tagid)`
* ` [TagID](#tagid)` innehåller alltid ett [namnutrymme](#tag-namespace)

* valfri `jcr:title`-egenskap (den titel som ska visas i användargränssnittet)

* valfri `jcr:description`-egenskap

* när den innehåller underordnade noder, kallas [behållartagg](#container-tags)
* lagras i databasen under en bassökväg som kallas [taxonomirotnod](#taxonomy-root-node)

### TaggID {#tagid}

Ett TagID identifierar en sökväg som löses till en taggnod i databasen.

TagID är vanligtvis ett kort TagID som börjar med namnutrymmet eller så kan det vara ett absolut TagID som börjar från [taxonomirotnoden](#taxonomy-root-node).

Om innehållet är taggat och inte finns ännu, läggs egenskapen ` [cq:tags](#tagged-content-cq-tags-property)` till i innehållsnoden och taggID läggs till i egenskapens värde för String-matrisen.

TagID består av ett [namnutrymme](#tag-namespace) följt av det lokala TagID:t. [Behållartaggar ](#container-tags) innehåller undertaggar som representerar en hierarkisk ordning i taxonomin. Undertaggar kan användas för att referera till taggar som är samma som alla lokala TagID. Det är till exempel tillåtet att tagga innehåll med&quot;frukt&quot;, även om det är en behållartagg med deltaggar, till exempel&quot;frukt/äpple&quot; och&quot;frukt/banan&quot;.

### Taxonomirotnod {#taxonomy-root-node}

Taxonomirotnoden är grundsökvägen för alla taggar i databasen. Taxonomirotnoden måste *inte* vara en nod av typen `  cq   :Tag`.

I AEM är bassökvägen `/content/  cq   :tags` och rotnoden är av typen `  cq   :Folder`.

### Namnområde för tagg {#tag-namespace}

Med namnutrymmen kan du gruppera saker. Det vanligaste användningsområdet är att ha ett namnutrymme per webbplats (till exempel public, internal och portal) eller per större program (till exempel WCM, Assets, Communities), men namnutrymmen kan användas för olika andra behov. Namnutrymmen används i användargränssnittet för att endast visa deluppsättningen taggar (d.v.s. taggar för ett visst namnutrymme) som är tillämpliga för det aktuella innehållet.

Taggens namnområde är den första nivån i taxonomiunderträdet, som är noden direkt under [taxonomirotnoden](#taxonomy-root-node). Ett namnutrymme är en nod av typen `cq:Tag` vars överordnade nod inte är en `cq:Tag`nodtyp.

Alla taggar har ett namnutrymme. Om inget namnutrymme anges tilldelas taggen standardnamnutrymmet, som är TagID `default` (titeln är `Standard Tags),`det är `/content/cq:tags/default.`

### Behållartaggar {#container-tags}

En behållartagg är en nod av typen `cq:Tag` som innehåller valfritt antal och typ av underordnade noder, vilket gör det möjligt att förbättra taggmodellen med anpassade metadata.

Dessutom fungerar behållartaggar (eller supertaggar) i en taxonomi som delsummering av alla undertaggar: Innehåll som till exempel är taggat med frukt/äpple anses också vara taggat med frukt, vilket innebär att om man söker efter innehåll som bara är taggat med frukt, hittas även innehållet som är taggat med frukt/äpple.

### Lösa tagg-ID:n {#resolving-tagids}

Om tagg-ID:t innehåller kolon &quot;:&quot; separerar kolon namnutrymmet från taggen eller undertaxonomin, som sedan separeras med vanliga snedstreck &quot;/&quot;. Om tagg-ID:t inte har ett kolon används standardnamnutrymmet.

Standardplatsen och den enda platsen för taggar är under /content/cq:tags.

Tagg som refererar till icke-befintliga sökvägar eller sökvägar som inte pekar på en cq:Tag-nod betraktas som ogiltiga och ignoreras.

I följande tabell visas några exempel på tagg-ID:n, deras element och hur tagg-ID:t tolkas till en absolut sökväg i databasen:

I följande tabell visas några exempel på tagg-ID:n, deras element och hur tagg-ID:t tolkas till en absolut sökväg i databasen:
I följande tabell visas några exempel på tagg-ID:n, deras element och hur tagg-ID:t tolkas till en absolut sökväg i databasen:

<table>
 <tbody>
  <tr>
   <td><strong>TaggID<br /> </strong></td>
   <td><strong>Namnutrymme</strong></td>
   <td><strong>Lokalt ID</strong></td>
   <td><strong>Behållartaggar</strong></td>
   <td><strong>Löv-tagg</strong></td>
   <td><strong>Databas<br /> Absolut taggsökväg</strong></td>
  </tr>
  <tr>
   <td>dam:frukt/äpple/braeburn</td>
   <td>dam</td>
   <td>frukt/äpple/braeburn</td>
   <td>frukt, äpple</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/Frukt/apple/braeburn</td>
  </tr>
  <tr>
   <td>färg/röd</td>
   <td>default</td>
   <td>färg/röd</td>
   <td>color</td>
   <td>röd</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>himmel</td>
   <td>standard</td>
   <td>himmel</td>
   <td>(inga)</td>
   <td>himmel</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>(inga)</td>
   <td>(inga)</td>
   <td>(ingen, namnutrymmet)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>kategori</td>
   <td>bil</td>
   <td>bil</td>
   <td>bil</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Lokalisering av taggtiteln {#localization-of-tag-title}

När taggen innehåller den valfria titelsträngen ( `jcr:title`) går det att lokalisera titeln för visning genom att lägga till egenskapen `jcr:title.<locale>`.

Mer information finns i

* [Taggar på olika språk](/help/sites-developing/building.md#tags-in-different-languages)  - som beskriver hur API:erna används
* [Hantera taggar på olika språk](/help/sites-administering/tags.md#managing-tags-in-different-languages)  - som beskriver hur du använder taggningskonsolen

### Åtkomstkontroll {#access-control}

Taggar finns som noder i databasen under [taxonomirotnoden](#taxonomy-root-node). Det går att skapa taggar i ett givet namnutrymme genom att ange lämpliga åtkomstkontrollistor i databasen och tillåta eller neka författare och besökare på platsen.

Om du dessutom nekar läsbehörighet för vissa taggar eller namnutrymmen kan du styra möjligheten att använda taggar för visst innehåll.

Ett typiskt exempel är:

* Tillåta skrivåtkomst för gruppen/rollen `tag-administrators` till alla namnutrymmen (lägg till/ändra under `/content/cq:tags`). Den här gruppen levereras med AEM.

* Ge användare/författare läsåtkomst till alla namnutrymmen som ska vara läsbara för dem (oftast alla).
* Ger användare/författare skrivåtkomst till de namnutrymmen där taggar ska kunna definieras fritt av användare/författare (add_node under `/content/cq:tags/some_namespace`)

## Taggbart innehåll: cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

För att programutvecklare ska kunna bifoga taggning till en innehållstyp måste nodens registrering ([CND](https://jackrabbit.apache.org/node-type-notation.html)) innehålla `cq:Taggable`-blandningen eller `cq:OwnerTaggable`-blandningen.

Blandningen `cq:OwnerTaggable`, som ärver från `cq:Taggable`, är avsedd att indikera att innehållet kan klassificeras av ägaren/författaren. I AEM är det bara ett attribut för noden `cq:PageContent`. `cq:OwnerTaggable`-blandningen krävs inte av taggningsramverket.

>[!NOTE]
>
>Du bör bara aktivera taggar på den översta noden i ett aggregerat innehållsobjekt (eller på dess jcr:content-nod). Exempel:
>
>* sidor ( `cq:Page`) där `jcr:content`noden är av typen `cq:PageContent` som innehåller `cq:Taggable`-mixen.
   >
   >
* resurser ( `cq:Asset`) där `jcr:content/metadata`-noden alltid har `cq:Taggable`-mixen.

>



### Nodtypsnotation (CND) {#node-type-notation-cnd}

Det finns nodtypsdefinitioner i databasen som CND-filer. CND-notationen definieras som en del av JCR-dokumentationen [här](https://jackrabbit.apache.org/node-type-notation.html).

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

Egenskapen `cq:tags` är en String-array som används för att lagra ett eller flera TagID:n när de tillämpas på innehåll av författare eller webbplatsbesökare. Egenskapen har bara betydelse när den läggs till i en nod som definieras med `[cq:Taggable](#taggable-content-cq-taggable-mixin)`-blandningen.

>[!NOTE]
>
>Om du vill utnyttja AEM taggningsfunktion ska anpassade utvecklade program inte definiera andra taggegenskaper än `cq:tags`.

## Flytta och sammanfoga taggar {#moving-and-merging-tags}

Nedan följer en beskrivning av effekterna i databasen när du flyttar eller sammanfogar taggar med [taggningskonsolen](/help/sites-administering/tags.md):

* När en tagg A flyttas eller sammanfogas till tagg B under `/content/cq:tags`:

   * tagg A tas inte bort och får en `cq:movedTo`-egenskap.
   * tagg B skapas (vid en flytt) och får en `cq:backlinks`-egenskap.

* `cq:movedTo` pekar på tagg B. Den här egenskapen innebär att tagg A har flyttats eller sammanfogats till tagg B. Om du flyttar tagg B uppdateras den här egenskapen i enlighet med detta. Tagg A är alltså dold och sparas bara i databasen för att matcha tagg-ID:n i innehållsnoder som pekar på tagg A. Taggskräpinsamlaren tar bort taggar som tagg A en gång och inga fler innehållsnoder pekar på dem.
Ett specialvärde för egenskapen `cq:movedTo` är `nirvana`: används när taggen tas bort men inte kan tas bort från databasen eftersom det finns undertaggar med ett `cq:movedTo` som måste behållas.

   >[!NOTE]
   >
   >Egenskapen `cq:movedTo` läggs bara till i den flyttade eller sammanslagna taggen om något av dessa villkor uppfylls:
   > 1. Taggen används i innehåll (vilket betyder att den har en referens) ELLER
   > 1. Taggen har underordnade objekt som redan har flyttats.


* `cq:backlinks` behåller referenserna i den andra riktningen, dvs. en lista över alla taggar som har flyttats till eller sammanfogats med tagg B. Detta krävs oftast för att hålla  `cq:movedTo`egenskaperna uppdaterade även när tagg B flyttas/sammanfogas/tas bort eller när tagg B aktiveras, och då måste även alla dess bakåttaggar aktiveras.

   >[!NOTE]
   >
   >Egenskapen `cq:backlinks` läggs bara till i den flyttade eller sammanslagna taggen om något av dessa villkor uppfylls:
   >
   > 1. Taggen används i innehåll (vilket betyder att den har en referens) ELLER    >
   > 1. Taggen har underordnade objekt som redan har flyttats.


* När du läser en `cq:tags`-egenskap för en innehållsnod utförs följande matchning:

   1. Om det inte finns någon matchning under `/content/cq:tags` returneras ingen tagg.
   1. Om taggen har en `cq:movedTo`-egenskap angiven följs det tagg-ID som refereras.
Det här steget upprepas så länge den efterföljande taggen har en `cq:movedTo`-egenskap.

   1. Om den följda taggen inte har någon `cq:movedTo`-egenskap läses taggen.

* Om du vill publicera ändringen när en tagg har flyttats eller sammanfogats måste noden `cq:Tag` och alla dess bakgrunder replikeras: detta görs automatiskt när taggen aktiveras i tagghanteringskonsolen.

* Senare uppdateringar av sidans `cq:tags`-egenskap rensar automatiskt de &quot;gamla&quot; referenserna. Detta utlöses eftersom en flyttad tagg som löses via API returnerar måltaggen och därmed anger måltaggens ID.

>[!NOTE]
>
>Förflyttning av taggar skiljer sig från migrering av taggar.

## Migrering av taggar {#tags-migration}

Taggar från och med Experience Manager 6.4 lagras under `/content/cq:tags`, som tidigare lagrats under `/etc/tags`. I scenarier där Adobe Experience Manager har uppgraderats från en tidigare version finns dock taggarna fortfarande på den gamla platsen `/etc/tags`. I uppgraderade system måste taggar migreras under `/content/cq:tags`.

>[!NOTE]
>
>På sidan Sidegenskaper för taggar rekommenderar vi att du använder tagg-ID (`geometrixx-outdoors:activity/biking`) i stället för att hårdkoda grundsökvägen för taggen (till exempel `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>`com.day.cq.tagging.servlets.TagListServlet` kan användas för att visa taggar.

>[!NOTE]
>
>Vi rekommenderar att du använder tagghanterings-API som resurs.

### Om den uppgraderade AEM instansen har stöd för TagManager API {#upgraded-instance-support-tagmanager-api}

1. I början av komponenten identifierar TagManager API om det är en uppgraderad AEM. I uppgraderat system lagras taggar under `/etc/tags`.

1. API:t TagManager körs sedan i bakåtkompatibilitetsläge, vilket innebär att API:t använder `/etc/tags` som bassökväg. Annars används den nya platsen `/content/cq:tags`.

1. Uppdatera platsen för taggarna.

1. Kör följande skript när du har migrerat taggar till den nya platsen:

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

Skriptet hämtar alla taggar som har `/etc/tags` i värdet för egenskapen `cq:movedTo/cq:backLinks`. Sedan itereras den genom den hämtade resultatuppsättningen och tolkar egenskapsvärdena `cq:movedTo` och `cq:backlinks` till `/content/cq:tags`-sökvägar (om `/etc/tags` upptäcks i värdet).

### Om den uppgraderade AEM instansen körs på det klassiska användargränssnittet {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>Klassiskt användargränssnitt är inte noll som är nedtidskompatibelt och stöder inte ny taggbassökväg. Om du vill använda ett klassiskt användargränssnitt än `/etc/tags` måste skapas följt av `cq-tagging` komponentomstart.

Vid uppgradering AEM instanser som stöds av TagManager API och körs i Classic UI:

1. När referenser till den gamla taggbassökvägen `/etc/tags` har ersatts med tagId eller den nya taggplatsen `/content/cq:tags` kan du migrera taggar till den nya platsen `/content/cq:tags` i CRX följt av komponentomstart.

1. Kör skriptet ovan när du har migrerat taggar till den nya platsen.
