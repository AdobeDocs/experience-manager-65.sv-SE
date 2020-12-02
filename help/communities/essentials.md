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
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 2%

---


# Grundläggande om komponenter, funktioner och funktioner {#component-function-and-feature-essentials}

AEM Communities funktioner kräver att webbplatsbesökarna blir medlemmar och loggar in på [communitywebbplatsen](overview.md#communitiessites) innan de kan publicera innehåll. Därför är [communitymallar](sites.md), från vilka en community-webbplats [skapas](sites-console.md), utformade för att innehålla en inloggningsfunktion samt användarprofiler, meddelanden, sökning, moderering och översättning.

En communitywebbplats stöder medlemmar som skapar communitygrupper när [communitygruppsfunktionen](functions.md#groups-function) inkluderas i den valda communitywebbplatsmallen.

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
* [Blog](blog-developer-basics.md) (  `Journal`)

* [Kalender](calendar-basics-for-developers.md)
* [Katalog](catalog-developer-essentials.md)
* [Innehåll](essentials-featured.md)
* [Filbibliotek](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Grupper](essentials-groups.md)
* [Ideation](ideation.md)
* [Ledartavla](leaderboard.md)
* [Frågor och svar](qna-essentials.md) `(QnA)`

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
* [Lagringsresursprovider](srp-and-ugc.md) `(SRP)`

* [Taggar](tag.md)

## Javadocs {#javadocs}

[online-javadocs](../../help/sites-developing/reference-materials.md) återspeglar de API:er som finns i AEM 6.3.
Communities-API:er finns i `com.adobe.cq.social.*`-paket.

För varje [funktionspaket](deploy-communities.md#latestfeaturepack) finns en javadoc jar tillgänglig. Mer information finns på [Using Maven for Communities](maven.md#javadocs).

## Ytterligare information {#additional-information}

* [Social Component Framework (SCF)](scf.md)

   * [Anpassningar på klientsidan](client-customize.md)
   * [Anpassningar på serversidan](server-customize.md)
   * [Översikt över lagringsresursprovider](srp.md)

* [Riktlinjer för kodning](code-guide.md)
* [Tutorials](tutorials.md)
* [Felsökning](troubleshooting.md)

