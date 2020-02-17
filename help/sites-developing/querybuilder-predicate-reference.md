---
title: Predikatreferens för Query Builder
seo-title: Predikatreferens för Query Builder
description: Fullständig predikatreferens för Query Builder API.
seo-description: Fullständig predikatreferens för Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Predikatreferens för Query Builder{#query-builder-predicate-reference}

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
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [huvudtillgång](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [medlemOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [inte utgånget](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
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

Matchar JCR BOOLEAN-egenskaper. Endast värdena &quot; `true`&quot; och &quot; `false`&quot; godkänns. Om det är &quot; `false`&quot; matchar det om egenskapen har värdet &quot; `false`&quot; eller om den inte finns alls. Detta kan vara användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Den ärvda parametern &quot; `operation`&quot; har ingen betydelse.

Stöder facetextrahering. Tillhandahåller bucket för varje `true` eller `false` värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **boolproperty** relativ sökväg till egenskap, till exempel `myFeatureEnabled` eller `jcr:content/myFeatureEnabled`

* **värde** för att kontrollera egenskapen för, &quot; `true`&quot; eller &quot; `false`&quot;

### innehållfragment {#contentfragment}

Begränsar resultatet till innehållsfragment.

Filtrering stöds inte.

Stöder inte facetextrahering.

#### Egenskaper {#properties-1}

* **contentfragment** Den kan användas med valfritt värde för att kontrollera om det finns innehållsfragment.

### dateComparison {#datecomparison}

Jämför två JCR DATE-egenskaper med varandra. Kan testa om de är lika, olika, större än eller större än eller lika med.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

#### Egenskaper {#properties-2}

* **property1**

   path to first date property

* **property2**

   path to second date, egenskap

* **operation**

   &quot; `=`&quot; för exakt matchning, &quot; `!=`&quot; för likhetsjämförelse, &quot; `>`&quot; för egenskap 1 större än egenskap 2, &quot; `>=`&quot; för egenskap 1 större än eller lika med egenskap 2. Standardvärdet är &quot; `=`&quot;.

### daterange {#daterange}

Matchar JCR DATE-egenskaper mot ett datum/tidsintervall. Detta använder ISO8601-formatet för datum och tid ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges i antal millisekunder sedan 1970 i UTC-tidszonen, det unika tidsformatet.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Stöder facetextrahering. Kommer att tillhandahålla fickor &quot;idag&quot;, &quot;den här veckan&quot;, &quot;den här månaden&quot;, &quot;de senaste tre månaderna&quot;, &quot;det här året&quot;, &quot;det senaste året&quot; och &quot;tidigare än det senaste året&quot;.

Filtrering stöds inte.

#### Egenskaper {#properties-3}

* **property**

   relativ sökväg till en `DATE` egenskap, till exempel `jcr:lastModified`

* **lowerBound**

   nedre gräns för att kontrollera egenskap för, till exempel `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (nyare) eller &quot; `>=`&quot; (på eller nyare) gäller för `lowerBound`. The default is &quot; `>`&quot;.

* **upperBound**

   övre gräns för att kontrollera egenskap för, till exempel `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (äldre) eller &quot; `<=`&quot; (äldre) gäller för `upperBound`. The default is &quot; `<`&quot;.

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

### group {#group}

Tillåter att kapslade villkor skapas. Grupper kan innehålla kapslade grupper. Allt i en querybuilder-fråga ingår implicit i en rotgrupp som också kan ha `p.or` och `p.not` parametrar.

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

Det här söker efter termen&quot;**Hantering**&quot; på sidor i `/content/geometrixx/en` eller i resurser i `/content/dam/geometrixx`.

Detta är begreppsmässigt `fulltext AND ( (path AND type) OR (path AND type) )`. Observera att sådana OR-kopplingar behöver bra index för att fungera.

#### Egenskaper {#properties-6}

* **p.or**

   om värdet är &quot; `true`&quot; får bara ett predikat i gruppen matcha. Standardvärdet är &quot; `false`&quot;, vilket innebär att alla måste matcha

* **p.not**

   om värdet är &quot; `true`&quot; negeras gruppen (standardvärdet är &quot; `false`&quot;)

* **&lt;predikat>**

   lägger till kapslade predikat

* **N_&lt;predikat>**

   lägger till flera kapslade predikat samtidigt, som `1_property, 2_property, ...`

### hasPermission {#haspermission}

Begränsar resultatet till objekt där den aktuella sessionen har angiven [JCR-behörighet.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **hasPermission**

   kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ha för noden i fråga. t.ex. `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Söker efter CQ-sidor på ett visst språk. Det här tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språket i en webbplatsstruktur på den översta nivån.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Stöder facetextrahering. Ger buketter för varje unik språkkod.

#### Egenskaper {#properties-8}

* **language**

   ISO-språkkod, till exempel &quot; `de`&quot;

### huvudtillgång {#mainasset}

Kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Detta är i stort sett alla noder som inte finns i en delresursnod. Observera att det här inte söker efter `dam:Asset` nodtypen. Om du vill använda det här predikatet anger du &quot; `mainasset=true`&quot; eller &quot; `mainasset=false`&quot; finns det inga fler egenskaper.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Stöder facetextrahering. Tillhandahåller 2 bucket för huvud- och deltillgångar.

#### Egenskaper {#properties-9}

* **huvudtillgång**

   boolesk,&quot; `true`&quot; för huvudtillgångar,&quot; `false`&quot; för deltillgångar

### medlemOf {#memberof}

Söker efter objekt som är medlemmar i en specifik [sling-resurssamling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex. Stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **medlemOf**

   sökväg till Sling-resurssamling

### nodename {#nodename}

Matchar JCR-nodnamn.

Stöder facetextrahering. Tillhandahåller bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **nodename**

   nodnamnsmönster som tillåter jokertecken: `*` = ett tecken eller inget tecken, `?` = valfritt tecken, `[abc]` = endast tecken inom hakparentes

### inte utgånget {#notexpired}

Matchar objekt genom att kontrollera om en JCR DATE-egenskap är större eller lika med den aktuella servertiden. Detta kan användas för att kontrollera en `expiresAt`liknande datumegenskap och begränsa till endast de som ännu inte har gått ut ( `notexpired=true`) eller som redan har gått ut ( `notexpired=false`).

Filtrering stöds inte.

Stöder facet-extrahering på samma sätt som daterange-predikatet.

#### Egenskaper {#properties-12}

* **inte utgånget**

   boolesk,&quot; `true`&quot; för ännu inte förfallit (datum i framtiden eller lika med),&quot; `false`&quot; för utgången (tidigare datum) (obligatoriskt)

* **property**

   relativ sökväg till den `DATE` egenskap som ska kontrolleras (obligatoriskt)

### orderby {#orderby}

Sortera resultatet. Om det krävs en ordning med flera egenskaper måste det här prefixet läggas till flera gånger med hjälp av talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **orderby**

   antingen JCR-egenskapsnamn som anges av till exempel `@jcr:lastModified` eller `@jcr:content/jcr:title`ett annat predikat i frågan `2_property`som ska sorteras

* **sortera**

   sorteringsriktning, antingen &quot; `desc`&quot; för fallande eller &quot; `asc`&quot; för stigande (standard)

* **case**

   om värdet är &quot; `ignore`&quot; kommer sorteringsskiftläget att bli okänsligt, vilket innebär att &quot;a&quot; kommer före &quot;B&quot;, om den är tom eller utelämnad är sorteringen skiftlägeskänslig, vilket betyder &quot;B&quot; kommer före &quot;a&quot;

### path {#path}

Söker i en viss bana.

Stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **path**

   banmönster, Beroende på exakt kommer antingen hela underträdet att matcha (som att lägga till `//*` i XPath, men observera att detta inte inkluderar bassökvägen) (exact=false, default) eller endast en exakt sökvägsmatchning, som kan innehålla jokertecken ( `*`). om self anges söks hela underträdet inklusive basnoden igenom

* **exakt**

   Om `exact` är true/on måste den exakta sökvägen matcha, men den kan innehålla enkla jokertecken ( `*`) som matchar namn, men inte &quot; `/`&quot;; om det är false (standard) inkluderas alla underordnade (valfritt)

* **platt**

   söker bara efter direkt underordnade objekt (som att lägga till &quot; `/*`&quot; i xpath) (används bara om &quot; `exact`&quot; inte är true, valfritt)

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

   använd `1_value`, `2_value`, ... för att kontrollera om det finns flera värden (i kombination med `OR` som standard med `AND` if och=true) (sedan 5.3)

* **and**

   anges till true för att kombinera flera värden ( `N_value`) med AND (sedan 5.3)

* **operation**

   &quot; `equals`&quot; för exakt matchning (standard), &quot; `unequals`&quot; för likhetsjämförelse, &quot; `like`&quot; för `jcr:like` XPath-funktionen (valfritt), &quot; `not`&quot; för ingen matchning (t.ex. &quot; `not(@prop)`&quot; i xpath ignoreras value param) eller &quot; `exists`&quot; för existenskontroll (värdet kan vara true - egenskapen måste finnas, standardvärdet - eller false - är samma som &quot; `not`&quot;)

* **djup**

   antal jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (t.ex. `property=size depth=2` kontrollerar nod/storlek, nod/&amp;ast;/size and node/&amp;ast;/&amp;ast;/size)

### rangegenskap {#rangeproperty}

Matchar en JCR-egenskap mot ett intervall. Detta gäller för egenskaper med linjära typer som `LONG`, `DOUBLE` och `DECIMAL`. Se `DATE` daterange-predikatet med optimerade indata för datumformat.

Du kan definiera en nedre gräns och en övre gräns eller endast en av dem. Åtgärden (t.ex. &quot;mindre än&quot; eller &quot;mindre eller lika med&quot;) kan också anges för enskilt nedre och övre gräns.

Stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **property**

   relativ sökväg till egenskap

* **lowerBound**

   nedre gräns för check-egenskap för

* **lowerOperation**

   &quot; `>`&quot; (standard) eller &quot; `>=`&quot; gäller för `lowerValue`

* **upperBound**

   övre gräns för check-egenskap för

* **upperOperation**

   &quot; `<`&quot; (standard) eller &quot; `<=`&quot; gäller för `lowerValue`

* **decimal**

   &quot; `true`&quot; om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Matchar `JCR DATE` egenskaper mot ett datum/tidsintervall med tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` använda antingen ett millisekundvärde eller bugzilla-syntaxen `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Använd prefixet &quot; `-`&quot; för att ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound`kommer den andra att få standardvärdet 0, vilket innebär den aktuella tiden.

Exempel:

* `upperBound=1h` (och nej `lowerBound`) väljer något under nästa timme
* `lowerBound=-1d` (och nej `upperBound`) väljer något under de senaste 24 timmarna
* `lowerBound=-6M` och `upperBound=-3M` skulle välja mellan sex månaders till tre månaders ålder
* `lowerBound=-1500` och `upperBound=5500` väljer mellan 1 500 millisekunder tidigare och 5 500 millisekunder i framtiden
* `lowerBound=1d` och `upperBound=2d` skulle välja vad som helst i övermorgon

Observera att programmet inte tar hänsyn till skottår och att alla månader är 30 dagar.

Filtrering stöds inte.

Stöder facet-extrahering på samma sätt som daterange-predikatet.

#### Egenskaper {#properties-17}

* **upperBound**

   övre datumgräns i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd &quot;-&quot; för negativ offset

* **lowerBound**

   nedre datumgräns i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd &quot;-&quot; för negativ offset

### root {#root}

Rotpredikatgrupp. Stöder alla funktioner i en grupp och tillåter att globala frågeparametrar ställs in.

Namnet &quot;root&quot; används aldrig i en fråga, det är implicit.

#### Egenskaper {#properties-18}

* **p.offset**

   tal som anger början på resultatsidan, d.v.s. hur många objekt som ska hoppas över

* **p.limit**

   nummer som anger sidstorleken

* **p.gissningTotal**

   rekommenderas: Undvik att beräkna det totala resultatet som kan vara kostsamt. antingen en siffra som anger den högsta summan att räkna upp till (t.ex. 1000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat) eller &quot; `true`&quot; för att räkna endast upp till det minsta nödvändiga `p.offset` + `p.limit`

* **p.excerpt**

   om värdet är &quot; `true`&quot;, inkludera utdrag av fullständig text i resultatet

* **p.hits**

   (endast för JSON-servern) väljer du hur träffar skrivs som JSON, med dessa standardinställningar (utbyggbara via ResultHitWriter-tjänsten):

   * **enkel**:

      minimala objekt som `path`, `title`, `lastmodified`, `excerpt` (om de anges)

   * **full**:

      snedställ JSON-återgivning av noden, med `jcr:path` en sökväg för träffen: Som standard anges bara nodens direkta egenskaper, inklusive ett djupare träd med 0 som `p.nodedepth=N`betyder hela det oändliga underträdet, lägg till `p.acls=true` för att inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **selektiv**:

      Endast egenskaper som anges i `p.properties`, som är blankstegsavgränsade (använd&quot;+&quot; i URL:er) med relativa sökvägar. Om den relativa sökvägen har ett djup > 1 representeras dessa som underordnade objekt. den speciella jcr:path-egenskapen innehåller träffens sökväg

### sparad fråga {#savedquery}

Inkluderar alla predikat för en beständig querybuilder-fråga i den aktuella frågan som ett undergruppsprediat.

Observera att detta inte kör en extra fråga utan utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan vara en strängegenskap med flera rader eller en `nt:file` nod som innehåller frågan som en textfil i Java-egenskapsformat.

Stöder inte facetextrahering för predikaten i den sparade frågan.

#### Egenskaper {#properties-19}

* **sparad fråga**

   sökväg till den sparade frågan (egenskapen String eller `nt:file` noden)

### liknande {#similar}

Likhetssökning med JCR XPath: `rep:similar()`.

Filtrering stöds inte. Stöder inte facetextrahering.

#### Egenskaper {#properties-20}

* **liknande** absolut sökväg till noden där liknande noder ska hittas

* **lokal** en relativ sökväg till en underordnad nod eller `.` för den aktuella noden (valfritt, standardvärdet är &quot; `.`&quot;)

### tag {#tag}

Söker efter innehåll som har taggats med en eller flera taggar genom att ange sökvägar för taggtiteln.

Stöder facetextrahering. Tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella namnsökväg för taggen.

#### Egenskaper {#properties-21}

* **tag**

   sökväg till tagg som du vill söka efter, t.ex. &quot;Resursegenskaper: Orientering / liggande&quot;

* **N_värde**

   använd `1_value`, `2_value`, ... om du vill söka efter flera taggar (i kombination med `OR` som standard med `AND` if och=true) (sedan 5.6)

* **property**

   egenskap (eller relativ sökväg till egenskap) att titta på (standard &quot; `cq:tags`&quot;)

### tagid {#tagid}

Söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Stöder facetextrahering. Tillhandahåller bucket för varje unik tagg med deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **tagid**

   tagg-id att söka efter, till exempel &quot; `properties:orientation/landscape`&quot;

* **N_värde**

   använd `1_value`, `2_value`, ... för att kontrollera om det finns flera taggar (i kombination med `OR` som standard med `AND` if och=true) (sedan 5.6)

* **property**

   egenskap (eller relativ sökväg till egenskap) att titta på (standard &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Då söker först efter taggar som innehåller dessa nyckelord i sina titlar och begränsar sedan resultatet till enbart objekt som taggats med dessa.

Stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **tagsearch**

   nyckelord som du vill söka efter i taggtitlar

* **property**

   egenskap (eller relativ sökväg till egenskap) att titta på (standard &quot; `cq:tags`&quot;)

* **lang**

   om du bara vill söka i en viss lokaliserad taggtitel (t.ex. &quot; `de`&quot;)

* **all**

   (bool) söka efter hela taggens fulltext, dvs. alla titlar, beskrivning osv. (har företräde framför&quot;l `ang`&quot;)

### type {#type}

Begränsar resultaten till en viss JCR-nodtyp, både primär nodtyp och blandningstyp. Detta söker även efter undertyper av den nodtypen. Observera att databasens sökindex måste omfatta nodtyperna för effektiv körning.

Stöder facetextrahering. Tillhandahåller bucket för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **type**

   nodtyp eller blandnamn att söka efter, till exempel `cq:Page`