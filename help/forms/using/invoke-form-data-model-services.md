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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# API för att anropa formulärdatamodelltjänst från anpassningsbara formulär {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Översikt {#overview}

Med AEM Forms kan formulärförfattare ytterligare förenkla och förbättra ifyllandet genom att anropa tjänster som konfigurerats i en formulärdatamodell inifrån ett adaptivt formulärfält. Om du vill anropa en datamodelltjänst kan du antingen skapa en regel i den visuella redigeraren eller ange ett JavaScript med `guidelib.dataIntegrationUtils.executeOperation` -API:t i kodredigeraren för [regelredigeraren](/help/forms/using/rule-editor.md).

Det här dokumentet fokuserar på att skriva ett JavaScript-skript med API:t för att anropa en tjänst. `guidelib.dataIntegrationUtils.executeOperation`

## Använda API {#using-the-api}

API:t anropar `guidelib.dataIntegrationUtils.executeOperation` en tjänst inifrån ett adaptivt formulärfält. API-syntaxen är följande:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

API kräver följande parametrar.

| Parameter | Beskrivning |
|---|---|
| `operationInfo` | Struktur för att ange identifierare för formulärdatamodell, åtgärdstitel och åtgärdsnamn |
| `inputs` | Struktur för att ange formulärobjekt vars värden är indata till serviceåtgärden |
| `outputs` | Struktur för att ange formulärobjekt som ska fyllas med värden som returneras av tjänståtgärden |

API:ts struktur anger `guidelib.dataIntegrationUtils.executeOperation` information om tjänståtgärden. Strukturen har följande syntax.

```
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
   <td><code>forDataModelId</code></td>
   <td>Ange databassökvägen till formulärdatamodellen inklusive dess namn</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Ange namnet på den tjänståtgärd som ska köras</td>
  </tr>
  <tr>
   <td><code>input</code></td>
   <td>Mappa ett eller flera formulärobjekt till indataargumenten för serviceåtgärden</td>
  </tr>
  <tr>
   <td>Utdata</td>
   <td>Mappa ett eller flera formulärobjekt till utdatavärden från tjänståtgärden för att fylla i formulärfält<br /> </td>
  </tr>
 </tbody>
</table>

## Exempelskript för att anropa en tjänst {#sample-script-to-invoke-a-service}

I följande exempelskript används API:t för att `guidelib.dataIntegrationUtils.executeOperation` anropa den `getAccountById` tjänståtgärd som konfigurerats i `employeeAccount` formulärdatamodellen.

Åtgärden tar `getAccountById` värdet i `employeeID` formulärfältet som indata för `empId` argumentet och returnerar medarbetarens namn, kontonummer och kontosaldo för motsvarande medarbetare. Utdatavärdena fylls i i de angivna formulärfälten. Värdet i `name` argumentet fylls till exempel i `fullName` formulärelementet och värdet för `accountNumber` argument i `account` formulärelementet.

```
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

