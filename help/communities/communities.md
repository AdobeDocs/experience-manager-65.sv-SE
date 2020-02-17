---
title: Utveckla webbgrupper
seo-title: Utveckla webbgrupper
description: Skapa och anpassa communityfunktioner som forum, användargrupper med mera
seo-description: Skapa och anpassa communityfunktioner som forum, användargrupper med mera
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utveckla webbgrupper {#developing-communities}

## Översikt {#overview}

AEM Communities förenklar skapandet och anpassningen av communityfunktioner som forum, användargrupper, bloggar, frågor och svar, kalendrar, kommentarer, granskningar, omröstningar, omdömen och uppdrag. Dessa funktioner gör att användargenererat innehåll (UGC) anges i publiceringsmiljön.

Grunden för en [communitywebbplats](overview.md#communitiessites) är den [sociala komponentens ramverk](scf.md) (SCF). Skapandet av en community-webbplats börjar med att en mall [för en](sites-console.md) community väljs som består av [communityfunktioner](functions.md).

En översikt och självstudiekurser för att komma igång finns på:

* [Översikt över AEM Communities](overview.md)
* [Komma igång med AEM Communities](getting-started.md)
* [Komma igång med AEM Communities för aktivering](getting-started-enablement.md)

>[!NOTE]
>
>Vi rekommenderar att du håller dig uppdaterad med de [senaste versionerna](deploy-communities.md#latest-releases).

## Rekommenderade distributioner {#recommended-deployments}

* [Community Content Storage](working-with-srp.md): diskuterar de tillgängliga SRP-valen för en gemensam lagringsplats för användargenererat innehåll
* [Rekommenderade topologier för Communities](topologies.md): diskuterar topologier baserat på användningsfall och SRP-val

## Ramverk för sociala komponenter {#social-component-framework}

* [Ramverk](scf.md)för sociala komponenter: översikt över ramverk och API:er
* [SCF Handlebars Helpers](handlebars-helpers.md): standardhjälpredor och skriva anpassade hjälpprogram
* [Anpassning](client-customize.md)på klientsidan: anpassa kod som körs i webbläsaren
* [Anpassning](server-customize.md)på serversidan: anpassa kod som körs på servern
* [Lagringsresursprovider (SRP)](srp.md): översikt över lagring av communityinnehåll
* [Riktlinjer](code-guide.md)för kodning: riktlinjer, tips och tricks
* [Community Components Guide](components-guide.md): interaktivt utvecklingsverktyg

## Grundläggande om komponenter, funktioner och funktioner {#component-function-and-feature-essentials}

Komponenter, funktioner och funktioner i AEM Communities utgör byggstenarna för [communitysajter](sites-console.md).

* [Grundläggande om komponenter, funktioner och funktioner](essentials.md)
* [Clientlibs for Communities Components](clientlibs.md)
* [Community-funktioner](functions.md)
* [Community-gruppmallar](tools-groups.md)
* [Mallar för communitywebbplatser](sites.md)

## Community-medlemmar {#community-members}

* [Hantera användare och användargrupper](users.md)
* [Social inloggning med Facebook och Twitter](social-login.md)

## Community-grupper {#community-groups}

[Community-grupper](overview.md#communitygroups) är konceptet att tillåta communitymedlemmar att bilda undergrupper på communitywebbplatsen. Skapande av en community-grupp kan ske i publicerings- eller författarmiljön.

* [Grundläggande om communitygrupper](essentials-groups.md)
* [Funktionen Grupper](functions.md#groups-function)
* [Community-gruppmallar](tools-groups.md)
* [Hantera användare och användargrupper](users.md)
* [Community Groups for Authors](creating-groups.md)

## Hantera data {#managing-data}

* [SRP och UGC Essentials](srp-and-ugc.md) - metoder och exempel för SRP API-verktyg
* [Tagg Essentials](tag.md) - möjlighet för communitymedlemmar att tagga UGC- och/eller katalogaktiveringsresurser

## Självstudiekurser {#tutorials}

* [Självstudiekurser på klientsidan](tutorials.md#client-side-customization)
* [Självstudiekurser på serversidan](tutorials.md#server-side-customization)
* [Instruktioner](tutorials.md#how-to-instructions)

## Felsökning {#troubleshooting}

* [Felsökning](troubleshooting.md)
* [Kända fel](/help/release-notes/known-issues.md)

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Distribuera communityn](deploy-communities.md) om du vill veta mer om rekommenderade distributioner och konfigurationer för dispatcher.

* Besök [Administrera communitysajter](administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, konfigurerar mallar för communitysajter, modererar communityinnehåll, hanterar medlemmar och konfigurerar meddelanden.

* Besök [Authoring Communities Components](author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar Communities-komponenter.

