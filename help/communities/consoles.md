---
title: Communities-konsoler
description: Läs mer om Adobe Experience Manager Community Consoles som är tillgängliga i redigeringsmiljön från den globala navigeringspanelen.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Communities-konsoler {#communities-consoles}

Konsolerna i AEM Communities, som finns i redigeringsmiljön från den globala navigeringspanelen, ger åtkomst till administrativa uppgifter som:

* [Skapa en communitywebbplats](sites-console.md)
* Lägger till [grupper](groups.md) kapslad inom webbplatsen
* Hantera [mallar för communitywebbplatser](sites.md)
* Hantera [community-medlemmar](members.md)
* [Moderering](moderate-ugc.md) användargenererat innehåll (UGC)
* Skapa [anpassade märken](badges.md)
* Konfigurera [standardlagring för UGC](srp-config.md)

När [UGC-lagring](working-with-srp.md) är konfigurerat att vara en gemensam lagringsplats som delas av författar- och publiceringsmiljöer, [modereringskonsol](moderation.md)som finns i både Author- och Publish-miljöer arbetar på en enda instans av UGC.

När du har loggat in med administratörsbehörighet i redigeringsmiljön visas `Communities` konsoler är tillgängliga från navigerings- och verktygskonsolerna.

>[!NOTE]
>
>I publiceringsmiljön kan du [communitywebbplats](sites-console.md) visar en `Administration` menyalternativ när den inloggade medlemmen har lämplig behörighet.

## Global navigeringspanel {#global-navigation-panel}

Välj `Adobe Experience Manager` -ikonen i det övre vänstra hörnet så att du kan öppna den globala navigeringspanelen och komma åt två ikoner:

* [Navigeringskonsol](#navigation-console)
* [Verktygskonsol](tools.md)

## Navigeringskonsol {#navigation-console}

Om du vill komma åt de olika webbgruppskonsolerna väljer du **navigering, Communities**.

![communities](assets/communities.png)

* [Sites](sites-console.md)

  Konsolen Sites är tillgänglig i redigeringsmiljön för att skapa och hantera communitysajter och dess [grupper](groups.md).

* [Moderering](moderation.md)

  Moderationskonsolen används för massmoderering av UGC och i författarmiljön. En liknande masmodereringskonsol är tillgänglig i publiceringsmiljön för communitymedlemmar som tilldelats rollen som [community moderator](users.md#publishenvironmentusersandgroups) för en eller flera communitywebbplatser.

* [Medlemmar, grupper](members.md)

  Konsolerna Medlemmar och Grupper används för att hantera communitymedlemmar och medlemsgrupper som finns i publiceringsmiljön från författarmiljön.

* [Rapporter](reports.md)

  I rapportkonsolen kan rapporter om tilldelningar, sidvisningar och publicerat innehåll (UGC) genereras när en communitywebbplats har [aktiverad Adobe Analytics](sites-console.md#analytics). Konsolen är bara tillgänglig i redigeringsmiljön.

## Verktygskonsol {#tools-console}

För åtkomst [Communities Tools](tools.md) (tidigare administrationskonsolen), från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]**
