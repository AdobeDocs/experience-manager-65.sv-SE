---
title: Skapa en SCF-sandlåda
seo-title: Skapa en SCF-sandlåda
description: Den här självstudiekursen är främst avsedd för utvecklare som inte är AEM och som är intresserade av att använda SCF-komponenter.  Här går vi igenom hur man skapar en SCF-sandlådeplats
seo-description: Den här självstudiekursen är främst avsedd för utvecklare som inte är AEM och som är intresserade av att använda SCF-komponenter.  Här går vi igenom hur man skapar en SCF-sandlådeplats
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---



# Skapa en SCF-sandlåda {#create-an-scf-sandbox}


Från och med AEM 6.1 Communities är det enklaste sättet att snabbt skapa en sandlåda att skapa en community-webbplats. Se [Komma igång med AEM Communities](getting-started.md).

Ett annat användbart verktyg för utvecklare är [Community Components Guide](components-guide.md), som gör det möjligt att utforska och snabbt skapa prototyper för Communities-komponenter och -funktioner.

Att skapa en webbplats kan vara användbart för att förstå strukturen hos en AEM webbplats som kan innehålla webbgruppsfunktioner, samtidigt som det finns enkla sidor där du kan utforska arbetet med [ramverket för sociala komponenter (SCF)](scf.md).

Den här självstudiekursen är främst avsedd för utvecklare som inte är AEM och som är intresserade av att använda SCF-komponenter. Här går vi igenom hur du skapar en SCF-sandlådewebbplats, ungefär som självstudiekursen för [Skapa en webbplats med alla funktioner](../../help/sites-developing/website.md) som fokuserar på webbplatsstrukturer som navigering, logotyp, sökning, verktygsfält och lista med underordnade sidor.

Utvecklingen sker i en författarinstans, medan det är bäst att experimentera med webbplatsen i en publiceringsinstans.

Stegen i den här självstudiekursen är:

* [Konfigurera webbplatsstruktur](setup-website.md)
* [Ursprungligt sandlådeprogram](initial-app.md)
* [Ursprungligt sandlådeinnehåll](initial-content.md)
* [Utveckla sandlådeprogram](develop-app.md)
* [Lägg till klienter](add-clientlibs.md)
* [Utveckla innehåll i sandlådan](develop-content.md)

>[!CAUTION]
>
>I den här självstudien skapas ingen communitywebbplats med de funktioner som skapats med [Webbplatskonsolen](sites-console.md). I den här självstudiekursen beskrivs till exempel inte hur du konfigurerar inloggning, självregistrering, [social inloggning](social-login.md), meddelanden, profiler och så vidare.
>
>Om du föredrar en enkel community-webbplats följer du självstudiekursen [Skapa en exempelsida](create-sample-page.md).

## Förutsättningar {#prerequisites}

I den här självstudien antas att du har en AEM författare och en AEM publiceringsinstans installerad som har [den senaste versionen](deploy-communities.md#latest-releases) av Communities.

Nedan följer några praktiska länkar för utvecklare som är nya för den AEM plattformen:

* [Komma igång](../../help/sites-deploying/deploy.md#getting-started): för att distribuera AEM instanser.

   * [Grunderna](../../help/sites-developing/the-basics.md): för utvecklare av webbplatser och funktioner.
   * [Steg 1 för författare](../../help/sites-authoring/first-steps.md): för att skapa sidinnehåll.

## Använda CRXDE Lite Development Environment {#using-crxde-lite-development-environment}

AEM utvecklare tillbringar mycket tid i [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)-utvecklingsmiljön på en författarinstans. CRXDE Lite ger mindre begränsad åtkomst till CRX-databasen. Klassiska användargränssnittsverktyg och pekaktiverade användargränssnittskonsoler ger mer strukturerad åtkomst till specifika delar av CRX-databasen.

När du har loggat in med administratörsbehörighet finns det olika sätt att få åtkomst till CRXDE Lite:

1. Välj navigering **[!UICONTROL Tools > CRXDE Lite]** från global navigering.

   ![crxde-lite](assets/tools-crxde.png)

2. Bläddra nedåt från [den klassiska gränssnittets välkomstsida](http://localhost:4502/welcome.html) och klicka på **[!UICONTROL CRXDE Lite]** i den högra panelen.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Bläddra direkt till `CRXDE Lite`: `<server>:<port>/crx/de`

   På en lokal författarinstans: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Om du vill arbeta med CRXDE Lite måste du logga in med utvecklar- eller administratörsbehörighet. För standardinstansen av localhost kan du logga in med

* `username: admin`
* `password: admin`


**Tänk** på att den här inloggningen kommer att tidsgränsen överskrids och du måste logga in igen med jämna mellanrum med listrutan till höger i verktygsfältet CRXDe Lite.

Om du inte är inloggad kan du inte navigera i JCR-databasen eller utföra några redigerings-/sparåtgärder.

***När du är osäker, logga in igen!***

![återinloggning](assets/relogin.png)
