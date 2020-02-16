---
title: Tagg Essentials
seo-title: Tagg Essentials
description: Översikt över taggar
seo-description: Översikt över taggar
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Tagg Essentials {#tag-essentials}

När AEM Communities-komponenter har konfigurerats med taggning aktiverat, kan communitymedlemmar tagga det innehåll de publicerar i publiceringsmiljön.

Den underliggande infrastrukturen för taggar som används i publiceringsmiljön är densamma som för taggar som används på innehåll i redigeringsmiljön, till exempel sidor och resurser:

* Mer information om hur du skapar och hanterar taggar finns i [Administrera taggar](../../help/sites-administering/tags.md) och [tagga användargenererat innehåll](tag-ugc.md) (UGC).

* Mer information om [taggningsramverket](../../help/sites-developing/tags.md) samt om hur du inkluderar och utökar taggar i [anpassade program finns i](../../help/sites-developing/framework.md) Tagga för utvecklare [](../../help/sites-developing/building.md).

* Se [Använda molnet](tagcloud.md) för sociala taggar för information om hur författare lägger till en `social tag cloud` komponent på en sida för att markera de taggar som används i UGC i publiceringsmiljön.

* Mer information om hur du taggar resurser [för kataloger finns i](tag-resources.md) Tagga aktiveringsresurser.

Taggning av UGC kan aktiveras när du konfigurerar en [communitywebbplats](sites-console.md#tagging) eller någon av följande funktioner:

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
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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

* [API för socialt taggmoln](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social Tag Manager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

## Taggsökning {#tag-searching}

Från och med [funktionspaket 1](deploy-communities.md#latestfeaturepack) (FP1) utförs taggsökning med [taggtitlar](../../help/sites-developing/framework.md#tag-characteristics).

Före FP1 utfördes sökningen med [tagg-ID](../../help/sites-developing/framework.md#tagid).
