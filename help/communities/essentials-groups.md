---
title: Grundläggande om communitygrupper
seo-title: Community Group Essentials
description: Skapa communitysajter dynamiskt
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Grundläggande om communitygrupper  {#community-group-essentials}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare från publicerings- och författarmiljöerna.

Från och med Communities [funktionspaket 1](deploy-communities.md#latestfeaturepack)kan grupper kapslas i andra grupper

## Grundläggande för klientsidan {#essentials-for-client-side}

### Medlemslista för communitygrupper {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmedlemslist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>egenskaper</strong></td>
   <td>Se <a href="creating-groups.md">Community Group</a></td>
  </tr>
 </tbody>
</table>

### Community-grupper {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/grupp/komponenter/hbs/communityggrupper</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [API för användargrupper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Slutpunkter för communitygrupp](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Funktionen Grupper {#groups-function}

En community-webbplatsstruktur som innehåller [Funktionen Grupper](functions.md#groups-function) kommer att stödja skapandet av nya `community groups` från publicerings- och författarmiljöerna. Den skapade communitygruppen kommer att innehålla en `community groups member list` som listar medlemmarna i gruppen.

En eller flera [communitygruppsmallar](tools-groups.md), som tillhandahåller designen för communitygruppssidor, kan konfigureras för funktionen Grupper när funktionen läggs till i en [mall för communitywebbplats](sites.md) eller kapslad i en community-gruppmall.

Om flera communitygruppsmallar ingår visas ett val av design för den behöriga användaren när en ny community-grupp skapas för communitywebbplatsen, vilket visas i avsnittet om [communitygrupper](creating-groups.md) för författare.

### Kapslade grupper {#nested-groups}

Från och med Communities [FP1](deploy-communities.md#latestfeaturepack)kan en gruppfunktion inkluderas i en gruppmall, vilket gör att det går att använda kapslade grupper (undergrupper).

När en communitywebbplats eller gruppmall innehåller funktionen Grupper kan du:

* Skapa en undercommunity i författarmiljön.

* Skapa en grupp i publiceringsmiljön när den är konfigurerad för att tillåta det.

När du skapar en grupp i författarmiljön måste du först publicera communitywebbplatsen och sedan publicera gruppen. När du publicerar communitywebbplatsen publiceras gruppens sidor, utan att det skapas undercommunityns medlemsgrupper som åtkomstkontrollistorna ställs in på. En begränsad (hemlig) grupp kan därför vara synlig tills gruppen uttryckligen publiceras.

## Länkar och tillhörande information {#links-and-related-information}

* [Hantera användare och användargrupper](users.md)
* [Konsolen Communities Groups](groups.md)
* [Funktionen Grupper](functions.md#groups-function)
* [Gruppmallar](tools-groups.md)
