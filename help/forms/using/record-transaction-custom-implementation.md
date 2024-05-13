---
title: Registrera en transaktion för anpassade implementeringar
description: Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
feature: Transaction Reports
exl-id: b0c4f72a-e65f-453a-af66-5d9f98a9d6df
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: acb023caf0a7e64fea9cf5d9198d672ee14c8d88
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Registrera en transaktion för anpassade implementeringar för AEM Forms på OSGi {#record-a-transaction-for-custom-implementations}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/record-transaction-custom-implementation) |
| AEM 6.5 | Den här artikeln |

Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt

Du kan använda anpassad kod för att skicka ett PDF-formulär eller för att skicka förhandsgransknings-URL:er till agentanvändargränssnittet till slutanvändare för att förhandsgranska en interaktiv kommunikation. Eller så skickar du ett formulär med egna metoder i stället för att använda de skicka-metoder som finns i AEM Forms. Alla tidigare nämnda åtgärder och anpassade implementeringar av AEM Forms API:er räknas inte som transaktioner. AEM Forms tillhandahåller ett API, [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), för att registrera sådana åtgärder som transaktioner.

Om du vill registrera en transaktion skriver du [standardsäljare](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) och anropa en klientserver för att registrera en transaktion. Du kan anropa servleten med AJAX eller någon annan standardmetod.

## Exempel på kod på serversidan {#sample-server-sided-code}

Du kan använda exempelkoden nedan för att köra TransactionRecorder API från en Java™-klass med ett anpassat OSGi-paket.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Exempel på kod på klientsidan {#sample-client-side-code}

Du kan använda exempelkoden nedan för att anropa den server som har `TransactionRecorder`API.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Relaterade artiklar {#related-articles}

* [Översikt över transaktionsrapporter för AEM Forms på OSGi](/help/forms/using/transaction-reports-overview.md)
* [Visa och förstå transaktionsrapporter för AEM Forms i OSGi](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [Transaction Reports Billable APIs for AEM Forms on OSGi](/help/forms/using/transaction-reports-billable-apis.md)
