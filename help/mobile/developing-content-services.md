---
title: Innehållstjänster
description: Lär dig hur du använder AEM Mobile Content Services för att begära innehåll som hanteras av AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Innehållstjänster{#content-services}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Funktionen Innehållstjänster är endast dokumenterad för förhandsgranskning.
>
>Reservation för ändringar i version 6.3 av Service Pack 1.

AEM Mobile Content Services är en lättviktig funktion för att begära innehåll som hanteras av AEM. Detta ger alla apputvecklare ett högpresterande sätt att hämta innehåll utan att behöva ha djupa kunskaper om AEM innehållsdatabas (JCR) och webbramverk (Sling). Det gör att de begärande programmen kan frikopplas från innehållsdatabasen.

Content Services introducerar flera nya AEM som gör att en utvecklare kan komma åt AEM-hanterat innehåll utan att känna till databasstrukturen för det innehållet.

Dessa konstruktioner är nödvändiga för att bibehålla flexibiliteten och möjliggöra framtida expansion genom att tillhandahålla ett abstraktionslager mellan det AEM innehållet och de mobilappar som konsumerar innehållet. Detta gör att AEM Content Services kan fungera som ett abstraktionslager mellan det inbyggda programmets innehållskrav och AEM innehållsdatabas.

Innehållstjänster kan leverera innehållet som resurser, paketerat HTML (HTML/CSS/JS) eller som kanaloberoende innehåll.

>[!CAUTION]
>
>**Förutsättningar:**
>
>Innan du börjar använda Content Services måste du aktivera flaggan Content Services. Aktivera datamodeller i Configuration Browser om du vill skapa och hantera modeller i appen.
>
>Mer information finns i **[Administrera innehållstjänster](/help/mobile/developing-content-services.md)** och dokumentationen för [Configuration Browser](/help/sites-administering/configurations.md).

![chlimage_1-143](assets/chlimage_1-143.png)

När du har angett flaggan Content Services och aktiverat datamodeller i Configuration Browser, se resurserna nedan för att komma igång med AEM Mobile Content Services. Bekanta dig med Content Services-koncept som modellhantering, enhetshantering följt av innehållsleverans/rendering för AEM Mobile Content Services.

* Modeller i databas
* Återgivning och leverans
