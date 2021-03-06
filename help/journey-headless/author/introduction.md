---
title: AEM Headless Content Author Journey
description: En introduktion till de kraftfulla och flexibla headlessfunktionerna i Adobe Experience Manager och hur du skapar innehåll för ditt projekt.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Om du skriver för Headless med AEM - en introduktion {#author-headless-introduction}

I den här delen av [AEM Headless Content Author Journey](overview.md)kan du lära dig de (grundläggande) begrepp och termer som behövs för att förstå hur du skapar innehåll för rubrikfri innehållsleverans med Adobe Experience Manager (AEM).

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Syfte**: Innehåller koncept och terminologi för Headless Authoring.

## CMS (Content Management System) {#content-management-system}

Vad är ett innehållshanteringssystem?

CMS (Content Management System) är precis vad det står att det är - ett datorsystem som används för att hantera innehåll. Det är lite allmänt, så för att vara mer exakt används det (vanligtvis) för att hantera innehåll som du vill göra tillgängligt på dina webbplatser.

## Headless CMS {#headless-cms}

Headless är en term som används för att beskriva system som effektivt skiljer innehållet från hur det visas på webben.

Traditionellt sett hanterar du innehållet i ett CMS-system, och samma CMS-system ansvarar för återgivningen av innehållet på webbsidorna.

Nu innebär headless att ditt innehåll kan hanteras i CMS och sedan nås av ett eller flera (oberoende) program.

Det innebär att innehållet kan levereras till alla enheter i en mängd olika format. Detta gör hela processen mycket mer flexibel och innebär också att du inte behöver bekymra dig om layout och formatering.

>[!NOTE]
>
>Om du vill veta mer om den tekniska informationen om Headless CMS kan du läsa mer på Learn About CMS Headless Development.

## Adobe Experience Manager {#aem-cms}

Så vad är AEM?

Först och främst är AEM ett innehållshanteringssystem med många olika funktioner som också kan anpassas efter dina behov.

Detta innebär att det kan användas som

* Headless CMS
   * För headless kan du skapa ditt innehåll som **Innehållsfragment**.
Detta är självständiga innehållsobjekt som kan nås direkt av ett antal program, eftersom de har en fördefinierad struktur som baseras på **Modeller för innehållsfragment**.
Det innebär att innehållet kan nå ut till en mängd olika enheter, i en mängd olika format och med ett stort urval av funktioner.
(Och som en dubbelpanorering kan dessa fragment också användas när du skapar AEM webbsidor - om du vill.)

* &quot;Traditionell&quot; CMS
   * Innehåll skapas för webbsidor med hjälp av en rad komponenter som anger hur innehållet ska återges på webbplatsen. Även här är AEM extremt flexibla eftersom projektteamet kan utveckla anpassade komponenter.

## Innehållsmodellering {#content-modeling}

Innehållsmodellering (även kallat datamodellering) är alltså en annan teknisk term - varför ska det intressera dig som författare?

För att de headless-appar ska kunna komma åt ditt innehåll och göra något med det måste innehållet verkligen ha en fördefinierad struktur. Det skulle vara möjligt att ha ert innehåll som fri form, men det skulle göra livet till *mycket* komplicerade för programmen.

Processen att definiera strukturen för ditt innehåll som ska följas inbegriper att utforma en modell - och detta kallas datamodellering.

För AEM rollen Innehållsarkitekt (ofta en annan person) utför datamodelleringen för att utforma en rad olika **Modeller för innehållsfragment** - som du sedan använder som grund för ditt innehåll genom att använda **Innehållsfragment**.

>[!NOTE]
>
>Om du vill veta mer om datamodellering kan du läsa mer under AEM Headless Content Architect Journey.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig koncept och terminologi är nästa steg att [Lär dig grunderna i att skapa innehållsfragment](basics.md). Då introduceras grundläggande hantering av AEM tillsammans med hur du skapar innehållsfragment.

## Ytterligare resurser {#additional-resources}

* AEM Headless Developer Journey
   * [Läs om CMS Headless Development](/help/journey-headless/developer/learn-about.md)

* [AEM Headless Content Architect Journey](/help/journey-headless/architect/overview.md)

* [AEM Headless Content Translation Journey](/help/journey-headless/translation/overview.md)
