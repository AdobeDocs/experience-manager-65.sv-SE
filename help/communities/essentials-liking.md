---
title: Länka viktiga
description: Lär dig hur du använder komponenten Liking, ett användbart verktyg som gör att medlemmar kan uttrycka en positiv åsikt om visst innehåll genom att markera hjärtikonen.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
pagetitle: Liking Essentials
exl-id: ef314385-cd5c-411c-91df-83691a81c1bc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Länka viktiga {#liking-essentials}

Komponenten Liking, en [tally](tally.md) -underklass, är ett användbart verktyg som gör att medlemmar kan uttrycka en positiv åsikt om ett visst innehållsavsnitt genom att helt enkelt välja hjärtikonen.

Det är tillåtet att placera flera instanser av en länkande komponent på samma sida. Varje instans måste konfigureras med en unik `tally name`-egenskap.

Anonym publicering av en gilla-markering stöds inte. Besökare på webbplatsen måste registrera sig och logga in för att kunna delta. Den inloggade besökaren (medlemmen) kan när som helst växla som på och av.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/like</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Ja - egenskaper kan redigeras i <i>designläge </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>egenskaper</strong></td>
   <td><p>Se <a href="liking.md">Använda länk</a></p> </td>
  </tr>
 </tbody>
</table>

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Tally API:er](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Slutpunkter &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

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
