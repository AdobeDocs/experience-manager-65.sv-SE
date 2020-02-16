---
title: Query Builder API
seo-title: Query Builder API
description: Funktionerna i Asset Share Query Builder visas via Java API och REST API.
seo-description: Funktionerna i Asset Share Query Builder visas via Java API och REST API.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Query Builder API{#query-builder-api}

Funktionerna i [Asset Share Query Builder](/help/assets/assets-finder-editor.md) visas via Java API och REST API. I det här avsnittet beskrivs dessa API:er.

Frågebyggaren ( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) på serversidan accepterar en frågebeskrivning, skapar och kör en XPath-fråga, kan även filtrera resultatuppsättningen och extrahera facets, om så önskas.

Frågebeskrivningen är bara en uppsättning prediktiv ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Exemplen innehåller ett fulltextpredikat, som motsvarar funktionen i XPath, och ett predikat för bildstorlek som söker efter bredd- och höjdegenskaper i DAM-resursens underträd. `jcr:contains()`

För varje predikattyp finns det en utvärderingskomponent ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) som kan hantera det specifika predikatet för XPath, filtrering och ansiktsextrahering. Det är mycket enkelt att skapa anpassade utvärderare, som kopplas in via OSGi-komponentkörningen.

REST API ger åtkomst till exakt samma funktioner via HTTP med svar som skickas i JSON.

>[!NOTE]
>
>QueryBuilder-API:t byggs med JCR-API:t. Du kan också fråga JCR-läsaren för Adobe Experience Manager genom att använda JCR-API:t i ett OSGi-paket. Mer information finns i [Fråga Adobe Experience Manager-data med JCR-API:t](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Gem-session {#gem-session}

[AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) är en serie tekniska djupdykningar i Adobe Experience Manager som levereras av Adobes experter. Den här sessionen som är avsedd för frågebyggaren är mycket användbar för en översikt över och användning av verktyget.

>[!NOTE]
>
>Se AEM Gem-sessionen [Söka enkelt i formulär med AEM querybuilder](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) för en detaljerad översikt av frågebyggaren.

## Exempelfrågor {#sample-queries}

Dessa exempel anges i Java-egenskapsformatsnotation. Om du vill använda dem med Java API använder du ett Java-exempel `HashMap` som i det följande API-exemplet.

För `QueryBuilder` JSON-servern innehåller varje exempel en länk till den lokala CQ-installationen (på standardplatsen `http://localhost:4502`). Observera att du måste logga in på CQ-instansen innan du använder länkarna.

>[!CAUTION]
>
>Som standard visas maximalt 10 träffar i frågeverktyget json.
>
>Om du lägger till följande parameter kan servleten visa alla frågeresultat:
>
>**`p.limit=-1`**

>[!NOTE]
>
>Om du vill visa returnerade JSON-data i webbläsaren kan du använda ett plugin-program som JSONView för Firefox.

### Returnera alla resultat {#returning-all-results}

**Följande fråga kommer att** returnera tio resultat **(eller max tio), men informera dig om** Antal träffar: som faktiskt finns tillgängliga:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

Samma fråga (med parametern `p.limit=-1`) **returnerar alla resultat** (detta kan vara ett högt tal beroende på instansen):

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### Använda p.gissningssumma för att returnera resultaten {#using-p-guesstotal-to-return-the-results}

Syftet med `p.guessTotal` parametern är att returnera rätt antal resultat som kan visas genom att kombinera de lägsta p.offset- och p.limit-värdena. Fördelen med den här parametern är bättre prestanda med stora resultatuppsättningar. På så sätt undviker du att beräkna hela summan (t.ex. genom att anropa result.getSize()) och läsa hela resultatuppsättningen, optimerad hela vägen ned till OAK-motorn och indexvärdet. Detta kan vara en stor skillnad när det finns 100 000 resultat, både när det gäller körningstid och minnesanvändning.

Nackdelen med parametern är att användarna inte ser exakt summa. Men du kan ange ett minimivärde som p.gissningstotal=1000 så att det alltid läses upp till 1000, så du får exakta summor för mindre resultatuppsättningar, men om det är mer än så kan du bara visa&quot;och mer&quot;.

Lägg `p.guessTotal=true` till frågan nedan för att se hur den fungerar:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

Frågan returnerar `p.limit` standardvärdet för `10` resultat med en `0` förskjutning:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

Från och med AEM 6.0 SP2 kan du även använda ett numeriskt värde för att räkna upp till ett anpassat antal maximala resultat. Använd samma fråga som ovan, men ändra värdet för `p.guessTotal` till `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

Den returnerar ett tal som är lika med standardgränsen på 10 resultat med förskjutningen 0, men som bara visar maximalt 50 resultat:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementera sidnumrering {#implementing-pagination}

Som standard ger Query Builder även antalet träffar. Beroende på den resulterande storleken kan det ta lång tid att fastställa det korrekta antalet, bland annat genom att kontrollera alla resultat för åtkomstkontroll. För det mesta används summan för att implementera sidnumrering för slutanvändargränssnittet. Eftersom det kan ta lång tid att fastställa det exakta antalet rekommenderar vi att du använder funktionen gissaTotal för att implementera sidnumreringen.

Gränssnittet kan till exempel anpassa följande metod:

* Hämta och visa det exakta antalet för det totala antalet träffar ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) eller totalt i querybuilder.json-svaret) är mindre än eller lika med 100.
* Ange `guessTotal` till 100 när du anropar Query Builder.

* Svaret kan ha följande resultat:

   * `total=43`, `more=false` - Anger att det totala antalet träffar är 43. Gränssnittet kan visa upp till tio resultat som en del av den första sidan och ge sidnumrering för de kommande tre sidorna. Du kan också använda den här implementeringen för att visa en beskrivande text som **&quot;43 resultat hittades&quot;**.
   * `total=100`, `more=true` - Anger att det totala antalet träffar är större än 100 och att det exakta antalet inte är känt. Gränssnittet kan visas upp till tio som en del av den första sidan och sidnumreringen kan göras för de kommande tio sidorna. Du kan också använda den här för att visa text som **&quot;fler än 100 resultat hittades&quot;**. När användaren går till nästa sida ökar anrop till Query Builder begränsningen för `guessTotal` och även för parametrarna `offset` och `limit` .

`guessTotal` bör också användas i de fall där användargränssnittet behöver använda oändlig rullning för att undvika att frågeverktyget avgör det exakta träffantalet.

### Hitta jar-filer och beställ dem, nyaste först {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Söka efter alla sidor och sortera dem efter senaste ändring {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Söka efter alla sidor och sortera dem efter senast ändrade, men fallande {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Fulltextsökning, sorterad efter poäng {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Sök efter sidor som taggats med en viss tagg {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&amp;tagid=marketing:interest/product&amp;tagid.property=jcr:content/cq:tags&quot;

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

Använd predikatet som i exemplet om du känner till det explicita tagg-ID:t. `tagid`

Använd predikatet för `tag` taggens titelbana (utan blanksteg).

Eftersom du i föregående exempel söker efter sidor ( `cq:Page` noder) måste du använda den relativa sökvägen från den noden för `tagid.property` predikatet, det vill säga `jcr:content/cq:tags`. Som standard `tagid.property` är det bara `cq:tags`.

### Sök under flera sökvägar (med grupper) {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

Den här frågan använder en *grupp* (med namnet &quot; `group`&quot;) som avgränsa deluttryck i en fråga, ungefär som parenteser gör i fler standardtecken. Den föregående frågan kan till exempel uttryckas i ett mer välbekant format som:

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

I gruppen i exemplet används predikatet flera gånger `path` . Om du vill differentiera och ordna de två instanserna av predikatet (ordning krävs för vissa prediat) måste du prefix prefixet med *N* `_ where`*N *är ordningsindex. I föregående exempel är resultatpredikaten`1_path`och`2_path`.

I `p` är `p.or` det en särskild avgränsare som anger att vad som följer (i det här fallet `or`) är en *parameter* i gruppen, i motsats till ett underpredikat för gruppen, som `1_path`.

Om inget `p.or` anges kombineras alla predikat med AND, vilket innebär att varje resultat måste uppfylla alla predikat.

>[!NOTE]
>
>Du kan inte använda samma numeriska prefix i en enda fråga, inte ens för olika predikat.

### Sök efter egenskaper {#search-for-properties}

Här söker du efter alla sidor i en viss mall med hjälp av `cq:template` egenskapen:

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

Det är en nackdel att `jcr:content` noderna på sidorna, inte själva sidorna, returneras. Du kan lösa detta genom att söka efter relativ sökväg:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### Sök efter flera egenskaper {#search-for-multiple-properties}

När du använder egenskapspredikatet flera gånger måste du lägga till nummerprefixen igen:

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Sök efter flera egenskapsvärden {#search-for-multiple-property-values}

Om du vill undvika stora grupper när du vill söka efter flera värden för en egenskap ( `"A" or "B" or "C"`) kan du ange flera värden för `property` predikatet:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

För flervärdesegenskaper kan du även kräva att flera värden matchar ( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## Förfina vad som returneras {#refining-what-is-returned}

Som standard returnerar JSON-servern för QueryBuilder en standarduppsättning med egenskaper för varje nod i sökresultatet (t.ex. sökväg, namn, titel). För att få kontroll över vilka egenskaper som returneras kan du göra något av följande:

Ange

```
p.hits=full
```

I så fall inkluderas alla egenskaper för varje nod:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

Användning

```
p.hits=selective
```

och ange de egenskaper som du vill hämta in

```
p.properties
```

avgränsat med blanksteg:

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Triangle)[p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.nodedepth=5&p.properties=sling%3aresourceType%20jcr%3apath&property=jcr%3atitle&property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

En annan sak du kan göra är att inkludera underordnade noder i QueryBuilder-svaret. För att kunna göra detta måste du ange

```
p.nodedepth=n
```

var `n` är antalet nivåer som du vill att frågan ska returnera. Observera att för att en underordnad nod ska kunna returneras måste den anges av egenskapsväljaren

```
p.hits=full
```

Exempel:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## Fler prognoser {#morepredicates}

Mer information finns på sidan [Predicate Reference i](/help/sites-developing/querybuilder-predicate-reference.md)Query Builder.

Du kan också kontrollera [Javadoc efter `PredicateEvaluator` klasserna](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Javadoc för dessa klasser innehåller en lista med egenskaper som du kan använda.

Prefixet för klassnamnet (till exempel &quot; `similar`&quot; in [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) är klassens *huvudegenskap* . Den här egenskapen är också namnet på predikatet som ska användas i frågan (i gemener).

För sådana huvudegenskaper kan du korta ned frågan och använda &quot; `similar=/content/en`&quot; i stället för den fullständigt kvalificerade varianten &quot; `similar.similar=/content/en`&quot;. Det fullständiga, kvalificerade formuläret måste användas för alla icke-huvudsakliga egenskaper i en klass.

## Exempel på API-användning för frågebyggaren {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>Mer information om hur du skapar ett OSGi-paket som använder QueryBuilder-API:t och använder det OSGi-paketet i ett Adobe Experience Manager-program finns i [Skapa Adobe CQ OSGi-paket som använder Query Builder-](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)API:t.

Samma fråga som körs över HTTP med JSON-servern (Query Builder):

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Lagra och läsa in frågor {#storing-and-loading-queries}

Frågor kan lagras i databasen så att du kan använda dem senare. I `QueryBuilder` finns&quot; `storeQuery` -metoden med följande signatur:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

När du använder [ metoden `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) lagras den angivna `Query` i databasen som en fil eller som en egenskap enligt `createFile` argumentvärdet. I följande exempel visas hur du sparar en fil `Query` i sökvägen `/mypath/getfiles` som en fil:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Tidigare lagrade frågor kan läsas in från databasen med [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) metoden:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

En fil som är sparad till sökvägen `Query` `/mypath/getfiles` kan till exempel läsas in med följande kodutdrag:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Testning och felsökning {#testing-and-debugging}

Om du vill spela upp runt och felsöka frågor Builder-frågor kan du använda felsökningskonsolen för QueryBuilder på

`http://localhost:4502/libs/cq/search/content/querydebug.html`

eller också kan querybuilder json servlet på

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` är bara ett exempel).

### Allmänna felsökningsrekommendationer {#general-debugging-recommendations}

### Få förklarlig XPath via loggning {#obtain-explain-able-xpath-via-logging}

Förklara **alla** frågor under utvecklingscykeln mot målindexuppsättningen.

* Aktivera DEBUG-loggar för QueryBuilder för att få underliggande, förklarlig XPath-fråga

   * Gå till https://&lt;serveradress>:&lt;serverport>/system/console/slinglog. Skapa en ny loggare för `com.day.cq.search.impl.builder.QueryImpl` på **DEBUG**.

* När DEBUG har aktiverats för ovanstående klass visas den XPath som genererats av Query Builder i loggarna.
* Kopiera XPath-frågan från loggposten för den associerade QueryBuilder-frågan, till exempel:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Klistra in XPath-frågan i [Förklara fråga](/help/sites-administering/operations-dashboard.md#explain-query) som XPath för att kringgå frågeplanen

### Hämta förklaringsbar XPath via felsökningsfunktionen i Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* Använd felsökningsprogrammet AEM Query Builder för att generera en förklarande XPath-fråga:

Förklara **alla** frågor under utvecklingscykeln mot målindexuppsättningen.

**Få förklarlig XPath via loggning**

* Aktivera DEBUG-loggar för QueryBuilder för att få underliggande, förklarlig XPath-fråga

   * Gå till https://&lt;serveradress>:&lt;serverport>/system/console/slinglog. Skapa en ny loggare för `com.day.cq.search.impl.builder.QueryImpl` på **DEBUG**.

* När DEBUG har aktiverats för ovanstående klass visas den XPath som genererats av Query Builder i loggarna.
* Kopiera XPath-frågan från loggposten för den associerade QueryBuilder-frågan, till exempel:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Klistra in XPath-frågan i [Förklara fråga](/help/sites-administering/operations-dashboard.md#explain-query) som XPath för att hämta frågeplanen

**Hämta förklaringsbar XPath via felsökningsfunktionen i Query Builder**

* Använd felsökningsprogrammet AEM Query Builder för att generera en förklarande XPath-fråga:

![chlimage_1-66](assets/chlimage_1-66a.png)

1. Ange frågan för Frågebyggaren i felsökningsprogrammet för Frågebyggaren
1. Utför sökningen
1. Hämta genererad XPath
1. Klistra in XPath-frågan i XPath som XPath för att hämta frågeplanen

>[!NOTE]
>
>Icke-querybuilder-frågor (XPath, JCR-SQL2) kan tillhandahållas direkt till Förklara fråga.

En demonstrationsvideo om hur du felsöker frågor med QueryBuilder finns nedan.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## Felsöka frågor med loggning {#debugging-queries-with-logging}

>[!NOTE]
>
>Konfigurationen av loggarna beskrivs i avsnittet [Skapa egna loggare och författare](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

Loggutdata (INFO-nivå) för frågebyggarimplementeringen när frågan som beskrivs i Testa och felsöka körs:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Om du har en fråga med prediktiva utvärderare som filtrerar eller som använder en anpassad ordning efter jämförelseoperatorn, kommer detta även att noteras i frågan:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc-länkar {#javadoc-links}

| **Javadoc** | **Beskrivning** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | Basic Query Builder och Query API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | Resultat-API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Fasetter |
| [com.day.cq.search.facets.bufickor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Bucklar (inneslutna i facets) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Förutse utvärderare |
| [com.day.cq.search.facets.extractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Fasettextraherare (för utvärderare) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | JSON Result Hit Writer för Querybuilder-servlet (/bin/querybuilder.json) |

