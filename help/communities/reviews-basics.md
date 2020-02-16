---
title: Grundläggande granskningar
seo-title: Grundläggande granskningar
description: Granska och Granska sammanfattningskomponenter
seo-description: Granska och Granska sammanfattningskomponenter
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Grundläggande granskningar {#reviews-essentials}

Den här funktionen består av två komponenter som fungerar tillsammans: recensioner och sammanfattning.

Recensioner är en sammansatt komponent som baseras på ett [kommentarsystem](essentials-comments.md) som innehåller en eller flera [klassificeringskomponenter](rating-basics.md) (tally).

Anonym publicering av en granskning stöds inte. Besökare på webbplatsen måste registrera sig och logga in för att kunna lägga till en granskning. Den inloggade besökaren (medlemmen) kan uppdatera sin granskning när som helst.

## Grundläggande för klientsidan {#essentials-for-client-side}

### Recensioner {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Ja - egenskaper kan redigeras i <i></i>designläge</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>egenskaper</strong></td>
   <td>Se <a href="reviews.md">Använda granskningar</a></td>
  </tr>
 </tbody>
</table>

### Granska sammanfattning {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**oklanderlig **](scf.md#add-or-include-a-communities-component) | Ja - egenskaper kan redigeras i *design *läge |
| [**klientlibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **egenskaper** | Se [Använda granskningar](reviews.md) |

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Granska API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Granska slutpunkter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförda granskningar (UGC) {#accessing-posted-reviews-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Moderera användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities omfattar användningen av en [gemensam butik](working-with-srp.md) för UGC programmatisk åtkomst till UGC oavsett valt lagringsalternativ (som ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över](srp.md) lagringsresursprovidern - introduktion och databasanvändning - översikt
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning
* [Omfaktorisering för SocialUtils](socialutils.md) - mappning av utgått verktygsmetoder till aktuella SRP-verktygsmetoder

