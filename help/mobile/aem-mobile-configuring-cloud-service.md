---
title: Konfigurera Adobe Target Cloud-tjänsten
seo-title: Konfigurera Adobe Target Cloud-tjänsten
description: Följ den här sidan för att lära dig hur du får rätt uppsättning behörigheter för användare och grupper, skapar molntjänster, konfigurerar programmet för aktiviteten och slutligen skapar innehållet.
seo-description: Följ den här sidan för att lära dig hur du får rätt uppsättning behörigheter för användare och grupper, skapar molntjänster, konfigurerar programmet för aktiviteten och slutligen skapar innehållet.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera Adobe Target Cloud-tjänsten {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Det här dokumentet ingår i [Getting Started with AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, en rekommenderad startpunkt för AEM Mobile-referens.

Det finns ett antal steg som måste sammanställas innan innehållsförfattare kan börja generera riktat innehåll för mobilappar: Vi får rätt behörighetsgrupp för användare och grupper, skapar molntjänster, konfigurerar programmet för aktiviteten och till slut skapar innehållet.

Det förutsätts att [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) har distribuerats och är tillgängligt via AEM Mobile Dashboard.

## Permissions {#permissions}

Användare som behöver åtkomst till personaliseringskonsolen måste ingå i `target-activity-authors` gruppen. Som en del av användar- och gruppinställningarna bör målaktivitetsgruppen läggas till i gruppen som administrerar program. Genom att lägga till gruppen target-activity-authors kan användarna se menyposten för personalisering.

Om du glömmer att lägga till de användare eller grupper som du vill ska ha tillgång till Admin Console för personalisering i gruppen target-activity-authors kommer det att förhindra användare från att se personaliseringskonsolen.

## Molntjänster {#cloud-services}

För att få målinriktat innehåll att fungera för mobilprogram finns det två tjänster som måste konfigureras: Adobe Target-tjänsten och Adobe Mobile Services-tjänsten. Adobe Target Service är motorn för bearbetning av klientförfrågningar och returnering av det personaliserade innehållet. Adobe Mobile Services-tjänsten tillhandahåller anslutningen mellan Adobes tjänster och mobilprogrammet via filen ADBMomobileConfig.json som används av plugin-programmet AMS Cordova. Från AEM Mobile Dashboard kan du konfigurera programmet genom att lägga till de två tjänsterna.

## Adobe Target Cloud-tjänst {#adobe-target-cloud-service}

På AEM Mobile Dashboard går du till Hantera molntjänster och klickar på plusknappen (+).

![chlimage_1-8](assets/chlimage_1-8.png)

I guiden Lägg till molntjänst väljer du molntjänstkortet&quot;Adobe Target&quot; och klickar på Nästa.

![chlimage_1-9](assets/chlimage_1-9.png)

I listrutan Välj en konfiguration kan du antingen skapa en ny konfiguration eller välja en befintlig konfiguration. Om du vill skapa en ny konfiguration väljer du Skapa konfiguration i listrutan. Ange en rubrik för målkonfigurationen. Ange klientkod, e-postadress och lösenord som är kopplade till ditt Target-konto. Om du inte känner till värdena för dessa fält kontaktar du Adobe Target-supporten. Klicka på Verifiera för att validera inloggningsuppgifterna. Klicka på knappen Skicka för att skapa molntjänsten.

Molntjänsten som skapas kopplas automatiskt till mobilprogrammet via guiden. Egenskapsvärdet cq:cloudserviceconfigs ställs in på jcr:content-noden i programgruppsnoden. För hybridappexemplet ställs det in på /content/mobileapps/hybrid-reference-app/jcr:content med värdet som pekar på den automatiskt genererade ramverksnoden som finns på /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Ramverksnoden har två egenskaper inställda som standard, kön och ålder. Ramverket används bara av AEM-förhandsgranskning och påverkar inte enheten.

När guiden har slutförts innehåller tjänstrutan Hantera molnet molntjänsten Target, men den innehåller en varning om att ett Adobe Mobile Service-konto saknas.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

Det är också nödvändigt att länka ett Adobe Mobile Services-konto (AMS) till programmet. AMS-tjänsten tillhandahåller den ADBMobleConfig.json-fil som krävs och som innehåller målklientens kodinformation. Innan du skapar en association med AMS-kontot måste AMS-kontot ändras av en användare som har behörighet till AMS.

### Klientkod {#client-code}

Om du vill logga in på AMS-tjänsterna går du till [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), väljer mobilprogrammet och klickar på inställningarna. Leta reda på fältet SDK-målalternativ, placera klientkoden i fältet och klicka på Spara.

![chlimage_1-11](assets/chlimage_1-11.png)

När nu klientkoden har kopplats till mobilprogrammet levereras inställningarna för tjänsten via ADBMobilConfig.json-filen när molntjänsten AMS har konfigurerats via Adobe Mobile Dashboard.

### Adobe Mobile Service Could Service {#adobe-mobile-service-could-service}

Nu när AMS har konfigurerats är det dags att koppla mobilappen till Adobe Mobile Dashboard. På AEM Mobile Dashboard går du till Hantera molntjänster och klickar på plusknappen (+).

![chlimage_1-12](assets/chlimage_1-12.png)

Välj Adobe Mobile Services-kortet och klicka på Nästa.

![chlimage_1-13](assets/chlimage_1-13.png)

Välj listrutan Mobiltjänst i steget Skapa eller Välj guide och välj posten Skapa konfiguration. Ange titel, företag, användarnamn, lösenord och välj lämpligt datacenter. Om du inte känner till dessa värden kontaktar du Adobe Mobile Service-administratören för att få dem. När alla fält har fyllts i klickar du på knappen Verifiera. Verifieringsprocessen går till AMS och verifierar kontots inloggningsuppgifter, och när valideringen är klar fylls en lista över mobilprogram i där du väljer det associerade mobilprogrammet i listrutan. Klicka på knappen Skicka för att slutföra guiden. Det kan ta en stund att hämta konfigurationsdata och associerade analyser till programmet. När processen är klar klickar du på knappen Klar på den modala för att återgå till Adobe Mobile Dashboard.

Om du går tillbaka till Mobile Dashboard kommer panelen Hantera molntjänster att innehålla AMS-molntjänsten. Du kommer också att lägga märke till att rutan Analysera mått fylls i med livscykelrapporter.

![chlimage_1-14](assets/chlimage_1-14.png)

## Synkroniseringshanterare för målinnehåll {#target-content-sync-handlers}

Att leverera innehåll till användarens enhetsinnehåll genereras genom att de erbjudanden som skapas av AEM-innehållsförfattare återges. Det finns en ny hanterare för innehållssynkronisering som hanterar återgivningen av målerbjudanden. Med Hybrid Reference Application som exempel innehåller det engelska innehållspaketet ContentSyncConfig med en [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) -hanterare. Nästa steg är avgörande för att återge erbjudanden till enheten. Hanteraren för mobileappoffers har en path-egenskap som identifierar sökvägen till den personaliseringsaktivitet som ska användas för programmet.

Om det till exempel finns en aktivitet som finns på */content/campaign/hybridref* kopierar du den här sökvägen och klistrar in den som värde för egenskapen *path* för hanteraren mobileappoffers.

För Hybrid Reference Application finns två mobileappoffers-hanterare en för dev och en för produktioner.

När aktivitetssökvägen har angetts i mobileappoffers-hanterarens path-egenskap sparar du hanteraren. Hanteraren är nu redo att börja återge erbjudanden för våra mobila enheter.

### Återgivningsläge {#render-mode}

Hanteraren för mobileappoffers är annorlunda konfigurerad för publicerings- och utvecklingsinställningar. För publiceringsinställningar finns egenskapen *renderMode* med värdet *publish* inställt på cq:ContentSyncConfig-noden. Hanteraren mobileappoffers refererar till renderMode och, om den anges för publicering, ändrar mbox-ID:t som skapas. Som standard har rutor som skapas av AEM ett —author-värde tillagt till mbox-ID:t. Detta identifierar att aktiviteten inte har publicerats och bör använda den opublicerade kampanjen för erbjudandelösningar.

När innehåll mellanlagras via Adobe Mobile Dashboard betraktas mellanlagrat innehåll som produktionsklart innehåll och återges via den icke-dev-konfiguration för innehållssynkronisering. Om du återger på det här sättet tas —author bort från alla mbox-ID:n och en publicerad aktivitet förväntas bli tillgänglig på målservern. Kontrollera att aktiviteten har publicerats innan du testar mellanlagrat innehåll.

## Skapa innehåll {#creating-content}

Nu när molntjänsterna har skapats och hanteraren för mobilappar har konfigurerats kan innehållsförfattare börja generera riktade upplevelser.
