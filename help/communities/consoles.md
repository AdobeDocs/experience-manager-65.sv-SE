---
title: Communities-konsoler
seo-title: Communities Consoles
description: Förklaring av Community-konsoler
seo-description: Community Consoles explained
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Communities-konsoler {#communities-consoles}

AEM Communities-konsolerna, som finns i författarmiljön från den globala navigeringspanelen, ger åtkomst till administrativa uppgifter som:

* [Skapa en communitywebbplats](sites-console.md)
* Lägger till [grupper](groups.md) kapslad inom webbplatsen
* Hantera [mallar för communitysajter](sites.md)
* Hantera [community-medlemmar](members.md)
* [Moderering](moderate-ugc.md) användargenererat innehåll (UGC)
* Skapa [anpassade märken](badges.md)
* Konfigurera [standardlagring för UGC](srp-config.md)

När [UGC-lagring](working-with-srp.md) är konfigurerad att vara en gemensam lagringsplats som delas av författar- och publiceringsmiljöer, [modereringskonsol](moderation.md), som finns i både författar- och publiceringsmiljöer, används i en enda instans av UGC.

När du har loggat in med administratörsbehörighet i redigeringsmiljön visas `Communities` konsoler är tillgängliga från navigerings- och verktygskonsolerna.

>[!NOTE]
>
>I publiceringsmiljön kan du [communitywebbplats](sites-console.md) visar `Administration` menyalternativ när den inloggade medlemmen har lämplig behörighet.

## Global navigeringspanel {#global-navigation-panel}

Välj `Adobe Experience Manager` ikonen i det övre vänstra hörnet för att öppna den globala navigeringspanelen och få tillgång till två ikoner:

* [Navigeringskonsol](#navigation-console)
* [Verktygskonsol](tools.md)

## Navigeringskonsol {#navigation-console}

Om du vill komma åt de olika webbgruppskonsolerna väljer du **navigering, Communities**.

![communities](assets/communities.png)

* [Sites](sites-console.md)

   Webbplatskonsolen är tillgänglig i författarmiljön för att skapa och hantera communitywebbplatser och dess [grupper](groups.md).

* [Moderering](moderation.md)

   Moderationskonsolen används för massmoderering av UGC och i författarmiljön. En liknande masmodereringskonsol är tillgänglig i publiceringsmiljön för communitymedlemmar som tilldelats rollen [community moderator](users.md#publishenvironmentusersandgroups) för en eller flera communitysajter.

* [Medlemmar, grupper](members.md)

   Konsolerna Medlemmar och Grupper används för att hantera communitymedlemmar och medlemsgrupper som finns i publiceringsmiljön från författarmiljön.

* [Rapporter](reports.md)

   I rapportkonsolen kan rapporter om tilldelningar, sidvisningar och publicerat innehåll (UGC) genereras när en communitywebbplats har [aktiverad Adobe Analytics](sites-console.md#analytics). Konsolen är bara tillgänglig i författarmiljön.

## Verktygskonsol {#tools-console}

För åtkomst [Communities Tools](tools.md) (tidigare administrationskonsolen) från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]**
