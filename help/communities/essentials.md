---
title: Grundläggande om komponenter, funktioner och funktioner
seo-title: Component, Function and Feature Essentials
description: Hur communitysajter, mallar och grupper fungerar
seo-description: How community sites, templates, and groups function
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 2%

---

# Grundläggande om komponenter, funktioner och funktioner  {#component-function-and-feature-essentials}

AEM Communities funktioner kräver att besökarna blir medlemmar och loggar in på [communitywebbplats](overview.md#communitiessites) innan du kan publicera innehåll. Således [mallar för communitysajter](sites.md), från vilken en communitywebbplats [skapad](sites-console.md), är utformade för att innehålla en inloggningsfunktion samt användarprofiler, meddelanden, sökning, moderering och översättning.

En communitywebbplats kommer att stödja medlemmar som skapar communitygrupper när [communitygruppsfunktion](functions.md#groups-function) ingår i den valda communitywebbplatsmallen.

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
* [Blogg](blog-developer-basics.md) ( `Journal`)

* [Kalender](calendar-basics-for-developers.md)
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

The [online javadocs](../../help/sites-developing/reference-materials.md) speglar de API:er som finns i AEM 6.3.
Communities-API:er finns i `com.adobe.cq.social.*` paket.

För varje [funktionspaket](deploy-communities.md#latestfeaturepack), finns en javadoc burk tillgänglig. Mer information finns på [Använda Maven for Communities](maven.md#javadocs).

## Ytterligare information {#additional-information}

* [Social Component Framework (SCF)](scf.md)

   * [Anpassningar på klientsidan](client-customize.md)
   * [Anpassningar på serversidan](server-customize.md)
   * [Översikt över lagringsresursprovider](srp.md)

* [Riktlinjer för kodning](code-guide.md)
* [Självstudiekurser](tutorials.md)
* [Felsökning](troubleshooting.md)
