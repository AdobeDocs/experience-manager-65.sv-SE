---
title: Registrera en transaktion för anpassade implementeringar
seo-title: Registrera en transaktion för anpassade implementeringar
description: Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt
seo-description: Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Registrera en transaktion för anpassade implementeringar {#record-a-transaction-for-custom-implementations}

Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt

Du kan använda en anpassad kod för att skicka ett PDF-formulär, för att skicka förhandsgransknings-URL:er för agentanvändargränssnittet till slutanvändare för att förhandsgranska en interaktiv kommunikation eller för att skicka ett formulär med anpassade metoder i stället för att använda skicka-metoder som finns i AEM Forms. Alla tidigare nämnda åtgärder och anpassade implementeringar av API:er för AEM Forms redovisas inte som transaktioner. AEM Forms innehåller ett API, [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), som används för att registrera åtgärder som transaktioner.

Om du vill spela in en transaktion skriver du [standardsäljservern](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) och anropar servertjänsten från en klient för att registrera en transaktion. Du kan anropa servleten med AJAX eller någon annan standardmetod.

## Exempel på kod på serversidan {#sample-server-sided-code}

Du kan använda exempelkoden nedan för att köra TransactionRecorder API från en JAVA-klass med ett anpassat OSGi-paket.

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

Du kan använda exempelkoden nedan för att anropa servern som har `TransactionRecorder`API:t.

```
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

* [Översikt över transaktionsrapporter](/help/forms/using/transaction-reports-overview.md)
* [Visa och förstå transaktionsrapporter](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [Fakturerbara API:er för transaktionsrapporter](/help/forms/using/transaction-reports-billable-apis.md)

