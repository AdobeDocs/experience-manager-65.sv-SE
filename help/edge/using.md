---
title: Använda Edge Delivery Services
description: Använda Edge Delivery Services
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
solution: Experience Manager, Experience Manager Assets
feature: Edge Delivery Services
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---

# Använda Edge Delivery Services {#usingedge}

Med Edge Delivery kan man snabbt skapa utvecklingsmiljöer där skribenterna snabbt kan uppdatera och publicera material och nya webbplatser snabbt kan lanseras. Därför kan du arbeta med flera olika innehållskällor på samma webbplats och publiceringen blir smidig och smidig oavsett vilken källa du väljer. Det tar därför bara några sekunder att gå från redigering till att se innehållet live på internet.

## Redigering {#authoring-edge}

Med Edge Delivery är det enkelt, snabbt och flexibelt att skapa. Du kan använda två olika sökvägar för att skapa i kontexten för Edge Delivery Services:

* Dokumentbaserad redigering (t.ex. Microsoft Word eller Google Docs) - [Mer information finns på den här länken](https://www.hlx.live/docs/authoring).
* Page Editor/Universal Editor - Kontakta din Adobe-säljare.

Om det finns dokumentbaserad redigering kan du arbeta med olika källor som Microsoft Word och Google Docs. Dokument från dessa källor blir sidor på din webbplats. Rubriker, listor, bilder, teckensnittselement och videor kan alla överföras från den ursprungliga källan till webbplatsen. Du kan lägga till metadata för SEO-syften eller använda block för att arbeta med strukturerat innehåll och lägga till funktioner.

## Publicering {#publishing-edge}

Med Edge Delivery är det smidigt att publicera innehåll oavsett innehållskälla. Processen är följande: du använder [sidespartillägget](#using-sidekick) för att utlösa publiceringsmekanismen, och ditt innehåll blir tillgängligt live på webbplatsen om några sekunder.

## Edge Delivery Services och GitHub {#github-edge}

Edge Delivery använder GitHub så att kunder kan hantera och driftsätta kod direkt från sina GitHub-databaser. Du kan till exempel skriva innehåll i antingen Google Docs eller Microsoft Word och utveckla webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub. Webbplatser skapas automatiskt för var och en av dina grenar, från förhandsgranskning av innehåll till produktion. Alla resurser du lägger in i GitHub-databasen är tillgängliga på din webbplats utan någon byggprocess.

## Använda Sidekick {#using-sidekick}

AEM har ett verktygsfält med sammanhangsberoende alternativ så att du enkelt kan redigera, förhandsgranska och publicera innehåll. När [har installerat](https://www.hlx.live/docs/sidekick-extension) kan tillägget AEM sidekick användas antingen i projektmiljöer eller när du redigerar ditt innehåll (till exempel i Google Docs). Beroende på miljön finns det flera tillgängliga åtgärder, som: Förhandsgranska, Läs in igen, Redigera och Publish. Du kan också växla miljöer när du använder sidekick, från förhandsgranskning till produktion och vice versa.

**Om du vill publicera** öppnar du sidosparken på en förhandsgranskningssida och använder Publish-åtgärden. När du har klickat på Publish är den aktuella förhandsvisningsversionen av sidan tillgänglig i lever- och produktionsmiljöer.

## Integrera AEM Assets med dokumentbaserad framtagning {#integrate-assets-edge}

Med Edge Delivery kan du använda bilder som finns i AEM Assets databaser när du redigerar dokument i Microsoft Word eller Google Docs.

Alternativen för att använda bilder i dina dokument är bara tillgängliga efter [att AEM Assets sidinslagsplugin ](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin) har konfigurerats.

Sidsparkpluginen för AEM Assets ger åtkomst till:

* AEM Assets as a Cloud Service

* AEM Assets Essentials

När du har konfigurerat AEM Assets-plugin-programmet för sidbrytning kan du [börja använda bilder i dina Google Docs- eller Microsoft Word-dokument](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## Ytterligare läsning {#further-reading}

Mer information finns på följande sidor:

* Mer information om hur du kommer igång med Edge Delivery finns i avsnittet [Skapa](https://www.hlx.live/docs/#build) i leveransdokumentationen för Edge.
* Mer information om hur du redigerar och publicerar innehåll med Edge Delivery finns i avsnittet [Publish](https://www.hlx.live/docs/authoring).
* Mer information om hur du använder sidosparktillägget finns i [Använda sidan för sidospark](https://www.hlx.live/docs/sidekick).
* AEM finns på sidan [Authoring Concepts](/help/sites-authoring/author.md))
