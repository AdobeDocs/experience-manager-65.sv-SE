---
title: Grundläggande granskningar
description: Lär dig mer om hur granskningar i AEM Communities är en sammansatt komponent som baseras på ett kommentarsystem som innehåller en eller flera klassificerings(tally) komponenter.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Grundläggande granskningar {#reviews-essentials}

Den här funktionen består av två komponenter som fungerar ihop: recensioner och sammanfattningar.

Recensioner är en sammansatt komponent som baseras på en [kommentarsystem](essentials-comments.md) som innehåller en eller flera [värdering](rating-basics.md) (tally)-komponenter.

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
   <td>Ja - egenskaper kan redigeras i <i>design </i>läge</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>klientlibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
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
| [**oklanderlig**](scf.md#add-or-include-a-communities-component) | Ja - egenskaper kan redigeras i *design *läge |
| [**klientlibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **mallar** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **egenskaper** | Se [Använda granskningar](reviews.md) |

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Granska API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Granska slutpunkter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförda granskningar (UGC) {#accessing-posted-reviews-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities används [gemensam lagringsplats](working-with-srp.md) för UGC omfattar programmatisk åtkomst till UGC oavsett vilket lagringsalternativ som valts (till exempel ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över lagringsresursprovider](srp.md) - Översikt över introduktion och databasanvändning.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - Riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.
