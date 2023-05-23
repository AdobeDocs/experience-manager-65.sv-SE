---
title: Grundläggande om sociala diagram
seo-title: Social Graph Essentials
description: följ komponent och följande komponentöversikt
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Grundläggande om sociala diagram  {#social-graph-essentials}

Möjligheten för en community-medlem att följa [verksamhet](essentials-activities.md) och som ska följas fastställs genom två komponenter:

The `following` måste vara associerad med en annan resurs, och den här associationen har redan upprättats för befintliga communitymedlemmar och funktioner i en [communitywebbplats](overview.md#communitiessites).

The `following` -komponenten visar de medlemmar som antingen följer den aktuella medlemmen eller som följs av den aktuella medlemmen. Det här sociala diagrammet över relationerna mellan medlemmar ingår i användarprofilen som har skapats för en community-webbplats.

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
   <td><strong> valfri<br /> property</strong></td>
   <td>
    <ul>
     <li>Namn: <strong><code>outgoing</code></strong></li>
     <li>Typ: Boolean</li>
     <li>Värde:<br />
      <ul>
       <li><i>True </i>- <code>following</code> -komponenten visar de medlemmar som den inloggade medlemmen <code>follows</code></li>
       <li><i>Falskt </i>- <code>following</code> -komponenten visar de medlemmar som <code>follow </code>den inloggade medlemmen</li>
      </ul> </li>
    </ul> <p>Standardvärdet är <i>true</i> om egenskapen saknas. För närvarande går det inte att ange den här egenskapen i redigeringsdialogrutan i redigeringsläge. Egenskapen måste läggas till i en instans av <code>following </code>nod som använder <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Följ {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**oklanderlig**](scf.md#add-or-include-a-communities-component) | Nej |
| **mallar** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [API för social grafik](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Slutpunkter för socialt diagram](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Anpassningar på serversidan](server-customize.md)
