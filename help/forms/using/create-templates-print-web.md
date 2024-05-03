---
title: "Självstudiekurs: Skapa mallar"
description: Skapa utskrifts- och webbmallar för interaktiv kommunikation
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 0%

---

# Självstudiekurs: Skapa mallar{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Den här självstudiekursen är ett steg i [Skapa din första interaktiva kommunikation](/help/forms/using/create-your-first-interactive-communication.md) serie. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet med självstudiekurser.

Om du vill skapa en interaktiv kommunikation måste du ha mallar tillgängliga på AEM server för utskrifts- och webbkanaler.

Mallarna för utskriftskanalen skapas i Adobe Forms Designer och överförs till AEM. Mallarna kan sedan användas när du skapar en interaktiv kommunikation.

Mallarna för webbkanalen skapas i AEM. Mallförfattare och administratörer kan skapa, redigera och aktivera webbmallar. När mallarna har skapats och aktiverats kan de användas när du skapar en interaktiv kommunikation.

I den här självstudiekursen får du hjälp med att skapa mallar för utskrifts- och webbkanaler så att de blir tillgängliga när du skapar interaktiv kommunikation. I slutet av den här självstudiekursen kan du:

* Skapa XDP-mallar för utskriftskanalen med Adobe Forms Designer
* Överför XDP-mallarna till AEM Forms Server
* Skapa och aktivera mallar för webbkanalen

## Skapa mall för utskriftskanal {#create-template-for-print-channel}

Skapa och hantera en mall för tryckkanalen i interaktiv kommunikation med hjälp av följande uppgifter:

* [Skapa en XDP-mall med Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Överföra en XDP-mall till AEM Forms Server](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Skapa en XDP-mall för layoutfragment](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Skapa en XDP-mall med Forms Designer {#create-xdp-template-using-forms-designer}

Baserat på [användningsfall](/help/forms/using/create-your-first-interactive-communication.md) och [anatomi](/help/forms/using/planning-interactive-communications.md)skapar du följande delformulär i XDP-mallen:

* Fakturainformation: Inkluderar ett dokumentfragment
* Kundinformation: Inkluderar ett dokumentfragment
* Faktureringssammanfattning: Inkluderar ett dokumentfragment
* Sammanfattning: Inkluderar ett dokumentfragment (delformuläret Avgifter) och ett diagram (delformuläret Diagram)
* Specificerade anrop: Innehåller en tabell (layoutfragment)
* Betala nu: Innehåller en bild
* Mervärdestjänster: Innehåller en bild

![create_print_template](assets/create_print_template.gif)

Dessa delformulär visas som målområden i utskriftsmallen när XDP-filen har överförts till Forms Server. Alla entiteter som dokumentfragment, diagram, layoutfragment och bilder läggs till i målområdena när interaktiv kommunikation skapas.

Så här skapar du en XDP-mall för utskriftskanalen:

1. Öppna Forms Designer och välj **Fil** > **Nytt** > **Använd ett tomt formulär,** välj **Nästa** och sedan markera **Slutför** om du vill öppna formuläret för att skapa en mall.

   Se till att **Objektbibliotek** och **Objekt** alternativen är markerade på menyn **Fönster** -menyn.

1. Dra och släpp **Delformulär** -komponenten från **Objektbibliotek** till formuläret.
1. Markera delformuläret så att du kan se alternativen för delformuläret i **Objekt** i den högra rutan.
1. Välj **Delformulär** och markera **Flödat** från **Innehåll** listruta. Dra i delformulärets vänstra slutpunkt om du vill justera längden.
1. I **Bindningar** tab:

   1. Ange **BillDetails** i **Namn** fält.

   1. Välj **Ingen databindning** från **Databindning** listruta.

   ![Delformulär för Designer](assets/forms_designer_subform_new.png)

1. Markera på samma sätt rotdelformuläret och markera **Delformulär** och markera **Flödat** från **Innehåll** listruta. I **Bindningar** tab:

   1. Ange **TelecaBill** i **Namn** fält.

   1. Välj **Ingen databindning** från **Databindning** listruta.

   ![Delformulär för utskriftsmall](assets/root_subform_print_template_new.png)

1. Upprepa steg 2-5 för att skapa följande delformulär:

   * BillDetails
   * CustomerDetails
   * BillSummary
   * Sammanfattning - Välj **Delformulär** och markera **Placerad** från **Innehåll** nedrullningsbar lista för det här delformuläret. Infoga följande delformulär i **Sammanfattning** delformulär.

      * Avgifter
      * Diagram

   * ItemCall
   * PayNow
   * ValueAddedServices

   För att spara tid kan du även kopiera och klistra in befintliga delformulär för att skapa ytterligare delformulär.

   Om du vill ändra **Diagram** till höger om delformuläret Charges väljer du **Diagram** i den vänstra rutan väljer du **Layout** och ange ett värde för **AnkarpunktX** fält. Värdet måste vara större än värdet för **Bredd** fält för **Avgifter** delformulär. Välj **Avgifter** delformulär och markera **Layout** -fliken så att du kan visa värdet för **Bredd** fält.

1. Dra och släpp **Text** objekt från **Objektbibliotek** till formuläret och ange **Ring XXXX för att prenumerera** text i rutan.
1. Högerklicka på textobjektet i den vänstra rutan och välj **Byt namn på objekt** och ange namnet på textobjektet som **Prenumerera**.

   ![XDP-mall](assets/print_xdp_template_subform_new.png)

1. Välj **Fil** > **Spara som** så här sparar du filen i det lokala filsystemet:

   1. Navigera till den plats där du kan spara filen och ange namnet som **create_first_ic_print_template**.
   1. Välj **.xdp** från **Spara som typ** listruta.

   1. Välj **Spara**.

### Överföra en XDP-mall till AEM Forms Server {#upload-xdp-template-to-the-aem-forms-server}

När du har skapat en XDP-mall med Forms Designer måste du överföra den till AEM Forms Server så att mallen kan användas när du skapar den interaktiva kommunikationen.

1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **Skapa** > **Filöverföring**.

   Navigera och markera **create_first_ic_print_template** mall (XDP) och välj **Öppna** om du vill importera XDP-mallen till AEM Forms Server.

### Skapa en XDP-mall för layoutfragment {#create-xdp-template-for-layout-fragments}

Om du vill skapa ett layoutfragment för tryckkanalen i den interaktiva kommunikationen skapar du en XDP-fil med Forms Designer och överför den till AEM Forms Server.

1. Öppna Forms Designer och välj **Fil** > **Nytt** > **Använd ett tomt formulär,** välj **Nästa** och sedan markera **Slutför** om du vill öppna formuläret för att skapa en mall.

   Se till att **Objektbibliotek** och **Objekt** alternativen är markerade på menyn **Fönster** -menyn.

1. Dra och släpp **Tabell** -komponenten från **Objektbibliotek** till formuläret.
1. I dialogrutan Infoga tabell:

   1. Ange antalet kolumner som **5**.
   1. Ange antalet innehållsrader som **1**.
   1. Välj **Inkludera rubrikrad i tabell** kryssrutan.
   1. Tabb **OK**.

1. Välj **+** i den vänstra rutan bredvid **Tabell** 1 och högerklicka **Cell1** och markera **Byt namn på objekt** till **Datum**.

   På samma sätt kan du ändra namn **Cell2**, **Cell3**, **Cell4** och **Cell5** till **Tid**, **Nummer**, **Varaktighet** och **Avgifter** respektive.

1. Klicka på rubriktextfälten i dialogrutan **Designervy** och döpa om dem till **Tid**, **Nummer**, **Varaktighet** och **Avgifter**.

   ![Layoutfragment](assets/layout_fragment_print_new.png)

1. Välj **Rad 1** i den vänstra rutan och väljer **Objekt** > **Bindning** > **Upprepa rad för varje dataobjekt**.

   ![Upprepa egenskaper för layoutfragment](assets/layout_fragment_print_repeat_new.png)

1. Dra och släpp **Textfält** -komponenten från **Objektbibliotek** till **Designervy**.

   ![Textfält för layoutavsnitt](assets/layout_fragment_print_text_field_new.png)

   På samma sätt kan du dra och släppa **Textfält** -komponenten till **Tid**, **Nummer**, **Varaktighet** och **Avgifter** rader.

1. Välj **Fil** > **Spara som** så här sparar du filen i det lokala filsystemet:

   1. Navigera till den plats där du kan spara filen och ange namnet som **table_lf**.
   1. Välj **.xdp** från **Spara som typ** listruta.

   1. Välj **Spara**.

   När du har skapat en XDP-mall för layoutfragment med Forms Designer måste du [ladda upp](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) till AEM Forms Server så att mallen är tillgänglig för användning när du skapar layoutfragment.

## Skapa en mall för webbkanal {#create-template-for-web-channel}

Skapa och hantera en mall för webbkanalen i interaktiv kommunikation med hjälp av följande uppgifter:

* [Skapa mapp för mallar](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Skapa mallen](../../forms/using/create-templates-print-web.md#create-the-template)
* [Aktivera mallen](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Aktivera knappar i interaktiv kommunikation](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Skapa en mapp för mallar {#create-folder-for-templates}

Om du vill skapa en webbkanalmall definierar du en mapp där du kan spara de skapade mallarna. När du har skapat en mall i den mappen aktiverar du mallen så att formuläranvändarna kan skapa en webbkanal för en interaktiv kommunikation som är baserad på mallen.

Så här skapar du en mapp för de redigerbara mallarna:

1. Välj **verktyg** ![hammer-icon](assets/hammer-icon.svg) > **Konfigurationsläsaren**.
   * Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.
1. På sidan Configuration Browser väljer du **Skapa**.
1. I **Skapa konfiguration** dialogruta, ange **Create_First_IC_templates** som mappens titel, kontrollera **Redigerbara mallar** och markera **Skapa**.

   ![Konfigurera webbmallar](assets/create_first_ic_web_template_new.png)

   The **Create_First_IC_templates** mappen skapas och visas på **Konfigurationsläsaren** sida.

### Skapa mallen {#create-the-template}

Baserat på [användningsfall](/help/forms/using/create-your-first-interactive-communication.md) och [anatomi](/help/forms/using/planning-interactive-communications.md)skapar du följande paneler i webbmallen:

* Fakturainformation: Inkluderar ett dokumentfragment
* Kundinformation: Inkluderar ett dokumentfragment
* Faktureringssammanfattning: Inkluderar ett dokumentfragment
* Sammanfattning av avgifter: Innehåller ett dokumentfragment och ett diagram (layout med två kolumner)
* Specificerade samtal: Innehåller ett register
* Betala nu: Innehåller en **Betala nu** och en bild
* Mervärdestjänster: Innehåller en bild och en **Prenumerera** -knappen.

![create_web_template](assets/create_web_template.gif)

Alla entiteter som dokumentfragment, diagram, tabeller, bilder och knappar läggs till när interaktiv kommunikation skapas.

Skapa en mall för webbkanalen i **Create_First_IC_templates** gör du så här:

1. Navigera till rätt mallmapp genom att välja **verktyg** > **Mallar** > **Create_First_IC_templates** mapp.
1. Välj **Skapa**.
1. På **Välj en malltyp** konfigurationsguide, välja **Interaktiv kommunikation - webbkanal** och markera **Nästa**.
1. På **Mallinformation** konfigurationsguide, ange **Create_First_IC_Web_Template** som malltitel. Ange en valfri beskrivning och välj **Skapa**.

   Ett bekräftelsemeddelande som **Create_First_IC_Web_Template** visas.

1. Välj **Öppna** om du vill öppna mallen i mallredigeraren.
1. Välj **Ursprungligt innehåll** från listrutan bredvid **Förhandsgranska** alternativ.

   ![Mallredigerare](assets/template_editor_initial_content_new.png)

1. Välj **Rotpanelen** och sedan **+** om du vill visa en lista med komponenter som du kan lägga till i mallen.
1. Lägga till en panel ovanför **Rotpanelen**, markera **Panel** från listan.
1. Välj **Innehåll** i den vänstra rutan. Den nya panelen som lagts till i steg 8 visas under **Rotpanelen** i trädet.

   ![Innehållsträd](assets/content_tree_root_panel_new.png)

1. Markera panelen och markera ![configure_icon](assets/configure_icon.png) (Konfigurera).
1. I rutan Egenskaper:

   1. Ange **fakturainformation** i fältet Namn.
   1. Ange **Fakturainformation** i fältet Titel.
   1. Välj **1** från **Antal kolumner** listruta.

   1. Om du vill spara egenskaperna väljer du ![Spara](/help/forms/using/assets/done_icon.png).

   Namnet på panelen uppdateras till **Fakturainformation** i trädet.

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

Så här aktiverar du webbmallen:

1. Välj **verktyg** ![hammer-icon](assets/hammer-icon.svg) > **Mallar**.
1. Navigera till **Create_First_IC_Web_Template** mall, markera den och markera **Aktivera**.
1. Välj **Aktivera** igen för att bekräfta.

   Mallen är aktiverad och dess status visas som Aktiverad. Du kan använda den här mallen när du skapar interaktiv kommunikation för webbkanalen.

### Aktivera knappar i interaktiv kommunikation {#enabling-buttons-in-interactive-communications}

Baserat på användningsfallet måste du inkludera **Betala nu** och **Prenumerera** knappar (adaptiva formulärkomponenter) i Interactive Communication. Så här aktiverar du de här knapparna i den interaktiva kommunikationen:

1. Välj **Struktur** från listrutan bredvid **Förhandsgranska** alternativ.
1. Välj **Dokumentbehållare** rotpanelen med hjälp av innehållsträdet och markera **Policy** för att välja vilka komponenter som får användas i interaktiv kommunikation.

   ![Konfigurera princip](assets/structure_configure_policy_new.png)

1. I **Tillåtna komponenter** -fliken i **Egenskaper** avsnitt, markera **Knapp** från **Adaptiv form** -komponenter.

   ![Tillåtna komponenter](assets/allowed_components_af_new.png)

1. Om du vill spara egenskaperna väljer du ![spara](assets/done_icon.png).
