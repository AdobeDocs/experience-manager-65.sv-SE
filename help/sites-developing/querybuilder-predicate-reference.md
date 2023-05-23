---
title: Predikatreferens för Query Builder
seo-title: Query Builder Predicate Reference
description: Fullständig predikatreferens för Query Builder API.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: f97eb2e028263016131b0c86be5a0508ae4def9b
workflow-type: tm+mt
source-wordcount: '2371'
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
* [exkluderingsdjup](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [fulltext](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [språk](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [huvudtillgång](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [medlemOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [inte utgånget](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [bana](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [property](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangegenskap](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativ](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [sparad fråga](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [liknande](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [type](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Matchar JCR BOOLEAN-egenskaper. Accepterar endast värdena &quot; `true`&quot; och &quot; `false`&quot;. Vid &quot; `false`&quot;, matchar det om egenskapen har värdet &quot; `false`&quot; eller om den inte finns alls. Detta kan vara användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Ärvda &quot; `operation`parametern har ingen betydelse.

Stöder facetextrahering. Tillhandahåller bucklar för varje `true` eller `false` värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **boolproperty**
relativ sökväg till egenskap, till exempel 
`myFeatureEnabled` eller `jcr:content/myFeatureEnabled`

* **value**
värde att kontrollera egenskap för, &quot; 
`true`&quot; eller &quot; `false`&quot;

### innehållfragment {#contentfragment}

Begränsar resultatet till innehållsfragment.

Filtrering stöds inte.

Stöder inte facetextrahering.

#### Egenskaper {#properties-1}

* **innehållfragment**
Den kan användas med vilket värde som helst för att kontrollera om det finns innehållsfragment.

### dateComparison {#datecomparison}

Jämför två JCR DATE-egenskaper med varandra. Kan testa om de är lika, olika, större än eller större än eller lika med.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

#### Egenskaper {#properties-2}

* **property1**

   path to first date property

* **property2**

   path to second date, egenskap

* **operation**

   &quot; `equals`&quot; för exakt matchning, &quot; `!=`&quot; för jämförelse av skillnader, &quot; `greater`&quot; for property1 större än property2, &quot; `>=`&quot; för property1 större än eller lika med property2. Standardvärdet är &quot; `equals`&quot;.

### daterange {#daterange}

Matchar JCR DATE-egenskaper mot ett datum/tidsintervall. Detta använder ISO8601-formatet för datum och tider ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges i antal millisekunder sedan 1970 i UTC-tidszonen, det unika tidsformatet.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Stöder facetextrahering. Kommer att tillhandahålla fickor &quot;idag&quot;, &quot;den här veckan&quot;, &quot;den här månaden&quot;, &quot;de senaste tre månaderna&quot;, &quot;det här året&quot;, &quot;det senaste året&quot; och &quot;tidigare än det senaste året&quot;.

Filtrering stöds inte.

#### Egenskaper {#properties-3}

* **property**

   relativ sökväg till en `DATE` egenskap, till exempel `jcr:lastModified`

* **lowerBound**

   nedre gräns för att kontrollera egenskap för, till exempel `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (nyare) eller &quot; `>=`&quot; (på eller nyare), gäller för `lowerBound`. Standardvärdet är &quot; `>`&quot;.

* **upperBound**

   övre gräns för att kontrollera egenskap för, till exempel `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (äldre) eller &quot; `<=`&quot; (vid eller äldre), gäller för `upperBound`. Standardvärdet är &quot; `<`&quot;.

* **timeZone**

   ID för den tidszon som ska användas när den inte anges som en ISO-8601-datumsträng. Standardvärdet är systemets standardtidszon.

### exkluderingsdjup {#excludepaths}

Utesluter noder från resultatet där deras sökväg matchar ett reguljärt uttryck.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Stöder inte facetextrahering.

#### Egenskaper {#properties-4}

* **exkluderingsdjup**

   reguljära uttryck som matchas mot resultatsökvägar, utan matchande sökvägar från resultatet.

### fulltext {#fulltext}

Söker efter termer i fulltextindexet.

Filtrering stöds inte.

Stöder inte facetextrahering.

#### Egenskaper {#properties-5}

* **fulltext**

   fulltextsöktermer

* **relPath**

   den relativa sökvägen som ska sökas i egenskapen eller undernoden. Den här egenskapen är valfri.

### grupp {#group}

Tillåter att kapslade villkor skapas. Grupper kan innehålla kapslade grupper. Allt i en fråga finns implicit i en rotgrupp som kan ha `p.or` och `p.not` parametrar också.

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

Detta är begreppsmässigt `fulltext AND ( (path AND type) OR (path AND type) )`. Observera att sådana OR-kopplingar behöver bra index för att fungera.

#### Egenskaper {#properties-6}

* **p.or**

   om inställt på &quot; `true`&quot;, måste bara ett predikat i gruppen matcha. Standardvärdet är &quot; `false`&quot;, vilket betyder att alla måste matcha

* **p.not**

   om inställt på &quot; `true`&quot;, negeras gruppen (standardvärdet är &quot; `false`&quot;)

* **&lt;predicate>**

   lägger till kapslade predikat

* **N_&lt;predicate>**

   lägger till flera kapslade predikat samtidigt, som `1_property, 2_property, ...`

### hasPermission {#haspermission}

Begränsar resultatet till objekt där den aktuella sessionen har den angivna [JCR-behörighet.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **hasPermission**

   kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ha för noden i fråga. till exempel `jcr:write`, `jcr:modifyAccessControl`

### språk {#language}

Söker efter CQ-sidor på ett visst språk. Det här tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språket i en webbplatsstruktur på den översta nivån.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Stöder facetextrahering. Ger buketter för varje unik språkkod.

#### Egenskaper {#properties-8}

* **språk**

   ISO-språkkod, till exempel &quot; `de`&quot;

### huvudtillgång {#mainasset}

Kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Detta är i stort sett alla noder som inte finns i en delresursnod. Observera att detta inte kontrollerar `dam:Asset` nodtyp. Ange bara &quot; `mainasset=true`&quot; eller &quot; `mainasset=false`&quot;, det finns inga fler egenskaper.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Stöder facetextrahering. Tillhandahåller 2 bucket för huvud- och deltillgångar.

#### Egenskaper {#properties-9}

* **huvudtillgång**

   boolesk, &quot; `true`&quot; for main assets, &quot; `false`&quot; för undertillgångar

### medlemOf {#memberof}

Söker efter objekt som tillhör en viss [resursinsamling för sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex. Stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **medlemOf**

   sökväg till Sling-resurssamling

### nodename {#nodename}

Matchar JCR-nodnamn.

Stöder facetextrahering. Tillhandahåller bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **nodename**

   nodnamnsmönster som tillåter jokertecken: `*` = ett eller inga tecken, `?` = any char, `[abc]` = endast tecken inom hakparentes

### inte utgånget {#notexpired}

Matchar objekt genom att kontrollera om en JCR DATE-egenskap är större eller lika med den aktuella servertiden. Detta kan användas för att kontrollera en `expiresAt`&quot; som date-egenskap och begränsa till endast de som ännu inte har gått ut ( `notexpired=true`) eller som redan har gått ut ( `notexpired=false`).

Filtrering stöds inte.

Stöder facet-extrahering på samma sätt som daterange-predikatet.

#### Egenskaper {#properties-12}

* **inte utgånget**

   boolesk, &quot; `true`&quot; för ännu inte förfallit (datum i framtiden eller lika med), &quot; `false`&quot; för utgången (tidigare datum) (obligatoriskt)

* **property**

   relativ sökväg till `DATE` egenskap som ska kontrolleras (obligatoriskt)

### orderby {#orderby}

Sortera resultatet. Om det krävs en ordning med flera egenskaper måste det här prefixet läggas till flera gånger med hjälp av talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **orderby**

   antingen JCR-egenskapsnamnet som anges av ett radavstånd på @, till exempel `@jcr:lastModified` eller `@jcr:content/jcr:title`eller ett annat predikat i frågan, till exempel `2_property`som sorteringen ska göras på

* **sortera**

   sorteringsriktning, antingen &quot; `desc`&quot; för fallande eller &quot; `asc`&quot; for ascending (default)

* **case**

   om inställt på &quot; `ignore`&quot; kommer att göra sorteringsskiftläget okänsligt, vilket innebär att &quot;a&quot; kommer före &quot;B&quot;, om den är tom eller utelämnad är sorteringen skiftlägeskänslig, vilket betyder &quot;B&quot; kommer före &quot;a&quot;

### bana {#path}

Söker i en viss bana.

Stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **bana**

   banmönster, beroende på exakt, kommer antingen hela underträdet att matcha (som att lägga till `//*` in xpath, but note that this does not include the base path) (exact=false, default) or only an exact path matching, which can include wilcards ( `*`). om self anges söks hela underträdet inklusive basnoden igenom

* **exakt**

   if `exact` är true/on, den exakta sökvägen måste matcha, men den kan innehålla enkla jokertecken ( `*`), som matchar namn, men inte &quot; `/`&quot;; om det är false (standard) inkluderas alla underordnade (valfritt)

* **platt**

   söker bara efter direkt underordnade objekt (som att lägga till &quot; `/*`&quot; in xpath) (används endast om &quot; `exact`&#39; är inte sant, valfritt)

* **self**

   söker i underträdet men inkluderar basnoden som angetts som sökväg (inga jokertecken)

### property {#property}

Matchar JCR-egenskaper och deras värden.

Stöder facetextrahering. Ger bucket för varje unikt egenskapsvärde i resultatet.

#### Egenskaper {#properties-15}

* **property**

   relativ sökväg till egenskap, till exempel `jcr:title`

* **value**

   Värde att kontrollera egenskap för. följer egenskapstypen JCR till strängkonverteringar

* **N_värde**

   use `1_value`, `2_value`, ... för att kontrollera om det finns flera värden (i kombination med `OR` som standard, med `AND` if och=true) (sedan 5.3)

* **och**

   anges till true för att kombinera flera värden ( `N_value`) med OCH (sedan 5.3)

* **operation**

   &quot;`equals`&quot; för exakt matchning (standard), &quot; `unequals`&quot; för jämförelse av skillnader, &quot; `like`&quot; för att använda `jcr:like` xpath-funktion (valfri), &quot; `not`&quot; utan matchning (t.ex. &quot;`not(@prop)`&quot; in xpath, value param will be ignore) or &quot; `exists`&quot; for exist check (value can be true - property must exist, the default - or false - same as &quot; `not`&quot;)

* **djup**

   antal jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (till exempel `property=size depth=2` kommer att kontrollera nod/storlek, nod/&amp;ast;/size och nod/&amp;ast;/&amp;ast;/size)

### rangegenskap {#rangeproperty}

Matchar en JCR-egenskap mot ett intervall. Detta gäller egenskaper med linjär typ som `LONG`, `DOUBLE` och `DECIMAL`. För `DATE` se daterange-predikatet som har optimerade indata för datumformat.

Du kan definiera en nedre gräns och en övre gräns eller endast en av dem. Åtgärden (t.ex. &quot;mindre än&quot; eller &quot;mindre eller lika med&quot;) kan också anges för enskilt nedre och övre gräns.

Stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **property**

   relativ sökväg till egenskap

* **lowerBound**

   nedre gräns för check-egenskap för

* **lowerOperation**

   &quot; `>`&quot; (standard) eller &quot; `>=`&quot;, gäller `lowerValue`

* **upperBound**

   övre gräns för check-egenskap för

* **upperOperation**

   &quot; `<`&quot; (standard) eller &quot; `<=`&quot;, gäller `lowerValue`

* **decimal**

   &quot; `true`&quot; om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Matchar `JCR DATE` egenskaper mot ett datum/tidsintervall med tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` med ett millisekundvärde eller bugzillasyntax `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Prefix med &quot; `-`&quot; om du vill ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound`blir det andra standardvärdet 0, vilket innebär den aktuella tiden.

Till exempel:

* `upperBound=1h` (och nej) `lowerBound`) skulle välja vad som helst under nästa timme
* `lowerBound=-1d` (och nej) `upperBound`) skulle välja vad som helst de senaste 24 timmarna
* `lowerBound=-6M` och `upperBound=-3M` väljer du mellan 6 månader och 3 månader
* `lowerBound=-1500` och `upperBound=5500` kan välja mellan 1 500 millisekunder tidigare och 5 500 millisekunder i framtiden
* `lowerBound=1d` och `upperBound=2d` skulle välja vad som helst i övermorgon

Observera att programmet inte tar hänsyn till skottår och att alla månader är 30 dagar.

Filtrering stöds inte.

Stöder facet-extrahering på samma sätt som daterange-predikatet.

#### Egenskaper {#properties-17}

* **upperBound**

   övre gräns för datum i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd &quot;-&quot; för negativ offset

* **lowerBound**

   nedre gräns i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd &quot;-&quot; för negativ offset

### root {#root}

Rotpredikatgrupp. Stöder alla funktioner i en grupp och tillåter att globala frågeparametrar ställs in.

Namnet &quot;root&quot; används aldrig i en fråga, det är underförstått.

#### Egenskaper {#properties-18}

* **p.offset**

   tal som anger början på resultatsidan, d.v.s. hur många objekt som ska hoppas över

* **p.limit**

   nummer som anger sidstorleken

* **p.gissningTotal**

   rekommenderas: Undvik att beräkna det totala resultatet som kan vara kostsamt. antingen en siffra som anger den högsta summan att räkna upp till (t.ex. 1000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat) eller &quot; `true`&quot; för att endast räkna upp till det minsta nödvändiga `p.offset` + `p.limit`

* **p.excerpt**

   om inställt på &quot; `true`&quot;, ta med utdrag av fullständig text i resultatet

* **p.hits**

   (endast för JSON-servern) väljer du hur träffar skrivs som JSON, med dessa standardinställningar (utbyggbara via ResultHitWriter-tjänsten):

   * **enkel**:

      minimala objekt som `path`, `title`, `lastmodified`, `excerpt` (om angivet)

   * **full**:

      sling JSON rendering of the node, with `jcr:path` som anger träffens sökväg: som standard visas bara de direkta egenskaperna för noden, inklusive ett djupare träd med `p.nodedepth=N`, med 0 avses hela det oändliga underträdet, add `p.acls=true` för att inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **selektiv**:

      endast egenskaper som anges i `p.properties`, som är en blankstegsavgränsad (använd&quot;+&quot; i URL-adresser) lista med relativa sökvägar, Om den relativa sökvägen har ett djup > 1 representeras dessa som underordnade objekt. den speciella jcr:path-egenskapen innehåller träffens sökväg

### sparad fråga {#savedquery}

Inkluderar alla predikat för en beständig querybuilder-fråga i den aktuella frågan som ett undergruppsprediat.

Observera att detta inte kör en extra fråga utan utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan antingen vara en flerradig String-egenskap eller en `nt:file` nod som innehåller frågan som en textfil i Java-egenskapsformat.

Stöder inte facetextrahering för predikaten i den sparade frågan.

#### Egenskaper {#properties-19}

* **sparad fråga**

   sökväg till den sparade frågan (egenskapen String eller `nt:file` nod)

### liknande {#similar}

Likhetssökning med JCR XPath `rep:similar()`.

Filtrering stöds inte. Stöder inte facetextrahering.

#### Egenskaper {#properties-20}

* **liknande**
absolut sökväg till noden som liknande noder ska hittas för

* **lokal**
en relativ sökväg till en underordnad nod eller 
`.` för den aktuella noden (valfritt) är &quot; `.`&quot;)

### tag {#tag}

Söker efter innehåll som har taggats med en eller flera taggar genom att ange sökvägar för taggtiteln.

Stöder facetextrahering. Tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella namnsökväg för taggen.

#### Egenskaper {#properties-21}

* **tag**

   sökväg till tagg som du vill söka efter, t.ex. &quot;Resursegenskaper: Orientering / liggande&quot;

* **N_värde**

   use `1_value`, `2_value`, ... att söka efter flera taggar (i kombination med `OR` som standard, med `AND` if och=true) (sedan 5.6)

* **property**

   egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`&quot;)

### tagid {#tagid}

Söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Stöder facetextrahering. Tillhandahåller bucket för varje unik tagg med deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **tagid**

   tagg-id att söka efter, till exempel &quot; `properties:orientation/landscape`&quot;

* **N_värde**

   use `1_value`, `2_value`, ... att söka efter flera taggar (i kombination med `OR` som standard, med `AND` if och=true) (sedan 5.6)

* **property**

   egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`&quot;)

### tagsearch {#tagsearch}

Söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Då söker först efter taggar som innehåller dessa nyckelord i sina titlar och begränsar sedan resultatet till enbart objekt som taggats med dessa.

Stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **tagsearch**

   nyckelord som du vill söka efter i taggtitlar

* **property**

   egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`&quot;)

* **lang**

   om du bara vill söka i en viss lokaliserad taggtitel (t.ex. &quot; `de`&quot;)

* **alla**

   (bool) söka efter hela taggens fulltext, dvs. alla titlar, beskrivning osv. (har företräde framför&quot;l&quot; `ang`&quot;)

### type {#type}

Begränsar resultaten till en viss JCR-nodtyp, både primär nodtyp och blandningstyp. Detta söker även efter undertyper av den nodtypen. Observera att databasens sökindex måste omfatta nodtyperna för effektiv körning.

Stöder facetextrahering. Tillhandahåller bucket för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **type**

   nodtyp eller blandnamn att söka efter, till exempel `cq:Page`
