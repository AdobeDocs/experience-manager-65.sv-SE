---
title: Skapar exportkonfiguration för delade resurser
description: Följ den här sidan om du vill veta mer om hur du exporterar delade resurser från Adobe Experience Manager (AEM) för överföring till AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Skapar exportkonfiguration för delade resurser{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Förutsättning**:
>
>Innan du lär dig mer om att skapa och ändra delade resurser, se [Innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md) för att förstå de grundläggande begreppen.

Adobe Experience Manager (AEM) Mobile-användare använder Content Sync för att exportera live-innehåll till statiskt innehåll för användning i mobilappar, och den här exporten sker när innehåll överförs till Mobile On Demand Services från AEM Mobile.

Egenskapen ***dps-exportTemplate*** som nämns i tabellen ovan definierar sökvägen till programmets exportkonfigurationer. Ange den här egenskapen för att skapa och ändra delade resurser.

Följande resurser beskriver hur du exporterar delade resurser från AEM för överföring till AEM Mobile.

Med delade HTML-resurser kan artiklar dela HTML-resurser som annars skulle dupliceras för alla artiklar, och de kan innehålla ikoner, teckensnitt, JavaScript och css.

Innehållssynkroniseringskonfigurationen finns på **&lt;dps-exporttemplate>/dps-HTMLResources>** bör vara konfigurerad för att exportera allt innehåll som en artikel kräver för statisk återgivning av egenskaper på enheten.

>[!CAUTION]
>
>Du kan bara utföra stegen nedan för att visa delade exempelresurser om du har:
>
>* har installerat exempelinnehållet
>* kör AEM
>* ingen konfigurerad anpassad kontext eller en annan port
>

Om du vill visa exempel på delad resurs, se stegen nedan:

1. Öppna CRXDE Lite på AEM.
1. Bläddra till den här sökvägen *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, för att visa de delade exempelresurserna.

   Du kan visa alla egenskaper som krävs för att skapa dina delade resurser enligt bilden nedan:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Delade resurser bör laddas upp eller exporteras till AEM Mobile On-demand Services när någon av de delade resurserna ändras.
