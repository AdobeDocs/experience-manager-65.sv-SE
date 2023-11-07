---
title: Bästa praxis för [!DNL Assets]
description: Förbättrar systemets stabilitet och prestanda under belastning genom att identifiera och följa bästa praxis som är beroende av din driftsättning och konfiguration.
contentOwner: AG
feature: Asset Management
role: Architect, Admin
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Bästa praxis för [!DNL Assets] {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets] är en viktig del i att leverera digitala marknadsföringsupplevelser av hög kvalitet som bidrar till att uppnå affärsmålen genom att öka innehållets hastighet. Om du arbetar med ett stort antal resurser i [!DNL Experience Manager Assets] eller regelbundet/regelbundet ladda upp flera resurser, inklusive videor och Dynamic Media, så är det avgörande att optimera upplevelsen av digital resurshantering för att systemet ska bli effektivt.

Beroende på hur du har placerat [!DNL Assets] för er organisation och de funktioner ni använder för materialinhämtning, renderingsgenerering och metadataextrahering. Genom att identifiera och följa bästa praxis inom olika områden förbättras systemets stabilitet och prestanda avsevärt vid inläsning.

När du har granskat följande riktlinjer får du de kunskaper och verktyg du behöver för att skapa och hantera ett resurshanteringssystem för företag som passar dina behov:

* The [Prestandajusteringsguide för resurser](/help/assets/performance-tuning-guidelines.md): Den här guiden innehåller en uppsättning metodtips som du kan följa när som helst i implementeringen, även när du är klar, för att vara säker på att du får ut så mycket som möjligt av systemet.
* The [Guide för resursstorlek](/help/assets/assets-sizing-guide.md): När uppskattningar för en [!DNL Assets] implementering är det viktigt att se till att det finns tillräckligt med resurser tillgängliga när det gäller lagring, processor, minne, IO och nätverksgenomströmning. Om du ändrar storlek på många av dessa objekt måste du förstå hur många resurser som läses in i systemet. Den här guiden innehåller bästa praxis som hjälper till att fastställa effektiva mått för beräkning av den infrastruktur och de resurser som krävs för driftsättning [!DNL Assets] och ett verktyg för storleksändring.
* The [Guide för resursmigrering](/help/assets/assets-migration-guide.md): Om du vill migrera resurser från ditt äldre system till Assets finns det flera steg som ska övervägas för att effektivisera migreringsprocessen. Migreringsguiden innehåller bästa praxis för de uppgifter du utför för att överföra resurser till [!DNL Experience Manager] på ett fasvis sätt. Detta inkluderar att lägga till metadata, generera återgivningar och aktivera resurserna för att publicera instanser.
* The [Resurser för dokument om nätverksaspekter](/help/assets/assets-network-considerations.md): Vid hantering [!DNL Experience Manager] driftsättning, det är viktigt att förstå nätverkstopologin för att förstå nätverkets prestanda, identifiera chokepoints och beskriva den förväntade användarupplevelsen. The [!DNL Assets] dokument som behandlar nätverkshänsyn tar upp nätverksfrågor när du utformar resursinstallationen.
* The [Resursövervakningsguide](/help/assets/assets-monitoring-best-practices.md): Efter [!DNL Experience Manager] distribueras bör du övervaka vissa uppgifter och systemet i allmänhet för att säkerställa systemintegriteten och effektiviteten i åtgärderna. Övervakningsguiden innehåller bästa praxis för övervakning av olika aspekter av ditt system.
* [Bästa praxis för Experience Manager-datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] datorprogrammet länkar din DAM-lösning (Digital Asset Management) till skrivbordet så att du kan öppna de filer som finns i [!DNL Experience Manager] webbgränssnittet direkt på skrivbordet. Skrivbordsappens lättanvända arbetsflöde aktiveras med hjälp av nätverksdelningsteknik från operativsystemen på datorn. Den här guiden förklarar viktiga funktioner och rekommenderar användning av [!DNL Experience Manager] datorprogram.
* [Bästa praxis för integrering mellan Experience Manager och Creative Cloud](/help/assets/aem-cc-integration-best-practices.md): Du kan integrera dina [!DNL Experience Manager] driftsättning med [!DNL Creative Cloud] på flera sätt. Om du följer några metodtips för att effektivisera arbetsflödena för integrering och överföring av resurser blir du mycket effektivare. Den här guiden innehåller metodtips om hur man integrerar [!DNL Assets] med [!DNL Adobe Creative Cloud].
