---
title: Rapporter om användning och delning av resurser
description: Rapporterar om dina resurser i [!DNL Adobe Experience Manager Assets] som hjälper dig att förstå användningen, aktiviteten och delningen av dina digitala resurser.
contentOwner: AG
role: Affärsledare, administratör
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 9%

---


# Materialrapporter {#asset-reports}

Med tillgångsrapportering kan du utvärdera verktyget för din [!DNL Adobe Experience Manager Assets]-distribution. Med [!DNL Assets] kan du generera olika rapporter för dina digitala resurser. Rapporterna innehåller användbar information om hur ditt system används, hur användarna interagerar med resurser och vilka resurser som hämtas och delas.

Använd informationen i rapporterna för att ta fram nyckeltal för att mäta hur [!DNL Assets] används i ert företag och av era kunder.

I [!DNL Assets]-rapporteringsramverket används [!DNL Sling]-jobb för att asynkront bearbeta rapportbegäranden på ett ordnat sätt. Den kan skalas för stora databaser. Asynkron rapportbearbetning ökar effektiviteten och hastigheten med vilken rapporter genereras.

Rapporthanteringsgränssnittet är intuitivt och innehåller detaljerade alternativ och kontroller för att komma åt arkiverade rapporter och visa rapportkörningsstatus (lyckad, misslyckad och köad).

När en rapport skapas meddelas du via ett e-postmeddelande (valfritt) och ett inkorgsmeddelande. Du kan visa, hämta eller ta bort en rapport från rapportlistsidan, där alla tidigare genererade rapporter visas.

## Förutsättning {#prerequisite-for-reporting}

Så här skapar du rapporter:

* Aktivera tjänsten [!UICONTROL Day CQ DAM Event Recorder] från **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
* Välj de aktiviteter eller händelser som du vill rapportera om. Om du till exempel vill generera en rapport om hämtade resurser väljer du [!UICONTROL Asset downloaded (DOWNLOADED)].

![Aktivera tillgångsrapportering i webbkonsolen](assets/reports-config-day-cq-dam-event-recorder.png)

## Generera rapporter {#generate-reports}

[!DNL Experience Manager Assets] genererar följande standardrapporter:

* Överför
* Hämta
* Förfaller
* Ändring
* Publicera
* [!DNL Brand Portal] publicera
* Diskanvändning
* Filer
* Länkdelning

[!DNL Adobe Experience Manager] administratörer kan enkelt generera och anpassa dessa rapporter för din implementering. Administratören kan följa de här stegen för att skapa en rapport:

1. I [!DNL Experience Manager]-gränssnittet klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.

   ![Verktygssida för att navigera bland resurser - rapport](assets/AssetsReportNavigation.png)

1. På sidan [!UICONTROL Asset Reports] klickar du på **[!UICONTROL Create]** i verktygsfältet.
1. Välj den rapport du vill skapa på sidan **[!UICONTROL Create Report]** och klicka på **[!UICONTROL Next]**.

   ![Välj rapporttyp](assets/choose_report.png)

   >[!NOTE]
   >
   >Som standard inkluderas innehållsfragment och länkdelningar i resursen [!UICONTROL Download]-rapporten. Välj lämpligt alternativ för att skapa en rapport över länkdelningar eller för att utesluta innehållsfragment från hämtningsrapporten.

   >[!NOTE]
   >
   >I [!UICONTROL Download]-rapporten visas endast information om de resurser som har hämtats efter att du har valt var för sig eller som har hämtats med Snabbåtgärd. Den innehåller dock inte information om resurserna som finns i en hämtad mapp.

1. Konfigurera rapportinformation som titel, beskrivning, miniatyrbild och mappsökväg i CRX-databasen där rapporten lagras. Som standard är mappsökvägen `/content/dam`. Du kan ange en annan sökväg.

   ![Sida för att lägga till rapportinformation](assets/report_configuration.png)

   Välj datumintervall för rapporten.

   Du kan välja att generera rapporten nu eller vid ett framtida datum och tid.

   >[!NOTE]
   >
   >Om du väljer att schemalägga rapporten senare måste du ange datum och tid i fälten Datum och Tid. Om du inte anger något värde behandlas det som en rapport som ska genereras omedelbart.

   Konfigurationsfälten kan variera beroende på vilken typ av rapport du skapar. Rapporten **[!UICONTROL Disk Usage]** innehåller till exempel alternativ för att inkludera resursåtergivningar när du beräknar det diskutrymme som används av resurserna. Du kan välja att inkludera eller exkludera resurser i undermappar för beräkning av diskanvändning.

   >[!NOTE]
   >
   >Rapporten **[!UICONTROL Disk Usage]** innehåller inga fält för datumintervall eftersom den endast visar hur mycket diskutrymme som används.

   ![Sidan Information om rapporten Diskanvändning](assets/disk_usage_configuration.png)

   När du skapar **[!UICONTROL Files]**-rapporten kan du inkludera/exkludera undermappar. Du kan dock inte inkludera resursåtergivningar för den här rapporten.

   ![Detaljsida för rapporten Filer](assets/files_report.png)

   I rapporten **[!UICONTROL Link Share]** visas URL:er till resurser som delas med externa användare inifrån [!DNL Assets]. Den innehåller e-post-ID:n för den användare som delat resurserna, e-post-ID:n för de användare som resurserna delas med, delningsdatum och utgångsdatum för länken. Det går inte att anpassa kolumnerna.

   **[!UICONTROL Link Share]**-rapporten innehåller inga alternativ för undermappar och återgivningar eftersom den bara publicerar de delade URL:er som visas under `/var/dam/share`.

   ![Detaljsida för länkdelningsrapport](assets/link_share.png)

1. Klicka på **[!UICONTROL Next]** i verktygsfältet.

1. På sidan **[!UICONTROL Configure Columns]** är vissa kolumner markerade för att visas i rapporten som standard. Du kan markera fler kolumner. Avbryt valet av en kolumn för att utesluta den i rapporten.

   ![Markera eller avbryta markeringen av rapportkolumner](assets/configure_columns.png)

   Om du vill visa ett anpassat kolumnnamn eller en egenskapssökväg konfigurerar du egenskaperna för resursens binärfil under noden `jcr:content` i CRX. Du kan också lägga till den via egenskapssökvägsväljaren.

   ![Markera eller avbryta markeringen av rapportkolumner](assets/custom_columns.png)

1. Klicka på **[!UICONTROL Create]** i verktygsfältet. Ett meddelande meddelar att rapportgenereringen har initierats.
1. På sidan [!UICONTROL Asset Reports] baseras rapportgenereringsstatusen på rapportjobbets aktuella tillstånd, till exempel [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] eller [!UICONTROL Scheduled]. Samma status visas i inkorgen för meddelanden.Om du vill visa rapportsidan klickar du på rapportlänken. Du kan också markera rapporten och klicka på **[!UICONTROL View]** i verktygsfältet.

   ![En genererad rapport](assets/report_page.png)

   Klicka på **[!UICONTROL Download]** i verktygsfältet för att hämta rapporten i CSV-format.

## Lägg till anpassade kolumner {#add-custom-columns}

Du kan lägga till anpassade kolumner i följande rapporter om du vill visa mer data för dina anpassade krav:

* Överför
* Hämta
* Förfaller
* Ändring
* Publicera
* [!DNL Brand Portal] publicera
* Filer

Följ de här stegen för att lägga till anpassade kolumner i de här rapporterna:

1. I [!DNL Manager interface] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. På sidan [!UICONTROL Asset Reports] klickar du på **[!UICONTROL Create]** i verktygsfältet.

1. Välj den rapport du vill skapa på sidan **[!UICONTROL Create Report]** och klicka på **[!UICONTROL Next]**.
1. Konfigurera rapportinformation som titel, beskrivning, miniatyrbild, mappsökväg och datumintervall.

1. Om du vill visa en anpassad kolumn anger du namnet på kolumnen under **[!UICONTROL Custom Columns]**.

   ![Ange namn för anpassad rapportkolumn](assets/custom_columns-1.png)

1. Lägg till egenskapssökvägen under noden `jcr:content` i CRXDE med egenskapssökvägsväljaren. Du kan också skriva sökvägen i fältet för egenskapssökväg.

   ![Mappa egenskapssökvägen från banor i jcr:content](assets/property_picker.png)

   Om du vill lägga till fler anpassade kolumner klickar du på **[!UICONTROL Add]** och upprepar steg 5 och 6.

1. Klicka på **[!UICONTROL Create]** i verktygsfältet. Ett meddelande meddelar att rapportgenereringen har initierats.

## Konfigurera rensningstjänsten {#configure-purging-service}

Om du vill ta bort rapporter som du inte längre behöver konfigurerar du tjänsten DAM Report Renge från webbkonsolen så att befintliga rapporter rensas baserat på antal och ålder.

1. Gå till webbkonsolen (konfigurationshanteraren) från `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL DAM Report Purge Service]**-konfigurationen.
1. Ange frekvens (tidsintervall) för rensningstjänsten i fältet `scheduler.expression.name`. Du kan också konfigurera åldern och tröskelvärdet för antal rapporter.
1. Spara ändringarna.

## Felsökningsinformation, tips och begränsningar {#best-practices-and-limitations}

* Om vissa rapporter eller siffror i rapporterna inte är tillgängliga eller som förväntat kontrollerar du att tjänsten [!UICONTROL Day CQ DAM Event Recorder] är aktiverad.

* Ta bort de rapporter som inte längre behövs. Använd konfigurationsalternativen i tjänsten DAM Report Renge för att konfigurera villkoren för att rensa rapporter.

* Om Diskanvändningsrapporten inte genereras och du använder [!DNL Dynamic Media] kontrollerar du att alla resurser är korrekta. Du löser problemet genom att bearbeta resurserna på nytt och sedan generera rapporten igen.
