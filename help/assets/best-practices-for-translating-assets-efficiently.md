---
title: Bästa tillvägagångssätt för att översätta resurser
description: Bästa tillvägagångssätt för effektiv hantering av resurser för att synkronisera olika översatta versioner och effektivisera översättningsarbetsflöden.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# Bästa tillvägagångssätt för att översätta resurser {#best-practices-for-translating-assets-efficiently}

Adobe Experience Manager Assets har stöd för flerspråkiga arbetsflöden för att översätta binära filer, metadata och taggar för digitala resurser till flera språkområden och för att hantera översatta resurser. Mer information finns i [Flerspråkiga resurser](multilingual-assets.md).

För effektiv hantering av resurser, för att säkerställa att olika översatta versioner förblir synkroniserade, skapar du [språkkopior](preparing-assets-for-translation.md) av resurser innan du kör översättningsarbetsflöden.

En språkkopia av en resurs eller en grupp av resurser är ett språkjämlikt (eller en version av resursen/resurserna på ett modersmål) med en liknande innehållshierarki.

Varje språkkopia är en oberoende resurs. Därför kan en översättning av resurser till flera språkområden drastiskt öka storleken på CRX-databasen. Om du till exempel översätter resurser med en kombinerad storlek på 10 GB till två språk kan databasstorleken öka med ungefär 20 GB (10 GB för varje språk).

Resurbinärfiler upptar mycket större lagringsutrymme jämfört med metadata och taggar. Om översättning av metadata och taggar bara har ditt syfte utelämnar du därför att översätta binärfilerna. Du kan behålla den ursprungliga kopian av binärfilerna i databasen för association med metadata och taggar översatta till olika språkområden. Genom att behålla en enda kopia av binärfiler, i stället för flera översatta versioner, minimeras påverkan på databasstorleken.

File Data Store och Amazon S3 Data Store tillhandahåller en lagringsinfrastruktur som passar bäst för dessa scenarier. De här lagringsdatabaserna lagrar en enda kopia av resursbinärfiler (inklusive återgivningar) som kan delas av metadata och taggar på flera språkområden. Databasstorleken påverkas därför inte om du skapar kopior av resurser och översätter metadata och taggar.

Du kan också göra några konfigurationsändringar i ett par arbetsflöden och översättningsintegrationsramverket för att ytterligare effektivisera processen.

1. Gör något av följande:

   * [Konfigurera arkiv för fildata](/help/sites-deploying/data-store-config.md)
   * [Konfigurera Amazon S3-datalagret](/help/sites-deploying/data-store-config.md)

1. Inaktivera arbetsflödet för [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) .

   Som namnet antyder skriver arbetsflödet om metadata till den binära filen [!UICONTROL DAM Metadata Writeback] . Eftersom metadata ändras efter översättning, genereras en annan binär fil för en språkkopia när du skriver tillbaka den till den binära filen.

   >[!NOTE]
   >
   >Om du inaktiverar arbetsflödet inaktiveras skrivningen av XMP-metadata för resurbinärfiler. [!UICONTROL DAM MetaData Writeback] Därför sparas inte längre framtida metadataändringar i resurserna. Utvärdera konsekvenserna innan du inaktiverar arbetsflödet.

1. Aktivera [!UICONTROL Set last modified date] arbetsflödet.

   Arbetsflödet [!UICONTROL DAM MetaData Writeback] konfigurerar det senaste ändringsdatumet för en resurs. Eftersom du inaktiverar det här arbetsflödet i steg 2 kan resurser inte längre hålla det senaste ändrade datumet för resurser uppdaterat. Aktivera därför arbetsflödet *Ange senaste ändringsdatum* för att se till att senaste ändrade datum för resurser är uppdaterade. Resurser med inaktuella senast ändrade datum kan orsaka fel.

1. [Konfigurera översättningsintegreringsramverket](/help/sites-administering/tc-tic.md) så att översättningen av resursbinärfiler avbryts. Avmarkera alternativet på fliken Resurser om du vill avbryta översättningen av resurbinärfiler. **[!UICONTROL Translate Assets]**
1. Översätt metadata/taggar för resurser med hjälp av [flerspråkiga arbetsflöden](multilingual-assets.md).
