---
title: '''Självstudiekurs: Skapa ett anpassat formulär'
seo-title: Create an adaptive form
description: Lär dig skapa, layouta och förhandsgranska ett anpassat formulär. Lär dig även att konfigurera skicka-åtgärder.
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# Självstudiekurs: Skapa ett anpassat formulär {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Den här självstudiekursen är ett steg i [Skapa ditt första adaptiva formulär](/help/forms/using/create-your-first-adaptive-form.md) serie. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

## Om självstudiekursen {#about-the-tutorial}

Adaptiva formulär är nya generationer som är dynamiska och responsiva. Ni kan använda adaptiva formulär för att leverera personaliserade upplevelser. Du kan även integrera adaptiva formulär med [!DNL Adobe Analytics] för användningsstatistik och [!DNL Adobe Campaign] för kampanjhantering. Mer information om funktioner för adaptiva formulär finns i [Introduktion till utveckling av anpassningsbara formulär](/help/forms/using/introduction-forms-authoring.md).

Det är enklare att skapa och hantera formulär när man följer en lämplig process. I den här artikeln får du lära dig att:

* [Skapa ett anpassningsbart formulär där kunden kan lägga till en leveransadress](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Layoutfält i ett anpassat formulär som visar och accepterar information från en kund](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Skapa en Skicka-åtgärd för att skicka ett e-postmeddelande med formulärinnehåll](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Förhandsgranska och skicka ett anpassat formulär](/help/forms/using/create-adaptive-form.md)

Du kommer att ha ett formulär som liknar följande i slutet av artikeln:\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Steg 1: Skapa det anpassade formuläret {#step-create-the-adaptive-form}

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**. Standardwebbadressen är [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Tryck **[!UICONTROL Create]** och markera **[!UICONTROL Adaptive Form]**. Ett alternativ för att välja en mall visas. Tryck på **[!UICONTROL Blank]** mall för att markera den och trycka på **[!UICONTROL Next]**.

1. Ett alternativ till **[!UICONTROL Add Properties]** visas. The **[!UICONTROL Title]** och **[!UICONTROL Name]** fält är obligatoriska:

   * **Titel:** Ange `Add new or update shipping address` i **[!UICONTROL Title]** fält. Titelfältet anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i AEM [!DNL Forms] användargränssnitt.
   * **Namn:** Ange `shipping-address-add-update-form` i **[!UICONTROL Name]** fält. Fältet Namn anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.

1. Tryck på **[!UICONTROL Create]**. Ett anpassat formulär skapas och en dialogruta öppnas där du kan öppna formuläret för redigering. Tryck **[!UICONTROL Open]** om du vill öppna det nya formuläret på en ny flik. Formuläret öppnas för redigering. Här visas också sidlisten där du kan anpassa det nya formuläret efter behov.

   Mer information om gränssnittet för att skapa adaptiva formulär och tillgängliga komponenter finns i [Introduktion till utveckling av anpassningsbara formulär](/help/forms/using/creating-adaptive-form.md).

   ![nyskapad-adaptiv form](assets/newly-created-adaptive-form.png)

## Steg 2: Lägg till sidhuvud och sidfot {#step-add-header-and-footer}

AEM [!DNL Forms] innehåller många komponenter som visar information i ett adaptivt formulär. Komponenterna för sidhuvud och sidfot ger formuläret ett enhetligt utseende och en enhetlig känsla. En rubrik innehåller vanligtvis ett företags logotyp, formulärets rubrik och sammanfattning. En sidfot innehåller vanligtvis copyrightinformation och länkar till andra sidor.

1. Tryck ![växlingspanel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Komponentwebbläsaren öppnas. Dra **[!UICONTROL Header]** från komponentwebbläsaren till det adaptiva formuläret.
1. Tryck på **[!UICONTROL Logo]**. Verktygsfältet visas. Tryck ![aem_6_3_edit](assets/aem_6_3_edit.png) i verktygsfältet skriver du **Vi.butik** och trycka ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Tryck på Bild. Verktygsfältet visas. Tryck ![cmppr](assets/cmppr.png). Egenskapsläsaren öppnas till vänster på skärmen. **[!UICONTROL Browse]** och ladda upp logotypbilden. Tryck ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Bilden visas i sidhuvudet.

   Du kan trycka på Hämta fil för att hämta logotypen som används i den här artikeln om du inte har någon.

[Hämta fil](assets/logo.png)

1. Dra **[!UICONTROL Footer]** komponent från ![treeexpandall](assets/treeexpandall.png) till den anpassningsbara formen. I det här skedet ser formuläret ut så här:

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## Steg 3: Lägga till komponenter för att hämta och visa information {#step-add-components-to-capture-and-display-information}

Komponenter är byggstenar i en adaptiv form. AEM [!DNL Forms] innehåller många komponenter för att samla in och visa information i en adaptiv form. Du kan dra komponenterna från ![treeexpandall](assets/treeexpandall.png) till ett formulär. Mer information om tillgängliga komponenter och motsvarande funktioner finns i [Introduktion till utveckling av anpassningsbara formulär](/help/forms/using/introduction-forms-authoring.md).

1. Dra **[!UICONTROL Numeric Box component]** till den anpassningsbara formen. Placera den före sidfotskomponenten. Öppna komponentens egenskaper, ändra **[!UICONTROL Title]** för komponenten till **`Customer ID`**, ändra **[!UICONTROL Element Name]** till **`customer_ID`**, aktivera **[!UICONTROL Required Field]** alternativ, aktivera **[!UICONTROL Use HTML5 Number Input Type]** och tryck ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Dra tre textrutekomponenter till det adaptiva formuläret. Placera dessa före sidfotskomponenten. Ange följande egenskaper för dessa textrutor.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Egenskap</b></td> 
      <td><b>Textruta 1<br/></b></td> 
      <td><b>Textruta 2<br/></b></td> 
      <td><b>Textruta 3</b></td> 
     </tr> 
     <tr> 
      <td>Titel</td> 
      <td>Namn<br /> </td> 
      <td>Leveransadress</td> 
      <td>Läge</td> 
     </tr> 
     <tr> 
      <td>Elementnamn</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>Obligatoriskt fält</td> 
      <td>Aktiverad</td> 
      <td>Aktiverad</td> 
      <td>Aktiverad</td> 
     </tr> 
     <tr> 
      <td>Tillåt flera rader<br /> </td> 
      <td>Handikappade</td> 
      <td>Aktiverad</td> 
      <td>Handikappade</td> 
     </tr> 
    </tbody> 
   </table>

1. Dra en **[!UICONTROL Numeric Box]** före sidfotskomponenten. Öppna komponentens egenskaper, ange värden i tabellen nedan, tryck ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | Titel | Postnummer |
   | Elementnamn | customer_ZIPCode |
   | Maximalt antal siffror | 6 |
   | Obligatoriskt fält | Aktiverad |
   | Visa mönstertyp | Inget mönster |

1. Dra en **[!UICONTROL Email]** före sidfotskomponenten. Öppna komponentens egenskaper, ange värden i tabellen nedan och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |---|---|
   | Titel | E-post |
   | Elementnamn | customer_Email |
   | Obligatoriskt fält | Aktiverad |

1. Dra en **[!UICONTROL File Attachment]** före sidfotskomponenten. Öppna komponentens egenskaper, ange värden i tabellen nedan och tryck på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Egenskap</b></td> 
      <td><b>Värde</b></td> 
     </tr> 
     <tr> 
      <td>Titel</td> 
      <td>Myndighetens adressbevis har godkänts<br /> </td> 
     </tr> 
     <tr> 
      <td>Elementnamn</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>Obligatoriskt fält</td> 
      <td>Aktiverad</td> 
     </tr> 
    </tbody> 
   </table>

1. Dra en **[!UICONTROL Submit Button]** till det adaptiva formuläret. Placera den före sidfotskomponenten. Öppna komponentens egenskaper, ändra elementnamn till `address_addition_update_submit`, trycka ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Formulärets layout är fullständig och formuläret ser ut så här:

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## Steg 4: Konfigurera skicka-åtgärd för anpassat formulär {#step-configure-submit-action-for-the-adaptive-form}

En skicka-åtgärd aktiveras när en användare trycker på Skicka-knappen på ett anpassat formulär. Du kan använda en skicka-åtgärd för att spara formulärdata i den lokala databasen, skicka formulärdata till en REST-slutpunkt, skicka formulärdata som e-post med mera. Adaptiva formulär innehåller några fler färdiga åtgärder för att skicka. Mer information finns i [Konfigurera åtgärden Skicka](/help/forms/using/configuring-submit-actions.md).

Med hjälp av följande steg kan du konfigurera e-poståtgärd för att skicka och demo för formuläret:

1. Konfigurera e-postservern. Mer information finns i [Konfigurerar e-postmeddelande](/help/sites-administering/notification.md).


1. Tryck **[!UICONTROL Form Container]** i innehållsläsaren och tryck på ![cmppr](assets/cmppr.png). Egenskapsläsaren öppnas till vänster.
1. Gå till **[!UICONTROL Submission]** >  **[!UICONTROL Submit Action]**. Välj **[!UICONTROL Send Email]**. Ange följande värden och tryck ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Egenskap | Värde |
   |--- |--- |
   | Från | `donotreply@weretail.com` |
   | Till | `${customer_Email}` |
   | Ämne | Bekräftelse: Du har lagt till leveransadress på webbplatsen We.Retail. |
   | E-postmall | Hej `${customer_Name}`, läggs följande adress till som leveransadress för ditt konto: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Med vänlig hälsning, vi.detaljhandel |
   | Inkludera bilagor | Aktiverad |

   Formuläret är klart. Nu kan du förhandsgranska formuläret och testa funktionen. Om du har använt namnet som nämns i självstudiekursen och har åtkomst till formuläret på den dator där AEM körs [!DNL Forms] server, finns formuläret tillgängligt på [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Steg 5: Förhandsgranska och skicka det anpassade formuläret {#step-preview-and-submit-the-adaptive-form}

Du kan använda **[!UICONTROL Preview option]** för att utvärdera ett formulärs utseende och beteende. Du kan skicka ett formulär i förhandsgranskningsläge och även kontrollera valideringar som används i ett formulär. Om till exempel ett fel visas när ett obligatoriskt fält lämnas tomt.

Med adaptiva formulär kan du också emulera upplevelsen av ett formulär för olika enheter. Exempel: iPhone, iPad och Desktop. Du kan använda båda **[!UICONTROL Preview]** och **[!UICONTROL Emulator]** ![linjal](assets/ruler.png) tillsammans med varandra för att förhandsgranska ett formulär för enheter med olika skärmstorlekar.

1. Tryck på **[!UICONTROL Preview]** till höger om formulärredigeraren. Formuläret öppnas i förhandsgranskningsläget. Om du har använt namnet som anges i självstudiekursen är URL:en för förhandsgranskning av formuläret [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Använd ![linjal](assets/ruler.png) för att visa hur formuläret ser ut på olika enheter.
1. Fyll i formulärfält och tryck **[!UICONTROL Submit]**. Formuläret skickas och du omdirigeras till standardinställningarna **Tack** sida. Du kan också ange en anpassad tacksida. Mer information finns i [Konfigurerar omdirigeringssida](/help/forms/using/configuring-redirect-page.md).

Det adaptiva formuläret för att lägga till en adress är klart. Om du har använt det namn som anges i självstudiekursen och har åtkomst till formuläret på den dator där AEM Forms-servern körs, finns formuläret tillgängligt på [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
