---
title: Grundläggande om aktivitetsström
seo-title: Activity Stream Essentials
description: Lista över senaste aktiviteter som utförts av en medlem eller en lista över senaste aktiviteter för en enskild tråd med innehåll
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Grundläggande om aktivitetsström {#activity-stream-essentials}

En inloggad community-medlems aktiviteter, till exempel publicering på ett forum eller en blogg, samlas i en ström som kan filtreras och visas på olika sätt genom konfiguration av aktivitetsströmkomponenten.

Möjligheten att följa efter lägger till ytterligare en uppsättning aktiviteter när communitymedlemmar följer inlägg av intresse eller andra communitymedlemmar.

Alla [communitysajter](/help/communities/overview.md#communitiessites) innehåller en användarprofilsida för den inloggade medlemmen som visar medlemsaktiviteter på samma sätt.

## Concepts {#concepts}

An *aktivitetsström* är en lista över de senaste aktiviteterna som utförts av en medlem eller en lista över de senaste aktiviteterna för en enskild innehållstråd, t.ex. ett forumämne eller en blogg.

En medlem kan följa en aktivitetsström antingen efter en annan person eller ett annat innehåll.

A *nyhetsfeed* är en sammanslagning av de aktivitetsströmmar som följs av en medlem till en enda ström.

A *[socialt diagram](/help/communities/essentials-socialgraph.md)* hämtar följande relationer mellan en medlem och en annan medlem.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>sociala/aktiva strömmar/komponenter/hbs/aktivitetsströmmar</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>Se <a href="/help/communities/activities.md">Funktionen Aktivitetsströmmar</a></td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](/help/communities/client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [API för aktivitetsströmmar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API för lyssnare för aktivitetsströmmar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Anpassningar på serversidan](/help/communities/server-customize.md)

### Funktion för aktivitetsström {#activity-stream-function}

En community-webbplatsstruktur som innehåller [Funktionen Aktivitetsström](/help/communities/functions.md#activity-stream-function), innehåller en konfigurerad `activity streams` -komponenten.
