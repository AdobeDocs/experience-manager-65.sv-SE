---
title: Skapa en SCF-sandlåda
description: Den här självstudiekursen är främst avsedd för utvecklare som inte är AEM och som är intresserade av att använda SCF-komponenter. Här går vi igenom hur man skapar en SCF-sandlådeplats
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Skapa en SCF-sandlåda  {#create-an-scf-sandbox}

Från och med AEM 6.1 Communities är det enklaste sättet att snabbt skapa en sandlåda att skapa en community-webbplats. Se [Komma igång med AEM Communities](getting-started.md).

Ett annat användbart verktyg för utvecklare är [Community Components Guide](components-guide.md), som gör det möjligt att utforska och snabbt skapa prototyper för communitykomponenter och -funktioner.

Att skapa en webbplats kan vara användbart för att förstå strukturen hos en AEM webbplats som kan innehålla funktioner för användargrupper, samtidigt som det kan finnas enkla sidor där du kan utforska arbetet med [ramverk för sociala komponenter (SCF)](scf.md).

Den här självstudiekursen är främst avsedd för utvecklare som inte är AEM och som är intresserade av att använda SCF-komponenter. Här går vi igenom hur du skapar en SCF-sandlådeplats, ungefär som självstudiekursen för [Skapa en komplett webbplats](../../help/sites-developing/website.md) som fokuserar på webbplatsstrukturer som navigering, logotyp, sökning, verktygsfält och underordnade sidor.

Utvecklingen sker i en författarinstans, medan det är bäst att experimentera med webbplatsen i en publiceringsinstans.

Stegen i den här självstudien är:

* [Konfigurera webbplatsstruktur](setup-website.md)
* [Ursprungligt sandlådeprogram](initial-app.md)
* [Ursprungligt sandlådeinnehåll](initial-content.md)
* [Utveckla sandlådeprogram](develop-app.md)
* [Lägg till klienter](add-clientlibs.md)
* [Utveckla innehåll i sandlådan](develop-content.md)

>[!CAUTION]
>
>I den här självstudiekursen skapas ingen community-webbplats med de funktioner som skapas med [Konsolen Webbplatser i Communities](sites-console.md). I den här självstudiekursen beskrivs till exempel inte hur du konfigurerar inloggning, självregistrering, [social inloggning](social-login.md), meddelanden, profiler och så vidare.
>
>Om du föredrar en enkel communitywebbplats ska du följa [Skapa en exempelsida](create-sample-page.md) självstudie.

## Förutsättningar {#prerequisites}

I den här självstudiekursen förutsätts att du har en AEM författare och en AEM publiceringsinstans installerad som har [senaste versionen](deploy-communities.md#latest-releases) av Communities.

Nedan följer några praktiska länkar för utvecklare som är nya för den AEM plattformen:

* [Komma igång](../../help/sites-deploying/deploy.md#getting-started): för distribution AEM instanser.

   * [Grunderna](../../help/sites-developing/the-basics.md): för utvecklare av webbplatser och funktioner.
   * [Steg 1 för författare](../../help/sites-authoring/first-steps.md): för redigering av sidinnehåll.

## Använda CRXDE Lite Development Environment {#using-crxde-lite-development-environment}

AEM utvecklare tillbringar mycket tid i [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) utvecklingsmiljö på en författarinstans. CRXDE Lite ger mindre begränsad åtkomst till CRX-databasen. Klassiska användargränssnittsverktyg och pekaktiverade användargränssnittskonsoler ger mer strukturerad åtkomst till specifika delar av CRX-databasen.

När du har loggat in med administratörsbehörighet finns det olika sätt att få åtkomst till CRXDE Lite:

1. Välj navigering från global navigering **[!UICONTROL Tools > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. Från [klassisk startsida för användargränssnitt](http://localhost:4502/welcome.html), rulla nedåt och klicka **[!UICONTROL CRXDE Lite]** i den högra panelen.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Gå direkt till `CRXDE Lite`: `<server>:<port>/crx/de`

   På en lokal författarinstans: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Om du vill arbeta med CRXDE Lite måste du logga in med utvecklar- eller administratörsbehörighet. Du kan logga in med

* `username: admin`
* `password: admin`


Inloggningen går ut och du måste logga in igen med jämna mellanrum med listrutan till höger i verktygsfältet CRXDE Lite.

Om du inte är inloggad kan du inte navigera i JCR-databasen eller utföra några redigerings-/sparåtgärder.

***Logga in igen när du är osäker!***

![återinloggning](assets/relogin.png)
