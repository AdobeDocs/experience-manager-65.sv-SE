---
title: Åtkomst till UGC med SRP
seo-title: Åtkomst till UGC med SRP
description: När en plats är konfigurerad att använda ASRP eller MSRP lagras inte den faktiska UGC:n i AEM nodstore (JCR)
seo-description: När en plats är konfigurerad att använda ASRP eller MSRP lagras inte den faktiska UGC:n i AEM nodstore (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Åtkomst till UGC med SRP {#accessing-ugc-with-srp}

## Om SRP {#about-srp}

Alla AEM Communities-komponenter och -funktioner bygger på [ramverket för sociala komponenter (SCF)](/help/communities/scf.md), som anropar SocialResourceProvider API för att få åtkomst till allt användargenererat innehåll (UGC).

Innan en community-plats skapas måste [lagringsresursprovidern (SRP)](/help/communities/working-with-srp.md) konfigureras att välja en implementering som överensstämmer med den underliggande [topologin](/help/communities/topologies.md). SRP-implementeringarna baseras på tre lagringsalternativ:

1. [ASRP](/help/communities/asrp.md)  - on demand-lagring i Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md)  - JCR

## Om UGC-lagring {#about-ugc-storage}

Det som är viktigt att veta om lagring av UGC är att när en plats har konfigurerats att använda ASRP eller MSRP lagras inte den faktiska UGC:n i AEM [nodstore](/help/sites-deploying/data-store-config.md) (JCR).

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

Olika SRP kan ha olika inbyggda frågespråk. Vi rekommenderar att du använder metoder från [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)-paketet för att köra rätt frågespråk.

Mer information finns i [Söka i Grundläggande](/help/communities/search-implementation.md).

## Resurser {#resources}

* [Community Content Storage](/help/communities/working-with-srp.md)  - diskuterar tillgängliga SRP-alternativ för en gemensam lagringsplats för användargenererat innehåll
* [Översikt över](/help/communities/srp.md)  lagringsresursprovidern - introduktion och databasanvändning - översikt
* [SRP och UGC Essentials](/help/communities/srp-and-ugc.md) - SRP-verktygsmetoder och -exempel
* [Search Essentials](/help/communities/search-implementation.md) - Essentials information for searching UGC
* [Omfaktorisering för SocialUtils](/help/communities/socialutils.md) - mappning av utgått verktygsmetoder till aktuella SRP-verktygsmetoder

