---
title: Introduktion till formulärsekvenser i flera steg
seo-title: Introduktion till formulärsekvenser i flera steg
description: Med AEM Forms kan du definiera en sekvens av formulärpanel där du vill att användarna ska navigera och fylla i ett anpassat formulär.
seo-description: Med AEM Forms kan du definiera en sekvens av formulärpanel där du vill att användarna ska navigera och fylla i ett anpassat formulär.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619

---


# Introduktion till formulärsekvenser i flera steg{#introduction-to-multi-step-form-sequence}

Med adaptiva blanketter kan man enkelt skapa datainhämtning i flera steg. Den har inbyggt stöd för att skapa flera paneler och koppla ihop varje panel med olika navigeringsmönster. Formulärförfattare kan gruppera formulärfält i logiska avsnitt och representera en grupp som en panel. Den övergripande navigeringen mellan paneler styrs med hjälp av panellayouten. Författare kan välja att ordna paneler i olika layouter, t.ex. placera sekventiellt med guidelayouten eller på ett ad hoc-sätt med hjälp av fliklayouten. Mer information om panellayouter finns i [Layoutfunktioner i adaptiva formulär](../../forms/using/layout-capabilities-adaptive-forms.md).

I en typisk miljö för ifyllnad av formulär finns det fler steg än att bara hämta in data. En fullständig inlämning av formulär kan omfatta andra steg, som att signera formuläret digitalt, verifiera den information som fylls i formuläret, bearbeta betalningar och så vidare. Det skiljer sig från fall till fall.

Om ditt användningsfall föreskriver en uppsättning steg för datainhämtning eller om det finns bestämmelser som kräver att vissa steg följs, kan AEM Forms använda den gemensamma strukturen i alla formulär. Den medföljande implementeringen av formulärstrukturen definierar stegsekvensen för ett formulär. ![Exempel på en formulärsekvens i flera steg](assets/formpipeline.png)

Exempel på en formulärsekvens i flera steg

Låt oss ta ett exempel där du behöver skapa en sekvens för att fylla i, verifiera, signera och bekräfta ett formulär. Så här skapar du en sådan sekvens:

1. Definiera en formulärmall och lägg till en obligatorisk panel i den. Observera att det bör finnas en panel för varje steg i sekvensen. Du kan dock inkludera underpaneler inuti en panel.

   I det här exemplet kan vi lägga till följande paneler:

   * **Fyllning**: Den innehåller formulärfält för datainhämtning. Här kan du ta med kapslade underpaneler för att skapa avsnitt för olika typer av information, t.ex. personlig, familj, ekonomi osv.

   * **Verifiera**: Den innehåller komponenten **Verify** som kan användas i en XFA-baserad adaptiv form. Den information som hämtas på panelen Fyllning visas i skrivskyddat läge för verifiering.

   * **E-signatur**: Den innehåller **Sign** -komponenten som kan användas i ett XFA-baserat adaptivt formulär. den tillhandahåller följande signeringstjänster:

      * Adobe Document Cloud eSign-tjänster
      * (Borttagen) Klottsignatur
   * **Bekräftelse**: Den innehåller komponenten **Sammanfattning** som visar ett meddelande som bekräftar att formuläret skickas när en användare har signerat formuläret och når steget Bekräfta (Sammanfattning) i sekvensen. Författare kan konfigurera texten i komponenten Sammanfattning, visa ett tackmeddelande, visa en länk till den genererade PDF-filen och så vidare.


1. Välj layouten för rotpanelen som **[!UICONTROL guide]**.
1. Slutför de återstående stegen för att skapa formulärmallen. Mer information finns i [Skapa en anpassad adaptiv formulärmall](../../forms/using/custom-adaptive-forms-templates.md).

När du har definierat formulärsekvensen i formulärmallen kan du använda den för att skapa formulär som har den grundläggande strukturen definierad som sekvensen på plats, även om du alltid kan anpassa formuläret efter dina behov.

