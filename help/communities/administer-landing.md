---
title: Communities Sites
description: Läs om grunderna i Adobe Experience Manager (AEM) Communities för administratörer som redan känner till dess grundläggande funktioner.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Communities Sites {#communities-sites}

Det här avsnittet är avsett för dem som administrerar AEM Communities och som är vana vid AEM Communities funktioner.

## Ökning {#overview}

En översikt och självstudiekurser för att komma igång finns på:

* [AEM Communities - översikt](overview.md)
* [Komma igång med AEM Communities](getting-started.md)

## Administrations- och konfigurationsområden {#administration-and-configuration-topics}

### Skapande och hantering av communitysajter {#communities-site-creation-and-management}

* Communities [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Grupper (undergrupper)](groups.md)

   * [Moderering](moderation.md)
   * [Hantering av medlemmar och grupper](members.md)
   * [Rapporter](reports.md)

* Webbgrupper [*verktyg*](tools.md):

   * [Webbplatsmallar](sites.md)
   * [Gruppmallar](tools-groups.md)
   * [Community-funktioner](functions.md)
   * [Lagringskonfiguration](srp-config.md)
   * [Komponentguide](components-guide.md)
   * [Badges](badges.md)


### Användargenererat innehåll {#user-generated-content}

En viktig egenskap hos AEM Communities är att skapa användargenererat innehåll (UGC) av besökare som är inloggade på webbplatsen (medlemmar). Mer information om hur du arbetar med UGC finns på:

* [Allmänt UGC-arkiv](working-with-srp.md): val av SRP för delad lagring av UGC
* [Modererar UGC](moderate-ugc.md): pålitliga medlemmar kan moderera UGC i bulk eller kontext
* [Taggning UGC](tag-ugc.md): funktioner kan konfigureras så att medlemmar kan tagga innehåll
* [Översätter UGC](translate-ugc.md): funktioner kan konfigureras för att översätta alla UGC eller tillåta medlemmar att översätta valda inlägg
* [Analyskonfiguration](analytics.md): aktiverar Adobe Analytics för att rapportera olika mått för medlemsaktivitet

### Community-medlemmar {#community-members}

* [Hantera användare och användargrupper](users.md): information om communitymedlemmar och medlemsgrupper, inklusive behöriga medlemmar.
* [Bidragsgränser](limits.md): möjlighet att begränsa publicering av nya medlemmar.
* [Tunneltjänsten](deploy-communities.md#tunnel-service-on-author): tillåter åtkomst till medlemmar och medlemsgrupper på publiceringssidan från författarmiljön.
* [Medlemmar och grupper-konsoler](members.md): tillåter att medlemmar och medlemsgrupper på publiceringssidan skapas och hanteras från författarmiljön.
* [Användarsynkronisering](sync.md): För synkronisering av medlemmar och medlemsgrupper över flera publiceringsinstanser.
* [Social Logga in med Facebook och Twitter](social-login.md): möjlighet för webbplatsbesökare att bli community-medlemmar med sina inloggningsuppgifter för Facebook eller Twitter.
* [Betygsättning och emblem](implementing-scoring.md): möjlighet att tilldela emblem till att identifiera roller för en medlem och för medlemmar att få brickor genom sitt deltagande i communityn.
* [Meddelanden](notifications.md): Medlemmar kan meddelas om aktivitet som de följer.
* [Prenumerationer](subscriptions.md): Medlemmar kan interagera med communityn via extern e-post.
* [Meddelanden](messaging.md): Medlemmar kan interagera med communityn med hjälp av interna meddelanden.

### Distribution {#deployment}

Distributionsavsnittet innehåller information som gäller AEM Communities.

Karaktären på hur man arbetar med communityinnehåll påverkar driftsättningens struktur:

* [Rekommenderade topologier för communities](topologies.md)

Det är viktigt att du installerar den senaste versionen av Communities på den AEM plattformen:

* [Senaste webbgruppsfunktionspaket](deploy-communities.md#latestfeaturepack)

På distributionssidan finns annan communityspecifik information, t.ex. för [Uppgradering](upgrade.md), [Dispatcher](dispatcher.md) och [replikering](deploy-communities.md#replication-agents-on-author).

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Distribuera communityn](deploy-communities.md) där du kan läsa mer om rekommenderade distributioner.

* Gå till [Utveckla communityn](communities.md) där du kan lära dig mer om det sociala komponentramverket (SCF) och anpassa webbcommunitykomponenter och -funktioner.

* Gå till [Komponenter för redigeringsgrupper](author-communities.md) där du kan lära dig hur du skapar med och konfigurerar webbgruppskomponenter.
