---
title: Grundläggande röstning
description: Lär dig hur du använder röstkomponenten som gör att medlemmar kan betygsätta en viss del av innehållet genom att markera upp- eller nedpilarna för att ange sin åsikt.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Grundläggande röstning {#voting-essentials}

Röstkomponenten, en [tally](tally.md)-underklass, är ett användbart verktyg som gör att medlemmar kan betygsätta en viss del av innehållet genom att bara markera upp- eller nedpilarna för att ange sin åsikt.

Det är tillåtet att placera flera instanser av en röstkomponent på samma sida. Varje instans måste konfigureras med en unik `tally name`-egenskap.

Anonym publicering av en röst stöds inte. Besökare på webbplatsen måste registrera sig och logga in för att kunna rösta endast en gång. Den inloggade besökaren (medlemmen) kan när som helst ändra sin röst.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voice</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Ja - egenskaper kan redigeras i <i>designläge </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>egenskaper</strong></td>
   <td><p>Se <a href="voting.md">Använda röstning</a></p> </td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Tally API:er](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Slutpunkter ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförd röstning (UGC) {#accessing-posted-voting-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities omfattar användningen av en [gemensam butik](working-with-srp.md) för UGC programmatisk åtkomst till UGC oavsett valt lagringsalternativ (som ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan varning**.

Se:

* [Lagringsresursprovideröversikt](srp.md) - introduktion och översikt över databasanvändningen.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - mappning av utfasade verktygsmetoder till aktuella SRP-verktygsmetoder.
