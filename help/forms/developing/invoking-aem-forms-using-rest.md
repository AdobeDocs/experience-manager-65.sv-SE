---
title: Anropa AEM-formulär med REST-begäran
seo-title: Anropa AEM-formulär med REST-begäran
description: 'null'
seo-description: 'null'
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Anropa AEM-formulär med REST-begäran {#invoking-aem-forms-using-rest-requests}

Processer som skapas i Workbench kan konfigureras så att du kan anropa dem via REST-begäranden (Representational State Transfer). REST-begäranden skickas från HTML-sidor. Det innebär att du kan anropa en formulärprocess direkt från en webbsida med hjälp av en REST-begäran. Du kan till exempel öppna en ny instans av en webbsida. Sedan kan du anropa en formulärprocess och läsa in ett återgivet PDF-dokument med data som skickades i en HTTP POST-begäran.

Det finns två typer av HTML-klienter. Den första HTML-klienten är en AJAX-klient som är skriven i JavaScript. Den andra klienten är ett HTML-formulär som innehåller en skicka-knapp. Ett HTML-baserat klientprogram är inte den enda möjliga REST-klienten. Alla klientprogram som stöder HTTP-begäranden kan anropa en tjänst med hjälp av ett REST-anrop. Du kan till exempel anropa en tjänst genom att använda ett REST-anrop från ett PDF-formulär. (Se [Anropa MyApplication/EncryptDocument-processen från Acrobat](#rest-invocation-examples).)

När du använder REST-begäranden bör du inte anropa Forms-tjänster direkt. Anropa i stället processer som skapats i Workbench. När du skapar en process som är avsedd för REST-anrop ska du använda en programmatisk startpunkt. I så fall läggs REST-slutpunkten till automatiskt. Mer information om hur du skapar processer i Workbench finns i [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

När du anropar en tjänst med REST uppmanas du att ange användarnamn och lösenord för AEM-formulär. Om du inte vill ange användarnamn och lösenord kan du inaktivera tjänstens säkerhet.

Konfigurera en REST-slutpunkt om du vill anropa en formulärtjänst (en process blir en tjänst när processen aktiveras) med REST. (Se Hantera slutpunkter i [administrationshjälpen](https://www.adobe.com/go/learn_aemforms_admin_63).)

När en REST-slutpunkt har konfigurerats kan du anropa en Forms-tjänst med hjälp av en HTTP GET-metod eller en POST-metod.

```as3
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

Det obligatoriska `ServiceName` värdet är namnet på den formulärtjänst som ska anropas. Det valfria `OperationName` värdet är namnet på tjänstens åtgärd. Om det här värdet inte anges blir det här namnet som standard `invoke`, vilket är det åtgärdsnamn som startar processen. Det valfria `ServiceVersion` värdet är den version som är kodad i X.Y-format. Om det här värdet inte anges används den senaste versionen. Värdet `enctype` kan också vara `application/x-www-form-urlencoded`.

## Datatyper som stöds {#supported-data-types}

Följande datatyper stöds när AEM Forms-tjänster anropas med REST-begäran:

* primitiva Java-datatyper, som strängar och heltal
* `com.adobe.idp.Document` datatyp
* XML-datatyper som `org.w3c.Document` och `org.w3c.Element`
* Samlingsobjekt som `java.util.List` och `java.util.Map`

   Dessa datatyper accepteras vanligen som indatavärden till processer som skapats i Workbench.

   Om en Forms-tjänst anropas med HTTP POST-metoden skickas argumenten inuti HTTP-begärandetexten. Om AEM Forms-tjänstens signatur har en strängindataparameter kan begärandetexten innehålla indataparameterns textvärde. Om tjänstens signatur definierar flera strängparametrar, kan begäran följa HTTP- `application/x-www-form-urlencoded` notationen med parameternamnen som används som formulärets fältnamn.

   Om en Forms-tjänst returnerar en strängparameter blir resultatet en textrepresentation av utdataparametern. Om en tjänst returnerar flera strängparametrar blir resultatet ett XML-dokument som kodar utdataparametrarna i följande format:
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >Värdet representerar `output-paramater1` utdataparameterns namn.

   Om en Forms-tjänst kräver en `com.adobe.idp.Document` parameter kan tjänsten bara anropas med HTTP POST-metoden. Om tjänsten kräver en `com.adobe.idp.Document` parameter blir HTTP-begärandetexten innehållet i indatadokumentobjektet.

   Om en AEM Forms-tjänst kräver flera indataparametrar måste HTTP-begärandetexten vara ett MIME-meddelande i flera delar enligt RFC 1867. (RFC 1867 är en standard som används av webbläsare för att överföra filer till webbplatser.) Varje indataparameter måste skickas som en separat del av multipart-meddelandet och kodas i `multipart/form-data` formatet. Namnet på varje del måste matcha parameterns namn.

   Listor och kartor används också som indatavärden till AEM Forms-processer som skapats i Workbench. Du kan därför använda dessa datatyper när du använder en REST-begäran. Java-matriser stöds inte eftersom de inte används som indatavärde i en AEM Forms-process.

   Om en indataparameter är en lista kan en REST-klient skicka den genom att ange parametern flera gånger (en gång för varje objekt i listan). Om A till exempel är en lista med dokument måste indata vara ett multipart-meddelande som består av flera delar med namnet A. I det här fallet blir varje del med namnet A ett objekt i indatalistan. Om B är en lista med strängar kan indata vara ett `application/x-www-form-urlencoded` meddelande som består av flera fält med namnet B. I det här fallet blir varje formulärfält med namnet B ett objekt i indatalistan.

   Om en indataparameter är en karta och det är den enda tjänstindataparametern, blir alla delar/fält i indatameddelandet en nyckel/värdepost i kartan. Namnet på varje del/fält blir postens nyckel. Innehållet i varje del/fält blir postens värde.

   Om en indatamappning inte är den enda tjänstindataparametern kan varje nyckel/värdepost som tillhör kartan skickas med en parameter som heter som en sammanfogning av parameternamnet och postens nyckel. En indatamappning som anropas `attributes` kan till exempel skickas med en lista med följande nyckel-/värdepar:

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   Detta innebär en karta över tre poster: `Color=red`, `Shape=box`och `Width=5`.

   Utdataparametrarna för list- och mappningstyperna blir en del av det resulterande XML-meddelandet. Utdatalistan representeras i XML som en serie XML-element med ett element för varje objekt i listan. Alla element får samma namn som parametern för utdatalista. Värdet för varje XML-element är en av två saker:

* En textbeteckning för objektet i listan (om listan består av strängtyper)
* En URL som pekar på dokumentets innehåll (om listan består av `com.adobe.idp.Document` objekt)

   Följande exempel är ett XML-meddelande som returneras av en tjänst som har en enda utdataparameter med namnet *list*, som är en lista med heltal.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`En parameter för utdatamappning representeras i det resulterande XML-meddelandet som en serie XML-element med ett element för varje post i kartan. Alla element får samma namn som kartpostens nyckel. Värdet för varje element är antingen en textrepresentation av kartpostens värde (om kartan består av poster med ett strängvärde) eller en URL som pekar på dokumentets innehåll (om kartan består av poster med `com.adobe.idp.Document` värdet). Nedan visas ett exempel på ett XML-meddelande som returneras av en tjänst som har en enda utdataparameter med namnet `map`. Det här parametervärdet är en karta som består av poster som associerar bokstäver med `com.adobe.idp.Document` objekt.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Asynkrona anrop {#asynchronous-invocations}

Vissa AEM Forms-tjänster, till exempel humancentrerade långvariga processer, kräver lång tid att slutföra. Dessa tjänster kan anropas asynkront på ett icke-blockerande sätt. (Se [Anropa humancentrerade, långvariga processer](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

En AEM Forms-tjänst kan anropas asynkront genom att ersätta `services` med `async_invoke` i anrops-URL:en, vilket visas i följande exempel.

```as3
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Den här URL:en returnerar identifierarvärdet (i formatet &quot;text/plain&quot;) för jobbet som är ansvarig för anropet.

Status för asynkront anrop kan hämtas med en anrops-URL som `services` ersätts med `async_status`. URL:en måste innehålla en `job_id` parameter som anger ID-värdet för jobbet som är associerat med det här anropet. Exempel:

```as3
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Den här URL:en returnerar ett heltalsvärde (i formatet &quot;text/plain&quot;) som kodar jobbstatusen enligt jobbuthanterarens specifikation (t.ex. 2 betyder att det körs, 3 betyder slutförd, 4 betyder misslyckad och så vidare).

Om jobbet är klart returnerar URL-adressen samma resultat som om tjänsten anropades synkront.

När jobbet har slutförts och resultatet har hämtats kan jobbet tas bort med hjälp av en anrops-URL med som `services` ersätts med `async_dispose`. URL:en ska även innehålla en `job_id` parameter som anger jobbets identifierarvärde. Exempel:

```as3
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Om jobbet har tagits bort returnerar den här URL:en ett tomt meddelande.

## Felrapportering {#error-reporting}

Om en synkron eller asynkron anropsbegäran inte kan slutföras på grund av att ett undantag utlöses på servern, rapporteras undantaget som en del av HTTP-svarsmeddelandet. Om anrops-URL:en (eller URL:en vid asynkront anrop) inte har suffixet .xml returnerar REST-providern HTTP-koden `async_result` `500 Internal Server Error` följt av ett undantagsmeddelande.

Om anrops-URL:en (eller URL:en vid asynkront anrop) har suffixet .xml returnerar REST-providern HTTP-koden `async_result` `200 OK`följt av ett XML-dokument som beskriver undantaget i följande format.

```as3
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

Elementet är valfritt och finns bara om undantaget är en instans av `DSCError` `com.adobe.idp.dsc.DSCException`.

## Säkerhet och autentisering {#security-and-authentication}

För att tillhandahålla REST-anrop med en säker transport kan en AEM-formuläradministratör aktivera HTTPS-protokollet på J2EE-programservern som är värd för AEM Forms. Den här konfigurationen är specifik för J2EE-programservern. den ingår inte i formulärserverkonfigurationen.

>[!NOTE]
>
>Som Workbench-utvecklare som vill visa dina processer via en REST-slutpunkt bör du tänka på XSS-problemet. XSS-säkerhetsluckor kan användas för att stjäla eller manipulera cookies, ändra presentationen av innehåll och äventyra konfidentiell information. Vi rekommenderar att du utökar processlogiken med ytterligare valideringsregler för in- och utdata om XSS-sårbarheten är ett problem.

## AEM Forms-tjänster som stöder REST-anrop {#aem-forms-services-that-support-rest-invocation}

Även om vi rekommenderar att du anropar processer som skapats med Workbench i motsats till tjänster direkt, finns det vissa AEM Forms-tjänster som stöder REST-anrop. Orsaken till att du bör anropa en process i stället för en tjänst direkt är att det är mer effektivt att anropa en process. Tänk på följande scenario. Anta att du vill skapa en princip från en REST-klient. Det innebär att du vill att REST-klienten ska definiera värden som principnamn och offlinelåneperiod.

Om du vill skapa en profil måste du definiera komplexa datatyper, till exempel ett `PolicyEntry` objekt. Ett `PolicyEntry` objekt definierar attribut som behörigheter som är kopplade till profilen. (Se [Skapa profiler](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

I stället för att skicka en REST-begäran för att skapa en princip (som skulle inkludera att definiera komplexa datatyper som till exempel ett `PolicyEntry` objekt), skapar du en process som skapar en princip med Workbench. Definiera processen för att acceptera primitiva indatavariabler, till exempel ett strängvärde som definierar processnamnet eller ett heltal som definierar offlinelåneperioden.

På så sätt behöver du inte skapa en REST-anropsbegäran som innehåller komplexa datatyper som krävs för åtgärden. Processen definierar de komplexa datatyperna och allt du gör från REST-klienten anropar processen och skickar primitiva datatyper. Mer information om hur du anropar en process med REST finns i [Anropa MyApplication/EncryptDocument-processen med REST](#rest-invocation-examples).

Följande listor anger vilka AEM Forms-tjänster som stöder direkt REST-anrop.

* Distiller Service
* Rights Management-tjänst
* GeneratePDF-tjänst
* Generate3dPDF-tjänst
* FormDataIntegration

## Exempel på REST-anrop {#rest-invocation-examples}

Följande exempel på REST-anrop finns:

* Skicka booleska värden till en AEM-formulärprocess
* Skicka datumvärden till en AEM-formulärprocess
* Skicka dokument till en AEM-formulärprocess
* Skicka dokument- och textvärden till en AEM-formulärsprocess
* Skicka uppräkningsvärden till en AEM-formulärprocess
* Anropa processen MyApplication/EncryptDocument med REST
* Anropa MyApplication/EncryptDocument-processen från Acrobat

   Varje exempel visar hur olika datatyper skickas till en AEM Forms-process

**Överföra booleska värden till en process**

I följande HTML-exempel skickas två `Boolean` värden till en AEM Forms-process med namnet `RestTest2`. Anropsmetodens namn är `invoke` och versionen är 1.0. Observera att metoden HTML Post används.

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Skicka datumvärden till en process**

I följande HTML-exempel skickas ett datumvärde till en AEM Forms-process med namnet `SOAPEchoService`. Anropsmetodens namn är `echoCalendar`. Observera att HTML- `Post` metoden används.

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Skicka dokument till en process**

I följande HTML-exempel anropas en AEM Forms-process med namnet `MyApplication/EncryptDocument` som kräver ett PDF-dokument. Mer information om detta finns i [Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Skicka dokument- och textvärden till en process**

I följande HTML-exempel anropas en AEM Forms-process med namnet `RestTest3` som kräver ett dokument och två textvärden. Observera att metoden HTML Post används.

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Skicka uppräkningsvärden till en process**

I följande HTML-exempel anropas en AEM Forms-process med namnet `SOAPEchoService` som kräver ett uppräkningsvärde. Observera att metoden HTML Post används.

```as3
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Anropa processen MyApplication/EncryptDocument med REST**

Du kan anropa en kort AEM Forms-process med namnet *MyApplication/EncryptDocument* genom att använda REST.

>[!NOTE]
>
>Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplet skapar du en process med namnet `MyApplication/EncryptDocument` med workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

   När den här processen anropas med en REST-begäran visas det krypterade PDF-dokumentet i webbläsaren. Innan du visar PDF-dokumentet anger du lösenordet (om inte skyddet är inaktiverat). Följande HTML-kod representerar en REST-anropsbegäran till `MyApplication/EncryptDocument` processen.

   ```as3
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Anropa MyApplication/EncryptDocument-processen från Acrobat**{#invoke-process-acrobat}

Du kan anropa en formulärprocess från Acrobat genom att använda en REST-begäran. Du kan till exempel anropa processen *MittProgram/KrypteraDokument* . Om du vill starta en formulärprocess från Acrobat placerar du en Skicka-knapp i en XDP-fil i Designer. (Se [Designer-hjälpen](https://www.adobe.com/go/learn_aemforms_designer_63).)

Ange URL-adressen som processen ska anropas i fältet *Skicka till URL* för knappen, vilket visas på följande bild.

Den fullständiga URL:en för att anropa processen är https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Om processen kräver ett PDF-dokument som indatavärde måste du skicka formuläret som PDF, vilket visades i föregående bild. Dessutom måste processen returnera ett PDF-dokument för att kunna anropa en process. Annars kan Acrobat inte hantera returvärdet och ett fel inträffar. Du behöver inte ange namnet på indataprocessvariabeln. Processen *MyApplication/EncryptDocument* har till exempel en indatavariabel med namnet `inDoc`. Du behöver inte ange inDoc så länge formuläret skickas som PDF.

Du kan också skicka formulärdata som XML till en formulärprocess. Om du vill skicka XML-data kontrollerar du att XML anges i `Submit As` listrutan. Eftersom processens returvärde måste vara ett PDF-dokument, visas PDF-dokumentet i Acrobat.
