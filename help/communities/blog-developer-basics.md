---
title: Blog Essentials
description: Lär dig hur du lägger till bloggfunktionen på en sida så att medlemmar i den inloggade communityn kan publicera bloggartiklar.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Blog Essentials {#blog-essentials}

Från och med AEM 6.1 Communities är en blogg en community-aktivitet. Bloggartiklar publiceras nu från publiceringsmiljön, där bloggartiklar tidigare bara kunde skapas i författarmiljön och publiceras.

Bloggartiklar kan nu skapas av alla communitymedlemmar, såvida de inte är begränsade till behöriga medlemmar.

Den här sidan innehåller viktig information om hur du arbetar med bloggfunktionen.

>[!NOTE]
>
>Den underliggande infrastrukturen för bloggfunktionen är journalfunktionen.

## Grundläggande för klientsidan {#essentials-for-client-side}

Bloggfunktionen består av två huvudkomponenter som är tillgängliga genom att lägga till [Bloggfunktionen](/help/communities/functions.md#blog-function) eller genom att lägga till komponenterna på en sida i redigeringsläge för författare.

### Blogg {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inkluderbar</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voice<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>mallar</strong></td>
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
| [**inkluderbar**](/help/communities/scf.md#add-or-include-a-communities-component) | Nej |
| [**clientlibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **mallar** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **egenskaper** | se [Bloggfunktion](/help/communities/blog-feature.md) |

* [Anpassningar på klientsidan](/help/communities/client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Blog API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Bloggslutpunkter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](/help/communities/server-customize.md)

### Bloggfunktion {#blog-function}

En community-platsstruktur som innehåller [bloggfunktionen](/help/communities/functions.md#blog-function) har `Blog` och `Blog Sidebar` komponenter konfigurerade. Bloggfunktionen stöder identifiering av en [privilegierad medlemsanvändargrupp](/help/communities/users.md#privileged-members-group).

### Åtkomst till blogginlägg (UGC) {#accessing-blog-entries-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

Från och med AEM 6.1 Communities omfattar användningen av en [gemensam butik](/help/communities/working-with-srp.md) för UGC programmatisk åtkomst till UGC oavsett valt lagringsalternativ (som ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan varning**.

Se :

* [Lagringsresursprovideröversikt](/help/communities/srp.md) - introduktion och översikt över databasanvändningen.
* [SRP och UGC Essentials](/help/communities/srp-and-ugc.md) - SRP-verktygsmetoder och exempel.
* [Åtkomst till UGC med SRP](/help/communities/accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](/help/communities/socialutils.md) - mappning av utfasade verktygsmetoder till aktuella SRP-verktygsmetoder.

## Primär utgivare {#primary-publisher}

När distributionen är en publiceringsgrupp måste du identifiera en primär utgivare som avfrågar artiklar som ska publiceras.

Mer information finns i [Primär utgivare](/help/communities/deploy-communities.md#primary-publisher).

## Tillåta multimedia {#allowing-rich-media}

Den AEM plattformen blockerar länkar från andra webbplatser för att förhindra XSS-attacker enligt beskrivningen i

* [Protect mot XSS (Cross-Site Scripting)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

Från och med AEM 6.2 inkluderas de ändringar som tidigare krävdes för att göras manuellt i standardkonfigurationsfilen för AntiSamy.

Multimedia är inbäddade i en bloggartikel genom att välja ikonen `Embed Media from External Sites` :

![media](assets/media-icon.png)
