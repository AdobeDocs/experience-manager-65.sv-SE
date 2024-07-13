---
title: Grundläggande om komponenter, funktioner och funktioner
description: Hur communitysajter, mallar och grupper fungerar
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# Grundläggande om komponenter, funktioner och funktioner  {#component-function-and-feature-essentials}

Adobe Experience Manager (AEM) Communities-funktioner kräver att webbplatsbesökare blir medlemmar och loggar in på [communitywebbplatsen](overview.md#communitiessites) innan de kan publicera innehåll. Därför är [communitymallar](sites.md), från vilka en communitywebbplats [skapas](sites-console.md), utformade för att innehålla en inloggningsfunktion och användarprofiler, meddelanden, sökning, moderering och översättning.

En community-webbplats har stöd för medlemmar som skapar communitygrupper när [communitygruppsfunktionen](functions.md#groups-function) ingår i den valda communitywebbplatsmallen.

Nedan finns länkar till viktig information för Communities-komponenter, -funktioner och -funktioner.

## Baskomponenter {#base-components}

* [Kommentar](essentials-comments.md)
* [Recensioner](reviews-basics.md)
* [Tal](tally.md)

   * [Länka](essentials-liking.md)
   * [Klassificering](rating-basics.md)
   * [Omröstning](essentials-voting.md)
   * *Avsökning (inte längre tillgängligt)*

## Komponenter med funktioner {#components-with-functions}

* [Aktivitetsströmmar](essentials-activities.md)
* [Blog](blog-developer-basics.md) ( `Journal`)

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
* [Sök](search-implementation.md)
* [Social Graph](essentials-socialgraph.md)
* [Lagringsresursprovider](srp-and-ugc.md) `(SRP)`

* [Taggar](tag.md)

## Javadocs {#javadocs}

[onlinejavadocs](../../help/sites-developing/reference-materials.md) återspeglar de API:er som finns i AEM 6.3-utgåvan.
Communities-API:er finns i `com.adobe.cq.social.*`-paket.

För varje [funktionspaket](deploy-communities.md#latestfeaturepack) finns en javadoc-burk tillgänglig. Mer information finns på [Använda Maven för Communities](maven.md#javadocs).

## Ytterligare information {#additional-information}

* [Social Component Framework (SCF)](scf.md)

   * [Anpassningar på klientsidan](client-customize.md)
   * [Anpassningar på serversidan](server-customize.md)
   * [Översikt över lagringsresursprovider](srp.md)

* [Riktlinjer för kodning](code-guide.md)
* [Självstudiekurser](tutorials.md)
* [Felsökning](troubleshooting.md)
