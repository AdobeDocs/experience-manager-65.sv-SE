---
title: Skapar exportkonfiguration för delade resurser
seo-title: Skapar exportkonfiguration för delade resurser
description: Följ den här sidan om du vill veta mer om hur du exporterar delade resurser från Adobe Experience Manager (AEM) för överföring till AEM Mobile.
seo-description: Följ den här sidan om du vill veta mer om hur du exporterar delade resurser från Adobe Experience Manager (AEM) för överföring till AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapar exportkonfiguration för delade resurser{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Krav**:
>
>Innan du får lära dig mer om hur du skapar och ändrar delade resurser läser du [Innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md) för att förstå de grundläggande begreppen.

AEM Mobile-användare använder innehållssynkronisering för att exportera live-innehåll till statiskt innehåll för användning i mobilappar, och den här exporten sker när innehåll överförs till Mobile On-Demand Services från AEM Mobile.

Egenskapen ***dps-exportTemplate*** som nämns i tabellen ovan definierar sökvägen till programmets exportkonfigurationer. Ange den här egenskapen för att skapa och ändra delade resurser.

I följande resurser beskrivs hur du exporterar delade resurser från Adobe Experience Manager (AEM) för överföring till AEM Mobile.

Med delade HTML-resurser kan artiklar dela HTML-resurser som annars skulle behöva dupliceras för alla artiklar och som kan innehålla ikoner, teckensnitt, javascript och css.

Konfigurationen för innehållssynkronisering som finns i **&lt;dps-exportTemplate>/dps-HTMLResources>** bör konfigureras för att exportera allt innehåll som en artikel behöver för statisk återgivning av egenskaper på enheten.

>[!CAUTION]
>
>Du kan bara utföra stegen nedan för att visa delade exempelresurser om du har:
>
>* har installerat exempelinnehållet
>* kör AEM-instans
>* ingen konfigurerad anpassad kontext eller en annan port
>



Om du vill visa exempel på delad resurs, se stegen nedan:

1. Öppna CRXDE Lite på AEM-servern.
1. Bläddra till den här sökvägen *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*för att visa delade exempelresurser.

   Du kan visa alla egenskaper som krävs för att skapa dina delade resurser enligt bilden nedan:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Delade resurser bör laddas upp eller exporteras till AEM Mobile On-Demand Services när någon av de delade resurserna ändras.

