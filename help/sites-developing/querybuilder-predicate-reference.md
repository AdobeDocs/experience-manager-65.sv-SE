---
title: Predikatreferens för Query Builder
description: Fullständig predikatreferens för Query Builder API.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 0%

---

# Predikatreferens för Query Builder{#query-builder-predicate-reference}

>[!CAUTION]
>
>Informationen på denna sida är inte uttömmande.
>
>Mer information finns i listan under **Tillgängliga predikat** på felsökningskonsolen i Query Builder, till exempel:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>Se till exempel:
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## Allmänt {#general}

* [root](#root)
* [grupp](#group)
* [orderby](#orderby)

## Predikat {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [innehållfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [exkluderingar](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [fulltext](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [språk](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [huvudtillgång](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [medlemOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [inte utgånget](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [bana](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [property](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeProperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativ](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [sparad fråga](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [liknande](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [type](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Matchar JCR BOOLEAN-egenskaper. Endast värdena &quot; `true`och &quot; `false`&quot;. If &quot; `false`&quot;, matchar om egenskapen har värdet &quot; `false`&quot; eller om den inte finns alls. Detta kan vara användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Ärvda &quot; `operation`parametern har ingen betydelse.

Stöder extrahering av ansikten. Tillhandahåller bucket för varje `true` eller `false` värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **boolproperty**
Relativ sökväg till egenskap, till exempel `myFeatureEnabled` eller `jcr:content/myFeatureEnabled`.

* **value**
Värde att kontrollera egenskap för, &quot; `true`&quot; eller &quot; `false`&quot;.

### innehållfragment {#contentfragment}

Begränsar resultatet till innehållsfragment.

Filtrering stöds inte.

Stöder inte facetextrahering.

#### Egenskaper {#properties-1}

* **innehållfragment**
Den kan användas med vilket värde som helst för att kontrollera om det finns innehållsfragment.

### dateComparison {#datecomparison}

Jämför två JCR DATE-egenskaper med varandra. Du kan testa om de är lika, olika, större än eller större än eller lika med.

Detta är ett predikat som bara kan filtreras och det går inte att använda ett sökindex.

#### Egenskaper {#properties-2}

* **property1**

  Sökväg till första datumegenskap.

* **property2**

  Sökväg till andra datumegenskap.

* **operation**

  &quot; `equals`&quot; för exakt matchning, &quot; `!=`&quot; för jämförelse av skillnader, &quot; `greater`&quot; for property1 större än property2, &quot; `>=`&quot; för property1 större än eller lika med property2. Standardvärdet är &quot; `equals`&quot;.

### daterange {#daterange}

Matchar JCR DATE-egenskaper mot ett datum/tidsintervall. Detta använder ISO8601-formatet för datum och tider ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges i antal millisekunder sedan 1970 i UTC-tidszonen, UNIX®-tidsformatet.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Stöder extrahering av ansikten. Innehåller fickorna&quot;idag&quot;,&quot;den här veckan&quot;,&quot;den här månaden&quot;,&quot;de senaste tre månaderna&quot;,&quot;det här året&quot;,&quot;det senaste året&quot; och&quot;tidigare än det senaste året&quot;.

Filtrering stöds inte.

#### Egenskaper {#properties-3}

* **property**

  Relativ sökväg till en `DATE` egenskap, till exempel `jcr:lastModified`.

* **lowerBound**

  Lägre bindningsdatum till check-egenskap, till exempel `2014-10-01`.

* **lowerOperation**

  &quot; `>`&quot; (nyare) eller &quot; `>=`&quot; (på eller nyare), gäller för `lowerBound`. Standardvärdet är &quot; `>`&quot;.

* **upperBound**

  Övre gräns till check property for, till exempel `2014-10-01T12:15:00`.

* **upperOperation**

  &quot; `<`&quot; (äldre) eller &quot; `<=`&quot; (vid eller äldre), gäller för `upperBound`. Standardvärdet är &quot; `<`&quot;.

* **timeZone**

  ID för den tidszon som ska användas när den inte anges som en ISO-8601-datumsträng. Standardvärdet är systemets standardtidszon.

### exkluderingar {#excludepaths}

Utesluter noder från resultatet där deras sökväg matchar ett reguljärt uttryck.

Detta är ett predikat som bara kan filtreras och det går inte att använda ett sökindex.

Stöder inte facetextrahering.

#### Egenskaper {#properties-4}

* **exkluderingar**

  Reguljära uttryck matchade mot resultatsökvägar, utan matchande sökvägar från resultatet.

### fulltext {#fulltext}

Söker efter termer i fulltextindexet.

Filtrering stöds inte.

Stöder inte facetextrahering.

#### Egenskaper {#properties-5}

* **fulltext**

  Fulltextsöktermer.

* **relPath**

  Den relativa sökvägen som ska sökas i egenskapen eller undernoden. Den här egenskapen är valfri.

### grupp {#group}

Tillåter att kapslade villkor skapas. Grupper kan innehålla kapslade grupper. Allt i en fråga i en frågeverktyget ingår implicit i en rotgrupp som kan ha `p.or` och `p.not` parametrar också.

Exempel på matchning av en av två egenskaper mot ett värde:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Detta är begreppsmässigt `(1_property` ELLER `2_property)`.

Exempel för kapslade grupper:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Detta söker efter termen &quot;**Förvaltning**&quot; på sidor i `/content/geometrixx/en` eller i tillgångar i `/content/dam/geometrixx`.

Detta är begreppsmässigt `fulltext AND ( (path AND type) OR (path AND type) )`. Sådana ELLER-kopplingar behöver bra index för att fungera.

#### Egenskaper {#properties-6}

* **p.or**

  Om inställt på &quot; `true`&quot;, måste bara ett predikat i gruppen matcha. Standardvärdet är &quot; `false`&quot;, vilket betyder att alla måste matcha

* **p.not**

  Om inställt på &quot; `true`&quot;, negeras gruppen (standardvärdet är &quot; `false`&quot;).

* **&lt;predicate>**

  Lägger till kapslade predikat.

* **N_&lt;predicate>**

  Lägger till flera kapslade predikat samtidigt, som `1_property, 2_property, ...`.

### hasPermission {#haspermission}

Begränsar resultatet till objekt där den aktuella sessionen har den angivna [JCR-behörighet.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Detta är ett predikat som bara kan filtreras och det går inte att använda ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **hasPermission**

  Kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ALLA ha noden i fråga. Till exempel: `jcr:write`, `jcr:modifyAccessControl`.

### språk {#language}

Söker efter CQ-sidor på ett visst språk. Det här tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språket i en webbplatsstruktur på den översta nivån.

Detta är ett predikat som bara kan filtreras och det går inte att använda ett sökindex.

Stöder extrahering av ansikten. Tillhandahåller bucket för varje unik språkkod.

#### Egenskaper {#properties-8}

* **språk**

  ISO-språkkod, till exempel &quot;`de`&quot;

### huvudtillgång {#mainasset}

Kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Detta är i stort sett alla noder som inte finns i en delresursnod. Detta söker inte efter `dam:Asset` nodtyp. Ange &quot; `mainasset=true`&quot; eller &quot; `mainasset=false`&quot;, det finns inga fler egenskaper.

Detta är ett predikat som bara kan filtreras och det går inte att använda ett sökindex.

Stöder facet-extrahering och ger två möjligheter för huvud- och delresurser.

#### Egenskaper {#properties-9}

* **huvudtillgång**

  Boolean, &quot; `true`&quot; for main assets, &quot; `false`&quot; för delresurser.

### medlemOf {#memberof}

Söker efter objekt som tillhör en viss [resursinsamling för sling](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Detta är ett predikat som bara kan filtreras och det går inte att använda ett sökindex. Stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **medlemOf**

  Sökväg till Sling-resurssamling.

### nodename {#nodename}

Matchar JCR-nodnamn.

Stöder extrahering av ansikten. Anger bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **nodename**

  Nodnamnsmönster som tillåter jokertecken: `*` = ett eller inga tecken, `?` = any char, `[abc]` = endast tecken inom hakparenteser.

### inte utgånget {#notexpired}

Matchar objekt genom att kontrollera om en JCR DATE-egenskap är större eller lika med den aktuella servertiden. Detta kan användas för att kontrollera en `expiresAt`&quot; som date-egenskap och begränsa till endast de som ännu inte har gått ut ( `notexpired=true`) eller som redan har gått ut ( `notexpired=false`).

Filtrering stöds inte.

Stöder facet-extrahering på samma sätt som daterange-predikatet.

#### Egenskaper {#properties-12}

* **inte utgånget**

  Boolean, &quot; `true`&quot; för ännu inte förfallit (datum i framtiden eller lika med), &quot; `false`&quot; för utgången (tidigare datum) (obligatoriskt).

* **property**

  Relativ sökväg till `DATE` egenskap som ska kontrolleras (obligatoriskt).

### orderby {#orderby}

Låter resultaten sorteras. Om det krävs en ordning efter flera egenskaper måste predikatet läggas till flera gånger med talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **orderby**

  Antingen JCR-egenskapsnamn som anges av t.ex. ett radavstånd på @ `@jcr:lastModified` eller `@jcr:content/jcr:title`eller ett annat predikat i frågan, till exempel `2_property`, som vi ska sortera efter.

* **sortera**

  Sorteringsriktning, antingen `desc`&quot; för fallande eller &quot; `asc`&quot; för stigande (standard).

* **case**

  Om inställt på `ignore`, blir sorteringsskiftläget okänsligt, vilket innebär att&quot;a&quot; kommer före&quot;B&quot;. Om det är tomt eller utelämnas är sorteringen skiftlägeskänslig, vilket innebär att&quot;B&quot; kommer före&quot;a&quot;

### bana {#path}

Söker i en viss bana.

Stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **bana**

  Banmönster. Beroende på exakt, matchar antingen hela underträdet (som att lägga till `//*` in xpath, but note that this does not include the base path) (exact=false, default), or only an exact path, which can include wilcards ( `*`); om self anges genomsöks hela underträdet inklusive basnoden.

* **exakt**

  If `exact` är true/on, den exakta sökvägen måste matcha, men den kan innehålla enkla jokertecken ( `*`), som matchar namn, men inte &quot; `/`&quot;; om det är false (standard) inkluderas alla underordnade (valfritt).

* **platt**

  Söker bara efter direkt underordnade objekt (som att lägga till &quot; `/*`&quot; in xpath) (används endast om &quot; `exact`&#39; är inte sant, valfritt).

* **self**

  Söker i underträdet men inkluderar basnoden som angetts som sökväg (inga jokertecken).

### property {#property}

Matchar JCR-egenskaper och deras värden.

Stöder extrahering av ansikten. Innehåller grupper för varje unikt egenskapsvärde i resultatet.

#### Egenskaper {#properties-15}

* **property**

  Relativ sökväg till egenskap, till exempel `jcr:title`.

* **value**

  Värde som egenskapen ska kontrolleras för; följer JCR-egenskapstypen till strängkonverteringar.

* **N_värde**

  Använd `1_value`, `2_value`, ... för att kontrollera om det finns flera värden (i kombination med `OR` som standard med `AND` if och=true) (sedan 5.3).

* **och**

  Ange som true för att kombinera flera värden ( `N_value`) med OCH (sedan 5.3).

* **operation**

  &quot;`equals`&quot; för exakt matchning (standard), &quot; `unequals`&quot; för jämförelse av skillnader, &quot; `like`&quot; för att använda `jcr:like` xpath-funktion (valfri), &quot; `not`&quot; för ingen matchning (till exempel &quot;`not(@prop)`&quot; in xpath, value param is ignore) eller &quot; `exists`&quot; for exist check (value can be true - property must exist, the default - or false - same as &quot; `not`&quot;).

* **djup**

  Antal jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (till exempel `property=size depth=2` kontrollerar nod/storlek, nod/&amp;ast;/size och nod/&amp;ast;/&amp;ast;/size).

### rangeProperty {#rangeproperty}

Matchar en JCR-egenskap mot ett intervall. Detta gäller egenskaper med linjär typ som `LONG`, `DOUBLE`och `DECIMAL`. För `DATE`, se daterange-predikatet som har optimerade indata för datumformat.

Du kan definiera en nedre gräns och en övre gräns eller endast en av dem. Åtgärden (t.ex. &quot;mindre än&quot; eller &quot;mindre eller lika med&quot;) kan också anges individuellt för den nedre och övre gränsen.

Stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **property**

  Relativ sökväg till egenskap.

* **lowerBound**

  Lägre gräns för att kontrollera egenskap för.

* **lowerOperation**

  &quot; `>`&quot; (standard) eller &quot; `>=`&quot;, gäller för `lowerValue`

* **upperBound**

  Övre gräns för att kontrollera egenskap för.

* **upperOperation**

  &quot; `<`&quot; (standard) eller &quot; `<=`&quot;, gäller för `lowerValue`

* **decimal**

  &quot; `true`&quot; om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Matchar `JCR DATE` egenskaper mot ett datum/tidsintervall med tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` med ett millisekundvärde eller bugzillasyntax `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Prefix med &quot; `-`&quot; om du vill ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound`blir den andra standardvärdet 0, vilket innebär den aktuella tiden.

Till exempel:

* `upperBound=1h` (och nej) `lowerBound`) skulle välja vad som helst under nästa timme
* `lowerBound=-1d` (och nej) `upperBound`) skulle välja vad som helst de senaste 24 timmarna
* `lowerBound=-6M` och `upperBound=-3M` väljer du mellan 6 månader och 3 månader
* `lowerBound=-1500` och `upperBound=5500` kan välja mellan 1 500 millisekunder tidigare och 5 500 millisekunder i framtiden
* `lowerBound=1d` och `upperBound=2d` skulle välja vad som helst i övermorgon

Den tar inte hänsyn till skottår och alla månader är 30 dagar.

Filtrering stöds inte.

Stöder facet-extrahering på samma sätt som daterange-predikatet.

#### Egenskaper {#properties-17}

* **upperBound**

  Övre gräns i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd &quot;-&quot; för negativ offset.

* **lowerBound**

  Nedre gräns för datum i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd &quot;-&quot; för negativ offset.

### root {#root}

Rotpredikatgrupp. Stöder alla funktioner i en grupp och låter dig ange globala frågeparametrar.

Namnet &quot;root&quot; används aldrig i en fråga, det är implicit.

#### Egenskaper {#properties-18}

* **p.offset**

  Numret som anger början på resultatsidan, det vill säga hur många objekt som ska hoppas över.

* **p.limit**

  Numret som anger sidstorleken.

* **p.gissningTotal**

  Rekommenderas: undvik att beräkna det totala resultatet som kan vara kostsamt; antingen en siffra som anger det högsta antalet som ska räknas upp till (t.ex. 1000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat) eller &quot; `true`&quot; för att endast räkna upp till det minsta nödvändiga `p.offset` + `p.limit`.

* **p.excerpt**

  Om inställt på &quot; `true`&quot;, inkludera utdrag av fullständig text i resultatet.

* **p.hits**

  (endast för JSON-servern) väljer du hur träffar skrivs som JSON, med dessa standardinställningar (utbyggbara via ResultHitWriter-tjänsten):

   * **enkel**:

     Minimala objekt som `path`, `title`, `lastmodified`, `excerpt` (om angivet).

   * **full**:

     Sling JSON rendering of the node, with `jcr:path` anger träffens sökväg: som standard visas bara nodens direkta egenskaper, inklusive ett djupare träd med `p.nodedepth=N`, med 0 betyder hela det oändliga underträdet, lägg till `p.acls=true` för att inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).

   * **selektiv**:

     Endast egenskaper som anges i `p.properties`, som är en blankstegsavgränsad lista (använd &quot;+&quot; i URL:er) med relativa sökvägar. Om den relativa sökvägen har ett djup > 1 representeras de som underordnade objekt. Den speciella egenskapen jcr:path innehåller sökvägen till träffen

### sparad fråga {#savedquery}

Inkluderar alla predikat för en beständig frågebyggarfråga i den aktuella frågan som ett undergruppsprediat.

Detta kör inte en extra fråga utan utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan vara en strängegenskap med flera rader eller en `nt:file` nod som innehåller frågan som en textfil i Java™-egenskapsformat.

Stöder inte facetextrahering för predikaten i den sparade frågan.

#### Egenskaper {#properties-19}

* **sparad fråga**

  Sökväg till den sparade frågan (egenskapen String eller `nt:file` nod).

### liknande {#similar}

Likhetssökning med JCR XPath `rep:similar()`.

Filtrering stöds inte. Stöder inte facetextrahering.

#### Egenskaper {#properties-20}

* **liknande**
Absolut sökväg till noden som liknande noder ska hittas för.

* **lokal**
En relativ sökväg till en underordnad nod eller `.` för den aktuella noden (valfritt) är &quot; `.`&quot;).

### tag {#tag}

Söker efter innehåll som har taggats med en eller flera taggar genom att ange sökvägar för taggtiteln.

Stöder extrahering av ansikten. Tillhandahåller bucket för varje unik tagg med hjälp av den aktuella taggtitelsökvägen.

#### Egenskaper {#properties-21}

* **tag**

  Taggtitelsökväg som du vill söka efter, t.ex. &quot;Resursegenskaper : Orientation / Landscape&quot;.

* **N_värde**

  Använd `1_value`, `2_value`, ... för att kontrollera om det finns flera taggar (i kombination med `OR` som standard med `AND` if och=true) (sedan 5.6).

* **property**

  Egenskap (eller relativ sökväg till egenskap) som ska kontrolleras (standard) `cq:tags`&quot;)

### tagid {#tagid}

Söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Stöder extrahering av ansikten. Tillhandahåller bucket för varje unik tagg med deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **tagid**

  Tagg-id så att du till exempel kan leta efter&quot; `properties:orientation/landscape`&quot;.

* **N_värde**

  Använd `1_value`, `2_value`, ... för att kontrollera om det finns flera taggar (i kombination med `OR` som standard med `AND` if och=true) (sedan 5.6).

* **property**

  Egenskap (eller relativ sökväg till egenskap) som ska kontrolleras (standard) `cq:tags`&quot;).

### tagsearch {#tagsearch}

Söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Detta söker först efter taggar som innehåller dessa nyckelord i sina titlar och begränsar sedan resultatet till endast objekt som taggats med dessa.

Stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **tagsearch**

  Nyckelord att söka efter i taggtitlar.

* **property**

  Egenskap (eller relativ sökväg till egenskap) som ska undersökas (standard) `cq:tags`).

* **lang**

  Om du bara vill söka i en viss lokaliserad taggtitel (till exempel `de`).

* **alla**

  (bool) Sök i hela taggens fulltext, det vill säga alla titlar, beskrivning och så vidare. Har företräde framför&quot;l&quot; `ang`&quot;.

### type {#type}

Begränsar resultaten till en viss JCR-nodtyp, både primär nodtyp och blandningstyp. Detta söker även efter undertyper av den nodtypen. Databasens sökindex måste omfatta nodtyperna för effektiv körning.

Stöder extrahering av ansikten. Innehåller grupper för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **type**

  Nodtyp eller mixnamn att söka efter, till exempel `cq:Page`.
