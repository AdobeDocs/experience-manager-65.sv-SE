---
title: Communities-konsoler
description: Läs mer om Adobe Experience Manager Community Consoles som är tillgängliga i redigeringsmiljön från den globala navigeringspanelen.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Communities-konsoler {#communities-consoles}

Konsolerna i AEM Communities, som finns i redigeringsmiljön från den globala navigeringspanelen, ger åtkomst till administrativa uppgifter som:

* [Skapa en communitywebbplats](sites-console.md)
* Lägger till [grupper](groups.md) som är kapslade på webbplatsen
* Hantera [communitywebbplatsmallar](sites.md)
* Hantera [communitymedlemmar](members.md)
* [Modererar](moderate-ugc.md) användargenererat innehåll (UGC)
* Skapa [egna emblem](badges.md)
* Konfigurerar standardlagringsutrymmet [för UGC](srp-config.md)

När [UGC-lagring](working-with-srp.md) är konfigurerad att vara en gemensam lagringsplats som delas av författare- och Publish-miljöer, fungerar [moderationskonsolen](moderation.md), som är tillgänglig både från författare- och Publish-miljöer, på en enda instans av UGC.

När du har loggat in med administratörsbehörighet i redigeringsmiljön är konsolerna `Communities` tillgängliga från navigerings- och verktygskonsolerna.

>[!NOTE]
>
>I Publish-miljön visar en [community-webbplats](sites-console.md) ett `Administration`-menyalternativ när den inloggade medlemmen har lämplig behörighet.

## Global navigeringspanel {#global-navigation-panel}

Välj ikonen `Adobe Experience Manager` i det övre vänstra hörnet så att du kan öppna den globala navigeringspanelen och få tillgång till två ikoner:

* [Navigeringskonsol](#navigation-console)
* [Verktygskonsol](tools.md)

## Navigeringskonsol {#navigation-console}

Om du vill komma åt de olika webbgruppskonsolerna väljer du **navigering, Communities** från global navigering.

![communities](assets/communities.png)

* [Sites](sites-console.md)

  Konsolen Platser är tillgänglig i redigeringsmiljön för att skapa och hantera communityplatser och dess [grupper](groups.md).

* [Moderering](moderation.md)

  Moderationskonsolen används för massmoderering av UGC och i författarmiljön. En liknande masmodereringskonsol är tillgänglig i Publish-miljön för communitymedlemmar som tilldelats rollen [community-moderator](users.md#publishenvironmentusersandgroups) för en eller flera communitywebbplatser.

* [Medlemmar, grupper](members.md)

  Konsolerna Medlemmar och Grupper används för att hantera communitymedlemmar och medlemsgrupper som finns i Publish-miljön från författarmiljön.

* [Rapporter](reports.md)

  Rapportkonsolen är där rapporter om tilldelningar, sidvisningar och publicerat innehåll (UGC) kan genereras när en communitywebbplats har [aktiverat Adobe Analytics](sites-console.md#analytics). Konsolen är bara tillgänglig i redigeringsmiljön.

## Verktygskonsol {#tools-console}

Om du vill komma åt [webbgruppsverktyg](tools.md) (tidigare administrationskonsolen) från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]**
