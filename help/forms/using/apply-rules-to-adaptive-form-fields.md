---
title: '"PUBLICERA INTE självstudiekurs: Använd regler för anpassningsbara formulärfält"'
seo-title: Tillämpa regler på anpassningsbara formulärfält
description: Skapa regler för att lägga till interaktivitet, affärslogik och smarta valideringar i ett anpassat formulär.
seo-description: Skapa regler för att lägga till interaktivitet, affärslogik och smarta valideringar i ett anpassat formulär.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: e3ecf724cdfcd20ef4c089605e644ad10ef1221b
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---


# Självstudiekurs: Använd regler för anpassningsbara formulärfält {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Den här självstudiekursen är ett steg i [Skapa ditt första adaptiva formulär](/help/forms/using/create-your-first-adaptive-form.md)-serien. Adobe rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet med självstudiekurser.

## Om självstudiekursen {#about-the-tutorial}

Du kan använda regler för att lägga till interaktivitet, affärslogik och smarta valideringar i ett anpassat formulär. Anpassningsbara formulär har en inbyggd regelredigerare. Regelredigeraren har en dra och släpp-funktion som liknar guidade rundturer. Metoden dra och släpp är den snabbaste och enklaste metoden att skapa regler. Regelredigeraren innehåller också ett kodfönster för användare som vill testa sina kodningskunskaper eller ta reglerna till nästa nivå.

Mer information om regelredigeraren finns i [Anpassad regelredigerare för Forms](/help/forms/using/rule-editor.md).

I slutet av självstudiekursen kommer du att lära dig att skapa regler för att:

* Anropa en formulärdatamodelltjänst för att hämta data från databasen
* Anropa en tjänst för formulärdatamodell för att lägga till data i databasen
* Kör en valideringskontroll och visa felmeddelanden

Med interaktiva GIF-bilder i slutet av varje avsnitt i självstudiekursen lär du dig och validerar snabbt funktionaliteten i det formulär du bygger.

## Steg 1: Hämta en kundpost från databasen {#retrieve-customer-record}

Du skapade en formulärdatamodell genom att följa artikeln [skapa formulärdatamodell](/help/forms/using/create-form-data-model.md). Nu kan du använda regelredigeraren för att anropa Forms datamodelltjänster för att hämta och lägga till information i databasen.

Varje kund tilldelas ett unikt Kund-ID-nummer som hjälper till att identifiera relevanta kunddata i en databas. I proceduren nedan används Kund-ID för att hämta information från databasen:

1. Öppna det adaptiva formuläret för redigering.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Tryck på fältet **[!UICONTROL Customer ID]** och tryck på ikonen **[!UICONTROL Edit Rules]**. Regelredigeraren öppnas.
1. Tryck på ikonen **[!UICONTROL + Create]** för att lägga till en regel. Den öppnar Visual Editor.

   Programsatsen **[!UICONTROL WHEN]** är markerad som standard i Visual Editor. Formulärobjektet (i det här fallet **[!UICONTROL Customer ID]**) från vilket du startade regelredigeraren anges i **[!UICONTROL WHEN]**-satsen.

1. Tryck på listrutan **[!UICONTROL Select State]** och välj **[!UICONTROL is changed]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. I **[!UICONTROL THEN]**-satsen väljer du **[!UICONTROL Invoke Service]** i listrutan **[!UICONTROL Select Action]**.
1. Välj tjänsten **[!UICONTROL Retrieve Shipping Address]** i listrutan **[!UICONTROL Select]**.
1. Dra och släpp fältet **[!UICONTROL Customer ID]** från fliken Formulärobjekt till fältet **[!UICONTROL Drop object or select here]** i rutan **[!UICONTROL INPUT]**.

   ![dropobjectToInputField-retriedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Dra och släpp fältet **[!UICONTROL Customer ID, Name, Shipping Address, State, and Zip Code]** från fliken Formulärobjekt till fältet **[!UICONTROL Drop object or select here]** i rutan **[!UICONTROL OUTPUT]**.

   ![dropobjectstoOutputField-retriedata](assets/dropobjectstooutputfield-retrievedata.png)

   Tryck på **[!UICONTROL Done]** för att spara regeln. Tryck på **[!UICONTROL Close]** i regelredigeringsfönstret.

1. Förhandsgranska det adaptiva formuläret. Ange ett ID i fältet **[!UICONTROL Customer ID]**. Formuläret kan nu hämta kundinformation från databasen.

   ![hämtningsinformation](assets/retrieve-information.gif)

## Steg 2: Lägg till den uppdaterade kundadressen i databasen {#updated-customer-address}

När kundinformationen har hämtats från databasen kan du uppdatera leveransadress, leveransstatus och postnummer. Proceduren nedan anropar en Form Data Model-tjänst för att uppdatera kundinformationen till databasen:

1. Markera fältet **[!UICONTROL Submit]** och tryck på ikonen **[!UICONTROL Edit Rules]**. Regelredigeraren öppnas.
1. Välj regeln **[!UICONTROL Submit - Click]** och tryck på ikonen **[!UICONTROL Edit]**. Alternativen för att redigera regeln Skicka visas.

   ![submit-rule](assets/submit-rule.png)

   I alternativet WHEN är alternativen **[!UICONTROL Submit]** och **[!UICONTROL is clicked]** redan markerade.

   ![skicka-i-klickning](assets/submit-is-clicked.png)

1. Tryck på alternativet **[!UICONTROL + Add Statement]** i **[!UICONTROL THEN]**-alternativet. Välj **[!UICONTROL Invoke Service]** i listrutan **[!UICONTROL Select Action]**.
1. Välj tjänsten **[!UICONTROL Update Shipping Address]** i listrutan **[!UICONTROL Select]**.

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectToInputField-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Dra och släpp fältet **[!UICONTROL Shipping Address, State, and Zip Code]** från fliken [!UICONTROL Form Objects] till motsvarande tabellnamnsegenskap (till exempel kundinformation .shippingAddress) för fältet **[!UICONTROL Drop object or select here]** i rutan **[!UICONTROL INPUT]**. Alla fält med tabellnamn som prefix (t.ex. kundinformation i det här fallet) fungerar som indata för uppdateringstjänsten. Allt innehåll i dessa fält uppdateras i datakällan.

   >[!NOTE]
   >
   >Dra och släpp inte fälten **[!UICONTROL Name]** och **[!UICONTROL Customer ID]** till motsvarande tabellename.property (t.ex. customerdetails.name). Det hjälper till att undvika att uppdatera kundens namn och ID av misstag.

1. Dra och släpp fältet **[!UICONTROL Customer ID]** från fliken [!UICONTROL Form Objects] till id-fältet i rutan **[!UICONTROL INPUT]**. Fält utan ett prefix-tabellnamn (t.ex. kundinformation i det här fallet) fungerar som sökparametrar för uppdateringstjänsten. Fältet **[!UICONTROL id]** i det här användningsfallet identifierar en post i tabellen **kundinformation**.
1. Tryck på **[!UICONTROL Done]** för att spara regeln. Tryck på **[!UICONTROL Close]** i regelredigeringsfönstret.
1. Förhandsgranska det adaptiva formuläret. Hämta information om en kund, uppdatera leveransadressen och skicka in formuläret. När du hämtar information om samma kund igen visas den uppdaterade leveransadressen.

## Steg 3: (Bonusavsnitt) Använd kodredigeraren för att köra valideringar och visa felmeddelanden {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Du bör köra valideringen i formuläret för att säkerställa att de data som anges i formuläret är korrekta och att ett felmeddelande visas om felaktiga data saknas. Om t.ex. ett icke-befintligt kund-ID anges i formuläret, ska ett felmeddelande visas.

Adaptiva formulär innehåller flera komponenter med inbyggda valideringar, till exempel e-post och numeriska fält som du kan använda för vanliga användningsområden. Använd regelredigeraren för avancerad användning, till exempel för att visa ett felmeddelande när databasen returnerar noll (0) poster (inga poster).

Följande procedur visar hur du skapar en regel som visar ett felmeddelande om det kund-ID som anges i formuläret inte finns i databasen. Regeln ger även fokus till och återställer fältet **[!UICONTROL Customer ID]**. Regeln använder [API:t dataIntegrationUtils för formulärdatamodelltjänsten](/help/forms/using/invoke-form-data-model-services.md) för att kontrollera om det finns ett kund-ID i databasen.

1. Tryck på fältet **[!UICONTROL Customer ID]** och tryck på ikonen `Edit Rules`. Fönstret [!UICONTROL Rule Editor] öppnas.
1. Tryck på ikonen **[!UICONTROL + Create]** för att lägga till en regel. Den öppnar Visual Editor.

   Programsatsen **[!UICONTROL WHEN]** är markerad som standard i Visual Editor. Formulärobjektet (i det här fallet **[!UICONTROL Customer ID]**) från vilket du startade regelredigeraren anges i **[!UICONTROL WHEN]**-satsen.

1. Tryck på listrutan **[!UICONTROL Select State]** och välj **[!UICONTROL is changed]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   I **[!UICONTROL THEN]**-satsen väljer du **[!UICONTROL Invoke Service]** i listrutan **[!UICONTROL Select Action]**.

1. Växla från **[!UICONTROL Visual Editor]** till **[!UICONTROL Code Editor]**. Växelkontrollen finns till höger i fönstret. Kodredigeraren öppnas och visar kod som liknar följande:

   ![kodredigerare](assets/code-editor.png)

1. Ersätt indatavariabelavsnittet med följande kod:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Ersätt `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)`-avsnittet med följande kod:

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

