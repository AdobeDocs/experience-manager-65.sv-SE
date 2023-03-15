---
title: Rekommenderade topologier för communities
seo-title: Recommended Topologies for Communities
description: Hur man hanterar användargenererat innehåll (UGC)
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Rekommenderade topologier för communities {#recommended-topologies-for-communities}

Från och med AEM Communities 6.1 har ett unikt tillvägagångssätt använts för att hantera användargenererat innehåll (UGC) som skickats in av webbplatsbesökare (medlemmar) från publiceringsmiljön.

Den här metoden skiljer sig i grunden från hur den AEM plattformen hanterar webbplatsinnehåll som vanligtvis hanteras från författarmiljön.

Den AEM plattformen använder ett nodarkiv som replikerar webbplatsinnehåll från författaren till publiceringen, medan AEM Communities använder en gemensam lagringsplats för UGC som aldrig replikeras.

För den vanliga UGC-butiken måste du välja en [lagringsresursprovider](working-with-srp.md). Rekommenderade alternativ är:

* [DSRP - Resursprovider för relativ databaslagring](dsrp.md)
* [MSRP - lagringsresursprovider för MongoDB](msrp.md)
* [ASRP - Adobe lagringsresursleverantör](asrp.md)

Ett annat SRP-alternativ, [JSRP - JCR-lagringsresursprovider](jsrp.md), har inte stöd för en gemensam UGC-butik för författaren och publiceringsmiljöer med båda åtkomsten.

Kräver en gemensam lagringsplats i följande rekommenderade topologier.

>[!NOTE]
>
>För AEM Communities [UGC replikeras aldrig](working-with-srp.md#ugc-never-replicated).
>
>När distributionen inte innehåller en [gemensam lagringsplats](working-with-srp.md), visas bara UGC i den AEM publicerings- eller författarinstansen som den angavs för.

>[!NOTE]
>
>Mer information om AEM finns i [Rekommenderade distributioner](../../help/sites-deploying/recommended-deploys.md) och [Introduktion till AEM](../../help/sites-deploying/data-store-config.md).

## För produktion {#for-production}

Det är viktigt att upprätta en gemensam butik för UGC, och därför är den underliggande distributionen beroende av dess förmåga att stödja en gemensam butik.

Två exempel:

1. Om den förväntade volymen av UGC är hög och en lokal MongoDB-instans är möjlig, skulle valet vara [MSRP](msrp.md).

1. För optimala prestanda för sidinnehåll väljer du [publicera servergrupp](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) och [ASRP](asrp.md) ger optimal skalning av UGC med relativt enkla operationer.

För båda kan distributionen baseras på valfri OAK-mikrokärna.

Om du vill välja en lämplig gemensam lagringsplats bör du tänka på den unika [egenskaper](working-with-srp.md#characteristics-of-srp-options) var och en.

Mer information om ekorrar finns på [Rekommenderade distributioner](../../help/sites-deploying/recommended-deploys.md).

### TjärMK-publiceringsgrupp {#tarmk-publish-farm}

När topologin är en publiceringsanläggning är viktiga ämnen:

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

### Rekommenderas: DSRP, MSRP eller ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | WEBBPLATSINNEHÅLLSPOSITION | ANVÄNDARGENERERAT INNEHÅLL | LAGRINGSRESURSANORDNARE | VANLIG FÖRVARING |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| alla | JCR | MySQL | DSRP | Ja |
| alla | JCR | MongoDB | MSRP | Ja |
| alla | JCR | Adobe on demand-lagring | ASRP | Ja |

### JSRP {#jsrp}


| Distribution | WEBBPLATSINNEHÅLLSPOSITION | ANVÄNDARGENERERAT INNEHÅLL | LAGRINGSRESURSANORDNARE | VANLIG FÖRVARING |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TARMK-servergrupp (standard) | JCR | JCR | JSRP | Nej |
| Oak Cluster | JCR | JCR | JSRP | Yesfor publish environment only |

## För utveckling {#for-development}

För icke-produktionsmiljöer [JSRP](jsrp.md) är enkelt att konfigurera en utvecklingsmiljö med en författarinstans och en publiceringsinstans.

Om du väljer [ASRP](asrp.md), [DSRP](dsrp.md) eller [MSRP](msrp.md) för produktion är det också möjligt att konfigurera en liknande utvecklingsmiljö med hjälp av Adobe on demand-lagring eller MongoDB. Ett exempel finns i [Så här konfigurerar du MongoDB för demo](demo-mongo.md).

## Referenser {#references}

* [Användarsynkronisering](sync.md)

   Diskuterar synkronisering av användardata mellan publiceringsgruppinstanser.

* [Hantera användare och användargrupper](users.md)

   Diskuterar roller för användare och användargrupper i författar- och publiceringsmiljöer.

* UGC [gemensam lagringsplats](working-with-srp.md)

   Beskriver lagring av communityinnehåll separat från webbplatsinnehåll.

* [Node Stores and Data Stores](../../help/sites-deploying/data-store-config.md)

   I princip lagras webbplatsinnehållet i en nodbutik. För Assets kan ett datalager konfigureras att lagra binära data. För Communities måste en gemensam butik konfigureras för att välja SRP.

* [Lagringselement](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Beskriver implementeringarna av lagring i två noder: Tjära och MongoDB.
