---
title: API för att anropa formulärdatamodelltjänst från anpassningsbara formulär
description: Beskriver det invokeWebServices-API som du kan använda för att anropa webbtjänster som skrivits i WSDL inifrån ett adaptivt formulärfält.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms, Foundation Components
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# API för att anropa formulärdatamodelltjänst från anpassningsbara formulär {#api-to-invoke-form-data-model-service-from-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

## Ökning {#overview}

Med AEM Forms kan formulärförfattare ytterligare förenkla och förbättra ifyllandet av formulär genom att anropa tjänster som konfigurerats i en formulärdatamodell inifrån ett adaptivt formulärfält. Om du vill anropa en datamodelltjänst kan du antingen skapa en regel i den visuella redigeraren eller ange ett JavaScript med `guidelib.dataIntegrationUtils.executeOperation` API i kodredigeraren för [regelredigerare](/help/forms/using/rule-editor.md).

Det här dokumentet fokuserar på att skriva ett JavaScript med `guidelib.dataIntegrationUtils.executeOperation` API för att anropa en tjänst.

## Använda API {#using-the-api}

The `guidelib.dataIntegrationUtils.executeOperation` API anropar en tjänst inifrån ett adaptivt formulärfält. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

Strukturen för `guidelib.dataIntegrationUtils.executeOperation` API anger information om tjänståtgärden. Strukturen har följande syntax.

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

Följande exempelskript använder `guidelib.dataIntegrationUtils.executeOperation` API för att anropa `getAccountById` tjänståtgärd konfigurerad i `employeeAccount` formulärdatamodell.

The `getAccountById` operationen tar värdet i `employeeID` formulärfält som indata för `empId` argument och returnerar medarbetarens namn, kontonummer och kontosaldo för motsvarande medarbetare. Utdatavärdena fylls i i de angivna formulärfälten. Värdet i `name` argumentet har fyllts i i `fullName` formulärelement och värde för `accountNumber` argument i `account` formulärelement.

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

Du kan också anropa datamodelltjänsten för formulär med `guidelib.dataIntegrationUtils.executeOperation` API med en återanropsfunktion. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

Återanropsfunktionen kan ha `success` och `failure` callback-funktioner.

### Exempelskript med återanropsfunktioner för lyckade och misslyckade åtgärder {#callback-function-success-failure}

Följande exempelskript använder `guidelib.dataIntegrationUtils.executeOperation` API för att anropa `GETOrder` tjänståtgärd konfigurerad i `employeeOrder` formulärdatamodell.

The `GETOrder` operationen tar värdet i `Order ID` formulärfält som indata för `orderId` argument och returnerar orderkvantitetsvärdet i `success` callback-funktion.  Om `success` callback-funktionen returnerar inte orderkvantiteten, `failure` callback-funktionen visar `Error occured` meddelande.

>[!NOTE]
>
>Om du använder `success` callback-funktionen, utdatavärdena fylls inte i i de angivna formulärfälten.

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
