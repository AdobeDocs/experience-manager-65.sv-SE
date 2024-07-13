---
title: Utveckla webbgrupper
description: Skapa och anpassa communityfunktioner som forum, användargrupper med mera.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Utveckla webbgrupper  {#developing-communities}

## Ökning {#overview}

Adobe Experience Manager (AEM) Communities förenklar framtagning och anpassning av communityfunktioner som forum, användargrupper, bloggar, frågor och svar, kalendrar, kommentarer, granskningar, omröstningar, betygsättning och uppdrag. Dessa funktioner gör att användargenererat innehåll (UGC) anges i publiceringsmiljön.

Grunden för en [community-webbplats](overview.md#communitiessites) är det [sociala ramverket](scf.md) (SCF). Skapandet av en community-webbplats börjar med att du väljer en [community-webbplatsmall](sites-console.md) som består av [community-funktioner](functions.md).

En översikt och självstudiekurser för att komma igång finns på:

* [AEM Communities - översikt](overview.md)
* [Komma igång med AEM Communities](getting-started.md)

>[!NOTE]
> 
>Vi rekommenderar att du håller dig uppdaterad med de [senaste versionerna](deploy-communities.md#latest-releases).

## Rekommenderade distributioner {#recommended-deployments}

* [Community Content Storage](working-with-srp.md): diskuterar de tillgängliga SRP-valen (Social Resource Provider) för en gemensam lagringsplats för användargenererat innehåll
* [Rekommenderade topologier för communities](topologies.md): diskuterar topologier baserat på användningsfall och SRP-val

## Ramverk för sociala komponenter {#social-component-framework}

* [Ramverk för sociala komponenter](scf.md): översikt över ramverk och API:er.
* [SCF Handlebars Helpers](handlebars-helpers.md): standardhjälpredor och hur du skriver anpassade hjälpredor.
* [Anpassning på klientsidan](client-customize.md): anpassar kod som körs i webbläsaren.
* [Anpassning på serversidan](server-customize.md): anpassar kod som körs på servern.
* [Lagringsresursprovider ](srp.md): översikt över lagring av communityinnehåll.
* [Riktlinjer för kodning](code-guide.md): riktlinjer, tips och tricks.
* [Användarhandbok för communitykomponenter](components-guide.md): interaktivt utvecklingsverktyg.

## Grundläggande om komponenter, funktioner och funktioner {#component-function-and-feature-essentials}

AEM Communities komponenter, funktioner och funktioner utgör byggstenarna för [communitywebbplatser](sites-console.md).

* [Grundläggande om komponenter, funktioner och funktioner](essentials.md)
* [Clientlibs for Communities Components](clientlibs.md)
* [Community-funktioner](functions.md)
* [Mallar för communitygrupper](tools-groups.md)
* [Mallar för communitywebbplatser](sites.md)

## Community-medlemmar {#community-members}

* [Hantera användare och användargrupper](users.md)
* [Social Logga in med Facebook och Twitter](social-login.md)

## Community-grupper {#community-groups}

[Community-grupper](overview.md#communitygroups) är ett koncept som tillåter communitymedlemmar att bilda undergrupper på communitywebbplatsen. Skapande av en community-grupp kan ske i publicerings- eller författarmiljön.

* [Grundläggande om communitygrupper](essentials-groups.md)
* [Funktionen Grupper](functions.md#groups-function)
* [Mallar för communitygrupper](tools-groups.md)
* [Hantera användare och användargrupper](users.md)
* [Community Groups for Authors](creating-groups.md)

## Hantera data {#managing-data}

* [SRP och UGC Essentials](srp-and-ugc.md) - Metoder och exempel för SRP API-verktyg
* [Tagg Essentials](tag.md) - möjlighet för communitymedlemmar att tagga UGC- och/eller katalogaktiveringsresurser

## Självstudiekurser {#tutorials}

* [Självstudiekurser på klientsidan](tutorials.md#client-side-customization)
* [Självstudiekurser på servern](tutorials.md#server-side-customization)
* [Instruktioner](tutorials.md#how-to-instructions)

## Felsökning {#troubleshooting}

* [Felsökning](troubleshooting.md)
* [Kända fel](/help/release-notes/release-notes.md)

## Dokumentation för relaterade communities {#related-communities-documentation}

* Gå till [Distribuera communityn](deploy-communities.md) om du vill veta mer om rekommenderade distributioner och Dispatcher-konfiguration.

* Gå till [Administrera communityplatser](administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, konfigurerar mallar för communitywebbplatser, modererar communityinnehåll, hanterar medlemmar och konfigurerar meddelanden.

* Gå till [Komponenter för redigeringsgrupper](author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar webbkomponenterna.
