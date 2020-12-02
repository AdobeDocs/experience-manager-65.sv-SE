---
title: '"Självstudiekurs: Skapa dokumentfragment"'
seo-title: Skapa dokumentfragment för interaktiv kommunikation
description: Skapa dokumentfragment för interaktiv kommunikation
seo-description: Skapa dokumentfragment för interaktiv kommunikation
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
translation-type: tm+mt
source-git-commit: e545fc5e2ea139bd8ebb7f84138ba68e03d71d19
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---


# Självstudiekurs: Skapa dokumentfragment{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Den här självstudiekursen är ett steg i [Skapa din första serie med interaktiv kommunikation](/help/forms/using/create-your-first-interactive-communication.md). Vi rekommenderar att du följer serien i kronologisk ordning för att förstå, utföra och demonstrera det fullständiga exemplet på självstudiekurser.

Dokumentfragment är återanvändbara komponenter i en korrespondens som används för att skapa en interaktiv kommunikation. Dokumentfragmenten är av följande typer:

* Text - En textresurs är en del av innehållet som består av ett eller flera textstycken. Ett stycke kan vara statiskt eller dynamiskt.
* List - List är en grupp dokumentfragment, inklusive text, listor, villkor och bilder.
* Villkor - Med villkor kan du definiera vilket innehåll som ska tas med i den interaktiva kommunikationen baserat på data som tas emot från formulärdatamodellen.

I den här självstudiekursen får du hjälp med att skapa flera textdokumentfragment baserat på anatomin i [Planera avsnittet Interaktiv kommunikation](/help/forms/using/planning-interactive-communications.md). I slutet av den här självstudiekursen kan du:

* Skapa dokumentfragment
* Skapa variabler
* Skapa och tillämpa regler

![text_document_fragments](assets/text_document_fragments.gif)

Här följer en lista över dokumentfragment som har skapats i den här självstudiekursen:

* [Fakturainformation](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Kundinformation](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Sammanfattning av faktura](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Sammanfattning av avgifter](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Varje dokumentfragment innehåller fält med statisk text, data som tagits emot från formulärdatamodellen och data som matats in med agentens användargränssnitt. Alla dessa fält har beskrivits i avsnittet [Planera interaktiv kommunikation](/help/forms/using/planning-interactive-communications.md).

När du skapar dokumentfragment i den här självstudiekursen skapas variabler för fält som tar emot data med hjälp av agentens användargränssnitt.

Använd **FDM_Create_First_IC**, enligt beskrivningen i [Skapa formulärdatamodell](../../forms/using/create-form-data-model0.md), som formulärdatamodell för att skapa dokumentfragment i den här självstudien.

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

   1. Ange **Bill_details_first_ic** som namn i fältet **Title**. Titeln fylls i automatiskt i fältet **Namn**.

   1. Välj **Formulärdatamodell** i avsnittet **Datamodell**.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck på **Välj**.

   1. Tryck på **Nästa**.

1. Välj fliken **Variabler** i den vänstra rutan och tryck på **Skapa**.
1. I avsnittet **Skapa variabel**:

   1. Ange **fakturanummer** som namn på variabeln.
   1. Välj **Sträng** som typ.
   1. Tryck på **Skapa**.

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

1. Placera markören bredvid fältet **Fakturanr** och dubbelklicka på variabeln **InvoiceNumber** på fliken **Variabler** i den vänstra rutan.
1. Placera markören bredvid fältet **Faktureringsperiod** och dubbelklicka på variabeln **Faktureringsperiod**.
1. Placera markören bredvid fältet **Faktureringsdatum** och dubbelklicka på variabeln **Faktureringsdatum**.
1. Välj fliken **Datamodellobjekt** i den vänstra rutan.
1. Placera markören bredvid fältet **Din plan** och dubbelklicka på egenskapen **customer** > **kundplan**.

   ![Bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Klicka på **Spara** för att skapa textdokumentfragmentet med faktureringsinformation.

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

   1. Ange **customer_details_first_ic** som namn i fältet **Title**. Titeln fylls i automatiskt i fältet **Namn**.

   1. Välj **Formulärdatamodell** i avsnittet **Datamodell**.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck på **Välj**.

   1. Tryck på **Nästa**.

1. Välj fliken **Variabler** i den vänstra rutan och tryck på **Skapa**.
1. I avsnittet **Skapa variabel**:

   1. Ange **Placesupply** som namn på variabeln.
   1. Välj **Sträng** som typ.
   1. Tryck på **Skapa**.

   Upprepa steg 4 och 5 för att skapa följande variabler:

   * Statskod: Nummertyp
   * Nummeranslutningar: Nummertyp


1. Välj fliken **Datamodellsobjekt**, placera markören i den högra rutan och dubbelklicka på egenskapen **customer** > **name**.
1. Tryck på Retur för att flytta markören till nästa rad och dubbelklicka på egenskapen **customer** > **address**.
1. Skapa statisk text för följande fält med den högra rutan:

   * Mobilnummer
   * Alternativt kontaktnummer
   * Leveransort
   * Relationsnummer
   * Statuskod
   * Antal anslutningar

   ![Statisk text för kundinformation](assets/customer_details_static_text_new.png)

1. Placera markören bredvid fältet **Mobilnummer** och dubbelklicka på egenskapen **customer** > **mobilenum**.
1. Placera markören bredvid fältet **Alternativt kontaktnummer** och dubbelklicka på egenskapen** kund** > **alternateNummer**.
1. Placera markören bredvid fältet **Relationsnummer** och dubbelklicka på egenskapen **customer** > **relationsnummer**.
1. Välj fliken **Variabler**, placera markören bredvid fältet **Leveransort** och dubbelklicka på variabeln **Placesupply**.
1. Placera markören bredvid fältet **Statskod** och dubbelklicka på variabeln **Statskod**.
1. Placera markören bredvid fältet **Antal anslutningar** och dubbelklicka på variabeln **Numberconnections**.

   ![Kundinformation](assets/customer_details_df2_new.png)

1. Klicka på **Spara** för att skapa textdokumentfragmentet Kundinformation.

## Steg 3: Skapa dokumentfragment för fakturasammanfattning {#step-create-bill-summary-text-document-fragment}

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

   1. Ange **Bill_summary_first_ic** som namn i fältet **Title**. Titeln fylls i automatiskt i fältet **Namn**.

   1. Välj **Formulärdatamodell** i avsnittet **Datamodell**.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck på **Välj**.

   1. Tryck på **Nästa**.

1. Välj fliken **Variabler** i den vänstra rutan och tryck på **Skapa**.
1. I avsnittet **Skapa variabel**:

   1. Ange **Förhandsbalans** som namn på variabeln.
   1. Välj **Number** som typ.
   1. Tryck på **Skapa**.

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

1. Placera markören bredvid fältet **Föregående balans** och dubbelklicka på variabeln **Föregående balans**.
1. Placera markören bredvid fältet **Betalningar** och dubbelklicka på variabeln **Betalningar**.
1. Placera markören bredvid fältet **Justeringar** och dubbelklicka på variabeln **Justeringar**.
1. Placera markören bredvid fältet **Belopp att betala** och dubbelklicka på variabeln **Belopp**.
1. Placera markören bredvid fältet **Förfallodatum** och dubbelklicka på variabeln **Duplicera**.
1. Välj fliken **Datamodellsobjekt**, placera markören bredvid fältet **Aktuell faktureringsperiod** i den högra rutan och dubbelklicka på egenskapen **växlar** > **avgifter**.

   ![Sammanfattning av faktura](assets/bill_summary_static_variables_new.png)

1. Klicka på **Spara** för att skapa textdokumentfragmentet Kundinformation.

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

   1. Ange **summary_addas_first_ic** som namn i fältet **Title**. Titeln fylls i automatiskt i namnfältet.

   1. Välj **Formulärdatamodell** i avsnittet **Datamodell**.

   1. Välj **FDM_Create_First_IC** som formulärdatamodell och tryck på **Välj**.

   1. Tryck på **Nästa**.

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

1. Välj fliken **Datamodellsobjekt**.
1. Placera markören bredvid fältet **Anropsavgifter** och dubbelklicka på egenskapen **Bill** > **Anrop**.
1. Placera markören bredvid fältet **Konferenssamtalsavgifter** och dubbelklicka på egenskapen **växlar** > **sammandragsavgifter**.
1. Placera markören bredvid fältet **SMS Charges** och dubbelklicka på egenskapen **Bill** > **smscharges**.
1. Placera markören bredvid fältet **Mobile Internet Charges** och dubbelklicka på egenskapen **Bill** > **internetaddar**.
1. Placera markören bredvid fältet **Nationella avgifter för nätverksväxling** och dubbelklicka på egenskapen **växlar** > **nationella**.
1. Placera markören bredvid fältet **International Roaming Charges** och dubbelklicka på egenskapen **Bill** > **RoamingInl**.
1. Placera markören bredvid fältet **Värdetillägg för avgifter** och dubbelklicka på egenskapen **växlar** > **arbetsyta**.
1. Placera markören bredvid fältet **Totalavgifter** och dubbelklicka på egenskapen **växlar** > **användaravgifter**.
1. Placera markören bredvid fältet **TOTAL PAYABLE** och dubbelklicka på egenskapen **Bill** > **usagecharges**.

   ![Sammanfattning av avgifter](assets/summary_charges_static_fdm_new.png)

1. Markera texten i raden **Värdetillägg för avgifter** och tryck på **Skapa regel** för att skapa ett villkor som baseras på raden som visas i det interaktiva meddelandet:
1. I popup-fönstret **Skapa regel**:

   1. Välj **Datamodeller och variabler** och sedan **växlar** > **avgifter**.

   1. Välj **är mindre än** som operator.
   1. Välj **Number** och ange värdet som **60**.

   Baserat på det här villkoret visas raden Värdetillägg för avgifter endast om värdet för fältet Anropsavgifter är mindre än 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Klicka på **Spara** för att skapa dokumentfragmentet Sammanfattning av avgifter.
