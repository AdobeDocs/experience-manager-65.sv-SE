---
title: Grundläggande om communitygrupper
description: Lär dig hur behöriga användare kan använda funktionen Community Groups för att dynamiskt skapa en undercommunity på en community-webbplats.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Grundläggande om communitygrupper  {#community-group-essentials}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare från publicerings- och författarmiljöerna.

Från och med [funktionspaketet ](deploy-communities.md#latestfeaturepack) för Communities är det möjligt att kapsla grupper inom andra grupper.

## Grundläggande för klientsidan {#essentials-for-client-side}

### Medlemslista för grupper {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmedlemslist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>egenskaper</strong></td>
   <td>Se <a href="creating-groups.md">Community-grupp</a></td>
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
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
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

* [API för communitygrupp](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Slutpunkter för communitygrupp](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Funktionen Grupper {#groups-function}

En community-webbplatsstruktur som innehåller en [gruppfunktion](functions.md#groups-function) har stöd för att skapa nya `community groups` från publicerings- och författarmiljöerna. Den skapade communitygruppen innehåller en `community groups member list`-komponent som listar medlemmarna i gruppen.

En eller flera [communitygruppsmallar](tools-groups.md), som tillhandahåller designen för communitygruppssidorna, kan konfigureras för funktionen Grupper. Detta gäller när funktionen läggs till i en [community-webbplatsmall](sites.md) eller kapslas i en community-gruppmall.

Om du använder flera mallar för communitygrupper blir det ett val. Det innebär att designvalet presenteras för den behöriga användaren när en community-grupp skapas för communitywebbplatsen. Se avsnittet [communitygrupper](creating-groups.md) för författare.

### Kapslade grupper {#nested-groups}

Från och med Communities [FP1](deploy-communities.md#latestfeaturepack) är det möjligt att en gruppfunktion inkluderas i en gruppmall, vilket möjliggör kapslade grupper (undergrupper).

När en communitywebbplats eller gruppmall innehåller funktionen Grupper kan du:

* Skapa en undercommunity i författarmiljön.

* Skapa en grupp i publiceringsmiljön när den är konfigurerad för att tillåta det.

När du skapar en grupp i författarmiljön måste du först publicera communitywebbplatsen och sedan publicera gruppen. När du publicerar communitywebbplatsen publiceras gruppens sidor, utan att undercommunityns medlemsgrupper som åtkomstkontrollistorna är inställda på skapas. En begränsad (hemlig) grupp kan därför vara synlig tills gruppen uttryckligen publiceras.

## Länkar och tillhörande information {#links-and-related-information}

* [Hantera användare och användargrupper](users.md)
* [Konsolen Communities-grupper](groups.md)
* [Funktionen Grupper](functions.md#groups-function)
* [Gruppmallar](tools-groups.md)
