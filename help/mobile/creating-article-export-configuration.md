---
title: Skapar artikelexportkonfiguration
description: Följ den här sidan om du vill veta mer om hur du exporterar innehåll från Adobe Experience Manager (AEM) för överföring till AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Skapar artikelexportkonfiguration{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Förutsättning**:
>
>Innan du får lära dig mer om att skapa och ändra delade resurser kan du läsa [Innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md) för att förstå de grundläggande begreppen.

AEM Mobile-användare använder Innehållssynkronisering för att exportera live-innehåll till statiskt innehåll för användning i mobilappar, och den här exporten sker när innehåll överförs till Mobile On-Demand Services från AEM Mobile.

Egenskapen ***dps-exportTemplate*** som nämns i tabellen ovan definierar sökvägen till programmets exportkonfigurationer. Ange den här egenskapen för att skapa och ändra delade resurser.

I följande resurser beskrivs hur du exporterar innehåll från Adobe Experience Manager (AEM) för överföring till AEM Mobile.

Artiklar har innehåll som behöver exporteras och överföras. En del av det här innehållet kan delas mellan artiklar.

Använd [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) för att samla ihop innehållet och skapa ett ***delat resurspaket***.

Den ContentSync-konfiguration som hittades på **&lt;dps-exportTemplate>/dps-article>** ska konfigureras att exportera allt innehåll som en artikel kräver för statisk återgivning av egenskaper på enheten.

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
1. Bläddra till den här sökvägen [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article) om du vill visa delade exempelresurser.

   Du kan visa alla egenskaper som krävs för att skapa dina delade resurser enligt bilden nedan:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Artiklar bör laddas upp eller exporteras till AEM Mobile On-demand Services när ett artikelinnehåll ändras.
