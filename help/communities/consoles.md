---
title: Communities-konsoler
seo-title: Communities-konsoler
description: Förklaring av Community-konsoler
seo-description: Förklaring av Community-konsoler
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Communities-konsoler {#communities-consoles}

AEM Communities-konsolerna, som finns i författarmiljön från den globala navigeringspanelen, ger åtkomst till administrativa uppgifter som:

* [Skapa en communitywebbplats](sites-console.md)
* Lägga till [grupper](groups.md) kapslade inom platsen
* Hantera [communitywebbplatsmallar](sites.md)
* Hantera [communitymedlemmar](members.md)
* [Hanterar ](moderate-ugc.md) användargenererat innehåll (UGC)
* Skapa [egna emblem](badges.md)
* Konfigurerar [standardlagring för UGC](srp-config.md)

När [UGC-lagring](working-with-srp.md) är konfigurerad att vara en gemensam butik som delas av författar- och publiceringsmiljöer, fungerar moderationskonsolen [](moderation.md), som är tillgänglig både från författar- och publiceringsmiljöer, på en enda instans av UGC.

När du har loggat in med administratörsbehörighet i redigeringsmiljön är `Communities`-konsolerna tillgängliga i navigerings- och verktygskonsolerna.

>[!NOTE]
>
>I publiceringsmiljön visar en [community-webbplats](sites-console.md) ett `Administration`-menyalternativ när den inloggade medlemmen har lämplig behörighet.

## Global navigeringspanel {#global-navigation-panel}

Välj ikonen `Adobe Experience Manager` i det övre vänstra hörnet för att öppna den globala navigeringspanelen och få tillgång till två ikoner:

* [Navigeringskonsol](#navigation-console)
* [Verktygskonsol](tools.md)

## Navigeringskonsol {#navigation-console}

Om du vill komma åt de olika webbgruppskonsolerna väljer du **navigering, Communities**.

![communities](assets/communities.png)

* [Sites](sites-console.md)

   Konsolen Sites är tillgänglig i författarmiljön för att skapa och hantera communityplatser och dess [grupper](groups.md).

* [Moderering](moderation.md)

   Moderationskonsolen används för massmoderering av UGC och i författarmiljön. En liknande masmodereringskonsol är tillgänglig i publiceringsmiljön för communitymedlemmar som tilldelats rollen [community moderator](users.md#publishenvironmentusersandgroups) för en eller flera communitywebbplatser.

* [Medlemmar, grupper](members.md)

   Konsolerna Medlemmar och Grupper används för att hantera communitymedlemmar och medlemsgrupper som finns i publiceringsmiljön från författarmiljön.

* [Rapporter](reports.md)

   Rapporteringskonsolen är den plats där rapporter om tilldelningar, sidvisningar och publicerat innehåll (UGC) kan genereras när en communitywebbplats har [Adobe Analytics](sites-console.md#analytics) aktiverat. Konsolen är bara tillgänglig i författarmiljön.

* [Resurser](resources.md)

   Resurskonsolen är där [aktiveringshanterare](enablement.md#communitymanagers) skapar, hanterar och tilldelar resurser till medlemmar på en [aktiveringscommunityplats](overview.md#enablement-community). Konsolen är bara tillgänglig i författarmiljön.

## Verktygskonsol {#tools-console}

Om du vill komma åt [Webbgruppsverktyg](tools.md) (tidigare administrationskonsolen) från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]**
