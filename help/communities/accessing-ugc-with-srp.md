---
title: Åtkomst till UGC med SRP
seo-title: Accessing UGC with SRP
description: När en plats är konfigurerad att använda ASRP eller MSRP lagras inte den faktiska UGC:n i AEM nodstore (JCR)
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Åtkomst till UGC med SRP {#accessing-ugc-with-srp}

## Om SRP {#about-srp}

Alla AEM Communities-komponenter och -funktioner bygger på [ramverk för sociala komponenter (SCF)](/help/communities/scf.md), som anropar SocialResourceProvider-API:t för att komma åt allt användargenererat innehåll (UGC).

Innan en community-webbplats skapas [lagringsresursprovider](/help/communities/working-with-srp.md) måste konfigureras för att välja en implementering som är konsekvent med den underliggande [topologi](/help/communities/topologies.md). SRP-implementeringarna baseras på tre lagringsalternativ:

1. [ASRP](/help/communities/asrp.md) - Adobe on demand-lagring
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Om UGC-lagring {#about-ugc-storage}

Det som är viktigt att veta om lagring av UGC är att när en plats har konfigurerats att använda ASRP eller MSRP lagras inte själva UGC i AEM [nodarkiv](/help/sites-deploying/data-store-config.md) (JCR).

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

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Metoder som ska undvikas:

* Nod-API
* JCR-händelser
* startprogram för arbetsflöden (som använder JCR-händelser)

### Använd söksamlingar {#use-search-collections}

Olika SRP kan ha olika inbyggda frågespråk. Vi rekommenderar att du använder metoder från [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) paket för att köra rätt frågespråk.

Mer information finns i [Sök i Grundläggande](/help/communities/search-implementation.md).

## Resurser {#resources}

* [Community-innehåll](/help/communities/working-with-srp.md) - diskuterar tillgängliga SRP-alternativ för en gemensam lagringsplats för användargenererat innehåll
* [Översikt över lagringsresursprovider](/help/communities/srp.md) - introduktion och databasanvändning - översikt
* [SRP och UGC Essentials](/help/communities/srp-and-ugc.md) - SRP-verktygsmetoder och exempel
* [Sök i Grundläggande](/help/communities/search-implementation.md) - viktig information för sökning i användargenererat innehåll
* [Omfaktorisering för SocialUtils](/help/communities/socialutils.md) - mappning av borttagna verktygsmetoder till aktuella SRP-verktygsmetoder
