---
title: API för att anropa formulärdatamodelltjänst från anpassningsbara formulär
seo-title: API för att anropa formulärdatamodelltjänst från anpassningsbara formulär
description: Beskriver det invokeWebServices-API som du kan använda för att anropa webbtjänster som skrivits i WSDL inifrån ett adaptivt formulärfält.
seo-description: Beskriver det invokeWebServices-API som du kan använda för att anropa webbtjänster som skrivits i WSDL inifrån ett adaptivt formulärfält.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# API för att anropa formulärdatamodelltjänst från anpassningsbara formulär {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Översikt {#overview}

AEM Forms gör det möjligt för formulärförfattare att ytterligare förenkla och förbättra formulärifyllningen genom att anropa tjänster som konfigurerats i en formulärdatamodell inifrån ett adaptivt formulärfält. Om du vill anropa en datamodelltjänst kan du antingen skapa en regel i den visuella redigeraren eller ange ett JavaScript med `guidelib.dataIntegrationUtils.executeOperation` -API:t i kodredigeraren för [regelredigeraren](/help/forms/using/rule-editor.md).

Det här dokumentet fokuserar på att skriva ett JavaScript-skript med API:t för att anropa en tjänst. `guidelib.dataIntegrationUtils.executeOperation`

## Använda API {#using-the-api}

API:t anropar `guidelib.dataIntegrationUtils.executeOperation` en tjänst inifrån ett adaptivt formulärfält. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

API:ts struktur anger `guidelib.dataIntegrationUtils.executeOperation` information om tjänståtgärden. Strukturen har följande syntax.

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
   <td>Kopplar ett eller flera formulärobjekt till utdatavärden från tjänståtgärden för att fylla i formulärfält<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Returnerar värden baserat på indataargumenten för serviceåtgärden. Det är en valfri parameter som används som en callback-funktion.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visar ett felmeddelande om återanropsfunktionen lyckas inte visa utdatavärden baserat på indataargumenten. Det är en valfri parameter som används som en callback-funktion.<br /> </td>
  </tr>
 </tbody>
</table>

## Exempelskript för att anropa en tjänst {#sample-script-to-invoke-a-service}

I följande exempelskript används API:t för att `guidelib.dataIntegrationUtils.executeOperation` anropa den `getAccountById` tjänståtgärd som konfigurerats i `employeeAccount` formulärdatamodellen.

Åtgärden tar `getAccountById` värdet i `employeeID` formulärfältet som indata för `empId` argumentet och returnerar medarbetarens namn, kontonummer och kontosaldo för motsvarande medarbetare. Utdatavärdena fylls i i de angivna formulärfälten. Värdet i `name` argumentet fylls till exempel i `fullName` formulärelementet och värdet för `accountNumber` argument i `account` formulärelementet.

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

## Använda API:t med återanropsfunktionen {#using-the-api-callback}

Du kan också anropa datamodelltjänsten för formulär med API:t med en callback-funktion `guidelib.dataIntegrationUtils.executeOperation` . API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

Återanropsfunktionen kan ha `success` - och `failure` återanropsfunktioner.

### Exempelskript med återanropsfunktioner för lyckade och misslyckade åtgärder {#callback-function-success-failure}

I följande exempelskript används API:t för att `guidelib.dataIntegrationUtils.executeOperation` anropa den `GETOrder` tjänståtgärd som konfigurerats i `employeeOrder` formulärdatamodellen.

Åtgärden tar `GETOrder` värdet i `Order ID` formulärfältet som indata för `orderId` argumentet och returnerar orderkvantitetsvärdet i `success` callback-funktionen.  Om återanropsfunktionen inte returnerar `success` ordningsantalet, visas `failure` meddelandet av återanropsfunktionen `Error occured` .

>[!NOTE]
>
> Om du använder återanropsfunktionen fylls inte utdatavärdena i de angivna formulärfälten. `success`

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
