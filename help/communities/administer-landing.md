---
title: Communities Sites
seo-title: Communities Sites
description: Översikt över AEM Communities-dokumentationen
seo-description: Översikt över AEM Communities-dokumentationen
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

Det här avsnittet är avsett för dem som administrerar AEM Communities och som är vana vid funktionerna i AEM Communities.

## Översikt {#overview}

En översikt och självstudiekurser för att komma igång finns på:

* [Översikt över AEM Communities](overview.md)
* [Komma igång med AEM Communities](getting-started.md)
* [Komma igång med AEM Communities för aktivering](getting-started-enablement.md)

## Administrations- och konfigurationsområden {#administration-and-configuration-topics}

### Skapande och hantering av communitysajter {#communities-site-creation-and-management}

* Communities- [konsoler](consoles.md)

   * [Webbplatser](sites-console.md)

      * [Grupper (undergrupper)](groups.md)
   * [Moderering](moderation.md)
   * [Hantering av medlemmar och grupper](members.md)
   * [Aktivera resurser](resources.md)
   * [Rapporter](reports.md)


* Communities- [*verktyg *](tools.md):

   * [Webbplatsmallar](sites.md)
   * [Gruppmallar](tools-groups.md)
   * [Community-funktioner](functions.md)
   * [Lagringskonfiguration](srp-config.md)
   * [Komponentguide](components-guide.md)
   * [Badges](badges.md)


### Användargenererat innehåll {#user-generated-content}

En viktig egenskap hos AEM Communities är att skapa användargenererat innehåll (UGC) av besökare som är inloggade på webbplatsen (medlemmar). Mer information om hur du arbetar med UGC finns på:

* [Vanligt UGC-arkiv](working-with-srp.md): val av SRP för delad lagring av UGC
* [Modererar UGC](moderate-ugc.md): pålitliga medlemmar kan moderera UGC-innehåll i bulk eller kontext
* [Taggning UGC](tag-ugc.md): funktioner kan konfigureras så att medlemmar kan tagga innehåll
* [Översätter UGC](translate-ugc.md): funktioner kan konfigureras för att översätta alla användargenererat innehåll eller tillåta medlemmar att översätta valda inlägg
* [Analyskonfiguration](analytics.md): göra det möjligt för Adobe Analytics att rapportera olika mätvärden för medlemsaktivitet

### Community-medlemmar {#community-members}

* [Hantera användare och användargrupper](users.md): information om communitymedlemmar och medlemsgrupper, inklusive behöriga medlemmar
* [Bidragsgränser](limits.md): möjlighet att begränsa bokföring av nya medlemmar
* [Tunneltjänst](deploy-communities.md#tunnel-service-on-author): ger åtkomst till medlemmar på publiceringssidan och medlemsgrupper från författarmiljön
* [Konsoler för medlemmar och grupper](members.md): tillåter att medlemmar och medlemsgrupper på publiceringssidan skapas och hanteras från författarmiljön
* [Användarsynkronisering](sync.md): för synkronisering av medlemmar och medlemsgrupper i flera publiceringsinstanser
* [Social inloggning med Facebook och Twitter](social-login.md): möjlighet för besökare att bli community-medlem med sina Facebook- eller Twitter-behörigheter
* [Betyg och märken](implementing-scoring.md): möjlighet att tilldelas emblem för att identifiera en medlems roll(er) och för medlemmar att få brickor genom sitt deltagande i communityn
* [Meddelanden](notifications.md): möjlighet för medlemmar att underrättas om den aktivitet de följer
* [Prenumerationer](subscriptions.md): möjlighet för medlemmarna att interagera med communityn via extern e-post
* [Meddelanden](messaging.md): möjlighet för medlemmarna att interagera med communityn med hjälp av interna meddelanden

### Aktiveringsfunktioner {#enablement-features}

* [Konfigurerar aktivering](enablement.md): nödvändig information för att korrekt konfigurera aktiveringsfunktionerna
* [Analyskonfiguration](analytics.md): nödvändig information för att aktivera funktioner i Adobe Analytics for Communities
* [Aktiveringsresurser](tag-resources.md)för taggning: nödvändig för att skapa aktiveringskataloger

### Distribution {#deployment}

Distributionsavsnittet innehåller information som är specifik för AEM Communities.

Karaktären på hur man arbetar med communityinnehåll påverkar driftsättningens struktur:

* [Rekommenderade topologier för communities](topologies.md)

Det är viktigt att du installerar den senaste versionen av Communities på AEM-plattformen:

* [Senaste webbgruppsfunktionspaket](deploy-communities.md#latestfeaturepack)

På distributionssidan finns annan information om communities, t.ex. för [uppgradering](upgrade.md), [Dispatcher](dispatcher.md) och [replikering](deploy-communities.md#replication-agents-on-author).

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Distribuera communityn](deploy-communities.md) om du vill veta mer om rekommenderade distributioner.

* Besök [Utvecklingsgrupper](communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar komponenter och funktioner i Communities.

* Besök [Authoring Communities Components](author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar Communities-komponenter.
