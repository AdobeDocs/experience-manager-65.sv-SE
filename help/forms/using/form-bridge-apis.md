---
title: API:er för Form Bridge för HTML5-formulär
seo-title: API:er för Form Bridge för HTML5-formulär
description: Externa program använder FormBridge API för att ansluta till XFA-mobilformuläret. API:t skickar en FormBridgeInitialized-händelse i det överordnade fönstret.
seo-description: Externa program använder FormBridge API för att ansluta till XFA-mobilformuläret. API:t skickar en FormBridgeInitialized-händelse i det överordnade fönstret.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# API:er för Form Bridge för HTML5-formulär {#form-bridge-apis-for-html-forms}

Du kan använda API:erna för Form Bridge för att öppna en kommunikationskanal mellan ett XFA-baserat HTML5-formulär och dina program. API:erna för Form Bridge tillhandahåller ett **connect**-API för att skapa anslutningen.

API:t **connect** accepterar en hanterare som ett argument. När en lyckad anslutning har skapats mellan ett XFA-baserat HTML5-formulär och Form Bridge anropas handtaget.

Du kan använda följande exempelkod för att skapa anslutningen.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>Se till att du skapar en anslutning innan du inkluderar filen formRuntime.jsp.

## Tillgängligt API för Form Bridge  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Returnerar versionsnumret för skriptbiblioteket

* **Indata**: Ingen
* **Utdata**: Versionsnummer för skriptbiblioteket
* **Fel**: Ingen

**isConnected()** Kontrollerar om formulärtillståndet har initierats

* **Indata**: Ingen
* **Utdata**:  **Om** tillståndet för XFA-formuläret har initierats

* **Fel**: Ingen

**connect(handler, context)** Skapar en anslutning till FormBridge och kör funktionen när anslutningen har upprättats och formulärstatusen har initierats

* **Indata**:

   * **hanterare**: Funktion som ska köras när Form Bridge är anslutet
   * **kontext**: Det objekt som kontexten (this) för  ** hanterarfunktionen är inställd på.

* **Utdata**: Ingen
* **Fel**: Ingen

**getDataXML(options)** Returnerar aktuella formulärdata i XML-format

* **Indata:**

   * **alternativ:** JavaScript-objekt som innehåller följande egenskaper:

      * **Fel**: Felhanterarfunktion
      * **lyckades**: Hanterarfunktionen Slutfört. Den här funktionen skickas till ett objekt som innehåller XML i egenskapen *data*.
      * **kontext**: Det objekt som kontexten (this) för  ** funktionen success anges till
      * **validationChecker**: Funktion som ska anropas för att kontrollera verifieringsfel som tagits emot från servern. Valideringsfunktionen skickar en array med felsträngar.
      * **formState**: JSON-tillståndet för XFA-formuläret som data-XML ska returneras för. Om inget anges returneras data-XML för det återgivna formuläret.

* **Utdata:** Ingen
* **Fel:** Ingen

**registerConfig(configName, config)** Registrerar användare/portalspecifika konfigurationer med FormBridge. Dessa konfigurationer åsidosätter standardkonfigurationerna. De konfigurationer som stöds anges i avsnittet config.

* **Indata:**

   * **configName:** Namnet på konfigurationen som ska åsidosättas

      * **widgetConfig:** Låter användaren åsidosätta standardwidgetar i formuläret med anpassade widgetar. Konfigurationen åsidosätts enligt följande:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Tillåter användaren att åsidosätta standardbeteendet för återgivning av endast den första sidan. Konfigurationen åsidosätts enligt följande:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled:  &lt;true>, crinkPageDisabled:  &lt;true> }).*

      * **LoggingConfig:** Låter användaren åsidosätta loggningsnivån, inaktivera loggning för en kategori eller visa loggkonsolen eller skicka till servern. Konfigurationen kan åsidosättas på följande sätt:

      ```javascript
      formBridge.registerConfig{
        "LoggerConfig" : {
      {
      "on":`<true *| *false>`,
      "category":`<array of categories>`,
      "level":`<level of categories>`, "
      type":`<"console"/"server"/"both">`
      }
        }
      ```

      * **SubmitServiceProxyConfig:** Tillåt användarna att registrera proxytjänster för sändning och inloggning.

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** Konfigurationens värde



* **Output:** Object containing original value of the configuration in  ** data property.

* **Fel:** Ingen

**hideFields(fieldArray)** Döljer de fält vars uttryck är angivna i fieldArray. Anger egenskapen presence för de angivna fälten till osynlig

* **Indata:**

   * **fieldArray:** Array med vissa uttryck för de fält som ska döljas

* **Utdata:** Ingen
* **Fel:** Ingen

**showFields(fieldArray)** Visar de fält vars uttryck anges i fieldArray. Anger egenskapen presence för de angivna fälten till visible

* **Indata:**

   * **fieldArray:** Array med vissa uttryck för de fält som ska visas

* **Utdata:** Ingen
* **Fel:** Ingen

**hideSubmitButtons()** Döljer alla skicka-knappar i formuläret

* **Indata**: Ingen
* **Utdata**: Ingen
* **Fel**: Utlöser ett undantag om formulärtillståndet inte har initierats

**getFormState()** Returnerar den JSON som representerar formulärläget

* **Indata:** Ingen
* **output:** Object containing JSON representing the current Form State in  ** data property.

* **Fel:** Ingen

**restoreFormState(options)** Återställer formulärtillståndet från det angivna JSON-läget i options-objektet. Läget används och hanterare för lyckade eller fel anropas när åtgärden har slutförts

* **Indata:**

   * **Alternativ:** JavaScript-objekt som innehåller följande egenskaper:

      * **Fel**: Felhanterarfunktion
      * **lyckades**: Hanterarfunktionen Slutfört
      * **kontext**: Det objekt som kontexten (this) för  ** efterföljande funktion anges till
      * **formState**: Formulärets JSON-tillstånd. Formuläret återställs till JSON-läget.

* **Utdata:** Ingen
* **Fel:** Ingen

**setFocus (som)** Anger fokus på fältet som anges i som-uttrycket

* **Indata:** Som uttryck för fältet som fokus ska ställas in på
* **Utdata:** Ingen
* **Fel:** Utlöser ett undantag om ett felaktigt &quot;SOM&quot;-uttryck används

**setFieldValue (som, value)** Anger värdet för fälten för de angivna som-uttrycken

* **Indata:**

   * **som:** Array som innehåller några uttryck för fältet. Det uttryck som anger fältets värde.
   * **value:** Array som innehåller värden som motsvarar de som anges i en  **** somarray. Om värdeets datatyp inte är densamma som fieldType ändras inte värdet.

* **Utdata:** Ingen
* **Fel:** Utlöser ett undantag om ett felaktigt som-uttryck används

**getFieldValue (som)** Returnerar värdet för fälten för angivna som-uttryck

* **Indata:** Array som innehåller uttryck för fält vars värde måste hämtas
* **output:** Object containing the result as Array in  **** data property.

* **Fel:** Ingen

### Exempel på getFieldValue() API {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** Hämta listan med värden för den angivna egenskapen i fälten som anges i vissa uttryck

* **Indata:**

   * **som:** Array som innehåller vissa-uttryck för fälten
   * **egenskap**: Namn på egenskapen vars värde krävs

* **output:** Object containing the result as Array in  ** data property

* **Fel:** Ingen

**setFieldProperties(som, property, values)** Anger värdet för den givna egenskapen för alla fält som anges i som-uttryck

* **Indata:**

   * **som:** Array som innehåller uttryck för de fält vars värde måste anges
   * **egenskap**: Egenskap vars värde måste anges
   * **value:** Array containing values of the given property for fields specified in As expressions

* **Utdata:** Ingen
* **Fel:** Ingen

## Exempel på användning av Form Bridge API {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
