---
title: '"Självstudiekurs: Skapa mallar"'
seo-title: Skapa utskrifts- och webbmallar för interaktiv kommunikation
description: Skapa utskrifts- och webbmallar för interaktiv kommunikation
seo-description: Skapa utskrifts- och webbmallar för interaktiv kommunikation
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
translation-type: tm+mt
source-git-commit: 3afe5bf8e49202608e4c9369b2ff3d26afa03dc4

---


# Självstudiekurs: Skapa mallar{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Den här självstudiekursen är ett steg i [Skapa din första interaktiva kommunikationsserie](/help/forms/using/create-your-first-interactive-communication.md) . Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

Om du vill skapa en interaktiv kommunikation måste du ha mallar tillgängliga på AEM-servern för utskrifts- och webbkanaler.

Mallarna för utskriftskanalen skapas i Adobe Forms Designer och överförs till AEM-servern. Mallarna kan sedan användas när du skapar en interaktiv kommunikation.

Mallarna för webbkanalen skapas i AEM. Mallförfattare och administratörer kan skapa, redigera och aktivera webbmallar. När mallarna har skapats och aktiverats kan de användas när du skapar en interaktiv kommunikation.

I den här självstudiekursen får du hjälp med att skapa mallar för utskrifts- och webbkanaler så att de blir tillgängliga när du skapar interaktiv kommunikation. I slutet av den här självstudiekursen kan du:

* Skapa XDP-mallar för tryckkanaler med Adobe Forms Designer
* Överför XDP-mallarna till AEM Forms Server
* Skapa och aktivera mallar för webbkanalen

## Skapa mall för utskriftskanal {#create-template-for-print-channel}

Skapa och hantera mallar för tryckkanalen i interaktiv kommunikation med hjälp av följande uppgifter:

* [Skapa XDP-mall med Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Överför XDP-mall till AEM Forms-servern](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Skapa XDP-mall för layoutfragment](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Skapa XDP-mall med Forms Designer {#create-xdp-template-using-forms-designer}

Baserat på [användningsfall](/help/forms/using/create-your-first-interactive-communication.md) och [anatomi](/help/forms/using/planning-interactive-communications.md)skapar du följande delformulär i XDP-mallen:

* Fakturainformation: Inkluderar ett dokumentfragment
* Kundinformation: Inkluderar ett dokumentfragment
* Fakturasammanfattning: Inkluderar ett dokumentfragment
* Sammanfattning: Innehåller ett dokumentfragment (delformuläret Charges) och ett diagram (delformuläret Charts)
* Specificerade samtal: Inkluderar en tabell (layoutfragment)
* Betala nu: Innehåller en bild
* Mervärdestjänster: Innehåller en bild

![create_print_template](assets/create_print_template.gif)

Dessa delformulär visas som målområden i utskriftsmallen när XDP-filen har överförts till Forms-servern. Alla entiteter som dokumentfragment, diagram, layoutfragment och bilder läggs till i målområdena när interaktiv kommunikation skapas.

Så här skapar du en XDP-mall för utskriftskanalen:

1. Öppna Forms Designer, välj **Arkiv** > **Nytt** > **Använd ett tomt formulär,** tryck på **Nästa** och sedan på **Slutför** för att öppna formuläret för att skapa en mall.

   Kontrollera att alternativen **Objektbibliotek** och **Objekt** är markerade på menyn **Fönster** .

1. Dra och släpp **delformulärskomponenten** från **objektbiblioteket** till formuläret.
1. Markera delformuläret för att visa alternativen för delformuläret i **objektfönstret** i den högra rutan.
1. Välj fliken **Delformulär** och välj **Flödat** i listrutan **Innehåll** . Dra delformulärets vänstra slutpunkt för att justera längden.
1. På fliken **Bindningar** :

   1. Ange **fakturainformation** i **fältet Namn** .

   1. Välj **Ingen databindning** i listrutan **Databindning** .
   ![Delformulär för Designer](assets/forms_designer_subform_new.png)

1. Markera på samma sätt rotdelformuläret, markera fliken **Delformulär** och välj **Flödat** i listrutan **Innehåll** . På fliken **Bindningar** :

   1. Ange **TelecaBill** i fältet **Name** (Namn).

   1. Välj **Ingen databindning** i listrutan **Databindning** .
   ![Delformulär för utskriftsmall](assets/root_subform_print_template_new.png)

1. Upprepa steg 2-5 för att skapa följande delformulär:

   * BillDetails
   * CustomerDetails
   * BillSummary
   * Sammanfattning - Välj fliken **Delformulär** och välj **Placerad** i listrutan **Innehåll** för det här delformuläret. Infoga följande delformulär i delformuläret **Sammanfattning** .

      * Avgifter
      * Diagram
   * SpecificeradeAnrop
   * PayNow
   * ValueAddedServices
   För att spara tid kan du även kopiera och klistra in befintliga delformulär för att skapa nya delformulär.

   Om du vill flytta delformuläret **Diagram** till höger om delformuläret Diagram markerar du delformuläret **Diagram** i den vänstra rutan, väljer fliken **Layout** och anger ett värde för fältet **FästpunktX** . Värdet måste vara större än värdet för fältet **Bredd** för delformuläret **Avgifter** . Markera delformuläret **Avgifter** och välj fliken **Layout** för att visa värdet för fältet **Bredd** .

1. Dra och släpp **textobjektet** från **objektbiblioteket** till formuläret och ange **uppringningsnumret XXXX för att prenumerera** på texten i rutan.
1. Högerklicka på textobjektet i den vänstra rutan, välj **Byt namn på objekt** och ange namnet på textobjektet som **Prenumerera**.

   ![XDP-mall](assets/print_xdp_template_subform_new.png)

1. Välj **Arkiv** > **Spara som** för att spara filen i det lokala filsystemet:

   1. Navigera till den plats där du vill spara filen och ange namnet som **create_first_ic_print_template**.
   1. Välj **.xdp** i listrutan **Spara som typ** .

   1. Tryck på **Spara**.

### Överför XDP-mall till AEM Forms-servern {#upload-xdp-template-to-the-aem-forms-server}

När du har skapat en XDP-mall med Forms Designer måste du överföra den till AEM Forms-servern så att mallen kan användas när du skapar den interaktiva kommunikationen.

1. Välj **Formulär** > **Formulär och dokument**.
1. Tryck på **Skapa** > **Filöverföring**.

   Navigera till och välj mallen **create_first_ic_print_template** (XDP) och tryck på **Öppna** för att importera XDP-mallen till AEM Forms-servern.

### Skapa XDP-mall för layoutfragment {#create-xdp-template-for-layout-fragments}

Om du vill skapa ett layoutfragment för tryckkanalen i den interaktiva kommunikationen skapar du en XDP-fil med Forms Designer och överför den till AEM Forms-servern.

1. Öppna Forms Designer, välj **Arkiv** > **Nytt** > **Använd ett tomt formulär,** tryck på **Nästa** och sedan på **Slutför** för att öppna formuläret för att skapa en mall.

   Kontrollera att alternativen **Objektbibliotek** och **Objekt** är markerade på menyn **Fönster** .

1. Dra och släpp **tabellkomponenten** från **objektbiblioteket** till formuläret.
1. I dialogrutan Infoga tabell:

   1. Ange antalet kolumner som **5**.
   1. Ange antalet innehållsrader som **1**.
   1. Markera kryssrutan **Inkludera rubrikrad i tabell** .
   1. Tabb **okej**.

1. Tryck **+** i den vänstra rutan bredvid **Tabell** 1 och högerklicka på **Cell1** och välj **Ändra namn på objekt** till **datum**.

   Du kan även byta namn på **Cell2**, **Cell3**, **Cell4** och **Cell5** till **Time************** ,Number,DurationUnder respektive¥ChargesUnder varandra.

1. Klicka på rubriktextfälten i **designervyn** och byt namn på dem till **Tid**, **Nummer**, **Varaktighet** och **Avgifter**.

   ![Layoutfragment](assets/layout_fragment_print_new.png)

1. Välj **Rad 1** i den vänstra rutan och välj **Objekt** > **Bindning** > **Upprepa rad för varje dataobjekt**.

   ![Upprepa egenskaper för layoutfragment](assets/layout_fragment_print_repeat_new.png)

1. Dra och släpp **textfältskomponenten** från **objektbiblioteket** till **designvyn**.

   ![Textfält för layoutfragment](assets/layout_fragment_print_text_field_new.png)

   Du kan också dra och släppa **textfältskomponenten** på raderna **Tid**, **Nummer**, **Varaktighet** och **Avgifter** .

1. Välj **Arkiv** > **Spara som** för att spara filen i det lokala filsystemet:

   1. Navigera till platsen där du vill spara filen och ange namnet som **table_lf**.
   1. Välj **.xdp** i listrutan **Spara som typ** .

   1. Tryck på **Spara**.
   När du har skapat en XDP-mall för layoutfragment med Forms Designer måste du [överföra](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) den till AEM Forms-servern så att mallen är tillgänglig för användning när du skapar layoutfragment.

## Skapa mall för webbkanal {#create-template-for-web-channel}

Skapa och hantera mallar för webbkanalen i interaktiv kommunikation med hjälp av följande uppgifter:

* [Skapa mapp för mallar](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Skapa mallen](../../forms/using/create-templates-print-web.md#create-the-template)
* [Aktivera mallen](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Aktivera knappar i interaktiv kommunikation](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Skapa mapp för mallar {#create-folder-for-templates}

Om du vill skapa en webbkanalmall definierar du en mapp där du kan spara de skapade mallarna. När du har skapat en mall i den mappen aktiverar du mallen så att formuläranvändarna kan skapa en webbkanal för en interaktiv kommunikation som är baserad på mallen.

Så här skapar du en mapp för de redigerbara mallarna:

1. Tryck på **Verktyg** ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/Tools.png) > **Konfigurationsläsaren**.
1. Tryck på **Skapa** på sidan Configuration Browser.
1. I dialogrutan **Skapa konfiguration** anger du **Create_First_IC_templates** som mappens titel, markerar **Redigerbara mallar** och trycker sedan på **Skapa**.

   ![Konfigurera webbmallar](assets/create_first_ic_web_template_new.png)

   Mappen **Create_First_IC_templates** skapas och visas på sidan **Konfigurationsläsare** .

### Skapa mallen {#create-the-template}

Baserat på [användningsfall](/help/forms/using/create-your-first-interactive-communication.md) och [anatomi](/help/forms/using/planning-interactive-communications.md)skapar du följande paneler i webbmallen:

* Fakturainformation: Inkluderar ett dokumentfragment
* Kundinformation: Inkluderar ett dokumentfragment
* Fakturasammanfattning: Inkluderar ett dokumentfragment
* Sammanfattning av avgifter: Innehåller ett dokumentfragment och ett diagram (layout med två kolumner)
* Specificerade samtal: Innehåller en tabell
* Betala nu: Innehåller en **Pay Now** -knapp och en bild
* Mervärdestjänster: Innehåller en bild och en **prenumerationsknapp** .

![create_web_template](assets/create_web_template.gif)

Alla entiteter som dokumentfragment, diagram, tabeller, bilder och knappar läggs till när interaktiv kommunikation skapas.

Så här skapar du en mall för webbkanalen i mappen **Create_First_IC_templates** :

1. Navigera till rätt mallmapp genom att välja **Verktyg** > **Mallar** > **Create_First_IC_templates** .
1. Tryck på **Skapa**.
1. Välj **Interaktiv kommunikation - webbkanal** och tryck på **Nästa** i konfigurationsguiden Välj en malltyp ****.
1. I konfigurationsguiden **Mallinformation** anger du **Create_First_IC_Web_Template** som mallrubrik. Ange en valfri beskrivning och tryck på **Skapa**.

   Ett bekräftelsemeddelande om att **Create_First_IC_Web_Template** visas.

1. Tryck på **Öppna** för att öppna mallen i mallredigeraren.
1. Välj **Ursprungligt innehåll** i listrutan bredvid alternativet **Förhandsgranska** .

   ![Mallredigerare](assets/template_editor_initial_content_new.png)

1. Tryck på **rotpanelen** och tryck sedan på **+** för att visa listan med komponenter som du kan lägga till i mallen.
1. Välj **Panel** i listan om du vill lägga till en panel ovanför **rotpanelen**.
1. Välj fliken **Innehåll** i den vänstra rutan. Den nya panelen som lagts till i steg 8 visas under **rotpanelen** i innehållsträdet.

   ![Innehållsträd](assets/content_tree_root_panel_new.png)

1. Markera panelen och tryck på ![](assets/configure_icon.png) (Konfigurera).
1. I rutan Egenskaper:

   1. Ange **fakturainformation** i fältet Namn.
   1. Ange **fakturainformation** i fältet Titel.
   1. Välj **1** i listrutan **Antal kolumner** .

   1. Tryck ![](/help/forms/using/assets/done_icon.png) för att spara egenskaperna.
   Panelens namn uppdateras till **Fakturainformation** i innehållsträdet.

1. Upprepa steg 7-11 om du vill lägga till paneler med följande egenskaper i mallen:

   | Namn | Titel | Antal kolumner |
   |---|---|---|
   | kundinformation | Kundinformation | 1 |
   | faktureringssammanfattning | Fakturasammanfattning | 1 |
   | summeringskostnader | Sammanfattning av avgifter | 2 |
   | objektanrop | Specificerade samtal | 1 |
   | nyttja | Betala nu | 2 |
   | arbetsyta | Mervärdestjänster | 1 |

   Följande bild visar innehållsträdet när alla paneler har lagts till i mallen:

   ![Innehållsträd för alla paneler](assets/content_tree_all_panels_new.png)

### Aktivera mallen {#enable-the-template}

När du har skapat webbmallen måste du aktivera den för användning när du skapar den.

Aktivera webbmallen genom att utföra följande steg:

1. Tryck på **Verktyg** ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/Tools.png) > **Mallar**.
1. Navigera till mallen **Create_First_IC_Web_Template** , markera den och tryck sedan på **Aktivera**.
1. Bekräfta genom att klicka på **Aktivera** igen.

   Mallen är aktiverad och dess status visas som Aktiverad. Du kan använda den här mallen när du skapar interaktiv kommunikation för webbkanalen.

### Aktivera knappar i interaktiv kommunikation {#enabling-buttons-in-interactive-communications}

Beroende på hur de används måste du inkludera knapparna **Betala nu** och **Prenumerera** (adaptiva formulärkomponenter) i Interaktiv kommunikation. Så här aktiverar du de här knapparna i den interaktiva kommunikationen:

1. Välj **Struktur** i listrutan bredvid alternativet **Förhandsgranska** .
1. Välj rotpanelen **Dokumentbehållare** med innehållsträdet och tryck på **Policy** för att välja de komponenter som får användas i den interaktiva kommunikationen.

   ![Konfigurera princip](assets/structure_configure_policy_new.png)

1. På fliken **Tillåtna komponenter** i avsnittet **Egenskaper** väljer du **Knapp** bland komponenterna i det **adaptiva formuläret** .

   ![Tillåtna komponenter](assets/allowed_components_af_new.png)

1. Tryck ![](assets/done_icon.png) för att spara egenskaperna.