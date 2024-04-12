---
title: Rikta din Adobe Campaign
description: Ni kan skapa riktade upplevelser för Adobe Campaign efter att ha skapat segmentering.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# Rikta in er på Adobe Campaign{#targeting-your-adobe-campaign}

Om du vill använda ditt Adobe Campaign-nyhetsbrev måste du först skapa segmentering, som bara är tillgängligt i det klassiska användargränssnittet (för klientkontext). Efter det kan ni skapa riktade upplevelser för Adobe Campaign. Båda beskrivs i det här avsnittet.

## Ställ in segmentering i AEM {#setting-up-segmentation-in-aem}

Om du vill ställa in segmentering måste du använda det klassiska användargränssnittet för att ställa in segmenten. De återstående stegen kan utföras i standardgränssnittet.

Att skapa segmentering innefattar att skapa segment, ett varumärke, en kampanj och upplevelser.

>[!NOTE]
>
>Segment-ID måste mappas till det på Adobe Campaign-sidan.

### Skapa segment {#creating-segments}

Så här skapar du segment:

1. Öppna [segmenteringskonsol](http://localhost:4502/miscadmin#/etc/segmentation) på **&lt;host>:&lt;port>/miscadmin#/etc/segmentering**.
1. Skapa en sida och ange en rubrik, till exempel **AC-segment**- och väljer **Segment (Adobe Campaign)** mall.
1. Markera den skapade sidan i trädvyn till vänster.
1. Skapa till exempel ett segment som riktar sig till manliga användare genom att skapa en sida under segmentet som du skapade som kallas hane och markera **Segment (Adobe Campaign)** mall.
1. Öppna den skapade segmentsidan och dra och släpp en **Segment-ID** från sidosparken till sidan.
1. Dubbelklicka på trait och ange det ID som i det här fallet representerar det manliga segment som definieras i Adobe Campaign, till exempel **MALE** - och klicka **OK**. Följande meddelande ska visas: *`targetData.segmentCode == "MALE"`*
1. Upprepa stegen för ett annat segment, till exempel ett segment som riktar sig till kvinnliga användare.

### Skapa ett varumärke {#creating-a-brand}

Så här skapar du ett varumärke:

1. I **Webbplatser**, navigera till **Kampanjer** mapp (till exempel i We.Retail).
1. Klicka **Skapa sida** och ange en rubrik för sidan, till exempel We.Retail Brand och välj **Varumärke** mall.

### Skapa en kampanj {#creating-a-campaign}

Skapa en kampanj:

1. Öppna **Varumärke** sida som du skapade.
1. Klicka **Skapa sida** och ange en rubrik för sidan, till exempel We.Retail Campaign, och välj **Campaign** mall och klicka på **Skapa**.

### Skapa upplevelser {#creating-experiences}

Så här skapar du upplevelser för segment:

1. Öppna **Campaign** sida som du skapade.
1. Skapa upplevelser för era segment genom att klicka **Skapa sida** och ange en rubrik för sidan, t.ex. Handla när du skapar en upplevelse för manligt segment, och välj **Upplevelse** mall.
1. Öppna den skapade Experience-sidan.
1. Klicka **Redigera** och sedan under Segment klickar du **Lägg till objekt**.
1. Ange sökvägen till det manliga segmentet, till exempel **/etc/segmentation/ac-segments/man** och klicka **OK**. Följande meddelande ska visas: *Upplevelsen är inriktad på: man*
1. Upprepa föregående steg för att skapa en upplevelse för alla segment, till exempel kvinnligt mål.

## Skapa ett nyhetsbrev med riktat innehåll {#creating-a-newsletter-with-targeted-content}

När ni har skapat segment, varumärken, kampanjer och upplevelser kan ni skapa ett nyhetsbrev med riktat innehåll. När ni har skapat upplevelsen länkar ni upplevelser till era segment.

>[!NOTE]
>
>[E-postexempel är bara tillgängliga i Geometrixx](/help/sites-developing/we-retail.md). Hämta exempelinnehåll för Geometrixx från paketresurs.

Så här skapar du ett nyhetsbrev med riktat innehåll:

1. Skapa ett nyhetsbrev med riktat innehåll: Klicka nedan på E-postkampanjer i Geometrixx Outdoors **Skapa** > **Sida** och välj en av Adobe Campaign Mail-mallarna.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Lägg till en text- och personaliseringskomponent i nyhetsbrevet.
1. Lägg till text i komponenten Text och Personalization, till exempel&quot;This is the default&quot;.
1. Klicka på pilen bredvid **Redigera** och markera **Målinriktning**.
1. Välj ert varumärke i den nedrullningsbara menyn Varumärke och välj er kampanj. (Detta är varumärket och kampanjen som du skapade tidigare).
1. Klicka **Börja målinrikta**. Dina segment visas i området Publiker. Standardupplevelsen används om inget av de definierade segmenten matchar.

   >[!NOTE]
   >
   >Som standard använder de e-postexempel som ingår i AEM Adobe Campaign som målmotor. För anpassade nyhetsbrev kan du behöva välja Adobe Campaign som målmotor. När du väljer mål klickar du på + i verktygsfältet, anger en rubrik för den nya aktiviteten och väljer **Adobe Campaign** som målinriktningsmotor.

1. Klicka **Standard** och sedan komponenten Text och Personalization som du har lagt till så ser du Bullseye med en pil. Klicka på ikonen om du vill ange komponenten som mål.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Navigera till ett annat segment (man) och klicka på **Lägg till erbjudande** och klicka på plusikonen +. Redigera sedan erbjudandet.
1. Navigera till ett annat segment (Kvinna) och klicka **Lägg till erbjudande** och plusikonen +. Redigera sedan erbjudandet.
1. Klicka **Nästa** för att se Mappning, klicka sedan på **Nästa** om du vill visa inställningar som inte gäller för Adobe Campaign, och klicka på **Spara**.

   AEM genererar automatiskt rätt målinriktningskod för Adobe Campaign när innehållet används i en leverans inom Adobe Campaign

1. Skapa leveransen i Adobe Campaign - välj **E-postleverans med AEM innehåll** och välj det lokala AEM och bekräfta dina ändringar.

   I HTML-vyn omges de olika upplevelserna av målkomponenter av Adobe Campaign målkod.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Om du även ställer in segmenten i Adobe Campaign klickar du på **Förhandsgranska** visar upplevelserna för varje segment.
