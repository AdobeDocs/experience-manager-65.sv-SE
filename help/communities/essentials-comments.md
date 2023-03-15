---
title: Grundläggande kommentarer
seo-title: Comments Essentials
description: Översikt över komponenten Kommentarer
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Grundläggande kommentarer {#comments-essentials}

På den här sidan finns information om hur du arbetar med kommentarsystemet (kommentarkomponenten) och alternativ för att hantera användargenererat innehåll (UGC) som genereras när medlemmar skickar kommentarer eller svar.

Kommentarskomponenten skapar ett kommentarsystem så att varje inlägg representeras av en kommentarkomponent (en). Det är kommentarsystemet som finns på sidan. Kommentarsystemet skapar de enskilda kommentarerna när de anropas.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/gemensam/komponent/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Ja - egenskaper kan redigeras i <i>design </i>läge</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>klientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.röstning</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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

* [API för kommentarer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Kommentarsslutpunkter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförda kommentarer (UGC) {#accessing-posted-comments-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities används [gemensam lagringsplats](working-with-srp.md) för UGC omfattar programmatisk åtkomst till UGC oavsett vilket lagringsalternativ som valts (till exempel ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över lagringsresursprovider](srp.md) - Översikt över introduktion och databasanvändning.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - Riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.
