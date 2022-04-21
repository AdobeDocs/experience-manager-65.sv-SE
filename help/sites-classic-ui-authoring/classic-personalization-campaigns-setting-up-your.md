---
title: Konfigurera kampanjen
seo-title: Setting up your campaign
description: För att skapa en ny kampanj måste ni skapa ett varumärke för era kampanjer, skapa en kampanj för upplevelser och slutligen definiera egenskaperna för den nya kampanjen.
seo-description: Setting up a new campaign requires creating a brand to hold your campaigns, creating a campaign to hold experiences, and finally defining the properties for your new campaign.
uuid: 244a150e-7b5e-4eff-bd15-e3b04be6a3e9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 19ad4751-1d5d-49de-b76b-3501b3e98e62
docset: aem65
exl-id: 1b607a52-f065-4e35-8215-d54df7c8403d
source-git-commit: a2623df38bcd683a6a43bdaf3483e11e40ac4a68
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 0%

---

# Konfigurera kampanjen{#setting-up-your-campaign}

I konfigurationen av en ny kampanj ingår följande (allmänna) steg:

1. [Skapa ett varumärke](#creating-a-new-brand) för era kampanjer.
1. Om det behövs kan du [definiera egenskaperna för ert nya varumärke](#defining-the-properties-for-your-new-brand).
1. [Skapa en kampanj](#creating-a-new-campaign) för upplevelser, till exempel teaser-sidor eller nyhetsbrev.
1. Om det behövs kan du [definiera egenskaperna för den nya kampanjen](#defining-the-properties-for-your-new-campaign).

Beroende på vilken typ av upplevelser du skapar måste du [skapa en upplevelse](#creating-a-new-experience). Hur upplevelsen ser ut och vilka åtgärder som följer efter att den har skapats beror på vilken typ av upplevelse du vill skapa:

* Om du skapar en Teaser:

   1. [Skapa en läroupplevelse](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience).
   1. [Lägg in material i teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser).
   1. [Skapa en kontaktyta för din Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (lägg till ditt suddgummi på en innehållssida).

* Om du skapar ett nyhetsbrev:

   1. [Skapa nyhetsbrev](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience).
   1. [Lägg till innehåll i nyhetsbrevet.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [Anpassa nyhetsbrevet.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [Skapa en engagerande startsida för nyhetsbrevet](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).
   1. [Skicka nyhetsbrevet](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) prenumeranter eller leads.

* Om du skapar ett Adobe Target-erbjudande (tidigare Test&amp;Target):

   1. [Skapa en upplevelse av Adobe Target-erbjudanden](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience).
   1. [Integrera med Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>Se [Segmentering](/help/sites-administering/campaign-segmentation.md) om du vill ha detaljerade anvisningar om hur du definierar segment.

## Skapa ett nytt varumärke {#creating-a-new-brand}

Så här skapar du ett nytt varumärke:

1. Öppna **MCM** och markera **Kampanjer** i den vänstra rutan.

1. Välj **Nytt...** för att ange **Titel** och **Namn** och mall som ska användas för ert nya varumärke:

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Klicka **Skapa**. Ditt nya varumärke kommer att visas i MCM (med en standardikon).

### Definiera egenskaperna för ditt nya varumärke {#defining-the-properties-for-your-new-brand}

1. Från **Kampanjer** i den vänstra rutan väljer du den nya varumärkesikonen i den högra rutan och klickar på **Egenskaper...**

   Du kan ange en **Titel**, **Beskrivning** och en bild som ska användas som ikon.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Klicka **OK** att spara.

### Skapa en ny kampanj {#creating-a-new-campaign}

Så här skapar du en ny kampanj:

1. Från **Kampanjer** markerar du ditt nya varumärke i den vänstra rutan eller dubbelklickar på ikonen i den högra rutan.

   Översikten visas (tom om varumärket är nytt).

1. Klicka **Nytt...** och ange **Titel**, **Namn** och mall som ska användas för din nya kampanj.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Klicka **Skapa**. Din nya kampanj visas i MCM.

### Definiera egenskaperna för din nya kampanj {#defining-the-properties-for-your-new-campaign}

Konfigurera kampanjegenskaper som styr beteendet:

* **Prioritet:** Den här kampanjens prioritet i förhållande till andra kampanjer. När flera kampanjer är aktiverade samtidigt styr kampanjen som har högst prioritet besökarupplevelsen.
* **På- och fråntid:** Dessa egenskaper styr tidsperioden när kampanjen styr besökarupplevelsen. Egenskapen On Time styr den tid då kampanjen börjar styra upplevelsen. Egenskapen Av-tid styr när kampanjerna slutar styra upplevelsen.
* **Bild:** Bilden som representerar kampanjen i AEM.
* **Cloud Services:** De Cloud Service som kampanjen är integrerad med. (Se [Integrera med Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md).)

* **Adobe Target:** Egenskaper som konfigurerar kampanjer som är integrerade med Adobe Target. (Se [Integrera med Adobe Target](/help/sites-administering/target.md).)

1. Från **Kampanjer**, välj ert varumärke. Välj kampanj i den högra rutan och klicka på **Egenskaper**.

   Du kan ange olika egenskaper, bland annat en **Titel**, **Beskrivning** och **Cloud Services** du vill ha.

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Klicka **OK** att spara.

### Skapa en ny upplevelse {#creating-a-new-experience}

Hur man skapar en ny upplevelse beror på vilken typ av upplevelse det är:

* [Skapa ett Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [Skapa ett nyhetsbrev](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [Skapa ett Adobe Target-erbjudande](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>Precis som i tidigare versioner är det fortfarande möjligt att skapa upplevelsen som en sida i **Webbplatser** konsol (och alla sådana sidor som skapats i tidigare versioner stöds fortfarande).
>
>Vi rekommenderar nu att du använder MCM för att skapa upplevelser.

### Konfigurera din nya upplevelse {#configuring-your-new-experience}

Nu när du har skapat det grundläggande skelettet för din upplevelse måste du fortsätta med följande åtgärder, beroende på vilken typ av upplevelse du har:

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers):

   * [Koppla ihop teaser-sidan med besökarsegment.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [Skapa en kontaktyta för din Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (lägg till ditt suddgummi på en innehållssida).

* [Nyhetsbrev](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters):

   * [Lägg till innehåll i nyhetsbrevet.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [Anpassa nyhetsbrevet.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [Skicka nyhetsbrevet](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) prenumeranter eller leads.
   * [Skapa en engagerande startsida för nyhetsbrevet](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).

* [Adobe Target-erbjudande](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers):

   * [Integrera med Adobe Target](/help/sites-administering/target.md)

### Lägga till en ny slutpunkt {#adding-a-new-touchpoint}

Om du har befintliga upplevelser kan du lägga till en kontaktyta direkt från kalendervyn i MCM:

1. Välj kalendervy för kampanjen.

1. Klicka **Lägg till kontaktpunkt..** för att öppna dialogrutan. Ange vilken upplevelse du vill lägga till:

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Klicka **OK** att spara.

## Arbeta med leads {#working-with-leads}

>[!NOTE]
>
>Adobe planerar inte att ytterligare förbättra denna funktion (Hantera leads).
>Rekommendationen är att [utnyttja Adobe Campaign och integrationen för att AEM](/help/sites-administering/campaign.md).

I AEM MCM kan du ordna och lägga till leads antingen genom att ange dem manuellt eller genom att importera en kommaseparerad lista, till exempel en utskickslista. Ytterligare sätt att generera leads är från nyhetsbrev eller communityregistreringar (om de är konfigurerade kan de utlösa ett arbetsflöde som fyller i leads).

Leads kategoriseras vanligtvis och placeras i en lista så att du senare kan utföra åtgärder i hela listan, till exempel skicka ut ett anpassat e-postmeddelande till en viss lista.

I Kontrollpanelen får du tillgång till alla leads genom att klicka på **Leads** från den vänstra rutan. Du kan även komma åt leads från **Listor** fönster.

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>Om du vill lägga till eller ändra avatarerna för användare öppnar du klickströmmolnet (Ctrl+Alt+c), läser in profilen och klickar på **Redigera**.

### Skapa nya leads {#creating-new-leads}

När du har skapat nya leads ska du se till att [aktivera dem](#activating-or-deactivating-leads) så att ni kan spåra deras aktivitet i publiceringsinstansen och personalisera deras upplevelse.

Så här skapar du en ny lead manuellt:

1. I AEM navigerar du till MCM. Klicka på **Leads**.
1. Klicka **Nytt**. The **Skapa nytt** öppnas.

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. Ange lämplig information i fälten. Klicka på **Adress** -fliken.

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. Ange adressinformation efter behov. Klicka **Spara** för att spara leadet. Om du behöver lägga till fler leads klickar du på **Spara och ny**.

   Det nya leadet visas i rutan Leads. När du klickar på posten visas all angiven information i den högra rutan. När du har skapat en lead kan du lägga till den i en lista.

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### Aktivera eller inaktivera leads {#activating-or-deactivating-leads}

Genom att aktivera leads kan ni spåra deras aktivitet i publiceringsinstansen och personalisera deras upplevelse. När du inte längre vill spåra deras aktivitet kan du inaktivera dem.

Till aktiva eller inaktiverade leads:

1. I AEM går du till MCM och klickar på **Leads**.

1. Markera leads som du vill aktivera eller inaktivera och klicka på **Aktivera** eller **Inaktivera**.

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   Precis som för AEM sidor anges publiceringsstatusen i **Publicerad** kolumn.

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### Importerar nya leads {#importing-new-leads}

När du importerar nya leads kan du automatiskt lägga till dem i en befintlig lista eller skapa en ny lista som inkluderar dessa leads.

Så här importerar du leads från en kommaavgränsad lista:

1. I AEM går du till MCM och klickar på **Leads**.

   >[!NOTE]
   >
   >Du kan också importera leads genom att göra något av följande:
   >
   >* Klicka på **Importera leads** i **Listor** fönster
   >* Klicka **Listor** och i **verktyg** meny, välja **Importera leads**.


1. I **verktyg** meny, välja **Importera** **Leads**.

1. Ange informationen enligt beskrivningen i Exempeldata. Följande fält kan importeras: e-post,familjenamn,givetNamn,kön,omMe,stad,land,telefonnummer,postnummer,region,gatuadress

   >[!NOTE]
   >
   >Den första raden i CSV-listan är fördefinierade etiketter som måste skrivas exakt som i exemplet:
   >
   >
   >`email,givenName,familyName` - om det skrivs som `givenname`systemet känner till exempel inte igen det.

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. Klicka på **Nästa**. Här förhandsgranskar du leads för att säkerställa att de är korrekta.

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. Klicka på **Nästa**. Välj den lista som du vill att leads ska tillhöra. Om du inte vill att de ska tillhöra en lista tar du bort informationen i fältet. Som standard skapar AEM ett listnamn som innehåller datum och tid. Klicka **Importera**.

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   Det nya leadet visas i rutan Leads. Om du klickar på posten visas all angiven information i den högra rutan. När du har skapat en lead kan du lägga till den i en lista.

### Lägga till leads i listor {#adding-leads-to-lists}

Så här lägger du till leads till befintliga listor:

1. Klicka på **Leads** för att visa alla tillgängliga leads.

1. Markera de leads som du vill lägga till i en lista genom att markera kryssrutan bredvid leadet. Du kan lägga till så många leads du vill.

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. I **verktyg** meny, välja **Lägg till i lista....** The **Lägg till i listan** öppnas.

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. Välj vilken lista du vill lägga till leads i och klicka på **OK**. leads läggs till i lämpliga listor.

### Visa leadinformation {#viewing-lead-information}

Om du vill visa lead-information klickar du i MCM-modulen på kryssrutan bredvid leadet och en höger ruta öppnas med all information om leadet, inklusive listtillhörighet.

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### Ändra befintliga leads {#modifying-existing-leads}

Så här ändrar du befintlig lead-information:

1. Klicka på **Leads**. I listan med leads markerar du kryssrutan bredvid det lead du vill redigera. All leadinformation visas i den högra rutan.

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >Du kan bara redigera en lead åt gången. Om du behöver ändra leads som ingår i samma lista kan du ändra listan i stället.

1. Klicka **Redigera**. The **Redigera lead** öppnas.

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. Redigera efter behov och klicka **Spara** för att spara ändringarna.

   >[!NOTE]
   >
   >Gå till användarprofilen om du vill ändra den ledande avataren. Du kan läsa in profilen i clickstream-molnet genom att trycka på CTRL+ALT+c och klicka på **Läs in** och sedan välja profilen.

### Tar bort befintliga leads {#deleting-existing-leads}

Om du vill ta bort befintliga leads i MCM markerar du kryssrutan bredvid leadet och klickar på **Ta bort**. Lead tas bort från leadlistan och alla associerade listor.

>[!NOTE]
>
>AEM bekräftar att du vill ta bort det befintliga leadet innan du tar bort det. När den har tagits bort kan den inte hämtas.

## Arbeta med listor {#working-with-lists}

>[!NOTE]
>
>Adobe planerar inte att ytterligare förbättra denna funktion (hantera listor).
>Rekommendationen är att [utnyttja Adobe Campaign och integrationen för att AEM](/help/sites-administering/campaign.md).

Med listor kan du ordna dina leads i grupper. Med listor kan ni inrikta era marknadsföringskampanjer på en viss grupp personer, till exempel kan ni skicka ett målinriktat nyhetsbrev till en lista. Listor visas i MCM-modulen, antingen på kontrollpanelen eller genom att klicka på **Listor**. Båda ger dig namnet på listan och antalet medlemmar.

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

Om du klickar **Listor** kan du även visa om listan är medlem i en annan lista och se en beskrivning.

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### Skapa nya listor {#creating-new-lists}

Så här skapar du en ny lista (grupp):

1. Klicka på **Ny lista ...** eller in **Listor**, klicka **Nytt** ... Fönstret Skapa lista öppnas.

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. Ange ett namn (obligatoriskt), en beskrivning och klicka på **Spara**. Listan visas i **Listor** fönster.

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### Ändra befintliga listor {#modifying-existing-lists}

Så här ändrar du en befintlig lista:

1. Klicka på **Listor**.

1. Markera kryssrutan bredvid listan som du vill redigera i listan och klicka på **Redigera**. The **Redigera lista** öppnas.

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >Du kan bara redigera en lista i taget.

1. Redigera efter behov och klicka **Spara** för att spara ändringarna.

### Tar bort befintliga listor {#deleting-existing-lists}

Om du vill ta bort befintliga listor markerar du kryssrutan intill listan i MCM och klickar på **Ta bort**. Listan tas bort. Leads som var kopplade till listan tas inte bort - bara kopplingen till listan tas bort.

>[!NOTE]
>
>AEM bekräftar att du vill ta bort de befintliga listorna innan du tar bort dem. När den har tagits bort kan den inte hämtas.

### Sammanfoga listor {#merging-lists}

Du kan sammanfoga en befintlig lista med en annan lista. När du gör detta blir den lista du sammanfogar medlem i den andra listan. Den finns fortfarande som en separat enhet och bör inte tas bort.

Du kan sammanfoga listor om du har samma konferens på två olika platser och vill sammanfoga dem i en deltagarlista över alla konferenser.

Så här sammanfogar du befintliga listor:

1. Klicka på **Listor**.

1. Markera den lista som du vill sammanfoga en annan lista med genom att markera kryssrutan bredvid den.

1. I **verktyg** meny, välja **Sammanfoga lista**.

   >[!NOTE]
   >
   >Du kan bara sammanfoga en lista i taget.

1. I **Sammanfoga lista** markerar du den lista som du vill sammanfoga med och klickar på **OK**.

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   Listan som du sammanfogade bör ökas med en medlem. Om du vill se att listan har sammanfogats markerar du listan som du har sammanfogat och i dialogrutan **verktyg** meny, välja **Visa leads**.

1. Upprepa steget tills du har sammanfogat alla listor som du vill ha.

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>Att ta bort en sammanfogad lista från dess medlemskap är detsamma som att ta bort en lead från en lista. Öppna **Listor** markerar du den lista som innehåller den sammanfogade listan och tar bort medlemskapet genom att klicka på den röda cirkeln bredvid listan.

### Visa leads i listor {#viewing-leads-in-lists}

Du kan när som helst visa vilka leads som hör till en viss lista genom att bläddra bland eller söka efter medlemmar.

Så här visar du leads som tillhör en lista:

1. Klicka på **Listor**.

1. Markera kryssrutan bredvid listan som du vill visa medlemmar för.

1. I **verktyg** meny, välja **Visa leads**. AEM visar leads som är medlemmar i den listan. Du kan bläddra igenom listan eller söka efter medlemmar.

   >[!NOTE]
   >
   >Du kan dessutom ta bort leads från en lista genom att markera dem och sedan klicka på **Ta bort medlemskap**.

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. Klicka **Stäng** för att återvända till MCM.
