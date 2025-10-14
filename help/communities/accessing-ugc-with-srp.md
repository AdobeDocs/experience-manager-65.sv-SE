---
title: Åtkomst till UGC med SRP
description: När en plats är konfigurerad att använda ASRP eller MSRP lagras inte den faktiska UGC:n i AEM nodarkiv (JCR)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Åtkomst till UGC med SRP {#accessing-ugc-with-srp}

## Om SRP {#about-srp}

Alla AEM Communities-komponenter och -funktioner bygger på [ramverket för sociala komponenter (SCF)](/help/communities/scf.md), som anropar SocialResourceProvider-API:t för att komma åt allt användargenererat innehåll (UGC).

Innan en community-plats skapas måste [lagringsresursprovidern &#x200B;](/help/communities/working-with-srp.md) konfigureras för att välja en implementering som är konsekvent med den underliggande [topologin](/help/communities/topologies.md). SRP-implementeringarna baseras på tre lagringsalternativ:

1. [ASRP](/help/communities/asrp.md) - lagring på begäran Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Om UGC-lagring {#about-ugc-storage}

Det som är viktigt att veta om lagring av UGC är att när en plats har konfigurerats att använda ASRP eller MSRP lagras inte den faktiska UGC:n i AEM [nodarkivet](/help/sites-deploying/data-store-config.md) (JCR).

Även om det kan finnas noder i JCR som skuggar UGC för att ge användbara metadata, ska dessa noder inte blandas ihop med själva UGC.

Se [Översikt över lagringsresursprovidern.](/help/communities/srp.md)

## Bästa praxis {#best-practice}

När du utvecklar anpassade komponenter bör utvecklare vara noga med att koda oberoende av den topologi som valts för tillfället, vilket ger flexibilitet att gå över till en ny topologi i framtiden.

### Anta att JCR inte är tillgängligt {#assume-jcr-not-available}

Metoder som är specifika för JCR bör undvikas.

Metoder som ska användas:

* Sling API (Sling Resource)

   * anta inte att det finns JCR-noder

* OSGi Events

   * anta inte att det finns JCR-händelser

* [Socialresursverktyg](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Metoder som ska undvikas:

* Nod-API
* JCR-händelser
* startprogram för arbetsflöden (som använder JCR-händelser)

### Använd söksamlingar {#use-search-collections}

Olika SRP kan ha olika inbyggda frågespråk. Använd metoder från paketet [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) för att köra rätt frågespråk.

Mer information finns i [Söka i Grundläggande](/help/communities/search-implementation.md).

## Resurser {#resources}

* [Community Content Storage](/help/communities/working-with-srp.md) - diskuterar tillgängliga SRP-alternativ för en gemensam UGC-butik
* [Lagringsresursprovideröversikt](/help/communities/srp.md) - översikt över introduktion och databasanvändning
* [SRP och UGC Essentials](/help/communities/srp-and-ugc.md) - SRP-verktygsmetoder och exempel
* [Söka efter viktiga](/help/communities/search-implementation.md) - viktig information för sökning i UGC
* [Omfaktorisering för SocialUtils](/help/communities/socialutils.md) - mappning av borttagna verktygsmetoder till aktuella SRP-verktygsmetoder
