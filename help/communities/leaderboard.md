---
title: Grundläggande om Ledningsbord
description: Lär dig hur du konfigurerar poängsättning och märkning för communityn så att du kan arbeta med komponenten Ledpanel i Adobe Experience Manager Communities.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Grundläggande om Ledningsbord {#leaderboard-essentials}

Den här sidan innehåller viktig information om hur du arbetar med funktionen Ledpanel.

Innan du inkluderar huvudpanelskomponenten på en sida måste du konfigurera [Webbgruppsbedömning och badges](implementing-scoring.md).

Se [Grundläggande om poäng och emblem](configure-scoring.md).

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/leaderboard</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>Se <a href="enabling-leaderboard.md">Ledarbordsfunktion</a></td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](client-customize.md)

### Filbiblioteksfunktion {#file-library-function}

En community-webbplatsstruktur som innehåller [Ledarpanelsfunktionen](functions.md#leaderboard-function), innehåller en konfigurerad `leaderboard`-komponent.
