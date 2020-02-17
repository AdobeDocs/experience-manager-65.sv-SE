---
title: Skapar artikelexportkonfiguration
seo-title: Skapar artikelexportkonfiguration
description: Följ den här sidan om du vill veta mer om hur du exporterar innehåll från Adobe Experience Manager (AEM) för överföring till AEM Mobile.
seo-description: Följ den här sidan om du vill veta mer om hur du exporterar innehåll från Adobe Experience Manager (AEM) för överföring till AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapar artikelexportkonfiguration{#creating-article-export-configuration}

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

Följande resurser beskriver hur du exporterar innehåll från Adobe Experience Manager (AEM) för överföring till AEM Mobile.

Artiklar har innehåll som behöver exporteras och överföras. En del av det här innehållet kan delas mellan artiklar.

Använd [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) för att samla ihop innehållet och skapa ett ***paket med delade resurser*** .

ContentSync-konfigurationen som finns i **&lt;dps-exportTemplate>/dps-article>** bör konfigureras att exportera allt innehåll som en artikel behöver för statisk återgivning av egenskaper på enheten.

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
1. Bläddra till den här sökvägen [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)för att visa delade exempelresurser.

   Du kan visa alla egenskaper som krävs för att skapa dina delade resurser enligt bilden nedan:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Artiklar bör laddas upp eller exporteras till AEM Mobile On-Demand Services när innehållet i artiklar ändras.

