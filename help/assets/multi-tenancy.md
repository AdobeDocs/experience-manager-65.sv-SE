---
title: Multi-tenancy för mallar för samlingar, fragment och fragment
description: Lär dig hur ni med funktionen för multi-tenancy kan segmentera innehåll i CRX-databasen baserat på kundorganisationen för att förhindra obehörig åtkomst.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Multi-tenancy för mallar för samlingar, fragment och fragment {#multi-tenancy-for-collections-snippets-and-snippet-templates}

Med funktionen för flera innehavare kan du separera innehåll i CRX baserat på organisationens prefix och organisations-ID för att skydda innehållet från obehörig åtkomst för användare i andra organisationer.

[!DNL Adobe Experience Manager Assets] lagrar data för varje organisation på olika sätt. Varje organisationsspecifik sökväg identifieras av organisationsprefixet och organisations-ID som ingår i den traditionella platsen där olika typer av resurser lagras i CRX.

Om du t.ex. skapar en mapp med namnet `Demo`, lagrar resurser vanligtvis mappen på [!DNL Experience Manager] `../content/dam/Demo`. När multi-tenancy är aktiverat kan du nu lagra data på `../content/dam/<organization prefix>/<organization id>Demo`

Om till exempel [!DNL Adobe Marketing Cloud] användare av [!DNL Assets] (on demand) som har tilldelats `aodpremium` organisationen kan du använda funktionen multi-tenancy för att konfigurera `../content/dam/<mac>/<aodpremium>Demo` sökvägen för att dela upp innehållet. I det här exemplet `mac` är organisationsprefixet och `aodpremium` organisations-ID.

Baserat på användarens organisation och ID visas den här kvalificerade sökvägen i gränssnittet och i olika guider, bland annat guiderna för att flytta och skapa fragment för att framtvinga separering. [!DNL Assets]

Med funktionen Multi-tenancy kan du dela upp följande typer av resurser och komponenter:

* Samlingar
* Offentliga samlingar
* Kataloger (inklusive guiden Lägg till/välj sida)
* Mallar
* Fragmentmallar
* Ljuslåda
