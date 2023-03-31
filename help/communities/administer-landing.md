---
title: Communities Sites
seo-title: Communities Sites
description: Översikt över AEM Communities-dokumentationen
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Communities Sites {#communities-sites}

Det här avsnittet är avsett för dem som administrerar AEM Communities och som är vana vid AEM Communities funktioner.

## Översikt {#overview}

En översikt och självstudiekurser för att komma igång finns på:

* [AEM Communities - översikt](overview.md)
* [Komma igång med AEM Communities](getting-started.md)

## Administrations- och konfigurationsområden {#administration-and-configuration-topics}

### Skapande och hantering av communitysajter {#communities-site-creation-and-management}

* Communities [konsoler](consoles.md)

   * [Sites](sites-console.md)

      * [Grupper (undergrupper)](groups.md)
   * [Moderering](moderation.md)
   * [Hantering av medlemmar och grupper](members.md)
   * [Rapporter](reports.md)


* Communities [*verktyg*](tools.md):

   * [Webbplatsmallar](sites.md)
   * [Gruppmallar](tools-groups.md)
   * [Community-funktioner](functions.md)
   * [Lagringskonfiguration](srp-config.md)
   * [Komponentguide](components-guide.md)
   * [Badges](badges.md)


### Användargenererat innehåll {#user-generated-content}

En viktig egenskap hos AEM Communities är att skapa användargenererat innehåll (UGC) av besökare som är inloggade på webbplatsen (medlemmar). Mer information om hur du arbetar med UGC finns på:

* [Gemensamt UGC-arkiv](working-with-srp.md): val av SRP för delad lagring av UGC
* [Kontrollerar UGC](moderate-ugc.md): pålitliga medlemmar kan moderera UGC-innehåll i bulk eller kontext
* [Taggning UGC](tag-ugc.md): funktioner kan konfigureras så att medlemmar kan tagga innehåll
* [Översätter UGC](translate-ugc.md): funktioner kan konfigureras för att översätta alla UGC eller tillåta medlemmar att översätta valda inlägg
* [Analyskonfiguration](analytics.md): göra det möjligt för Adobe Analytics att rapportera olika mätvärden för medlemsaktivitet

### Community-medlemmar {#community-members}

* [Hantera användare och användargrupper](users.md): Uppgifter om communitymedlemmar och medlemsgrupper, inklusive behöriga medlemmar.
* [Bidragsgränser](limits.md): möjlighet att begränsa bokföring av nya medlemmar.
* [Tunneltjänst](deploy-communities.md#tunnel-service-on-author): gör att medlemmar och medlemsgrupper på publiceringssidan kan nås från redigeringsmiljön.
* [Konsoler för medlemmar och grupper](members.md): tillåter att medlemmar och medlemsgrupper på publiceringssidan skapas och hanteras från författarmiljön.
* [Användarsynkronisering](sync.md): för synkronisering av medlemmar och medlemsgrupper i flera publiceringsinstanser.
* [Social inloggning med Facebook och Twitter](social-login.md): möjlighet för webbplatsbesökare att bli community-medlemmar med sina Facebook- eller Twitter-behörigheter.
* [Betygsättning och emblem](implementing-scoring.md): Möjlighet att tilldela emblem till att identifiera en medlems roll(er) och för medlemmar att få brickor genom sitt deltagande i communityn.
* [Meddelanden](notifications.md): möjlighet för medlemmar att underrättas om den aktivitet de följer.
* [Prenumerationer](subscriptions.md): möjlighet för medlemmarna att interagera med communityn via extern e-post.
* [Meddelanden](messaging.md): möjlighet för medlemmarna att interagera med communityn med hjälp av interna meddelanden.

### Distribution {#deployment}

Distributionsavsnittet innehåller information som är specifik för AEM Communities.

Karaktären på hur man arbetar med communityinnehåll påverkar driftsättningens struktur:

* [Rekommenderade topologier för communities](topologies.md)

Det är viktigt att du installerar den senaste versionen av Communities på den AEM plattformen:

* [Senaste webbgruppsfunktionspaket](deploy-communities.md#latestfeaturepack)

På distributionssidan finns annan specifik information om Communities, t.ex. för [Uppgraderar](upgrade.md), [Dispatcher](dispatcher.md) och [Replikering](deploy-communities.md#replication-agents-on-author).

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Distribuera webbgrupper](deploy-communities.md) om du vill veta mer om rekommenderade distributioner.

* Besök [Utveckla webbgrupper](communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar komponenter och funktioner i Communities.

* Besök [Komponenter i redigeringsgrupper](author-communities.md) om du vill lära dig hur du redigerar med och konfigurerar Communities-komponenter.
