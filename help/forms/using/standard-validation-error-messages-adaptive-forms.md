---
title: Standardvalideringsfelmeddelanden för anpassade formulär
seo-title: Standardvalideringsfelmeddelanden för anpassade formulär
description: Omvandla valideringsfelmeddelanden för adaptiva formulär till standardformat med anpassade felhanterare
seo-description: Omvandla valideringsfelmeddelanden för adaptiva formulär till standardformat med anpassade felhanterare
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 0%

---


# Standardvalideringsfelmeddelanden för adaptiva formulär {#standard-validation-error-messages}

Anpassade formulär validerar indata som du anger i fält baserat på ett förinställt valideringskriterier. Valideringskriterierna hänvisar till godkända indatavärden för fält i ett adaptivt formulär. Du kan ange valideringskriterier baserat på den datakälla som du använder med det anpassade formuläret. Om du till exempel använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil.

Om indatavärdena uppfyller valideringskriterierna skickas värdena till datakällan. Annars visas ett felmeddelande i det adaptiva formuläret.

På liknande sätt kan adaptiva formulär nu integreras med anpassade tjänster för datavalidering. Om indatavärdena inte uppfyller valideringskriterierna och det valideringsfelmeddelande som servern returnerar har standardmeddelandeformatet, visas felmeddelandena på fältnivå i formuläret.

Om indatavärdena inte uppfyller valideringskriterierna och servervalideringsfelmeddelandet inte har standardmeddelandeformatet, erbjuder adaptiva formulär en mekanism för att omvandla valideringsfelmeddelandena till ett standardformat så att de visas på fältnivå i formuläret. Du kan omvandla felmeddelandet till standardformat på något av följande två sätt:

* Lägg till en anpassad felhanterare när formulär skickas med adaptiv form
* Lägg till anpassad hanterare för att anropa tjänståtgärden med regelredigeraren

I den här artikeln beskrivs standardformatet för valideringsfelmeddelanden och instruktionerna för att omvandla felmeddelanden från ett anpassat till standardformatet.

## Standardfelmeddelandeformat för validering {#standard-validation-message-format}

De adaptiva formulären visar felen på fältnivå om servervalideringsfelmeddelanden är i följande standardformat:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

Var:

* `errorCausedBy` beskriver orsaken till felet
* `errors` ange SOM-uttrycket för de fält som underkändes i valideringskriterierna tillsammans med valideringsfelmeddelandet
* `originCode` innehåller felkoden som returneras av den externa tjänsten
* `originMessage` innehåller råa feldata som returneras av den externa tjänsten

## Konfigurera adaptiv formulärsändning för att lägga till anpassade hanterare {#configure-adaptive-form-submission}

Om servervalideringsfelmeddelandet inte visas i standardformat kan du aktivera asynkron sändning och lägga till en anpassad felhanterare vid adaptiv formulärsändning för att konvertera meddelandet till ett standardformat.

### Konfigurera asynkron sändning av anpassningsbara formulär {#configure-asynchronous-adaptive-form-submission}

Innan du lägger till en anpassad hanterare måste du konfigurera det adaptiva formuläret för asynkron överföring. Utför följande steg:

1. I redigeringsläget för anpassningsbara formulär väljer du objektet Formulärbehållare och trycker på ![adaptiva formuläregenskaper](assets/configure_icon.png) för att öppna dess egenskaper.
1. Aktivera **[!UICONTROL Use asynchronous submission]** i egenskapsavsnittet för **[!UICONTROL Submission]**.
1. Välj **[!UICONTROL Revalidate on server]** för att validera indatafältvärdena på servern innan de skickas.
1. Välj åtgärden Skicka:

   * Välj **[!UICONTROL Submit using Form Data Model]** och välj lämplig datamodell om du använder RESTful-webbtjänstbaserad [formulärdatamodell](work-with-form-data-model.md) som datakälla.
   * Välj **[!UICONTROL Submit to REST endpoint]** och ange **[!UICONTROL Redirect URL/Path]** om du använder RESTful-webbtjänster som datakälla.

   ![adaptiva egenskaper för att skicka formulär](assets/af_submission_properties.png)

1. Tryck på ![Spara](assets/save_icon.png) för att spara egenskaperna.

### Lägg till en anpassad felhanterare vid sändning av anpassningsbara formulär {#add-custom-error-handler-af-submission}

AEM Forms har färdiga funktioner och felhanterare för att skicka in formulär. Hanterare är funktioner på klientsidan som körs baserat på serversvaret. När ett formulär skickas skickas data till servern för validering, som returnerar ett svar till klienten med information om om huruvida överföringen lyckades eller inte. Informationen skickas som parametrar till den relevanta hanteraren för att köra funktionen.

Utför följande steg för att lägga till en anpassad felhanterare när formulär skickas med adaptiv kod:

1. Öppna det adaptiva formuläret i redigeringsläge, markera ett formulärobjekt och tryck på <!--![Rule Editor](assets/af_edit_rules.png)--> för att öppna regelredigeraren.
1. Välj **[!UICONTROL Form]** i trädet Formulärobjekt och tryck på **[!UICONTROL Create]**.
1. Välj **[!UICONTROL Error in Submission]** i listrutan Händelse.
1. Skriv en regel för att konvertera en anpassad felstruktur till standardfelstrukturen och tryck på **[!UICONTROL Done]** för att spara regeln.

Här följer ett exempel på kod som konverterar en anpassad felstruktur till standardfelstrukturen:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

I `var som_map` visas SOM-uttrycket för de adaptiva formulärfält som du vill omvandla till standardformatet. Du kan visa SOM-uttrycket för vilket fält som helst i ett adaptivt formulär genom att trycka på fältet och välja **[!UICONTROL View SOM Expression]**.

Med den här anpassade felhanteraren konverterar det adaptiva formuläret fälten i `var som_map` till standardfelmeddelandeformat. Därför visas valideringsfelmeddelanden på fältnivå i det adaptiva formuläret.

## Lägg till anpassad hanterare med åtgärden Anropa tjänst

Utför följande steg för att lägga till felhanterare för att konvertera en anpassad felstruktur till standardfelstrukturen med [Regelredigerarens](rule-editor.md) Invoke Service-åtgärd:

1. Öppna det adaptiva formuläret i redigeringsläge, markera ett formulärobjekt och tryck på ![Regelredigeraren](assets/rule_editor_icon.png) för att öppna regelredigeraren.
1. Tryck på **[!UICONTROL Create]**.
1. Skapa ett villkor i avsnittet **[!UICONTROL When]** i regeln. När[fältnamnet] har ändrats. Välj **[!UICONTROL is changed]** i listrutan **[!UICONTROL Select State]** för att uppnå det här villkoret.
1. I avsnittet **[!UICONTROL Then]** väljer du **[!UICONTROL Invoke Service]** i listrutan **[!UICONTROL Select Action]**.
1. Välj en posttjänst och dess motsvarande databindningar i avsnittet **[!UICONTROL Input]**. Om du till exempel vill validera fälten **Namn**, **ID** och **Status** i anpassningsformuläret, markerar du en posttjänst (husdjur) och väljer pet.name, pet.id och pet.status i avsnittet **[!UICONTROL Input]**.

Som ett resultat av den här regeln valideras de värden som du anger för fälten **Namn**, **ID** och **Status** så fort fältet som definieras i steg 2 ändras och du tabbar ut från fältet i formuläret.

1. Välj **[!UICONTROL Code Editor]** i listrutan för lägesval.
1. Tryck på **[!UICONTROL Edit Code]**.
1. Ta bort följande rad från den befintliga koden:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Skriv en regel för att konvertera en anpassad felstruktur till standardfelstrukturen och tryck på **[!UICONTROL Done]** för att spara regeln.
Lägg till exempel till följande exempelkod i slutet för att konvertera en anpassad felstruktur till standardfelstrukturen:

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   I `var som_map` visas SOM-uttrycket för de adaptiva formulärfält som du vill omvandla till standardformatet. Du kan visa SOM-uttrycket för vilket fält som helst i ett adaptivt formulär genom att trycka på fältet och välja **[!UICONTROL View SOM Expression]** från **[!UICONTROL More Opions]** (..)-menyn.

   Kontrollera att du kopierar följande rad med exempelkoden till den anpassade felhanteraren:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   API:t executeOperation innehåller parametrarna `null` och `errorHandler` baserat på den nya anpassade felhanteraren.

   Med den här anpassade felhanteraren konverterar det adaptiva formuläret fälten i `var som_map` till standardfelmeddelandeformat. Därför visas valideringsfelmeddelanden på fältnivå i det adaptiva formuläret.