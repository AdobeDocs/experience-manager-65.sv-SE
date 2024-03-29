---
title: Lägg till en anpassad felhanterare i Adaptive Forms baserat på kärnkomponenter för AEM Adaptive Forms
description: AEM Forms har körklara hanterare och felhanterare för ett formulär som använder REST-slutpunkten som konfigurerats för att anropa en extern tjänst. Du kan lägga till en standardfelhanterare och en anpassad felhanterare i en AEM anpassad form.
keywords: Lägg till en anpassad felhanterare, lägg till en standardfelhanterare, lägg till en felhanterare i formuläret, använd regelredigerarens anropstjänst för att lägga till en anpassad felhanterare, konfigurera regelredigeraren för att lägga till en anpassad felhanterare, lägg till en anpassad felhanterare med regelredigeraren
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 2118d77f-1314-48f1-88e3-e27dd8e9f17b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2251'
ht-degree: 0%

---

# Felhanterare i adaptiv Forms (kärnkomponenter) {#error-handlers-in-adaptive-form}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/add-custom-error-handler-adaptive-forms-core-components.html) |
| AEM 6.5 | Den här artikeln |

AEM Forms har färdiga funktioner och felhanterare för att skicka in formulär. Den innehåller även funktioner för att anpassa felhanterarfunktioner. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar. Hanterare är funktioner på klientsidan som körs baserat på serversvaret. När en extern tjänst anropas med API:er överförs data till servern för validering, som returnerar ett svar till klienten med information om lyckad eller felhändelse för överföringen. Informationen skickas som parametrar till den relevanta hanteraren för att köra funktionen. En felhanterare hjälper till att hantera och visa fel eller valideringsproblem som påträffats.

![felhanterararbetsflöde för att förstå hur du lägger till en anpassad felhanterare i formulär](/help/forms/using/assets/error-handler-workflow.png)

Det adaptiva formuläret validerar indata som du anger i fält baserat på förinställda valideringskriterier och söker efter olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst. Du kan ange valideringskriterier baserat på den datakälla som du använder med det adaptiva formuläret. Om du till exempel använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil.

Om indatavärdena uppfyller valideringskriterierna skickas värdena till datakällan i annat fall visas ett felmeddelande i Adaptiv form med hjälp av en felhanterare. På samma sätt som detta arbetssätt integreras Adaptive Forms med anpassade felhanterare för datavalidering. Om indatavärdena inte uppfyller valideringskriterierna visas felmeddelandena på fältnivå i det adaptiva formuläret. Detta inträffar när det valideringsfelmeddelande som returneras av servern har standardmeddelandeformatet.


## Användning av felhanterare {#uses-of-error-handler}

Felhanterare används för olika syften. Några av användningsområdena för felhanterarfunktioner visas nedan:

* **Utför validering**: Felhanteringen börjar med att användarindata valideras mot fördefinierade regler eller villkor. När användarna fyller i ett adaptivt formulär validerar felhanteraren indata så att det uppfyller det format, den längd eller andra begränsningar som krävs.

* **Ge feedback i realtid**: När ett fel upptäcks visar felhanteraren direkt feedback till användaren, t.ex. textbundna felmeddelanden under motsvarande formulärfält. Denna feedback hjälper användarna att identifiera och åtgärda fel utan att behöva skicka in formuläret och vänta på ett svar.


* **Visa felmeddelanden**: När en sändning med adaptiva formulär påträffar ett valideringsfel visas ett felmeddelande i felhanteraren. Felmeddelandena ska vara tydliga, koncisa och markera de specifika fält som behöver åtgärdas.

* **Markerar det felaktiga fältet**: För att dra användarens uppmärksamhet till specifika felaktiga fält markeras eller visas motsvarande fält. Den utförs genom att ändra bakgrundsfärgen, lägga till en ikon eller kantlinje eller någon annan visuell indikator som hjälper användarna att snabbt hitta och åtgärda felen.


## Fel-/felsvarsformat {#failure-response-format}

I ett adaptivt formulär visas felen på fältnivå om servervalideringsfelmeddelanden är i följande standardformat.
Koden nedan visar den befintliga strukturen för felsvar:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


Var:

* `errorCausedBy` beskriver orsaken till felet.
* `errors` Ange det kvalificerade fältnamnet för de fält som underkändes i valideringskriterierna tillsammans med valideringsfelmeddelandet.
* `originCode` fält som lagts till av AEM och innehåller http-statuskoden som returneras av den externa tjänsten.
* `originMessage` fält som lagts till av AEM och innehåller rådata som returnerats av den externa tjänsten.

Med förbättringarna i funktioner och efterföljande uppdateringar i AEM Forms-versionerna har den befintliga felsvarsstrukturen ändrats till ett nytt format baserat på RFC7807, som är bakåtkompatibel med den befintliga felsvarsstrukturen:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR" (required)
        "title": "Server side validation failed/Third party service invocation failed" (optional)
        "detail": "" (optional)
        "instance": "" (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code> (optional - if there is SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - if there is SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Kontrollera att felsvarsstrukturen innehåller antingen **fieldName** eller **dataRef**.
> * Se till att **ContentType** header is **application/problem+json**.

Var:
* `type (required)` anger feltypen. Det kan vara något av följande värden:
   * `SERVER_SIDE_VALIDATION` indikerar ett fel på grund av validering på serversidan.
   * `FORM_SUBMISSION` anger ett fel när formulär skickas
   * `SERVICE_INVOCATION` indikerar ett fel under ett anrop till en tjänst från tredje part.
   * `FAILURE` anger ett allmänt fel.
   * `VALIDATION_ERROR` indikerar ett fel på grund av ett valideringsfel.

* `title (optional)` innehåller en titel eller kort beskrivning av felet.
* `detail (optional)` innehåller ytterligare information om felet om det behövs.
* `instance (optional)` representerar en instans eller identifierare som är associerad med felet och hjälper till att spåra eller identifiera den specifika förekomsten av felet.
* `validationErrors (required)` innehåller information om valideringsfel. Den innehåller följande fält:
   * `fieldname` anger det kvalificerade fältnamnet för de fält som inte uppfyller valideringskriterierna.
   * `dataRef` representerar JSON-sökvägen eller XPath för de fält som underkändes vid valideringen.
   * `details` innehåller valideringsfelmeddelandet med det felaktiga fältet.
* `originCode (optional)` fält som lagts till av AEM och innehåller http-statuskoden som returneras av den externa tjänsten
* `originMessage (optional)` fält som lagts till av AEM och innehåller rådata som returnerats av den externa tjänsten.

### Exempel på felsvarsformat {#sample-error-response-format}

Vissa av alternativen för att visa felsvaren är:

+++  Baserat på egenskapen Adaptive Form fieldName


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```


+++


+++ Baserat på egenskapen dataRef för adaptiv form

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

+++

## Förutsättningar {#prerequisites}

Innan du använder felhanterare i en adaptiv Forms:

* [Aktivera adaptiva Forms Core-komponenter för din miljö](enable-adaptive-forms-core-components.md).
* Grundläggande kunskap till [skapa en anpassad funktion](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* Installera den senaste versionen av [Apache Maven](https://maven.apache.org/download.cgi).

## Lägg till felhanterare med Regelredigeraren {#add-error-handler-using-rule-editor}

Använda [Regelredigerarens anropstjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) definierar du valideringskriterierna baserat på den datakälla som du använder med det adaptiva formuläret. Om du använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil. Genom att använda felhanterarfunktionerna och regelredigeraren i Adaptive Forms kan du effektivt hantera och anpassa felhanteringen. Du definierar villkoren med Regelredigeraren och konfigurerar de åtgärder som ska utföras när regeln aktiveras. Adaptiv form validerar indata som du anger i fält baserat på förinställda valideringskriterier. Om indatavärdena inte uppfyller valideringskriterierna visas felmeddelandena på fältnivån i ett adaptivt formulär.

>[!NOTE]
>
> * Konfigurera Adaptiv Forms med en formulärdatamodell om du vill använda felhanterare med åtgärden Invoke i regelredigeraren.
> * En standardfelhanterare tillhandahålls för att visa felmeddelanden i fält om felsvaret finns i standardschemat. Du kan också anropa standardfelhanteraren från den anpassade felhanterarfunktionen.

Med regelredigeraren kan du:

* [Lägg till standardfelhanterarfunktion](#add-default-errror-handler)
* [Lägg till anpassad felhanterarfunktion](#add-custom-errror-handler)


### Lägg till standardfelhanterarfunktion {#add-default-errror-handler}

En standardfelhanterare stöds för att visa felmeddelanden i fält om felsvaret är i standardschema eller i valideringsfel på serversidan.
Så här använder du en standardfelhanterare med [Regelredigerarens anropstjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) åtgärd, ta ett exempel på ett enkelt adaptivt formulär med två fält, **Djurs-ID** och **Djurnamn** och använder en standardfelhanterare på **Djurs-ID** fält för att kontrollera olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst, till exempel `200 - OK`,`404 - Not Found`, `400 - Bad Request`. Så här lägger du till en standardfelhanterare med hjälp av åtgärden Anropa tjänst i regelredigeraren:

1. Öppna ett adaptivt formulär i redigeringsläge, markera en formulärkomponent och markera **[!UICONTROL Rule Editor]** för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create]**.
1. Skapa ett villkor i **När** -delen av regeln. Till exempel: **När[Namn på Pet ID-fält]** ändras. Markeringen ändras från **Välj läge** listruta.
1. I **Sedan** avsnitt, markera **[!UICONTROL Invoke Service]** från **Välj åtgärd** listruta.
1. Välj en **Bokför tjänst** och dess motsvarande databindningar från **Indata** -avsnitt. Validera till exempel **Djurs-ID** väljer du en **Bokför tjänst** as **GET /husdjur/{petId}** och markera **Djurs-ID** i **Indata** -avsnitt.
1. Välj databindningar på menyn **Utdata** -avsnitt. Välj **Djurnamn** i **Utdata** -avsnitt.
1. Välj **[!UICONTROL Default Error Handler]** från **Felhanterare** -avsnitt.
1. Klicka på **[!UICONTROL Done]**.

![lägga till en standardfelhanterare för fältvalideringskontroller i ett formulär](/help/forms/using/assets/default-error-handler.png)

Som ett resultat av den här regeln anger du värden för **Djurs-ID** kontrollerar validering för **Djurnamn** med en extern tjänst som anropas av REST-slutpunkten. Om valideringskriterierna som baseras på datakällan misslyckas, visas felmeddelandena på fältnivå.

![visa standardfelmeddelandet när du lägger till en standardfelhanterare i ett formulär för att hantera felsvar](/help/forms/using/assets/default-error-message.png)

### Lägg till anpassad felhanterarfunktion {#add-custom-errror-handler}

Du kan lägga till en anpassad felhanterarfunktion för att utföra några av åtgärderna:

* hantera felsvar som använder icke-standard- eller standardfelsvar. Observera att dessa felsvar som inte är standard inte följer [standardschema för felsvar](#failure-response-format).
* skicka analyshändelser till alla analysplattformar. Exempel: Adobe Analytics.
* visa modal dialog med felmeddelanden.

Förutom de ovannämnda åtgärderna kan de anpassade felhanterarna användas för att utföra anpassade funktioner som uppfyller specifika användarkrav.

Den anpassade felhanteraren är en funktion (klientbibliotek) som är utformad för att svara på fel som returneras av en extern tjänst och leverera ett anpassat svar till slutanvändarna. Alla klientbibliotek med anteckningar `@errorHandler` betraktas som en anpassad felhanterarfunktion. Den här anteckningen hjälper till att identifiera felhanterarfunktionen som anges i `.js` -fil.

Så här skapar och använder du en anpassad felhanterare med [Regelredigerarens anropstjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) åtgärd, låt oss ta ett exempel på Adaptiv form med två fält, **Djurs-ID** och **Djurnamn** och använda en anpassad felhanterare på **Djurs-ID** fält för att kontrollera olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst, till exempel `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

Så här lägger du till och använder en anpassad felhanterare i ett adaptivt formulär:

1. [Skapa en anpassad felhanterare](#create-custom-error-message)
1. [Använd regelredigeraren för att konfigurera en anpassad felhanterare](#use-custom-error-handler)

#### 1. Skapa en anpassad felhanterare {#create-custom-error-message}

Så här skapar du en anpassad felfunktion:

1. Logga in `http://server:port/crx/de/index.jsp#`.
1. Skapa en mapp under `/apps` mapp. Skapa till exempel en mapp med namnet som `experience-league`.
1. Spara ändringarna.
1. Navigera till den skapade mappen och skapa en nod av typen `cq:ClientLibraryFolder` as `clientlibs`.
1. Navigera till den nyskapade `clientlibs` mapp och lägg till `allowProxy` och `categories` egenskaper:

   ![Egenskaper för anpassad biblioteksnod](/help/forms/using/assets/customlibrary-properties.png)

   >[!NOTE]
   >
   > Du kan ange valfritt namn i stället för `customfunctionsdemo`.

1. Spara ändringarna.

1. Skapa en mapp med namnet `js` under `clientlibs` mapp.
1. Skapa en JavaScript-fil med namnet `functions.js` under `js` mapp
1. Skapa en fil med namnet `js.txt` under `clientlibs` mapp.
1. Spara ändringarna.
Den skapade mappstrukturen ser ut så här:

   ![Mappstruktur för klientbibliotek har skapats](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. Dubbelklicka på `functions.js` för att öppna redigeraren. Filen innehåller koden för den anpassade felhanteraren.
Låt oss lägga till följande kod i JavaScript-filen för att visa svar och rubriker som tagits emot från REST-tjänstens slutpunkt i webbläsarkonsolen.

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           alert("CustomErrorHandler - Please enter valid PetId.")
           globals.invoke('defaultErrorHandler',response, headers)
           console.log("Custom Error Handler processing end...");
       }
   ```

   Följande rad i exempelkoden används för att anropa standardfelhanteraren från din anpassade felhanterare:
   `globals.invoke('defaultErrorHandler',response, headers) `

1. Spara `function.js`.
1. Navigera till `js.txt` och lägg till följande kod:

   ```javascript
       #base=js
       functions.js
   ```

1. Spara `js.txt` -fil.

Nu ska vi förstå hur du konfigurerar och använder en anpassad felhanterare med hjälp av regelredigerarens Invoke-tjänst i AEM Forms.

#### 2. Använd regelredigeraren för att konfigurera en anpassad felhanterare {#use-custom-error-handler}

Innan du implementerar den anpassade felhanteraren i ett adaptivt formulär måste du kontrollera att klientbibliotekets namn finns i **[!UICONTROL Client Library Category]** justerar med namnet som anges i kategorialternativet i `.content.xml` -fil.

![Lägga till namnet på klientbiblioteket i konfigurationen för adaptiv formulärbehållare](/help/forms/using/assets/client-library-category-name-core-component.png)

I det här fallet anges klientbiblioteksnamnet som `customfunctionsdemo` i `.content.xml` -fil.

Använda en anpassad felhanterare med **[!UICONTROL Rule Editor's Invoke Service]** åtgärd:

1. Öppna ett adaptivt formulär i redigeringsläge, markera en formulärkomponent och markera **[!UICONTROL Rule Editor]** för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create]**.
1. Skapa ett villkor i **När** -delen av regeln. Till exempel När **[Namn på Pet ID-fält]** ändras, välj **ändras** från **Välj läge** listruta.
1. I **Sedan** avsnitt, markera **[!UICONTROL Invoke Service]** från **Välj åtgärd** listruta.
1. Välj en **Bokför tjänst** och dess motsvarande databindningar från **Indata** -avsnitt. Validera till exempel **Djurs-ID** väljer du en **Bokför tjänst** as **GET /husdjur/{petId}** och markera **Djurs-ID** i **Indata** -avsnitt.
1. Välj databindningar på menyn **Utdata** -avsnitt. Välj till exempel **Djurnamn** i **Utdata** -avsnitt.
1. Välj **[!UICONTROL Custom Error Handler]** från **[!UICONTROL Error Handler]** -avsnitt.
1. Klicka på **[!UICONTROL Done]**.

![lägga till anpassad felhanterare i ett formulär för att hantera felsvar](/help/forms/using/assets/custom-error-handler.png)

Som ett resultat av den här regeln anger du värden för **Djurs-ID** kontrollerar validering för **Djurnamn** med en extern tjänst som anropas av REST-slutpunkten. Om valideringskriterierna som baseras på datakällan misslyckas, visas felmeddelandena på fältnivå.

![lägga till en anpassad felhanterare i ett formulär för att hantera felsvar](/help/forms/using/assets/custom-error-handler-message-core-component.png)

Öppna webbläsarkonsolen och kontrollera svaret och rubriken som tagits emot från REST-tjänstens slutpunkt för valideringsfelmeddelandet.

Den anpassade felhanterarfunktionen ansvarar för att utföra ytterligare åtgärder, som att visa en modal dialogruta eller skicka en analyshändelse, baserat på felsvaret. En anpassad felhanterarfunktion ger flexibilitet att anpassa felhanteringen efter specifika användarkrav.

## Se även {#see-also}

* [Skapa en fristående grundkomponentbaserad adaptiv form](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Skapa stilar eller teman för formulären](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Skapa eller lägga till ett anpassat formulär på AEM Sites-sidan](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)
