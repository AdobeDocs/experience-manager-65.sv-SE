---
title: Grundläggande om sociala diagram
seo-title: Grundläggande om sociala diagram
description: följ komponent och följande komponentöversikt
seo-description: följ komponent och följande komponentöversikt
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Grundläggande om sociala diagram {#social-graph-essentials}

Möjligheten för en gemenskapsmedlem att följa [verksamheterna](essentials-activities.md) samt att följa dessa är fastställd i två delar:

Den här `follow`komponenten måste associeras med en annan resurs, och den här associationen är redan upprättad för befintliga communitymedlemmar och funktioner på en [communitywebbplats](overview.md#communitiessites).

I `following`komponenten visas de medlemmar som antingen följer den aktuella medlemmen eller som följs av den aktuella medlemmen. Det här sociala diagrammet över relationerna mellan medlemmar ingår i användarprofilen som har skapats för en community-webbplats.

## Grundläggande för klientsidan {#essentials-for-client-side}

### Följande {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>socialt/socialt diagram/komponenter/hbs/relationer</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>Se <a href="socialgraph.md">Använda socialt diagram</a></td>
  </tr>
  <tr>
   <td><strong> optional<br /> property</strong></td>
   <td>
    <ul>
     <li>Namn: <strong><code>outgoing</code></strong></li>
     <li>Typ:Boolean</li>
     <li>Värde:<br />
      <ul>
       <li><i>true </i>- <code>following</code> komponenten visar de medlemmar som den inloggade medlemmen <code>follows</code></li>
       <li><i>false </i>- <code>following</code> komponenten visar de medlemmar som <code>follow </code>den inloggade medlemmen</li>
      </ul> </li>
    </ul> <p>Standardvärdet är <i>true</i> om egenskapen saknas. För närvarande går det inte att ange den här egenskapen i redigeringsdialogrutan i redigeringsläge. Egenskapen måste läggas till i en instans av <code>following </code>noden med <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Följ {#follow}

| **resourceType** | socialt/socialt diagram/komponenter/hbs/följande |
|---|---|
| [**oklanderlig **](scf.md#add-or-include-a-communities-component) | Nej |
| **templates** | /libs/social/socialgraph/components/hbs/following/following.hbs |
| **css** | /libs/social/socialgraph/components/hbs/following/clientlibs/following.css |

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [API för social grafik](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Slutpunkter för socialt diagram](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Anpassningar på serversidan](server-customize.md)

