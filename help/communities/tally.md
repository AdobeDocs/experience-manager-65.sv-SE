---
title: Helt grundläggande
seo-title: Helt grundläggande
description: Översikt över klassen Tally
seo-description: Översikt över klassen Tally
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Grundläggande om heltal {#tally-essentials}

Tally är en abstrakt klass som tillhandahåller en standardmetod för att samla in feedback från medlemmar om hur de värdesätter specifika produkter och tjänster. Anonym feedback stöds inte. Besökaren måste registrera sig och logga in för att kunna delta och logga in för att kunna ändra sin feedback. Kravet på inloggning underlättar moderering och ökar värdet på feedback genom att förhindra flera inlägg.

Du kan skapa en anpassad tally-komponent genom att utöka den abstrakta tally-klassen.

[Likingär ](essentials-liking.md) en tillämpning av tally som är en enkel form av uttryck för en positiv åsikt.

[Votinging är en ](essentials-voting.md) tillämpning av tally som är en enkel form av uttryck för en positiv eller negativ åsikt.

[Ratinging ](rating-basics.md) är en implementering av tally som använder ett stjärnsystem för att uttrycka en rad åsikter, från positiv till negativ.

Från och med AEM 6.1 är avsökningskomponenten inte längre tillgänglig.

[](reviews-basics.md) Granskning är en SCF-komponent som är en hybrid med  [](essentials-comments.md) kommentarer och  [gradering](rating-basics.md).

## Grundläggande för klientsidan {#essentials-for-client-side}

* [Anpassningar på klientsidan](client-customize.md)

## Grundläggande för serversidan {#essentials-for-server-side}

* [Tally API:er](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Slutpunkter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Anpassningar på serversidan](server-customize.md)

### Åtkomst till bokförda tallies (UGC) {#accessing-posted-tallies-ugc}

UGC bör modereras med någon av standardmetoderna för moderering.
Se [Moderating User Generated Content](moderate-ugc.md).

Från och med AEM 6.1 Communities omfattar användningen av en [gemensam butik](working-with-srp.md) för UGC programmatisk åtkomst till UGC oavsett valt lagringsalternativ (som ASRP, MSRP eller JSRP).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

Se:

* [Översikt över](srp.md)  lagringsresursprovidern - Introduktion och översikt över databasanvändningen.
* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel.
* [Använder UGC med riktlinjerna för SRP](accessing-ugc-with-srp.md) -kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar utgått verktygsmetod till aktuella SRP-verktygsmetoder.

