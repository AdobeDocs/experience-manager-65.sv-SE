---
title: Grundläggande om communitygrupper
seo-title: Grundläggande om communitygrupper
description: Skapa communitysajter dynamiskt
seo-description: Skapa communitysajter dynamiskt
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Grundläggande om communitygrupper {#community-group-essentials}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare från publicerings- och författarmiljöerna.

Från och med [funktionspaket 1](deploy-communities.md#latestfeaturepack)för Communities är det möjligt att kapsla grupper inom andra grupper

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

En community-webbplatsstruktur som innehåller en [gruppfunktion](functions.md#groups-function) har stöd för att skapa nya `community groups` från publicerings- och författarmiljöerna. Den skapade communitygruppen kommer att innehålla en `community groups member list` komponent som visar gruppens medlemmar.

En eller flera mallar [för](tools-groups.md)communitygrupper, som tillhandahåller designen för communitygruppssidor, kan konfigureras för funktionen Grupper när funktionen läggs till i en mall för en [community-webbplats](sites.md) eller kapslas i en mall för communitygrupper.

Om flera communitygruppsmallar ingår visas ett urval av designalternativ för den behöriga användaren när en ny community-grupp skapas för communitywebbplatsen, vilket visas i avsnittet om [communitygrupper](creating-groups.md) för författare.

### Kapslade grupper {#nested-groups}

Från och med Communities [FP1](deploy-communities.md#latestfeaturepack)är det möjligt att inkludera en gruppfunktion i en gruppmall, vilket möjliggör kapslade grupper (undergrupper).

När en communitywebbplats eller gruppmall innehåller funktionen Grupper är det möjligt att

* Skapa en undercommunity i författarmiljön
* Skapa en grupp i publiceringsmiljön när den är konfigurerad för att tillåta den

När du skapar en grupp i författarmiljön måste du först publicera communitywebbplatsen och sedan publicera gruppen. När du publicerar communitywebbplatsen publiceras gruppens sidor, utan att det skapas undercommunityns medlemsgrupper som åtkomstkontrollistorna ställs in på. En begränsad (hemlig) grupp kan därför vara synlig tills gruppen uttryckligen publiceras.

## Länkar och tillhörande information {#links-and-related-information}

* [Hantera användare och användargrupper](users.md)
* [Konsolen Communities Groups](groups.md)
* [Funktionen Grupper](functions.md#groups-function)
* [Gruppmallar](tools-groups.md)

