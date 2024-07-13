---
title: Konfigurera Adobe Target Cloud Service
description: Följ den här sidan för att lära dig hur du får rätt uppsättning behörigheter för användare och grupper, skapar molntjänster, konfigurerar programmet för aktiviteten och slutligen skapar innehållet.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 1%

---

# Konfigurera Adobe Target Cloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Det här dokumentet är en del av [Komma igång med Adobe Experience Manager (AEM) Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, en rekommenderad startpunkt för AEM Mobile referens.

Det finns flera steg som måste utföras innan innehållsförfattare kan börja generera riktat innehåll för mobilappar: rätt uppsättning behörigheter för användare och grupper hämtas, molntjänster skapas, programmet konfigureras för aktiviteten konfigureras och innehållet slutligen genereras.

Antagandet som går framåt är att [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) har distribuerats och är tillgängligt via AEM Mobile Dashboard.

## Behörigheter {#permissions}

Användare som behöver åtkomst till personaliseringskonsolen måste ingå i gruppen `target-activity-authors`. Som en del av användar- och gruppinställningarna bör målaktivitetsgruppen läggas till i gruppen som administrerar program. Genom att lägga till gruppen target-activity-authors kan användarna se menyposten i Personalization.

Om du glömmer att lägga till de användare eller grupper som du vill ska ha tillgång till Admin Console i personaliseringen i gruppen target-activity-authors, kan användarna inte se personaliseringskonsolen.

## Cloud Service {#cloud-services}

För att få målinriktat innehåll att fungera för mobilprogram finns det två tjänster som måste konfigureras: Adobe Target-tjänsten och Adobe-tjänsten för mobiltjänster. Adobe Target-tjänsten tillhandahåller motorn för bearbetning av klientförfrågningar och returnering av det anpassade innehållet. Tjänsten Adobe Mobile Services tillhandahåller anslutningen mellan Adobes tjänster och mobilprogrammet via filen ADBMomobileConfig.json som används av plugin-programmet AMS Cordova. Från AEM Mobile Dashboard kan du konfigurera programmet genom att lägga till de två tjänsterna.

## Adobe Target Cloud Service {#adobe-target-cloud-service}

Gå till Cloud Servicen Hantera på AEM Mobile Dashboard och klicka på plusknappen (+).

![chlimage_1-8](assets/chlimage_1-8.png)

I guiden Lägg till Cloud Service väljer du molntjänstkortet&quot;Adobe Target&quot; och klickar på Nästa.

![chlimage_1-9](assets/chlimage_1-9.png)

I listrutan Välj en konfiguration kan du antingen skapa en konfiguration eller välja en befintlig konfiguration. Om du vill skapa en konfiguration väljer du Skapa konfiguration i listrutan. Ange en rubrik för målkonfigurationen. Ange klientkod, e-postadress och lösenord som är kopplade till ditt Target-konto. Om du inte känner till värdena för dessa fält kan du kontakta Adobe Target support. Klicka på Verifiera för att validera inloggningsuppgifterna. Klicka på knappen Skicka för att skapa molntjänsten.

Molntjänsten som skapas kopplas automatiskt till mobilprogrammet via guiden. Egenskapsvärdet cq:cloudserviceconfigs ställs in på jcr:content-noden i programgruppsnoden. För hybridappexemplet ställs det in på /content/mobileapps/hybrid-reference-app/jcr:content med värdet som pekar på den automatiskt genererade ramverksnoden på /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Ramverksnoden har två egenskaper inställda som standard, kön och ålder. Ramverket används bara för AEM förhandsgranskning och påverkar inte enheten.

När guiden har slutförts innehåller rutan Hantera Cloud Service molntjänsten Target, men den innehåller en varning om att ett Adobe-mobiltjänstkonto saknas.

![chlimage_1-10](assets/chlimage_1-10.png)

## Mobiltjänsten Adobe {#adobe-mobile-service}

Det är också nödvändigt att länka ett AMS-konto (Adobe Mobile Services) till programmet. AMS-tjänsten tillhandahåller den ADBMobleConfig.json-fil som krävs och som innehåller målklientens kodinformation. Innan du skapar en association med AMS-kontot måste AMS-kontot ändras av en användare som har behörighet till AMS.

### Klientkod {#client-code}

Om du vill logga in på AMS-tjänsterna går du till [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), väljer mobilprogrammet och klickar på inställningarna. Leta reda på fältet SDK-målalternativ, placera klientkoden i fältet och klicka på Spara.

![chlimage_1-11](assets/chlimage_1-11.png)

När nu klientkoden har kopplats till mobilprogrammet levereras inställningarna för tjänsten via ADBMobilConfig.json-filen när AMS-molntjänsten har konfigurerats via Adobe Mobile Dashboard.

### Adobe Mobile Service Could Service {#adobe-mobile-service-could-service}

Nu när AMS har konfigurerats är det dags att associera mobilappen i kontrollpanelen för mobiler i Adobe. Gå till Cloud Servicen Hantera på AEM Mobile Dashboard och klicka på plusknappen (+).

![chlimage_1-12](assets/chlimage_1-12.png)

Markera Adobe Mobile Services-kortet och klicka på Next.

![chlimage_1-13](assets/chlimage_1-13.png)

Välj listrutan Mobiltjänst i steget Skapa eller Välj guide och välj posten Skapa konfiguration. Ange titel, företag, användarnamn, lösenord och välj lämpligt datacenter. Om du inte känner till de här värdena kontaktar du Adobe-administratören för mobiltjänsten för att få dem. När alla fält har fyllts i klickar du på **Verifiera**. Verifieringsprocessen går till AMS och verifierar kontots inloggningsuppgifter, och när valideringen är klar fylls en lista över mobilprogram i där du väljer det associerade mobilprogrammet i listrutan. Klicka på knappen Skicka för att slutföra guiden. Det kan ta en stund att hämta konfigurationsdata och associerade analyser till programmet. När processen är klar klickar du på **Klar** på den modala för att återgå till instrumentpanelen för mobiler i Adobe.

Återgår till Mobile Dashboard och rutan Hantera Cloud Service innehåller AMS-molntjänsten. Dessutom innehåller rutan Analyze Metrics (Analysera mätvärden) livscykelrapporter.

![chlimage_1-14](assets/chlimage_1-14.png)

## Synkroniseringshanterare för målinnehåll {#target-content-sync-handlers}

För att leverera innehåll till användarens enhet genereras innehållet genom att de erbjudanden som skapas av AEM återges. För att hantera återgivningen av målerbjudanden finns det en ny hanterare för innehållssynkronisering som bearbetar erbjudandena. Med Hybrid Reference Application som exempel innehåller det engelska (engelska) innehållspaketet ContentSyncConfig med en [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) -hanterare. Nästa steg är avgörande för att återge erbjudanden till enheten. Hanteraren för mobileappoffers har en path-egenskap som identifierar sökvägen till den personaliseringsaktivitet som används för programmet.

Om det till exempel finns en aktivitet på */content/campaign/hybridref* kopierar du den här sökvägen och klistrar in den som värdet för egenskapen *path* i hanteraren för mobileappoffers.

För Hybrid Reference Application finns det två mobileappoffers-hanterare, en för dev och en för produktioner.

När aktivitetssökvägen har angetts i mobileappoffers-hanterarens path-egenskap sparar du hanteraren. Hanteraren är nu redo att börja återge erbjudanden för mobila enheter.

### Återgivningsläge {#render-mode}

Hanteraren för mobileappoffers är annorlunda konfigurerad för publicerings- och utvecklingsinställningar. För publiceringsinställningar finns egenskapen *renderMode* med värdet *publish* inställt på cq:ContentSyncConfig-noden. Hanteraren mobileappoffers refererar till renderMode och redigerar, om den är inställd på publicering, det mbox-id som skapas. Som standard har rutor som skapas av AEM ett —author-värde tillagt till mbox-ID:t. Detta identifierar att aktiviteten inte har publicerats och bör använda den opublicerade kampanjen för erbjudandelösningar.

När innehåll mellanlagras via Adobe Mobile Dashboard betraktas mellanlagrat innehåll som produktionsklart innehåll och återges via den icke-dev-konfiguration för innehållssynkronisering. Om du återger på det här sättet tas —author bort från alla mbox-ID:n och en publicerad aktivitet förväntas bli tillgänglig på målservern. Kontrollera att aktiviteten är publicerad innan du testar mellanlagrat innehåll.

## Skapa innehåll {#creating-content}

Nu när molntjänsterna har skapats och hanteraren för mobilappar har konfigurerats kan innehållsförfattare börja generera riktade upplevelser.
