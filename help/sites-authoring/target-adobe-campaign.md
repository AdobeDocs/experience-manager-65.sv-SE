---
title: Inrikta er på Adobe Campaign
seo-title: Inrikta er på Adobe Campaign
description: Du kan skapa riktade upplevelser för Adobe Campaign efter att ha konfigurerat segmentering
seo-description: Du kan skapa riktade upplevelser för Adobe Campaign efter att ha konfigurerat segmentering
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Inrikta er på Adobe Campaign{#targeting-your-adobe-campaign}

Om du vill skapa ett nyhetsbrev om Adobe Campaign måste du först skapa segmentering, som bara är tillgängligt i det klassiska användargränssnittet (för kundsammanhang). Efter det kan ni skapa målinriktade upplevelser för Adobe Campaign. Båda beskrivs i det här avsnittet.

## Ställa in segmentering i AEM {#setting-up-segmentation-in-aem}

Om du vill ställa in segmentering måste du använda det klassiska användargränssnittet för att ställa in segmenten. De återstående stegen kan utföras i standardgränssnittet.

Att skapa segmentering innefattar att skapa segment, ett varumärke, en kampanj och upplevelser.

>[!NOTE]
>
>Segment-ID måste mappas till det på Adobe Campaign-sidan.

### Skapa segment {#creating-segments}

Så här skapar du segment:

1. Öppna [segmenteringskonsolen](http://localhost:4502/miscadmin#/etc/segmentation) på **&lt;värd>:&lt;port>/miscadmin#/etc/segmentering**.
1. Skapa en ny sida och ange en titel - till exempel **AC-segment**- och välj mallen **Segment (Adobe Campaign)** .
1. Markera den skapade sidan i trädvyn till vänster.
1. Skapa ett segment, till exempel för manliga användare, genom att skapa en ny sida under segmentet som du skapade som kallas hane och välja mallen **Segment (Adobe Campaign)** .
1. Öppna den skapade segmentsidan och dra och släpp ett **segment-ID** från sidosparken på sidan.
1. Dubbelklicka på trait, ange det ID som representerar i det här fallet det manliga segment som definieras i Adobe Campaign - till exempel **MALE** - och klicka på **OK**. Följande meddelande ska visas: *`targetData.segmentCode == "MALE"`*
1. Upprepa stegen för ett annat segment, till exempel ett segment som riktar sig till kvinnliga användare.

### Skapa ett varumärke {#creating-a-brand}

Så här skapar du ett varumärke:

1. Gå till mappen **Campaigns** i **Sites** (till exempel i We.Retail).
1. Klicka på **Skapa sida** och ange en rubrik för sidan, till exempel We.Retail Brand och välj **Brand** -mallen.

### Skapa en kampanj {#creating-a-campaign}

Så här skapar du en kampanj:

1. Öppna sidan **Varumärke** som du nyss skapade.
1. Klicka på **Skapa sida** och ange en rubrik för sidan, till exempel We.Retail Campaign, och välj **Campaign** -mallen och klicka på **Skapa**.

### Skapa upplevelser {#creating-experiences}

Så här skapar du upplevelser för segment:

1. Öppna **Campaign** -sidan som du nyss skapade.
1. Skapa upplevelser för era segment genom att klicka på **Skapa sida** och ange en titel för sidan, till exempel&quot;Male&quot; när du skapar en upplevelse för&quot;Male&quot;-segmentet, och välj **Experience** -mallen.
1. Öppna den skapade Experience-sidan.
1. Klicka på **Redigera** och sedan under Segment klickar du på **Lägg till objekt**.
1. Ange sökvägen till det manliga segmentet, till exempel **/etc/segmentering/ac-segment/man** och klicka på **OK**. Följande meddelande ska visas: Upplevelsen *inriktas på följande: Man*
1. Upprepa föregående steg för att skapa en upplevelse för alla segment, till exempel kvinnligt mål.

## Skapa ett nyhetsbrev med riktat innehåll {#creating-a-newsletter-with-targeted-content}

När ni har skapat segment, varumärken, kampanjer och upplevelser kan ni skapa ett nyhetsbrev med riktat innehåll. När ni har skapat upplevelsen länkar ni upplevelser till era segment.

>[!NOTE]
>
>[E-postexempel är bara tillgängliga i Geometrixx](/help/sites-developing/we-retail.md). Hämta exempelinnehåll för Geometrixx från paketresurs.

Så här skapar du ett nyhetsbrev med riktat innehåll:

1. Skapa ett nyhetsbrev med riktat innehåll: Klicka eller tryck på **Skapa** > **Sida** och välj en av Adobe Campaign-e-postmallarna nedan för e-postkampanjer i Geometrixx Outdoor.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Lägg till en text- och personaliseringskomponent i nyhetsbrevet.
1. Lägg till text i komponenten Text och Personalization, till exempel&quot;This is the default&quot;.
1. Klicka på pilen bredvid **Redigera** och välj **Mål**.
1. Välj ert varumärke i den nedrullningsbara menyn Varumärke och välj er kampanj. (Detta är varumärket och kampanjen som du skapade tidigare).
1. Klicka på **Starta mål**. Dina segment visas i området Publiker. Standardupplevelsen används om inget av de definierade segmenten matchar.

   >[!NOTE]
   >
   >Som standard använder de e-postexempel som ingår i AEM Adobe Campaign som målmotor. För anpassade nyhetsbrev kan du behöva välja Adobe Campaign som målmotor. Vid målanpassning trycker eller klickar du på + i verktygsfältet, anger en titel för den nya aktiviteten och väljer **Adobe Campaign** som målmotor.

1. Klicka på **Standard** och sedan på komponenten Text och anpassning som du lade till så visas Bullseye med en pil. Klicka på ikonen om du vill ange komponenten som mål.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Navigera till ett annat segment (Man), klicka på **Lägg till erbjudande** och klicka på plusikonen +. Redigera sedan erbjudandet.
1. Navigera till ett annat segment (Kvinna) och klicka på **Lägg till erbjudande** och plustecknet +. Redigera sedan erbjudandet.
1. Klicka på **Nästa** för att se Mappning, klicka sedan på **Nästa** för att visa Inställningar, som inte gäller för Adobe Campaign, och klicka på **Spara**.

   AEM genererar automatiskt rätt målkod för Adobe Campaign när innehållet används i en leverans i Adobe Campaign

1. Skapa leveransen i Adobe Campaign - välj **E-postleverans med AEM-innehåll** och välj det lokala AEM-kontot, beroende på vad som är lämpligt, och bekräfta ändringarna.

   I HTML-vyn visas de olika upplevelserna av målkomponenter i målkoden för Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Om du även ställer in segmenten i Adobe Campaign kan du visa upplevelserna för varje segment genom att klicka på **Förhandsgranska** .

