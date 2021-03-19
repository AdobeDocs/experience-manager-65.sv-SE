---
title: API för att anropa formulärdatamodelltjänst från anpassningsbara formulär
seo-title: API för att anropa formulärdatamodelltjänst från anpassningsbara formulär
description: Beskriver det invokeWebServices-API som du kan använda för att anropa webbtjänster som skrivits i WSDL inifrån ett adaptivt formulärfält.
seo-description: Beskriver det invokeWebServices-API som du kan använda för att anropa webbtjänster som skrivits i WSDL inifrån ett adaptivt formulärfält.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptiv Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# API för att anropa formulärdatamodelltjänst från adaptiva formulär {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Översikt {#overview}

Med AEM Forms kan formulärförfattare ytterligare förenkla och förbättra ifyllandet av formulär genom att anropa tjänster som konfigurerats i en formulärdatamodell inifrån ett adaptivt formulärfält. Om du vill anropa en datamodelltjänst kan du antingen skapa en regel i den visuella redigeraren eller ange ett JavaScript med hjälp av API:t `guidelib.dataIntegrationUtils.executeOperation` i kodredigeraren för [regelredigeraren](/help/forms/using/rule-editor.md).

Det här dokumentet fokuserar på att skriva ett JavaScript med hjälp av `guidelib.dataIntegrationUtils.executeOperation`-API:t för att anropa en tjänst.

## Använda API {#using-the-api}

API:t `guidelib.dataIntegrationUtils.executeOperation` anropar en tjänst från ett adaptivt formulärfält. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

Strukturen för API:t `guidelib.dataIntegrationUtils.executeOperation` anger information om tjänståtgärden. Strukturen har följande syntax.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API-strukturen anger följande information om tjänståtgärden.

<table>
 <tbody>
  <tr>
   <th>Parameter</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Struktur för att ange identifierare för formulärdatamodell, åtgärdstitel och åtgärdsnamn</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Anger databassökvägen till formulärdatamodellen inklusive dess namn</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Anger namnet på den tjänståtgärd som ska köras</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Kopplar ett eller flera formulärobjekt till indataargumenten för tjänståtgärden</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Mappar ett eller flera formulärobjekt till utdatavärden från tjänståtgärden för att fylla i formulärfält<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Returnerar värden baserat på indataargumenten för serviceåtgärden. Det är en valfri parameter som används som en återanropsfunktion.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visar ett felmeddelande om återanropsfunktionen lyckas inte visa utdatavärden baserat på indataargumenten. Det är en valfri parameter som används som en återanropsfunktion.<br /> </td>
  </tr>
 </tbody>
</table>

## Exempelskript för att anropa en tjänst {#sample-script-to-invoke-a-service}

Följande exempelskript använder API:t `guidelib.dataIntegrationUtils.executeOperation` för att anropa den `getAccountById`-tjänståtgärd som konfigurerats i formulärdatamodellen `employeeAccount`.

Åtgärden `getAccountById` tar värdet i formulärfältet `employeeID` som indata för argumentet `empId` och returnerar medarbetarens namn, kontonummer och kontosaldo för motsvarande medarbetare. Utdatavärdena fylls i i de angivna formulärfälten. Värdet i argumentet `name` fylls till exempel i i formulärelementet `fullName` och värdet för argumentet `accountNumber` i formulärelementet `account`.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Använda API:t med callback-funktionen {#using-the-api-callback}

Du kan också anropa datamodelltjänsten för formulär med API:t `guidelib.dataIntegrationUtils.executeOperation` med en callback-funktion. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

Återanropsfunktionen kan ha callback-funktionerna `success` och `failure`.

### Exempelskript med återanropsfunktioner för lyckade och misslyckade {#callback-function-success-failure}

Följande exempelskript använder API:t `guidelib.dataIntegrationUtils.executeOperation` för att anropa den `GETOrder`-tjänståtgärd som konfigurerats i formulärdatamodellen `employeeOrder`.

Åtgärden `GETOrder` tar värdet i formulärfältet `Order ID` som indata för argumentet `orderId` och returnerar orderkvantitetsvärdet i callback-funktionen `success`.  Om återanropsfunktionen `success` inte returnerar ordningsantalet visar återanropsfunktionen `failure` meddelandet `Error occured`.

>[!NOTE]
>
> Om du använder callback-funktionen `success` fylls inte utdatavärdena i de angivna formulärfälten.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
