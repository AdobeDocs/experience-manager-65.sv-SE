---
title: Tagg Essentials
description: Lär dig mer om när webbgruppskomponenter har konfigurerats med taggning aktiverat, så kan communitymedlemmar tagga innehåll som de publicerar i publiceringsmiljön.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Tagg Essentials {#tag-essentials}

När AEM Communities-komponenter har konfigurerats med taggning aktiverat, kan communitymedlemmar tagga det innehåll de publicerar i publiceringsmiljön.

Den underliggande infrastrukturen för taggar som används i publiceringsmiljön är densamma som för taggar som används på innehåll i redigeringsmiljön, till exempel sidor och resurser:

* Mer information om hur du skapar och hanterar taggar finns i [Administrera taggar](../../help/sites-administering/tags.md) och [Tagga användargenererat innehåll](tag-ugc.md) (UGC).

* Mer information om [taggningsramverket](../../help/sites-developing/framework.md) och om hur du inkluderar och utökar taggar i [anpassade program](../../help/sites-developing/building.md) finns i [Tagga för utvecklare](../../help/sites-developing/tags.md).

* Se [Använda molnet för sociala taggar](tagcloud.md) för information om hur författare lägger till en `social tag cloud`-komponent på en sida för att markera de taggar som används i användargenererat innehåll i publiceringsmiljön.

Taggning av UGC kan vara aktiverad när du konfigurerar en [community-webbplats](sites-console.md#tagging) eller någon av följande funktioner:

* [Blogg](blog-feature.md)
* [Kalender](calendar.md)
* [Filbibliotek](file-library.md)
* [Forum](forum.md)
* [QnA](working-with-qna.md)

## Grundläggande för klientsidan {#essentials-for-client-side}

### Social Tag Cloud {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/komma/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>egenskaper</strong></td>
   <td>Se <a href="tagcloud.md">Använda molnet för sociala taggar</a></td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Cloud-API:t för sociala taggar](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Hanteraren för sociala taggar](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

## Taggsökning {#tag-searching}

Från och med [funktionspaket 1](deploy-communities.md#latestfeaturepack) (FP1) utförs taggsökning med [taggtitlar](../../help/sites-developing/framework.md#tag-characteristics).

Före FP1 utfördes sökningen med [tagg-ID](../../help/sites-developing/framework.md#tagid).
