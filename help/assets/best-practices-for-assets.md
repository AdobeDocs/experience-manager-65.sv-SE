---
title: Metodtips för Assets
description: Beroende på hur ni använder Experience Manager Assets och vilka funktioner ni använder för materialintag, renderingsgenerering och metadataextrahering kan det vara bra att identifiera och följa bästa praxis inom olika områden, vilket förbättrar systemets stabilitet och prestanda vid inläsning.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Metodtips för Assets {#best-practices-for-assets}

Adobe Experience Manager Assets är en viktig del i att leverera högkvalitativa digitala marknadsföringsupplevelser som bidrar till att uppnå affärsmålen genom att öka innehållets hastighet. Om du arbetar med ett stort antal mediefiler i Experience Manager Assets eller regelbundet/regelbundet överför flera mediefiler, inklusive videor och dynamiska media, är det viktigt att optimera din digitala resurshantering för att systemet ska bli effektivt.

Beroende på hur ni har positionerat Assets för organisationen och vilka funktioner ni använder när det gäller tillgångsintag, återgivningsgenerering och metadataextrahering, kan det vara bra att identifiera och följa vedertagna metoder inom olika områden och förbättra systemets stabilitet och prestanda vid inläsning.

När du har granskat följande riktlinjer får du de kunskaper och verktyg du behöver för att skapa och hantera ett resurshanteringssystem för företag som passar dina behov:

* Guiden [Prestandajustering för](/help/assets/performance-tuning-guidelines.md)resurser: Den här guiden innehåller en uppsättning metodtips som du kan följa när som helst i implementeringen, även när du är klar, för att vara säker på att du får ut så mycket som möjligt av systemet.
* The [Assets Size guide](/help/assets/assets-sizing-guide.md): När du skapar uppskattningar för en resursimplementering är det viktigt att se till att det finns tillräckliga resurser tillgängliga när det gäller lagring av resurser, processor, minne, IO och nätverksgenomströmning. Om du ändrar storlek på många av dessa objekt måste du förstå hur många resurser som läses in i systemet. Den här guiden innehåller bästa praxis som hjälper till att fastställa effektiva mått för att beräkna den infrastruktur och de resurser som krävs för att driftsätta Assets samt ett storleksbedömningsverktyg.
* Handboken för [resursmigrering](/help/assets/assets-migration-guide.md): Om du vill migrera resurser från ditt äldre system till Assets finns det flera steg som ska övervägas för att effektivisera migreringsprocessen. Migreringsguiden innehåller metodtips för de uppgifter du utför för att ta in resurserna i Experience Manager på ett fasvis sätt. Detta inkluderar att lägga till metadata, generera återgivningar och aktivera resurserna för att publicera instanser.
* Dokumentet [Assets Network Considerations](/help/assets/assets-network-considerations.md): När du hanterar driftsättning i Experience Manager är det viktigt att förstå nätverkstopologin för att förstå nätverksprestanda, identifiera kontrollpunkter och beskriva den förväntade användarupplevelsen. Dokumentet Assets Network Considerations behandlar nätverksaspekter när du designar din resursdistribution.
* The [Assets Monitoring Guide](/help/assets/assets-monitoring-best-practices.md): När distributionen av Experience Manager är klar bör du övervaka vissa uppgifter och systemet i allmänhet för att säkerställa systemintegriteten och effektiviteten i åtgärderna. Övervakningsguiden innehåller bästa praxis för övervakning av olika aspekter av ditt system.
* [Bästa praxis](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app-best-practices.html)för Experience Manager-datorprogram: Skrivbordsappen Experience Manager länkar din DAM-lösning (Digital Asset Management) till skrivbordet så att du kan öppna de filer som finns i användargränssnittet för Experience Manager direkt på skrivbordet. Skrivbordsappens lättanvända arbetsflöde aktiveras med hjälp av nätverksdelningsteknik från operativsystemen på datorn. I den här guiden förklaras de viktigaste funktionerna och den rekommenderade användningen av datorprogrammet Experience Manager.
* [Bästa praxis](/help/assets/aem-cc-integration-best-practices.md)för integrering mellan Experience Manager och Creative Cloud: Du kan integrera din Experience Manager-distribution med Creative Cloud på flera sätt. Om du följer några metodtips för att effektivisera arbetsflödena för integrering och överföring av resurser blir det effektivare. Den här guiden innehåller metodtips om hur du integrerar resurser med Adobe Creative Cloud.
