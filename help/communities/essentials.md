---
title: Grundläggande om komponenter, funktioner och funktioner
seo-title: Grundläggande om komponenter, funktioner och funktioner
description: Hur communitysajter, mallar och grupper fungerar
seo-description: Hur communitysajter, mallar och grupper fungerar
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Grundläggande om komponenter, funktioner och funktioner {#component-function-and-feature-essentials}

Funktionerna i AEM Communities kräver att besökarna blir medlemmar och loggar in på [communitywebbplatsen](overview.md#communitiessites) innan de kan publicera innehållet. Därför är mallarna [för](sites.md)communitysajter, som används för att [skapa](sites-console.md)en communitywebbplats, utformade för att innehålla en inloggningsfunktion samt användarprofiler, meddelanden, sökning, moderering och översättning.

En communitywebbplats kommer att stödja medlemmar som skapar communitygrupper när funktionen [för](functions.md#groups-function) communitygrupper ingår i den valda communitywebbplatsmallen.

Nedan följer länkar till viktig information för Communities-komponenter, -funktioner och -funktioner.

## Baskomponenter {#base-components}

* [Kommentarer](essentials-comments.md)
* [Recensioner](reviews-basics.md)
* [Tal](tally.md)

   * [Länka](essentials-liking.md)
   * [Klassificering](rating-basics.md)
   * [Omröstning](essentials-voting.md)
   * *Omröstning (ej längre tillgänglig)*

## Komponenter med funktioner {#components-with-functions}

* [Aktivitetsströmmar](essentials-activities.md)
* [Uppdrag](essentials-assignments.md)
* [Blogg](blog-developer-basics.md) ( `Journal`)

* [Kalender](calendar-basics-for-developers.md)
* [Katalog](catalog-developer-essentials.md)
* [Innehåll](essentials-featured.md)
* [Filbibliotek](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Grupper](essentials-groups.md)
* [Ideation](ideation.md)
* [Ledartavla](leaderboard.md)
* [Frågor och svar](qna-essentials.md)`(QnA)`

## Funktioner {#features}

* [Klientbibliotek](clientlibs.md)
* [Community Sites](sites-for-developers.md)
* [OSGi-komponenthändelser](events.md)
* [Komponentsidladdning](sideloading.md)
* [Meddelanden](essentials-messaging.md)
* [RTF-redigerare](rte.md)
* [Betygsättning och emblem](configure-scoring.md)
* [Sökning](search-implementation.md)
* [Social Graph](essentials-socialgraph.md)
* [Lagringsresursprovider](srp-and-ugc.md)`(SRP)`

* [Taggar](tag.md)

## Javadocs {#javadocs}

Javadoskorna [online](../../help/sites-developing/reference-materials.md) återspeglar API:erna i AEM 6.3-versionen.
Communities-API:er finns i `com.adobe.cq.social.*` paket.

För varje [funktionspaket](deploy-communities.md#latestfeaturepack)finns en javadoc burk. Mer information finns på [Using Maven for Communities](maven.md#javadocs).

## Additional Information {#additional-information}

* [Social Component Framework (SCF)](scf.md)

   * [Anpassningar på klientsidan](client-customize.md)
   * [Anpassningar på serversidan](server-customize.md)
   * [Översikt över lagringsresursprovider](srp.md)

* [Riktlinjer för kodning](code-guide.md)
* [Självstudiekurser](tutorials.md)
* [Felsökning](troubleshooting.md)

