---
title: Grundläggande röstning
seo-title: Voting Essentials
description: Översikt över röstkomponenten
seo-description: Voting component overview
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Grundläggande röstning {#voting-essentials}

Röstkomponenten, en [tally](tally.md) underklass, är ett användbart verktyg som gör att medlemmar kan betygsätta en viss del av innehållet genom att bara markera upp- eller nedpilarna för att ange sin åsikt.

Det är tillåtet att placera flera instanser av en röstkomponent på samma sida. varje instans måste konfigureras med en unik `tally name` -egenskap.

Anonym publicering av en röst stöds inte. Besökare på platsen måste registrera sig och logga in för att endast delta i omröstningen en gång. Den inloggade besökaren (medlemmen) kan när som helst ändra sin röst.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voice</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Ja - egenskaper kan redigeras i <i>design </i>läge</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>klientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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

* [Tally API:er](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Slutpunkter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförd röstning (UGC) {#accessing-posted-voting-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities används [gemensam lagringsplats](working-with-srp.md) för UGC omfattar programmatisk åtkomst till UGC oavsett vilket lagringsalternativ som valts (till exempel ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över lagringsresursprovider](srp.md) - introduktion och översikt över databasanvändningen.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - mappning av borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.
