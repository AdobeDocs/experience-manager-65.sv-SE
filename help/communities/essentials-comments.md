---
title: Grundläggande kommentarer
description: Lär dig hur du arbetar med kommentarsystemet (komponenten Comments) och hanterar det användargenererade innehållet (UGC) i inlägg från communitymedlemmar.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Grundläggande kommentarer {#comments-essentials}

Den här sidan innehåller grunderna för hur du arbetar med kommentarsystemet (kommentarkomponenten) och alternativ för att hantera användargenererat innehåll (UGC) som genereras när medlemmar skickar kommentarer eller svar.

Kommentarskomponenten skapar ett kommentarsystem så att varje inlägg representeras av en kommentarkomponent (en). Det är kommentarsystemet som finns på sidan. Kommentarsystemet skapar de enskilda kommentarerna när de anropas.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/gemensam/komponent/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>include</strong></a></td>
   <td>Ja - egenskaper kan redigeras i <i>designläge </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voice</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td> Se <a href="comments.md">Använda kommentarer</a></td>
  </tr>
 </tbody>
</table>

[Anpassningar på klientsidan](client-customize.md)

### En instans per sida {#one-instance-per-page}

Sidnumrering och användning av URL:er för cachelagring och länkning kräver att URL:en är unik per kommentarsystem. Därför tillåts bara en instans av ett kommentarsystem per sida.

Kommentarsystemet finns redan i andra funktioner. Dessa är:

* [Blogg](blog-developer-basics.md)
* [Kalender](calendar-basics-for-developers.md)
* [Filbibliotek](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [QnA](qna-essentials.md)
* [Recensioner](reviews-basics.md)

### Flaggorsakslista {#flag-reason-list}

Anledningslistan för flaggning kan anpassas genom att du lägger till flagreasonlist.hbs i appen för att skriva över det som finns i

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Detta gäller alla komponenter som utökar ett kommentarsystem.

## Grundläggande för serversidan {#essentials-for-server-side}

* [Kommentar-API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Kommentarsslutpunkter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförda kommentarer (UGC) {#accessing-posted-comments-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities omfattar användningen av en [gemensam butik](working-with-srp.md) för UGC programmatisk åtkomst till UGC oavsett valt lagringsalternativ (som ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan varning**.

Se:

* [Lagringsresursprovideröversikt](srp.md) - Översikt över introduktion och databasanvändning.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.
