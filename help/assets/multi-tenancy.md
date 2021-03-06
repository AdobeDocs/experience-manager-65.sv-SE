---
title: Multi-tenancy för mallar för samlingar, fragment och fragment
description: Lär dig hur ni med funktionen för multi-tenancy kan segmentera innehåll i CRX-databasen baserat på kundorganisationen för att förhindra obehörig åtkomst.
contentOwner: AG
role: Architect, Admin, Leader
feature: Samlingar
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 1%

---

# Multi-tenancy för mallar för samlingar, fragment och fragment {#multi-tenancy-for-collections-snippets-and-snippet-templates}

Med funktionen för flera innehavare kan du separera innehåll i CRX baserat på organisationens prefix och organisations-ID för att skydda innehållet från obehörig åtkomst för användare i andra organisationer.

[!DNL Adobe Experience Manager Assets] lagrar data för varje organisation på olika sätt. Varje organisationsspecifik sökväg identifieras av organisationens prefix och organisations-ID
som ingår i den traditionella platsen där olika typer av resurser lagras i CRX.

Om du till exempel skapar en mapp med namnet `Demo`, lagrar [!DNL Experience Manager]-resurser vanligtvis mappen på `../content/dam/Demo`. När multi-tenancy är aktiverat kan du nu lagra data på `../content/dam/<organization prefix>/<organization id>Demo`

Om du till exempel har [!DNL Adobe Marketing Cloud]-användare av [!DNL Assets] (on demand) som är tilldelade till `aodpremium`-organisationen kan du använda funktionen multi-tenancy för att konfigurera `../content/dam/<mac>/<aodpremium>Demo`-sökvägen för att dela upp innehållet. I det här exemplet är `mac` organisationsprefixet och `aodpremium` organisations-ID.

Baserat på användarens organisation och ID visas den här kvalificerade sökvägen i [!DNL Assets]-gränssnittet och i olika guider, inklusive guiderna för att skapa Flytta och Fragment för att framtvinga separation.

Med funktionen Multi-tenancy kan du dela upp följande typer av resurser och komponenter:

* Samlingar
* Offentliga samlingar
* Kataloger (inklusive guiden Lägg till/välj sida)
* Mallar
* Fragmentmallar
* Ljuslåda
