---
title: "Självstudiekurs: Skapa dokumentfragment"
seo-title: Create document fragments for Interactive Communication
description: Skapa dokumentfragment för interaktiv kommunikation
seo-description: Create document fragments for Interactive Communication
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 0%

---

# Självstudiekurs: Skapa dokumentfragment{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Den här självstudiekursen är ett steg i [Skapa din första interaktiva kommunikation](/help/forms/using/create-your-first-interactive-communication.md) serie. Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

Dokumentfragment är återanvändbara komponenter i en korrespondens som används för att skapa en interaktiv kommunikation. Dokumentfragmenten är av följande typer:

* Text - En textresurs är en del av innehållet som består av ett eller flera textstycken. Ett stycke kan vara statiskt eller dynamiskt.
* List - List är en grupp dokumentfragment, inklusive text, listor, villkor och bilder.
* Villkor - Med villkor kan du definiera vilket innehåll som ska tas med i den interaktiva kommunikationen baserat på data som tas emot från formulärdatamodellen.

I den här självstudiekursen får du hjälp med att skapa flera textdokumentfragment baserat på anatomin i [Planera interaktiv kommunikation](/help/forms/using/planning-interactive-communications.md) -avsnitt. I slutet av den här självstudiekursen kan du:

* Skapa dokumentfragment
* Skapa variabler
* Skapa och tillämpa regler

![text_document_fragments](assets/text_document_fragments.gif)

Här följer en lista över dokumentfragment som har skapats i den här självstudiekursen:

* [Fakturainformation](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Kundinformation](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Sammanfattning av faktura](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Sammanfattning av avgifter](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Varje dokumentfragment innehåller fält med statisk text, data som tagits emot från formulärdatamodellen och data som matats in med agentens användargränssnitt. Alla dessa fält har beskrivits i [Planera interaktiv kommunikation](/help/forms/using/planning-interactive-communications.md) -avsnitt.

När du skapar dokumentfragment i den här självstudiekursen skapas variabler för fält som tar emot data med hjälp av agentens användargränssnitt.

Använd **FDM_Create_First_IC**, enligt beskrivningen i [Skapa formulärdatamodell](../../forms/using/create-form-data-model0.md) som formulärdatamodell för att skapa dokumentfragment i den här självstudiekursen.

## Steg 1: Skapa textdokumentfragment för fakturainformation {#step-create-bill-details-text-document-fragment}

Dokumentfragmentet med faktureringsinformation innehåller följande fält:

| Fält | Datakälla |
|---|---|
| Fakturanummer | Agentgränssnitt |
| Faktureringsperiod | Agentgränssnitt |
| Faktureringsdatum | Agentgränssnitt |
| Din plan | Formulärdatamodell |

Utför följande steg för att skapa variabler för fält med användargränssnittet för agent som datakälla, skapa statisk text och använda formulärdatamodellelement i dokumentfragmentet:

1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Document Fragments]**.

1. Välj **Skapa** > **Text**.
1. Ange följande information:

   1. Retur **Bill_details_first_ic** som namnet i **Titel** fält. Titeln fylls i automatiskt i **Namn** fält.

   1. Välj **Formulärdatamodell** från **Datamodell** -avsnitt.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck **Välj**.

   1. Tryck **Nästa**.

1. Välj **Variabler** i den vänstra rutan och tryck på **Skapa**.
1. I **Skapa variabel** avsnitt:

   1. Retur **Fakturanummer** som namnet på variabeln.
   1. Välj **Sträng** som typ.
   1. Tryck **Skapa**.

   ![Skapa en variabel av typen String](assets/variable_create_string_new.png)

   Upprepa steg 4 och 5 för att skapa följande variabler:

   * Faktureringsperiod: Strängtyp
   * Faktureringsdatum: Datumtyp

   ![Fakturainformation](assets/variable_bill_details_new.png)

1. Skapa statisk text för följande fält med den högra rutan:

   * Fakturanummer
   * Faktureringsperiod
   * Faktureringsdatum
   * Din plan

   ![Statisk text](assets/variable_bill_details_static_text_new.png)

1. Placera markören bredvid **Fakturanummer** och dubbelklicka på **Fakturanummer** variabel från **Variabler** i den vänstra rutan.
1. Placera markören bredvid **Faktureringsperiod** och dubbelklicka på **Faktureringsperiod** variabel.
1. Placera markören bredvid **Faktureringsdatum** och dubbelklicka på **Faktureringsdatum** variabel.
1. Välj **Datamodellsobjekt** i den vänstra rutan.
1. Placera markören bredvid **Din plan** och dubbelklicka på **kund** > **kundplan** -egenskap.

   ![Bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Klicka **Spara** om du vill skapa textdokumentfragmentet med faktureringsinformation.

## Steg 2: Skapa textdokumentfragment för kundinformation {#step-create-customer-details-text-document-fragment}

Dokumentfragmentet Kundinformation innehåller följande fält:

| Fält | Datakälla |
|---|---|
| Kundnamn | Formulärdatamodell |
| Adress | Formulärdatamodell |
| Leveransort | Agentgränssnitt |
| Statuskod | Agentgränssnitt |
| Mobilnummer | Formulärdatamodell |
| Alternativt kontaktnummer | Formulärdatamodell |
| Relationsnummer | Formulärdatamodell |
| Antal anslutningar | Agentgränssnitt |

Utför följande steg för att skapa variabler för fält med användargränssnittet för agent som datakälla, skapa statisk text och använda formulärdatamodellelement i dokumentfragmentet:

1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Document Fragments]**.
1. Välj **Skapa** > **Text**.
1. Ange följande information:

   1. Retur **customer_details_first_ic** som namnet i **Titel** fält. Titeln fylls i automatiskt i **Namn** fält.

   1. Välj **Formulärdatamodell** från **Datamodell** -avsnitt.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck **Välj**.

   1. Tryck **Nästa**.

1. Välj **Variabler** i den vänstra rutan och tryck på **Skapa**.
1. I **Skapa variabel** avsnitt:

   1. Retur **Placesupply** som namnet på variabeln.
   1. Välj **Sträng** som typ.
   1. Tryck **Skapa**.

   Upprepa steg 4 och 5 för att skapa följande variabler:

   * Statskod: Nummertyp
   * Nummeranslutningar: Nummertyp


1. Välj **Datamodellsobjekt** placerar du markören i den högra rutan och dubbelklickar på **kund** > **name** -egenskap.
1. Tryck på Retur för att flytta markören till nästa rad och dubbelklicka på **kund** > **adress** -egenskap.
1. Skapa statisk text för följande fält med den högra rutan:

   * Mobilnummer
   * Alternativt kontaktnummer
   * Leveransort
   * Relationsnummer
   * Statuskod
   * Antal anslutningar

   ![Statisk text för kundinformation](assets/customer_details_static_text_new.png)

1. Placera markören bredvid **Mobilnummer** och dubbelklicka på **kund** > **mobilenum** -egenskap.
1. Placera markören bredvid **Alternativt kontaktnummer** och dubbelklicka på** kund** > **alternatemobilenumber** -egenskap.
1. Placera markören bredvid **Relationsnummer** och dubbelklicka på **kund** > **relationsnummer** -egenskap.
1. Välj **Variabler** placerar du markören bredvid **Leveransort** och dubbelklicka på **Placesupply** variabel.
1. Placera markören bredvid **Statuskod** och dubbelklicka på **Statskod** variabel.
1. Placera markören bredvid **Antal anslutningar** och dubbelklicka på **Nummeranslutningar** variabel.

   ![Kundinformation](assets/customer_details_df2_new.png)

1. Klicka **Spara** för att skapa textdokumentfragmentet Kundinformation.

## Steg 3: Skapa textdokumentfragment för fakturasammanfattning {#step-create-bill-summary-text-document-fragment}

Dokumentfragmentet Faktureringssammanfattning innehåller följande fält:

| Fält | Datakälla |
|---|---|
| Föregående saldo | Agentgränssnitt |
| Betalningar | Agentgränssnitt |
| Justeringar | Agentgränssnitt |
| Aktuell faktureringsperiod för avgifter | Formulärdatamodell |
| Belopp att betala | Agentgränssnitt |
| Förfallodatum | Agentgränssnitt |

Utför följande steg för att skapa variabler för fält med användargränssnittet för agent som datakälla, skapa statisk text och använda formulärdatamodellelement i dokumentfragmentet:

1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Document Fragments]**.
1. Välj **Skapa** > **Text**.
1. Ange följande information:

   1. Retur **Bill_summary_first_ic** som namnet i **Titel** fält. Titeln fylls i automatiskt i **Namn** fält.

   1. Välj **Formulärdatamodell** från **Datamodell** -avsnitt.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck **Välj**.

   1. Tryck **Nästa**.

1. Välj **Variabler** i den vänstra rutan och tryck på **Skapa**.
1. I **Skapa variabel** avsnitt:

   1. Retur **Förhandsbalans** som namnet på variabeln.
   1. Välj **Nummer** som typ.
   1. Tryck **Skapa**.

   Upprepa steg 4 och 5 för att skapa följande variabler:

   * Betalningar: Nummertyp
   * Justeringar: Nummertyp
   * Belopp: Nummertyp
   * Duedat: Datumtyp


1. Skapa statisk text för följande fält med den högra rutan:

   * Föregående saldo
   * Betalningar
   * Justeringar
   * Aktuell faktureringsperiod för avgifter
   * Belopp att betala
   * Förfallodatum
   * Sena betalningsavgifter efter förfallodatumet är $ 20

   ![Statisk text i fakturasammanfattning](assets/bill_summary_static_new.png)

1. Placera markören bredvid **Föregående saldo** och dubbelklicka på **Förhandsbalans** variabel.
1. Placera markören bredvid **Betalningar** och dubbelklicka på **Betalningar** variabel.
1. Placera markören bredvid **Justeringar** och dubbelklicka på **Justeringar** variabel.
1. Placera markören bredvid **Belopp att betala** och dubbelklicka på **Belopp som förfaller** variabel.
1. Placera markören bredvid **Förfallodatum** och dubbelklicka på **Duedate** variabel.
1. Välj **Datamodellsobjekt** placerar du markören bredvid **Aktuell faktureringsperiod för avgifter** i den högra rutan och dubbelklicka på **växlar** > **usagecharges** -egenskap.

   ![Sammanfattning av faktura](assets/bill_summary_static_variables_new.png)

1. Klicka **Spara** för att skapa textdokumentfragmentet Kundinformation.

## Steg 4: Skapa sammanfattning av dokumentfragment för avgiftstext {#step-create-summary-of-charges-text-document-fragment}

Dokumentfragmentet Sammanfattning av avgifter innehåller följande fält:

| Fält | Datakälla |
|---|---|
| samtalsavgifter | Formulärdatamodell |
| Konferenssamtalsavgifter | Formulärdatamodell |
| SMS-avgifter | Formulärdatamodell |
| Mobila internetavgifter | Formulärdatamodell |
| National Roaming Charts | Formulärdatamodell |
| Internationella roamingavgifter | Formulärdatamodell |
| Avgifter för värdeökade tjänster | Formulärdatamodell |
| Totala avgifter | Formulärdatamodell |
| TOTALT BETALNINGSBART | Formulärdatamodell |

Utför följande steg för att skapa statisk text och använda modellelement för formulärdata i dokumentfragmentet:

1. Välj **[!UICONTROL Forms]** > **[!UICONTROL Document Fragments]**.
1. Välj **Skapa** > **Text**.
1. Ange följande information:

   1. Retur **summary_addas_first_ic** som namnet i **Titel** fält. Titeln fylls i automatiskt i namnfältet.

   1. Välj **Formulärdatamodell** från **Datamodell** -avsnitt.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck **Välj**.

   1. Tryck **Nästa**.

1. Skapa statisk text för följande fält med den högra rutan:

   * samtalsavgifter
   * Konferenssamtalsavgifter
   * SMS-avgifter
   * Mobila internetavgifter
   * National Roaming Charts
   * Internationella roamingavgifter
   * Avgifter för värdeökade tjänster
   * Totala avgifter
   * TOTALT BETALNINGSBART

   ![Sammanfattningsavgifter](assets/summary_charges_static_new.png)

1. Välj **Datamodellsobjekt** -fliken.
1. Placera markören bredvid **samtalsavgifter** och dubbelklicka på **växlar** > **callCharts** -egenskap.
1. Placera markören bredvid **Konferenssamtalsavgifter** och dubbelklicka på **växlar** > **sammandragande** -egenskap.
1. Placera markören bredvid **SMS-avgifter** och dubbelklicka på **växlar** > **smscharges** -egenskap.
1. Placera markören bredvid **Mobila internetavgifter** och dubbelklicka på **växlar** > **internetavgifter** -egenskap.
1. Placera markören bredvid **National Roaming Charts** och dubbelklicka på **växlar** > **roamingnationell** -egenskap.
1. Placera markören bredvid **Internationella roamingavgifter** och dubbelklicka på **växlar** > **roamingInl** -egenskap.
1. Placera markören bredvid **Avgifter för värdeökade tjänster** och dubbelklicka på **växlar** > **arbetsyta** -egenskap.
1. Placera markören bredvid **Totala avgifter** och dubbelklicka på **växlar** > **usagecharges** -egenskap.
1. Placera markören bredvid **TOTALT BETALNINGSBART** och dubbelklicka på **växlar** > **usagecharges** -egenskap.

   ![Sammanfattning av avgifter](assets/summary_charges_static_fdm_new.png)

1. Markera texten i **Avgifter för värdeökade tjänster** rad och knacka **Skapa regel** om du vill skapa ett villkor baserat på vilket raden visas i det interaktiva meddelandet:
1. På **Skapa regel** popup-fönster:

   1. Välj **Datamodeller och variabler** och sedan **växlar** > **callCharts**.

   1. Välj **är mindre än** som -operatorn.
   1. Välj **Nummer** och ange värdet som **60**.

   Baserat på det här villkoret visas raden Värdetillägg för avgifter endast om värdet för fältet Anropsavgifter är mindre än 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Klicka **Spara** för att skapa dokumentfragmentet Sammanfattning av avgifter.
