---
title: Skapa en SCF-sandlåda
seo-title: Skapa en SCF-sandlåda
description: Den här självstudiekursen är främst avsedd för utvecklare som är nybörjare i AEM och som är intresserade av att använda SCF-komponenter.  Här går vi igenom hur man skapar en SCF-sandlådeplats
seo-description: Den här självstudiekursen är främst avsedd för utvecklare som är nybörjare i AEM och som är intresserade av att använda SCF-komponenter.  Här går vi igenom hur man skapar en SCF-sandlådeplats
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---



# Skapa en SCF-sandlåda {#create-an-scf-sandbox}


Från och med AEM 6.1 Communities är det enklaste sättet att snabbt skapa en sandlåda att skapa en community-webbplats. Se [Komma igång med AEM Communities](getting-started.md).

Ett annat användbart verktyg för utvecklare är [Community Components Guide](components-guide.md), som gör det möjligt att utforska och snabbt skapa prototyper för Communities-komponenter och -funktioner.

Att skapa en webbplats kan vara användbart för att förstå strukturen på en AEM-webbplats, som kan innehålla webbgruppsfunktioner, samtidigt som det finns enkla sidor där man kan utforska arbetet med ramverket för [sociala komponenter (SCF)](scf.md).

Den här självstudiekursen är främst avsedd för utvecklare som är nybörjare i AEM och som är intresserade av att använda SCF-komponenter. Här beskrivs hur du skapar en SCF-sandlådewebbplats, ungefär som självstudiekursen [How to Create a Fully Featured Internet Website](../../help/sites-developing/website.md) , som fokuserar på webbplatsstrukturer som navigering, logotyp, sökning, verktygsfält och listning av underordnade sidor.

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
>I den här självstudiekursen skapas ingen communitywebbplats med de funktioner som har skapats med konsolen [](sites-console.md)Communities Sites. I den här självstudiekursen beskrivs till exempel inte hur du konfigurerar inloggning, självregistrering, [social inloggning](social-login.md), meddelanden, profiler och så vidare.
>
>Om du föredrar en enkel communitywebbplats ska du följa självstudiekursen [Skapa en exempelsida](create-sample-page.md) .

## Förutsättningar {#prerequisites}

I den här självstudien antas att du har en AEM-författare och en AEM-publiceringsinstans installerad som har den [senaste versionen](deploy-communities.md#latest-releases) av Communities.

Nedan följer några praktiska länkar för utvecklare som är nya på AEM-plattformen:

* [Komma igång](../../help/sites-deploying/deploy.md#getting-started): för distribution av AEM-instanser

   * [Grunderna](../../help/sites-developing/the-basics.md): för utvecklare av webbplatser och funktioner
   * [Steg 1 för författare](../../help/sites-authoring/first-steps.md): för att skapa sidinnehåll

## Använda CRXDE Lite Development Environment {#using-crxde-lite-development-environment}

AEM-utvecklare tillbringar mycket tid i utvecklingsmiljön [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) på en författarinstans. CRXDE Lite ger mindre begränsad åtkomst till CRX-databasen. Klassiska användargränssnittsverktyg och pekaktiverade användargränssnittskonsoler ger mer strukturerad åtkomst till specifika delar av CRX-databasen.

När du har loggat in med administratörsbehörighet finns det olika sätt att få åtkomst till CRXDE Lite:

1. Välj Navigeringsverktyg **[!UICONTROL > CRXDE Lite]** i den globala navigeringen.

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. På välkomstsidan [för det](http://localhost:4502/welcome.html)klassiska användargränssnittet bläddrar du nedåt och klickar på **[!UICONTROL CRXDE Lite]** i den högra panelen.

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. Bläddra direkt till `CRXDE Lite`: `<server>:<port>/crx/de`

   På en lokal författarinstans: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Om du vill arbeta med CRXDE Lite måste du logga in med utvecklar- eller administratörsbehörighet. För standardinstansen av localhost kan du logga in med

* `username: admin`
* `password: admin`


**Tänk på** att den här inloggningen kommer att timeout och du måste logga in igen regelbundet med hjälp av listrutan till höger i verktygsfältet CRXDe Lite.

Om du inte är inloggad kan du inte navigera i JCR-databasen eller utföra några redigerings-/sparåtgärder.

***När du är osäker, logga in igen!***

![chlimage_1-352](assets/chlimage_1-352.png)
