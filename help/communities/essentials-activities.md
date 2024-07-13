---
title: Grundläggande om aktivitetsström
description: Lista över senaste aktiviteter som utförts av en medlem eller en lista över senaste aktiviteter för en enskild tråd med innehåll
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Grundläggande om aktivitetsström {#activity-stream-essentials}

En inloggad community-medlems aktiviteter, till exempel publicering på ett forum eller en blogg, samlas i en ström som kan filtreras och visas på olika sätt genom konfiguration av aktivitetsströmkomponenten.

Möjligheten att följa efter lägger till ytterligare en uppsättning aktiviteter när communitymedlemmar följer inlägg av intresse eller andra communitymedlemmar.

Alla [communitywebbplatser](/help/communities/overview.md#communitiessites) innehåller en användarprofilsida för den inloggade medlemmen som visar medlemsaktiviteter på samma sätt.

## Concepts {#concepts}

En *aktivitetsström* är en lista över de senaste aktiviteterna som utförts av en medlem eller en lista över de senaste aktiviteterna för en enskild tråd med innehåll, till exempel ett forumämne eller en blogg.

En medlem kan följa en aktivitetsström antingen efter en annan person eller ett annat innehåll.

En *nyhetsfeed* är en sammanslagning av aktivitetsströmmar som följs av en medlem till en enda ström.

Ett *[socialt diagram](/help/communities/essentials-socialgraph.md)* fångar följande relationer mellan en medlem och en annan.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>sociala/aktiva strömmar/komponenter/hbs/aktivitetsströmmar</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td>Se funktionen <a href="/help/communities/activities.md">Aktivitetsströmmar</a></td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](/help/communities/client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [API för aktivitetsströmmar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API för lyssnare för aktivitetsströmmar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Anpassningar på serversidan](/help/communities/server-customize.md)

### Funktion för aktivitetsström {#activity-stream-function}

En community-webbplatsstruktur som innehåller funktionen [Aktivitetsström](/help/communities/functions.md#activity-stream-function) innehåller en konfigurerad `activity streams` -komponent.
