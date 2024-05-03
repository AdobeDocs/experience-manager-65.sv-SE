---
title: "Självstudiekurs: Skapa interaktiv kommunikation"
description: Skapa en interaktiv kommunikation med alla byggstenar
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 0%

---

# Självstudiekurs: Skapa interaktiv kommunikation {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Den här självstudiekursen är ett steg i [Skapa din första interaktiva kommunikation](/help/forms/using/create-your-first-interactive-communication.md) serie. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga självstudiekurserna.

När du har skapat alla byggstenar, t.ex. formulärdatamodell, dokumentfragment, mallar och teman för webbversionen, kan du börja skapa en interaktiv kommunikation.

Interaktiv kommunikation kan distribueras via två kanaler: tryck och webb. Du kan också skapa en interaktiv kommunikationskanal med utskriftskanalen som master. Skriv ut som huvudalternativ för webbkanal säkerställer att innehållet, arvet och databindningen för webbkanalen hämtas från utskriftskanalen. Det ser också till att ändringarna som görs i utskriftskanalen synkroniseras i webbkanalen. De som skapar interaktiv kommunikation får dock bryta arvet för vissa komponenter i webbkanalen.

I den här självstudiekursen får du hjälp med att skapa interaktiv kommunikation för tryck- och webbkanaler. I slutet av den här självstudiekursen kan du:

* Skapa interaktiv kommunikation för tryckkanalen
* Skapa interaktiv kommunikation för webbkanalen
* Skapa trycksaker och webbinteraktiv kommunikation med Skriv ut som mall

## Skapa interaktiv kommunikation för tryck och webb utan synkronisering {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Skapa interaktiv kommunikation för tryckkanaler {#create-interactive-communication-for-print-channel}

Nedan följer en lista över resurser som redan har skapats i den här självstudiekursen och som behövs när du skapar den interaktiva kommunikationen för utskriftskanalen:

**Utskriftsmall:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Formulärdatamodell:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Dokumentfragment:** [Bill_details_first_ic, customer_details_first_ic, Bill_summary_first_ic, summary_addas_first_ic](../../forms/using/create-document-fragments.md)

**Layoutfragment:** [table_lf](../../forms/using/create-templates-print-web.md)

**Bilder:** PayNow och ValueAddedServices

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **Skapa** och markera **Interaktiv kommunikation**. The **Skapa interaktiv kommunikation** visas.
1. Ange **create_first_ic** i **Titel** och **Namn** fält. Välj **FDM_Create_First_IC** som formulärdatamodell och välj **Nästa**.
1. I **Kanaler** guide:

   1. Ange **create_first_ic_print_template** som utskriftsmall och välja **Välj**. Se till att **Använd Skriv ut som mallsida för webbkanal** är inte markerad.

   1. Ange **Create_First_IC_templates** mapp > **Create_First_IC_Web_Template** som webbmall och välj **Välj**.

   1. Välj **Skapa**.

   Ett bekräftelsemeddelande visas om att den interaktiva kommunikationen har skapats.

1. Välj **Redigera** för att öppna den interaktiva kommunikationen i den högra rutan.
1. Gå till **Resurser** och tillämpa filtret för att bara visa dokumentfragmenten i den vänstra rutan.
1. Dra och släpp följande dokumentfragment till målområdena i interaktiv kommunikation:

   | Dokumentfragment | Målområde |
   |---|---|
   | Bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | Bill_summary_first_ic | BillSummary |
   | summary_addas_first_interactive_communication | Avgifter |

   ![Dokumentfragment för interaktiv kommunikation](assets/create_first_ic_doc_fragments_new.png)

1. Välj **Diagram** målområde och markera **+** för att lägga till **Diagram** -komponenten.
1. Markera diagramkomponenten och markera ![configure_icon](assets/configure_icon.png) (Konfigurera). Diagramegenskaperna visas i den vänstra rutan:

   1. Ange ett namn för diagrammet.
   1. Välj **Cirkel** från **Diagramtyp** listruta.
   1. Välj **calltype** -egenskapen från **samtal** datamodellens objekttyp i **X-axel** -avsnitt. Välj ![ready_icon](assets/done_icon.png).
   1. Välj **Frekvens** från **Funktion** listruta.
   1. Välj **calltype** -egenskapen från **samtal** datamodellens objekttyp i **Y-axel** -avsnitt. Välj ![ready_icon](assets/done_icon.png).
   1. Välj ![ready_icon](assets/done_icon.png) om du vill spara diagramegenskaperna.

1. Gå till **Resurser** och använda filtret för att endast visa layoutfragmenten i den vänstra rutan. Dra och släpp **table_lf** layoutfragment till **Specificerade samtal** målområde.
1. Markera textfältet i dialogrutan **Datum** kolumn och markera ![configure_icon](assets/configure_icon.png) (Konfigurera).
1. Välj **Datamodellsobjekt** från **Bindningstyp** nedrullningsbar lista och välj **samtal** > **calldate**. Välj ![ready_icon](assets/done_icon.png) två gånger för att spara egenskaperna.

   På samma sätt kan du skapa bindning med **calltime**, **callnumber**, **callduration** och **callCharts** för textfält i **Tid**, **Nummer**, **Varaktighet** och **Avgifter** kolumner.

1. Välj **PayNow** målområde och markera **+** för att lägga till **Bild** -komponenten.
1. Markera bildkomponenten och markera ![configure_icon](assets/configure_icon.png) (Konfigurera). Bildegenskaperna visas i den vänstra rutan:

   1. Ange **PayNow** som namnet på bilden i **Namn** fält.
   1. Välj **Överför** markerar du den bild som har sparats i det lokala filsystemet och väljer **Öppna**.
   1. Välj ![ready_icon](assets/done_icon.png) för att spara bildegenskaperna.

1. Upprepa steg 13 och 14 för att lägga till **ValueAddedServices** bilden till **ValueAddedServices** målområde.

### Skapa interaktiv kommunikation för webbkanal {#create-interactive-communication-for-web-channel}

Nedan följer en lista över resurser som redan har skapats i den här självstudiekursen och som behövs när du skapar interaktiv kommunikation för webbkanalen:

**Webbmall:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Formulärdatamodell:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Dokumentfragment:** [Bill_details_first_ic, customer_details_first_ic, Bill_summary_first_ic, summary_addas_first_ic](../../forms/using/create-document-fragments.md)

**Bilder:** PayNowWeb och ValueAddedServicesWeb

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **Skapa** och markera **Interaktiv kommunikation**. The **Skapa interaktiv kommunikation** visas.
1. Ange **create_first_ic** i **Titel** och **Namn** fält. Välj **FDM_Create_First_IC** som formulärdatamodell och välj **Nästa**.
1. I **Kanaler** guide:

   1. Ange **create_first_ic_print_template** som utskriftsmall och välja **Välj**. Se till att **Använd Skriv ut som mallsida för webbkanal** är inte markerad.

   1. Ange **Create_First_IC_templates** mapp > **Create_First_IC_Web_Template** som webbmall och välj **Välj**.

   1. Välj **Skapa**.

   Ett bekräftelsemeddelande visas om att den interaktiva kommunikationen har skapats.

1. Välj **Redigera** för att öppna den interaktiva kommunikationen i den högra rutan.
1. Välj **Kanaler** -fliken i den vänstra rutan och väljer **Webb**.
1. Gå till **Resurser** och tillämpa filtret för att bara visa dokumentfragmenten i den vänstra rutan.
1. Dra och släpp följande dokumentfragment till målområdena i interaktiv kommunikation:

   | Dokumentfragment | Målområde |
   |---|---|
   | Bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | Bill_summary_first_ic | BillSummary |
   | summary_addas_first_interactive_communication | Avgifter |

1. Välj **Sammanfattning av avgifter** målområde och markera **+** för att lägga till **Diagram** -komponenten.
1. Markera diagramkomponenten och markera ![configure_icon](assets/configure_icon.png) (Konfigurera). Diagramegenskaperna visas i den vänstra rutan:

   1. Ange ett namn för diagrammet.
   1. Välj **Cirkel** från **Diagramtyp** listruta.

   1. Välj **calltype** -egenskapen från **samtal** datamodellens objekttyp i **X-axel** -avsnitt. Välj ![ready_icon](assets/done_icon.png).

   1. Välj **Frekvens** från **Funktion** listruta.

   1. Välj **calltype** -egenskapen från **samtal** datamodellens objekttyp i **Y-axel** -avsnitt. Välj ![ready_icon](assets/done_icon.png).

   1. Välj ![ready_icon](assets/done_icon.png) om du vill spara diagramegenskaperna.

1. Välj **Datakällor** från den vänstra rutan och dra och släpp **samtal** datamodellsobjekt till **Specificerade samtal** målområde. Alla egenskaper i **samtal** datamodellsobjektet visas som tabellkolumner i **Specificerade samtal** målområde i den högra rutan.

   Baserat på användningsfallet behöver du kolumnerna Samtalsdatum, Samtalstid, Samtalsnummer, Samtalsvaraktighet och Samtalsavgifter i tabellen.

   ![Tabell för interaktiv kommunikation](assets/table_ic_web_new.png)

1. Välj **Mobil** tabellkolumnrubrik och markera **Fler alternativ** > **Ta bort kolumn**. På samma sätt tar du bort **Calltype** kolumn.
1. Välj **Anropa** tabellkolumnrubrik och markera ![redigera](assets/edit.png) (Redigera) för att byta namn på texten till **Samtalsdatum**. Du kan också byta namn på andra kolumnrubriker i tabellen.
1. Baserat på användningsexemplet infogar du en **Betala nu** i interaktiv kommunikation som ger användaren möjlighet att göra betalningen genom att klicka på knappen. Gör så här för att infoga knappen:

   1. Välj **Betala nu** målområde och markera **+** för att lägga till **Text** -komponenten.

   1. Markera textkomponenten och markera ![redigera](assets/edit.png) (Redigera).
   1. Byt namn på texten till **Betala nu**.
   1. Markera texten och välj ikonen Hyperlänk.
   1. Ange betalnings-URL i **Bana** fält.
   1. Välj **Ny flik** från **Mål** listruta.

   1. Välj ![ready_icon](assets/done_icon.png) för att spara hyperlänksegenskaperna.

1. Välj **Stil** från listrutan bredvid **Förhandsgranska** alternativ.

   ![Välj stilläge för interaktiv kommunikation](assets/select_style_ic_web_new.png)

1. Gör så här för att formatera hyperlänktexten så att den visas som en knapp i det interaktiva meddelandet:

   1. Markera textkomponenten och markera ![redigera](assets/edit.png) (Redigera).
   1. I **Kant** avsnitt, ange **1,5 px** as **Kantbredd**, markera **Heldragen** as **Kantstil** och ange **46px** as **Kantradie**.

   1. Välj Röd som bakgrundsfärg för knappen på menyn **Bakgrund** -avsnitt.
   1. I **Marginal** fält för **Dimensioner och position** väljer du **Redigera samtidigt** -ikonen och ange **Höger** marginal som **450px**. Fälten Överkant, Underkant och Vänster är tomma.

   ![Infoga hyperlänk i interaktiv kommunikation](assets/ic_web_hyperlink_new.png)

1. Välj **Betala nu** målområde och markera **+** för att lägga till **Bild** -komponenten.
1. Markera bildkomponenten och markera ![configure_icon](assets/configure_icon.png) (Konfigurera). Bildegenskaperna visas i den vänstra rutan:

   1. Ange **PayNow** som namnet på bilden i **Namn** fält.

   1. Välj **Överför** väljer du **PayNowWeb** bilden som har sparats i det lokala filsystemet, och väljer **Öppna**.

   1. Välj ![ready_icon](assets/done_icon.png) för att spara bildegenskaperna.

1. Baserat på användningsexemplet infogar du en **Prenumerera** i interaktiv kommunikation som ger användaren möjlighet att prenumerera på mervärdesskapande tjänster genom att klicka på knappen.

   Upprepa steg 13-17 för att lägga till en **Prenumerera** till **Mervärdestjänster** målområde och lägg till **ValueAddedServicesWeb** bild.

## Skapa interaktiv kommunikation för tryck och webb med automatisk synkronisering {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

Du kan också skapa en interaktiv kommunikation genom att aktivera automatisk synkronisering mellan utskrifts- och webbkanaler. Om du vill aktivera automatisk synkronisering väljer du Skriv ut som mall när du skapar den interaktiva kommunikationen. Om du väljer alternativet Skriv ut som mallsida kommer innehållet, arvet och databindningen för webbkanalen att härledas från utskriftskanalen. Det ser också till att de ändringar som görs i utskriftskanalen återspeglas i webbkanalen.

Utför följande steg för att härleda webbkanalsinnehållet med hjälp av Print channel:

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **Skapa** och markera **Interaktiv kommunikation**. The **Skapa interaktiv kommunikation** visas.
1. Ange **create_first_ic** i **Titel** och **Namn** fält. Välj **FDM_Create_First_IC** som formulärdatamodell och välj **Nästa**.
1. I **Kanaler** guide:

   1. Ange **create_first_ic_print_template** som utskriftsmall och välja **Välj**.

   1. Välj **Använd Skriv ut som mallsida för webbkanal** kryssrutan.
   1. Ange **Create_First_IC_templates** mapp > **Create_First_IC_Web_Template** som webbmall och välj **Välj**.

   1. Välj **Skapa**.

   Ett bekräftelsemeddelande visas om att den interaktiva kommunikationen har skapats.

1. Välj **Redigera** för att öppna den interaktiva kommunikationen i den högra rutan.
1. Utför steg 6 - 15 av [Skapa interaktiv kommunikation för tryckkanaler](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) -avsnitt.
1. Välj **Kanaler** -fliken i den vänstra rutan och väljer **Webb** för att automatiskt generera innehåll för webbkanalen från utskriftskanalen.
1. Som **Använd Skriv ut som mallsida för webbkanal** är markerad i steg 4, och innehållet och bindningarna genereras automatiskt för webbkanalen från utskriftskanalen.

   Utskriftskanalinnehållet infogas under webbkanalens mallinnehåll. Om du vill ändra webbkanalsinnehållet som har genererats automatiskt från utskriftskanalen kan du avbryta arvet för alla målområden.

   Hovra över det relevanta målområdet i webbkanalen och välj ![avbrytarv](assets/cancelinheritance.png) (Avbryt arv) och sedan i **Avbryt arv** dialogruta, välja **Ja**.

   ![Avbryt arv](assets/cancel_inheritance_web_channel_new.png)

   Om du har avbrutit arvet av en komponent kan du återaktivera den. Om du vill återaktivera arv håller du pekaren över gränsen för det relevanta målområdet, som innehåller komponenten, och väljer ![återaktivera arv](assets/reenableinheritance.png).

1. Välj **Innehåll** i den vänstra rutan.
1. Dra och släpp det automatiskt genererade webbkanalsinnehållet till de befintliga panelerna i webbmallen med hjälp av innehållsträdet. Nedan följer en lista över komponenter som behöver ordnas om:

   * Fakturainformation-komponent till panelen Faktureringsinformation
   * Kundinformationskomponent till panelen Kundinformation
   * Faktureringssammanfattningskomponent till faktureringssammanfattningspanelen
   * Sammanfattning av avgiftskomponenten till panelen Sammanfattning av avgifter
   * Layoutfragment (tabell) till panelen Specificerade samtal

   ![Webbinnehållsträd](assets/ic_web_content_tree_new.png)

1. Upprepa steg 13-18 av [Skapa interaktiv kommunikation för webbkanal](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) för att infoga **Betala nu** och **Prenumerera** hyperlänkar i webbkanalen i Interactive Communication.
