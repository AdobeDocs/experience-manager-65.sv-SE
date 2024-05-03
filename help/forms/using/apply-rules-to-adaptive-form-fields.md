---
title: Tillämpa regler på anpassningsbara formulärfält
description: Skapa regler för att lägga till interaktivitet, affärslogik och smarta valideringar i ett anpassat formulär.
page-status-flag: de-activated
products: SG_EXPERIENCEMANAGER/6.3/FORMS
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# Självstudiekurs: Använda regler i anpassade formulärfält {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Den här självstudiekursen är ett steg i [Skapa ditt första adaptiva formulär](/help/forms/using/create-your-first-adaptive-form.md) serie. Adobe rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet med självstudiekurser.

## Om självstudiekursen {#about-the-tutorial}

Du kan använda regler för att lägga till interaktivitet, affärslogik och smarta valideringar i ett anpassat formulär. Anpassningsbara formulär har en inbyggd regelredigerare. Regelredigeraren har en dra och släpp-funktion som liknar guidade rundturer. Metoden dra och släpp är den snabbaste och enklaste metoden att skapa regler. Regelredigeraren innehåller också ett kodfönster för användare som vill testa sina kodningskunskaper eller ta reglerna till nästa nivå.

Du kan läsa mer om regelredigeraren på [Anpassad regelredigerare för Forms](/help/forms/using/rule-editor.md).

I slutet av självstudiekursen kommer du att lära dig att skapa regler för att:

* Anropa en formulärdatamodelltjänst för att hämta data från databasen
* Anropa en tjänst för formulärdatamodell för att lägga till data i databasen
* Kör en valideringskontroll och visa felmeddelanden

Med hjälp av interaktiva GIF-bilder i slutet av varje avsnitt i självstudiekursen kan du snabbt lära dig och validera funktionaliteten i det formulär du bygger.

## Steg 1: Hämta en kundpost från databasen {#retrieve-customer-record}

Du skapade en formulärdatamodell genom att följa följande [skapa formulärdatamodell](/help/forms/using/create-form-data-model.md) artikel. Nu kan du använda regelredigeraren för att anropa Forms datamodelltjänster för att hämta och lägga till information i databasen.

Varje kund tilldelas ett unikt Kund-ID-nummer som hjälper till att identifiera relevanta kunddata i en databas. I proceduren nedan används Kund-ID för att hämta information från databasen:

1. Öppna det adaptiva formuläret för redigering.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Välj **[!UICONTROL Customer ID]** och välj **[!UICONTROL Edit Rules]** -ikon. Regelredigeraren öppnas.
1. Välj **[!UICONTROL + Create]** om du vill lägga till en regel. Den öppnar Visual Editor.

   I den visuella redigeraren **[!UICONTROL WHEN]** -programsatsen är markerad som standard. Formulärobjektet (i det här fallet **[!UICONTROL Customer ID]**) från vilken du startade regelredigeraren anges i **[!UICONTROL WHEN]** -programsats.

1. Välj **[!UICONTROL Select State]** nedrullningsbar meny och välj **[!UICONTROL is changed]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. I **[!UICONTROL THEN]** programsats, välj **[!UICONTROL Invoke Service]** från **[!UICONTROL Select Action]** nedrullningsbar meny.
1. Välj **[!UICONTROL Retrieve Shipping Address]** från **[!UICONTROL Select]** nedrullningsbar meny.
1. Dra och släpp **[!UICONTROL Customer ID]** från fliken Formulärobjekt till **[!UICONTROL Drop object or select here]** fältet i **[!UICONTROL INPUT]** box.

   ![dropobjectToInputField-retriedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Dra och släpp **[!UICONTROL Customer ID, Name, Shipping Address, State, and Zip Code]** från fliken Formulärobjekt till **[!UICONTROL Drop object or select here]** fältet i **[!UICONTROL OUTPUT]** box.

   ![dropobjectstoOutputField-retriedata](assets/dropobjectstooutputfield-retrievedata.png)

   Välj **[!UICONTROL Done]** för att spara regeln. I regelredigeringsfönstret väljer du **[!UICONTROL Close]**.

1. Förhandsgranska det adaptiva formuläret. Ange ett ID i dialogrutan **[!UICONTROL Customer ID]** fält. Formuläret kan nu hämta kundinformation från databasen.

   ![hämtningsinformation](assets/retrieve-information.gif)

## Steg 2: Lägg till den uppdaterade kundadressen i databasen {#updated-customer-address}

När kundinformationen har hämtats från databasen kan du uppdatera leveransadress, leveransstatus och postnummer. Proceduren nedan anropar en Form Data Model-tjänst för att uppdatera kundinformationen till databasen:

1. Välj **[!UICONTROL Submit]** och välj **[!UICONTROL Edit Rules]** -ikon. Regelredigeraren öppnas.
1. Välj **[!UICONTROL Submit - Click]** och välj **[!UICONTROL Edit]** -ikon. Alternativen för att redigera regeln Skicka visas.

   ![submit-rule](assets/submit-rule.png)

   I alternativet WHEN **[!UICONTROL Submit]** och **[!UICONTROL is clicked]** har redan valts.

   ![skicka-i-klickning](assets/submit-is-clicked.png)

1. I **[!UICONTROL THEN]** väljer du **[!UICONTROL + Add Statement]** alternativ. Välj **[!UICONTROL Invoke Service]** från **[!UICONTROL Select Action]** nedrullningsbar meny.
1. Välj **[!UICONTROL Update Shipping Address]** från **[!UICONTROL Select]** nedrullningsbar meny.

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectToInputField-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Dra och släpp **[!UICONTROL Shipping Address, State, and Zip Code]** fält från [!UICONTROL Form Objects] till motsvarande tabellnamn (t.ex. kundinformation.shippingAddress) för **[!UICONTROL Drop object or select here]** fältet i **[!UICONTROL INPUT]** box. Alla fält med tabellnamn som prefix (t.ex. kundinformation i det här fallet) fungerar som indata för uppdateringstjänsten. Allt innehåll i dessa fält uppdateras i datakällan.

   >[!NOTE]
   >
   >Dra och släpp inte **[!UICONTROL Name]** och **[!UICONTROL Customer ID]** fält till motsvarande tabellename.property (till exempel customerdetails.name). Det hjälper till att undvika att uppdatera kundens namn och ID av misstag.

1. Dra och släpp **[!UICONTROL Customer ID]** fält från [!UICONTROL Form Objects] till ID-fältet i **[!UICONTROL INPUT]** box. Fält utan ett prefix-tabellnamn (t.ex. kundinformation i det här fallet) fungerar som sökparametrar för uppdateringstjänsten. The **[!UICONTROL id]** i det här användningsfallet identifierar en post unikt i  **kundinformation**  tabell.
1. Välj **[!UICONTROL Done]** för att spara regeln. I regelredigeringsfönstret väljer du **[!UICONTROL Close]**.
1. Förhandsgranska det adaptiva formuläret. Hämta information om en kund, uppdatera leveransadressen och skicka in formuläret. När du hämtar information om samma kund igen visas den uppdaterade leveransadressen.

## Steg 3: (Bonusavsnitt) Använd kodredigeraren för att köra valideringar och visa felmeddelanden {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Du bör köra valideringen i formuläret för att säkerställa att de data som anges i formuläret är korrekta och att ett felmeddelande visas om felaktiga data finns. Om t.ex. ett icke-befintligt kund-ID anges i formuläret, ska ett felmeddelande visas.

Adaptiva formulär innehåller flera komponenter med inbyggda valideringar, till exempel e-post och numeriska fält som du kan använda för vanliga användningsområden. Använd regelredigeraren för avancerad användning, till exempel för att visa ett felmeddelande när databasen returnerar noll (0) poster (inga poster).

Följande procedur visar hur du skapar en regel som visar ett felmeddelande om det kund-ID som anges i formuläret inte finns i databasen. Regeln fokuserar också på och återställer **[!UICONTROL Customer ID]** fält. Regeln använder [API:t dataIntegrationUtils för formulärdatamodelltjänsten](/help/forms/using/invoke-form-data-model-services.md) för att kontrollera om det finns ett kund-ID i databasen.

1. Välj **[!UICONTROL Customer ID]** och välj `Edit Rules` -ikon. The [!UICONTROL Rule Editor] öppnas.
1. Välj **[!UICONTROL + Create]** om du vill lägga till en regel. Den öppnar Visual Editor.

   I den visuella redigeraren **[!UICONTROL WHEN]** -programsatsen är markerad som standard. Formulärobjektet (i det här fallet **[!UICONTROL Customer ID]**) från vilken du startade regelredigeraren anges i **[!UICONTROL WHEN]** -programsats.

1. Välj **[!UICONTROL Select State]** nedrullningsbar meny och välj **[!UICONTROL is changed]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   I **[!UICONTROL THEN]** programsats, välj **[!UICONTROL Invoke Service]** från **[!UICONTROL Select Action]** nedrullningsbar meny.

1. Växla från **[!UICONTROL Visual Editor]** till **[!UICONTROL Code Editor]**. Växelkontrollen finns till höger i fönstret. Kodredigeraren öppnas och visar kod som liknar följande:

   ![kodredigerare](assets/code-editor.png)

1. Ersätt indatavariabelavsnittet med följande kod:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Ersätt `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` med följande kod:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. Förhandsgranska det adaptiva formuläret. Ange ett felaktigt kund-ID. Ett felmeddelande visas.

   ![display-validation-error](assets/display-validation-error.gif)
