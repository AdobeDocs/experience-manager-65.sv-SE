---
title: Bästa tillvägagångssätt för [!DNL Assets]
description: Förbättrar systemets stabilitet och prestanda under belastning genom att identifiera och följa bästa praxis som är beroende av din driftsättning och konfiguration.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Metodtips för [!DNL Assets] {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets] är en viktig del i att leverera digitala marknadsföringsupplevelser av hög kvalitet som bidrar till att uppnå affärsmålen genom att öka innehållets hastighet. Om du arbetar med ett stort antal resurser inom [!DNL Experience Manager Assets] eller regelbundet/regelbundet överför flera resurser, inklusive videor och dynamiska media, är det viktigt att optimera upplevelsen av den digitala resurshanteringen för att systemet ska bli effektivt.

Beroende på hur du har placerat [!DNL Assets] för din organisation och vilka funktioner du använder för materialintag, återgivningsgenerering och metadataextrahering, kan du identifiera och följa vedertagna metoder inom olika områden för att förbättra systemets stabilitet och prestanda vid inläsning.

När du har granskat följande riktlinjer får du de kunskaper och verktyg du behöver för att skapa och hantera ett resurshanteringssystem för företag som passar dina behov:

* [Guide för prestandajustering av resurser](/help/assets/performance-tuning-guidelines.md): Den här guiden innehåller en uppsättning metodtips som du kan följa när som helst i implementeringen, även när du är klar, för att vara säker på att du får ut så mycket som möjligt av systemet.
* [Handboken för resursstorlek](/help/assets/assets-sizing-guide.md): När du skapar uppskattningar för en [!DNL Assets]-implementering är det viktigt att se till att det finns tillräckligt med resurser tillgängliga när det gäller resurslagring, processor, minne, IO och nätverksgenomströmning. Om du ändrar storlek på många av dessa objekt måste du förstå hur många resurser som läses in i systemet. Den här guiden innehåller bästa praxis som hjälper till att fastställa effektiva mått för beräkning av den infrastruktur och de resurser som krävs för att distribuera [!DNL Assets] samt ett storleksbedömningsverktyg.
* Guiden [Resursmigrering](/help/assets/assets-migration-guide.md): Om du vill migrera resurser från ditt äldre system till Assets finns det flera steg som ska övervägas för att effektivisera migreringsprocessen. Migreringsguiden innehåller metodtips om de åtgärder du utför för att överföra resurserna till [!DNL Experience Manager] på ett fasvis sätt. Detta inkluderar att lägga till metadata, generera återgivningar och aktivera resurserna för att publicera instanser.
* [Resursens dokument om nätverksaspekter](/help/assets/assets-network-considerations.md): När du hanterar [!DNL Experience Manager]-distribution är det viktigt att förstå nätverkstopologin för att förstå nätverksprestanda, identifiera kontrollpunkter och beskriva den förväntade användarupplevelsen. I [!DNL Assets]-dokumentet om nätverksfrågor beskrivs nätverksaspekter när du utformar resursdistributionen.
* [Resursövervakningsguiden](/help/assets/assets-monitoring-best-practices.md): När din [!DNL Experience Manager]-distribution har distribuerats bör du övervaka vissa uppgifter och systemet i allmänhet för att säkerställa systemintegriteten och effektiviteten för åtgärderna. Övervakningsguiden innehåller bästa praxis för övervakning av olika aspekter av ditt system.
* [Bästa praxis](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html) för Experience Manager-datorprogram:  [!DNL Experience Manager] datorprogrammet länkar DAM-lösningen (Digital Asset Management) till skrivbordet så att du kan öppna de filer som finns i  [!DNL Experience Manager] webbgränssnittet direkt på skrivbordet. Skrivbordsappens lättanvända arbetsflöde aktiveras med hjälp av nätverksdelningsteknik från operativsystemen på datorn. I den här guiden förklaras de viktigaste funktionerna och den rekommenderade användningen av [!DNL Experience Manager]-datorprogrammet.
* [Bästa praxis](/help/assets/aem-cc-integration-best-practices.md) för integrering mellan Experience Manager och Creative Cloud: Ni kan integrera er  [!DNL Experience Manager] driftsättning  [!DNL Creative Cloud] med på flera sätt. Om du följer några metodtips för att effektivisera arbetsflödena för integrering och överföring av resurser blir det effektivare. Den här guiden innehåller metodtips om hur du integrerar [!DNL Assets] med [!DNL Adobe Creative Cloud].
