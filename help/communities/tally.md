---
title: Grundläggande om helheten
description: Lär dig hur Tally är en abstrakt klass med en standardmetod för att samla in feedback från medlemmar om hur de värdesätter specifika produkter och tjänster.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Grundläggande om helheten {#tally-essentials}

Tally är en abstrakt klass som tillhandahåller en standardmetod för att samla in feedback från medlemmar om hur de värdesätter specifika produkter och tjänster. Anonym feedback stöds inte. Besökare på webbplatsen måste registrera sig och logga in för att kunna delta och logga in för att kunna ändra sin feedback. Kravet på inloggning underlättar moderering och ökar värdet på feedback genom att förhindra flera inlägg.

Du kan skapa en anpassad tally-komponent genom att utöka den abstrakta tally-klassen.

[Länka](essentials-liking.md) är ett genomförande av tally som är en enkel form av att uttrycka en positiv åsikt.

[Omröstning](essentials-voting.md) är ett genomförande av tally som är en enkel form av ett positivt eller negativt yttrande.

[Klassificering](rating-basics.md) är en implementering av tally som använder ett stjärnsystem för att uttrycka olika åsikter, från positiva till negativa.

Från och med AEM 6.1 är avsökningskomponenten inte längre tillgänglig.

[Recensioner](reviews-basics.md) är en SCF-komponent som är en hybrid av [kommentarer](essentials-comments.md) och [värdering](rating-basics.md).

## Grundläggande för klientsidan {#essentials-for-client-side}

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Tally API:er](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Slutpunkter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförda tallier (UGC) {#accessing-posted-tallies-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Modererar användargenererat innehåll](moderate-ugc.md).

Från och med AEM 6.1 Communities används [gemensam lagringsplats](working-with-srp.md) för UGC omfattar programmatisk åtkomst till UGC oavsett vilket lagringsalternativ som valts (till exempel ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över lagringsresursprovider](srp.md) - Översikt över introduktion och databasanvändning.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - Riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.
