---
title: Innehållstjänster
seo-title: Innehållstjänster
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---


# Innehållstjänster{#content-services}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Funktionen Innehållstjänster är endast dokumenterad för förhandsgranskning.
>
>Reservation för ändringar i och med lanseringen av 6,3 GA Service Pack 1.

AEM Mobile Content Services är en lättviktig funktion för att begära innehåll som hanteras av AEM. Detta ger alla apputvecklare ett högpresterande sätt att hämta innehåll utan att behöva ha djupa kunskaper om AEM innehållsdatabas (JCR) och webbramverk (Sling). Det gör att de begärande programmen kan frikopplas från innehållsdatabasen.

Content Services introducerar flera nya AEM som gör att en utvecklare kan komma åt AEM hanterat innehåll utan att känna till databasstrukturen för det innehållet.

Dessa konstruktioner är nödvändiga för att bibehålla flexibiliteten och möjliggöra framtida expansion genom att tillhandahålla ett abstraktionslager mellan det AEM hanterade innehållet och de mobilappar som konsumerar innehållet. Detta gör att AEM Content Services kan fungera som ett abstraktionslager mellan det inbyggda programmets innehållskrav och AEM innehållsdatabas.

Content Services kan leverera innehållet som resurser, paketerad HTML (HTML/CSS/JS) eller som kanaloberoende innehåll.

>[!CAUTION]
>
>**Förutsättningar:**
>
>Innan du börjar använda Content Services måste du aktivera flaggan Content Services. Om du vill kunna skapa och hantera modeller i din app måste du aktivera datamodeller i Configuration Browser.
>
>Mer information finns i **[Administrera innehållstjänster](/help/mobile/developing-content-services.md)** och [Configuration Browser](/help/sites-administering/configurations.md) -dokumentationen.

![chlimage_1-143](assets/chlimage_1-143.png)

När du har angett flagga för innehållstjänster och aktiverat datamodeller i Configuration Browser ska du läsa resurserna nedan för att komma igång med AEM Mobile Content Services, lära dig mer om innehållstjänstkoncept som modellhantering, enhetshantering följt av innehållsleverans/rendering för AEM Mobile Content Services.

* Modeller i databas
* Återgivning och leverans
