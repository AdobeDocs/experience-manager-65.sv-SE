---
title: Multi-tenancy för mallar för samlingar, fragment och fragment
description: Lär dig hur ni med funktionen för multi-tenancy kan segmentera innehåll i CRX-databasen baserat på kundorganisationen för att förhindra obehörig åtkomst.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Multi-tenancy för mallar för samlingar, fragment och fragment {#multi-tenancy-for-collections-snippets-and-snippet-templates}

Med funktionen för flera innehavare kan du separera innehåll i CRX baserat på organisationens prefix och organisations-ID för att skydda innehållet från obehörig åtkomst för användare i andra organisationer.

Adobe Experience Manager (AEM) Assets lagrar data för varje organisation på olika sätt. Varje organisationsspecifik sökväg identifieras av organisationsprefixet och organisations-ID som ingår i den traditionella platsen där olika typer av resurser lagras i CRX.

Om du till exempel skapar en mapp med namnet `Demo`, lagrar AEM-resurserna vanligtvis mappen på `../content/dam/Demo`. När multi-tenancy är aktiverat kan du nu lagra data på `../content/dam/<organization prefix>/<organization id>Demo`

Om till exempel användare av AEM Resurser (on demand) som har tilldelats till [!DNL Adobe Marketing Cloud] organisationen kan du använda funktionen multi-tenancy för att konfigurera `aodpremium` `../content/dam/<mac>/<aodpremium>Demo` sökvägen för att dela upp innehållet. I det här exemplet `mac` är organisationsprefixet och `aodpremium` organisations-ID.

Baserat på användarens organisation och ID visas den här kvalificerade sökvägen i gränssnittet för AEM Resurser och i olika guider, inklusive guiderna för att skapa Flytta och Fragment för att framtvinga separering.

Med funktionen Multi-tenancy kan du dela upp följande typer av resurser och komponenter:

* Samlingar
* Offentliga samlingar
* Kataloger (inklusive guiden Lägg till/välj sida)
* Mallar
* Fragmentmallar
* Ljuslåda
