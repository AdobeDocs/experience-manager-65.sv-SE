---
title: Grundläggande om sociala diagram
description: Lär dig mer om grunderna i Social Graph genom att använda komponenterna nedan och Följ på en communitywebbplats.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Grundläggande om sociala diagram  {#social-graph-essentials}

Möjligheten för en community-medlem att följa [aktiviteter](essentials-activities.md) och följas har skapats genom två komponenter:

Komponenten `following` måste vara associerad med en annan resurs, och den här associationen har redan upprättats för befintliga communitymedlemmar och funktioner på en [communitywebbplats](overview.md#communitiessites).

Komponenten `following` visar de medlemmar som antingen följer den aktuella medlemmen eller som följs av den aktuella medlemmen. Det här sociala diagrammet över relationerna mellan medlemmar ingår i användarprofilen som har skapats för en community-webbplats.

## Grundläggande för klientsidan {#essentials-for-client-side}

### Följande {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>socialt/socialt diagram/komponenter/hbs/relationer</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
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
   <td><strong> valfri <br />-egenskap</strong></td>
   <td>
    <ul>
     <li>Namn: <strong><code>outgoing</code></strong></li>
     <li>Typ: Boolean</li>
     <li>Värde:<br />
      <ul>
       <li><i>Sant </i>- Komponenten <code>following</code> visar de medlemmar som den inloggade medlemmen tillhör <code>follows</code></li>
       <li><i>Falskt </i>- Komponenten <code>following</code> listar de medlemmar som <code>follow </code> den inloggade medlemmen</li>
      </ul> </li>
    </ul> <p>Standardvärdet är <i>true</i> om egenskapen saknas. Det går inte att ange den här egenskapen i redigeringsdialogrutan i redigeringsläget. Egenskapen måste läggas till i en instans av noden <code>following</code> med <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Följ {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**inkluderbar**](scf.md#add-or-include-a-communities-component) | Nej |
| **mallar** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [API för social grafik](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Slutpunkter för sociala diagram](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Anpassningar på serversidan](server-customize.md)
