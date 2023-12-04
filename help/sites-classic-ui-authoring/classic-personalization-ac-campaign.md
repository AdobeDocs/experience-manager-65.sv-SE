---
title: Arbeta med Adobe Campaign 6.1 och Adobe Campaign Standard
description: Du kan skapa e-postinnehåll i AEM och bearbeta det i Adobe Campaign e-postmeddelanden.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 2%

---

# Arbeta med Adobe Campaign 6.1 och Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

Du kan skapa e-postinnehåll i AEM och bearbeta det i Adobe Campaign e-postmeddelanden. Om du vill göra det måste du:

1. Skapa ett nyhetsbrev i AEM från en Adobe Campaign-specifik mall.
1. Välj [en Adobe Campaign-tjänst](#selectingtheadobecampaigncloudservice) innan du redigerar innehållet för att få tillgång till alla funktioner.
1. Redigera innehållet.
1. Validera innehållet.

Innehållet kan sedan synkas med en leverans i Adobe Campaign. Detaljerade instruktioner beskrivs i det här dokumentet.

>[!NOTE]
>
>Innan du kan använda den här funktionen måste du konfigurera AEM att integrera med [Adobe Campaign](/help/sites-administering/campaignonpremise.md) eller [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Skicka e-postinnehåll via Adobe Campaign {#sending-email-content-via-adobe-campaign}

När du har konfigurerat AEM och Adobe Campaign kan du skapa e-postleveransinnehåll direkt i AEM och sedan bearbeta det i Adobe Campaign.

När du skapar Adobe Campaign-innehåll i AEM måste du länka till en Adobe Campaign-tjänst innan du redigerar innehållet för att få tillgång till alla funktioner.

Det finns två möjliga fall:

* Innehållet kan synkas med en leverans från Adobe Campaign. På så sätt kan du använda AEM innehåll i en leverans.
* (Endast Adobe Campaign lokalt) Innehållet kan skickas direkt till Adobe Campaign, som automatiskt genererar en ny e-postleverans. Det här läget har begränsningar.

Detaljerade instruktioner beskrivs i det här dokumentet.

### Skapa nytt e-postinnehåll {#creating-new-email-content}

>[!NOTE]
>
>När du lägger till e-postmallar ska du se till att lägga till dem under **/content/campaign** för att göra dem tillgängliga.
>

1. AEM väljer du **Webbplatser** bläddra sedan i utforskaren för att hitta var era e-postkampanjer hanteras. I följande exempel är den berörda noden **Webbplatser** > **Kampanjer** > **Geometrixx Outdoors** > **E-postkampanjer**.

   >[!NOTE]
   >
   >[E-postexempel är bara tillgängliga i Geometrixx](/help/sites-developing/we-retail.md#weretail). Hämta exempelinnehåll för Geometrixx från paketresurs.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Välj **Nytt** > **Ny sida** för att skapa nytt e-postinnehåll.
1. Välj en av de tillgängliga mallarna för Adobe Campaign och fyll sedan i de allmänna egenskaperna för sidan. Tre mallar är tillgängliga som standard:

   * **Adobe Campaign Email (AC 6.1)**: gör att du kan lägga till innehåll i en fördefinierad mall innan du skickar den till Adobe Campaign 6.1 för leverans.
   * **Adobe Campaign Email (ACS)**: gör att du kan lägga till innehåll i en fördefinierad mall innan du skickar den till Adobe Campaign Standard för leverans.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Klicka **Skapa** för att skapa e-post eller nyhetsbrev.

### Välja molntjänst och mall för Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Om du vill integrera med Adobe Campaign måste du lägga till en molntjänst från Adobe Campaign på sidan. Om du gör det får du tillgång till personalisering och annan Adobe Campaign-information.

Dessutom kan du behöva välja Adobe Campaign-mallen, ändra ämnet och lägga till oformaterad text för användare som inte vill visa e-postmeddelandet i HTML.

1. Välj **Sida** -fliken i sidosparken och sedan väljer **Sidegenskaper.**
1. I **Molntjänster** i popup-fönstret väljer du **Lägg till tjänst** för att lägga till tjänsten Adobe Campaign och klicka på **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Välj den konfiguration som matchar din Adobe Campaign-instans i listrutan och klicka sedan på **OK**.

   >[!NOTE]
   >
   >Var noga med att klicka **OK** eller **Använd** efter att du lagt till molntjänsten. Detta aktiverar **Adobe Campaign** för att fungera.

1. Om du vill använda en särskild e-postleveransmall (från Adobe Campaign), annan än standardmallen **mail** mall, välja **Sidegenskaper** igen. I **Adobe Campaign** anger du e-postleveransmallens interna namn i den relaterade Adobe Campaign-instansen.

   I Adobe Campaign Standard är mallen **Leverera med AEM**. I Adobe Campaign 6.1 är mallen **E-postleverans med AEM innehåll**.

   När du väljer en mall aktiveras AEM automatiskt **Adobe Campaign Newsletter** -komponenter.

### Redigera e-postinnehåll {#editing-email-content}

Du kan redigera e-postinnehåll antingen i det klassiska användargränssnittet eller i det pekoptimerade användargränssnittet.

1. Ange ämne och textversion för e-postmeddelandet genom att markera **Sidegenskaper** > **E-post** från verktygslådan.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Redigera e-postinnehåll genom att lägga till de element du vill ha från de som finns i sidosparken. Det gör du genom att dra och släppa dem. Dubbelklicka sedan på det element som du vill redigera.

   Du kan till exempel lägga till text som innehåller anpassningsfält.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Se [Adobe Campaign Components](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) om du vill ha en beskrivning av de komponenter som finns för Adobe Campaign nyhetsbrev/e-postkampanjer.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Infogar personalisering {#inserting-personalization}

När du redigerar innehåll kan du infoga:

* Adobe Campaign-kontextfält. Det här är fält som du kan infoga i texten och som anpassas efter mottagarens data (t.ex. förnamn, efternamn eller andra data i måldimensionen).
* Adobe Campaign personaliseringsblock. Detta är block med fördefinierat innehåll som inte är relaterat till mottagarens data, t.ex. en logotyp eller en länk till en spegelsida.

Se [Adobe Campaign Components](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) för en fullständig beskrivning av Campaign-komponenterna.

>[!NOTE]
>
>* Endast Adobe Campaign **Profiler** målgruppsdimensionen beaktas.
>* När egenskaper visas från **Webbplatser** har du inte åtkomst till Adobe Campaign kontextfält. Du kan komma åt dessa direkt från e-postmeddelandet när du redigerar.
>

1. Infoga en ny **Nyhetsbrev** > **Text och personalisering (kampanj)** -komponenten.
1. Öppna komponenten genom att dubbelklicka. The **Redigera** -fönstret har en funktion som gör att du kan infoga anpassningselementen.

   >[!NOTE]
   >
   >De tillgängliga kontextfälten motsvarar **Profiler** målgruppsdimensionen i Adobe Campaign.
   >
   >Se [Länka en AEM till ett Adobe Campaign-e-postmeddelande](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Välj **Klientkontext** på sidan för att testa personaliseringsfälten med hjälp av data i personprofilerna.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Ett fönster visas där du kan välja den person du vill använda. Anpassningsfälten ersätts automatiskt av data från den valda profilen.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Förhandsgranska ett nyhetsbrev {#previewing-a-newsletter}

Du kan förhandsgranska hur nyhetsbrevet kommer att se ut och förhandsgranska personaliseringen.

1. Öppna nyhetsbrevet som du vill förhandsgranska och klicka på Förhandsgranska (förstoringsglas) för att krympa sidbrytaren.
1. Klicka på en av ikonerna för e-postklienten för att se hur nyhetsbrevet ser ut i varje e-postklient.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Expandera sidosparken för att börja redigera igen.

### Godkänna innehåll i AEM {#approving-content-in-aem}

När innehållet är klart kan du starta godkännandeprocessen. Gå till **Arbetsflöde** och väljer **Godkänn för Adobe Campaign** arbetsflöde.

Det här färdiga arbetsflödet består av två steg: revision, godkännande eller revision och avvisande. Arbetsflödet kan dock utvidgas och anpassas till en mer komplex process.

![chlimage_1-182](assets/chlimage_1-182.png)

Om du vill godkänna innehåll för Adobe Campaign tillämpar du arbetsflödet genom att välja **Arbetsflöde** i sidosparken och välja **Godkänn för Adobe Campaign** och klicka **Starta arbetsflöde**. Gå igenom stegen och godkänn innehållet. Du kan också avvisa innehållet genom att markera **Avvisa** i stället för **Godkänn** i det sista arbetsflödessteget.

![chlimage_1-183](assets/chlimage_1-183.png)

När innehållet har godkänts visas det som godkänt i Adobe Campaign. E-postmeddelandet kan sedan skickas.

I Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

I Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>Ej godkänt innehåll kan synkroniseras med en leverans i Adobe Campaign, men leveransen kan inte utföras. Endast godkänt innehåll kan skickas via kampanjleveranser.

## Länka AEM med Adobe Campaign Standard och Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Se [Länka AEM med Adobe Campaign Standard och Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) under [Arbeta med Adobe Campaign 6.1 och Adobe Campaign Standard](/help/sites-authoring/campaign.md) i standarddokumentationen.
