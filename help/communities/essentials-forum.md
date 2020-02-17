---
title: Grundläggande om forum
seo-title: Grundläggande om forum
description: Översikt över forum
seo-description: Översikt över forum
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Grundläggande om forum {#forum-essentials}

Den här sidan innehåller viktig information om hur du arbetar med forumfunktionen.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voice<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>Se <a href="forum.md">forumfunktion</a></td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Forum-API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Slutpunkter för forum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Forum {#forum-function}

En community-webbplatsstruktur som innehåller [forumfunktionen](functions.md#forum-function), innehåller en konfigurerad `forum` komponent samt inställningar som påverkar moderering, taggning och översättning.

### Åtkomst till foruminlägg (UGC) {#accessing-forum-posts-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Moderera användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities omfattar användningen av en [gemensam butik](working-with-srp.md) för UGC programmatisk åtkomst till UGC oavsett valt lagringsalternativ (som ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över](srp.md) lagringsresursprovidern - introduktion och databasanvändning - översikt
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning
* [Omfaktorisering för SocialUtils](socialutils.md) - mappning av utgått verktygsmetoder till aktuella SRP-verktygsmetoder

