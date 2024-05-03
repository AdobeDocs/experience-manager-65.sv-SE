---
title: Registrera en transaktion för API:t för anpassade komponenter för AEM Forms på JEE.
description: Lär dig hur du använder TransactionRecorder API för att registrera transaktioner för en anpassad komponent.
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Registrera en transaktion för anpassade komponent-API:er för AEM Forms i JEE {#record-a-transaction-for-custom-components}

När du använder fakturerbara API:er i din anpassade komponent kan du aktivera transaktionsrapportering för komponenten. Om du vill aktivera transaktionsrapportering ändrar du `component.xml` komponentfilen och lägg till taggen som anges nedan under åtgärden som transaktionsrapportering måste aktiveras för.

**Tagg**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Gammal åtgärdstagg | Ny åtgärdstagg |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Om du måste hämta mer än en transaktion för ett API, till exempel ett batch-API där antalet transaktioner varierar beroende på antalet indata, hanterar du antalet transaktioner på API-nivå.

**Så här registrerar du antalet varierade transaktioner:**

1. Importera klass `"com.adobe.idp.dsc.InvocationContextStack"` i koden. Klassen ingår i `adobe-livecycle-client.jar` sdk-fil. SDK-filen är tillgänglig på `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Uppdatera klientfilen som delas ovan i ditt klientprojekt med den nya filen om den redan är paketerad.

1. I det API som varierade transaktioner måste loggas för:
   1. Lägg till logik så att du kan lagra antalet transaktioner i vissa heltalsvariabler, som `transaction_count`.
   1. Lägg till `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Relaterade artiklar

* [Aktivera och visa transaktionsrapporter för AEM Forms i JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Lista över fakturerbara API:er för AEM Forms i JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)
