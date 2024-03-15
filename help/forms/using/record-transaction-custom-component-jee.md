---
title: Registrera en transaktion för API:t för anpassade komponenter för AEM Forms på JEE.
description: Använd TransactionRecorder-API:t för att registrera transaktion för anpassad komponent.
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Registrera en transaktion för anpassade komponent-API:er för AEM Forms i JEE {#record-a-transaction-for-custom-components}

När du använder fakturerbara API:er i din anpassade komponent kan du aktivera transaktionsrapportering för komponenten. Om du vill aktivera transaktionsrapportering ändrar du `component.xml` komponentfilen och lägg till taggen som anges nedan under åtgärden som transaktionsrapportering måste aktiveras för.

**Tagg**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Gammal åtgärdstagg | Ny åtgärdstagg |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Om det finns ett krav på att hämta mer än en transaktion för ett API, till exempel för ett batch-API där antalet transaktioner kan variera med antalet indatamängder, måste du i de fallen hantera antalet transaktioner på API-nivå. Nedan följer de angivna stegen för att registrera antalet olika transaktioner:

1. Importera klass `"com.adobe.idp.dsc.InvocationContextStack"` i koden. Klassen ingår i `adobe-livecycle-client.jar` sdk-fil. SDK-filen är tillgänglig på `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Uppdatera klientfilen som delas ovan i ditt klientprojekt med den nya filen om den redan är paketerad.

1. I det API som varierade transaktioner måste loggas för:
   1. Lägg till logik för att lagra antalet transaktioner i vissa heltalsvariabler, som `transaction_count`.
   1. Lägg till `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Relaterade artiklar

* [Aktivera och visa transaktionsrapport för AEM Forms på JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Lista över fakturerbara API:er för AEM Forms i JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)


