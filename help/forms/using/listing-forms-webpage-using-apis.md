---
title: Visa formulär på en webbsida med API:er
seo-title: Visa formulär på en webbsida med API:er
description: Fråga Forms Manager programmatiskt om du vill hämta en filtrerad lista över formulär och visa den på dina egna webbsidor.
seo-description: Fråga Forms Manager programmatiskt om du vill hämta en filtrerad lista över formulär och visa den på dina egna webbsidor.
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: db69c393fc44ca2fcb30f9fcb0c5ca456ba35ed5

---


# Visa formulär på en webbsida med API:er {#listing-forms-on-a-web-page-using-apis}

AEM Forms innehåller ett REST-baserat söknings-API som webbutvecklare kan använda för att fråga efter och hämta en uppsättning formulär som uppfyller sökvillkoren. Du kan använda API:er för att söka efter formulär baserat på olika filter. Svarsobjektet innehåller formulärattribut, egenskaper och återge formulärens slutpunkter.

Om du vill söka efter formulär med REST API skickar du en GET-begäran till servern `https://[server]:[port]/libs/fd/fm/content/manage.json` med frågeparametrar som beskrivs nedan.

## Frågeparametrar {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Attributnamn<br /> </strong></td>
   <td><strong>Beskrivning<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>Anger den funktion som ska anropas. Om du vill söka efter formulär anger du värdet för <code>func </code>attributet till <code>searchForms</code>.</p> <p>Exempel: <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong></strong> Obs! <em>Den här parametern är obligatorisk.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>Anger den programsökväg som ska användas för att söka efter formulär. Som standard söker attributet appPath igenom alla program som finns på rotnodnivån.<br /> </p> <p>Du kan ange flera programsökvägar i en enda sökfråga. Avgränsa flera banor med vertikalstreck (|). </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>Anger vilka egenskaper som ska hämtas med resurserna. Du kan använda asterisk (*) för att hämta alla egenskaper samtidigt. Använd vertikalstrecksoperatorn (|) om du vill ange flera egenskaper. </p> <p>Exempel: <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>Obs</strong>: </p>
    <ul>
     <li><em>Egenskaper som id, sökväg och namn hämtas alltid. </em></li>
     <li><em>Alla resurser har olika egenskapsuppsättningar. Egenskaper som formUrl, pdfUrl och guideUrl är inte beroende av attributet cutpoints. Dessa egenskaper beror på resurstypen och hämtas därefter. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>Anger de relaterade resurser som ska hämtas tillsammans med sökresultaten. Du kan välja något av följande alternativ för att hämta relaterade resurser:
    <ul>
     <li><strong>NO_RELATION</strong>: Hämta inte relaterade resurser.</li>
     <li><strong>OMEDELBART</strong>: Hämtar resurser som är direkt relaterade till sökresultat.</li>
     <li><strong>ALLA</strong>: Hämta direkt och indirekt relaterade tillgångar.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>Anger maximalt antal formulär som ska hämtas.</td>
  </tr>
  <tr>
   <td>offset</td>
   <td>Anger antalet formulär som ska hoppas över från början.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>Anger om sökresultaten som matchar det angivna villkoret ska returneras eller inte. </td>
  </tr>
  <tr>
   <td>programsatser</td>
   <td><p>Anger listan med programsatser. Frågorna körs i listan med programsatser som anges i JSON-format. </p> <p>Exempel:</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>I exemplet ovan </p>
    <ul>
     <li><strong>namn</strong>: Anger namnet på egenskapen som ska sökas efter.</li>
     <li><strong>värde</strong>: anger värdet på den egenskap som du vill söka efter.</li>
     <li><strong>operator</strong>: anger vilken operator som ska användas vid sökning. Följande operatorer stöds:
      <ul>
       <li>EQ - lika med </li>
       <li>NEQ - Inte lika med</li>
       <li>GT - större än</li>
       <li>LT - Mindre än</li>
       <li>GTEQ - större än eller lika med</li>
       <li>LTEQ - mindre än eller lika med</li>
       <li>CONTAINS - A innehåller B om B är en del av A</li>
       <li>FULLTEXT - Fullständig textsökning</li>
       <li>STARTSWITH - A börjar med B om B är den första delen av A</li>
       <li>ENDSWITH - A slutar med B om B är slutdelen av A</li>
       <li>LIKE - Implementerar operatorn LIKE</li>
       <li>AND - Kombinera flera programsatser</li>
      </ul> <p><strong></strong> Obs! Operatorer för <em>GT, LT, GTEQ och LTEQ kan användas för egenskaper av linjär typ, till exempel LONG, DUBLE och DATE.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>orderfunktioner<br /> </td>
   <td><p>Anger sökresultatens ordningsvillkor. Kriterierna definieras i JSON-formatet. Du kan sortera sökresultat i mer än ett fält. Resultatet sorteras i den ordning som fälten visas i frågan.</p> <p>Exempel:</p> <p>Om du vill hämta frågeresultat ordnade efter title-egenskap i stigande ordning lägger du till följande parameter: </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>namn</strong>: Anger namnet på den egenskap som ska användas för att ordna sökresultaten.</li>
     <li><strong>villkor</strong>: Anger resultatordningen. Attributet order accepterar följande värden:
      <ul>
       <li>ASC - Använd ASC för att ordna resultatet i stigande ordning.<br /> </li>
       <li>DES - Använd DES för att ordna resultatet i fallande ordning.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>Anger om det binära innehållet ska hämtas eller inte. Attributet <code>includeXdp</code> gäller för tillgångar av typen <code>FORM</code>, <code>PDFFORM</code>och <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>Anger de resurstyper som ska hämtas från alla publicerade resurser. Använd vertikalstrecksoperatorn (|) för att ange flera resurstyper. Giltiga resurstyper är FORM, PDFFORM, PRINTFORM, RESOURCE och GUIDE.</td>
  </tr>
 </tbody>
</table>

## Exempelbegäran {#sample-request}

```
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## Exempelsvar {#sample-response}

```
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## Relaterade artiklar

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](/help/forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](/help/forms/using/draft-submission-component.md)
* [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md)