---
title: Blog Essentials
seo-title: Blog Essentials
description: Översikt över bloggar
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Blog Essentials {#blog-essentials}

Från och med AEM 6.1 Communities är en blogg en community-aktivitet. Bloggartiklar publiceras nu från publiceringsmiljön, där bloggartiklar tidigare bara kunde skapas i författarmiljön och publiceras.

Bloggartiklar kan nu skapas av alla communitymedlemmar, såvida de inte är begränsade till behöriga medlemmar.

Den här sidan innehåller viktig information om hur du arbetar med bloggfunktionen.

>[!NOTE]
>
>Den underliggande infrastrukturen för bloggfunktionen är journalfunktionen.

## Grundläggande för klientsidan {#essentials-for-client-side}

Bloggfunktionen består av två huvudkomponenter som är tillgängliga genom att lägga till [Bloggfunktion](/help/communities/functions.md#blog-function) eller genom att lägga till komponenterna på en sida i redigeringsläge.

### Blogg {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.röstning<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>se <a href="/help/communities/blog-feature.md">Bloggfunktion</a></td>
  </tr>
 </tbody>
</table>

### Blogg, marginallist {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**oklanderlig**](/help/communities/scf.md#add-or-include-a-communities-component) | Nej |
| [**klientlibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **egenskaper** | se [Bloggfunktion](/help/communities/blog-feature.md) |

* [Anpassningar på klientsidan](/help/communities/client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Blogg-API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Bloggslutpunkter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](/help/communities/server-customize.md)

### Bloggfunktion {#blog-function}

En community-webbplatsstruktur som innehåller [Bloggfunktion](/help/communities/functions.md#blog-function) har konfigurerats `Blog` och `Blog Sidebar` -komponenter. Funktionen Blog har stöd för att identifiera en [privilegierad medlemsanvändargrupp](/help/communities/users.md#privileged-members-group).

### Åtkomst till blogginlägg (UGC) {#accessing-blog-entries-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

Från och med AEM 6.1 Communities används [gemensam lagringsplats](/help/communities/working-with-srp.md) för UGC omfattar programmatisk åtkomst till UGC oavsett vilket lagringsalternativ som valts (till exempel ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se :

* [Översikt över lagringsresursprovider](/help/communities/srp.md) - introduktion och översikt över databasanvändningen.
* [SRP och UGC Essentials](/help/communities/srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Åtkomst till UGC med SRP](/help/communities/accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](/help/communities/socialutils.md) - mappning av borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.

## Primär utgivare {#primary-publisher}

När distributionen är en publiceringsgrupp är det nödvändigt att identifiera en primär utgivare som söker efter artiklar som är schemalagda att publiceras.

Se [Primär utgivare](/help/communities/deploy-communities.md#primary-publisher) för mer information.

## Tillåta multimedia {#allowing-rich-media}

Den AEM plattformen blockerar länkar från andra webbplatser för att förhindra XSS-attacker enligt beskrivningen i

* [Protect mot XSS (Cross-Site Scripting)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

Från och med AEM 6.2 inkluderas de ändringar som tidigare krävdes för att göras manuellt i standardkonfigurationsfilen för AntiSamy.

Multimedia är inbäddade i en bloggartikel genom att välja `Embed Media from External Sites` icon:

![media](assets/media-icon.png)
