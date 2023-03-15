---
title: Grundläggande granskningar
seo-title: Reviews Essentials
description: Granska och Granska sammanfattningskomponenter
seo-description: Reviews and Review Summary components
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Grundläggande granskningar {#reviews-essentials}

Den här funktionen består av två komponenter som fungerar tillsammans: recensioner och sammanfattning.

Recensioner är en sammansatt komponent som baseras på en [kommentarsystem](essentials-comments.md) som innehåller en eller flera [värdering](rating-basics.md) (tally).

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
| [**oklanderlig**](scf.md#add-or-include-a-communities-component) | Ja - egenskaper kan redigeras i *design *läge |
| [**klientlibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
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
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities används [gemensam lagringsplats](working-with-srp.md) för UGC omfattar programmatisk åtkomst till UGC oavsett vilket lagringsalternativ som valts (till exempel ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över lagringsresursprovider](srp.md) - Översikt över introduktion och databasanvändning.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - Riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.
