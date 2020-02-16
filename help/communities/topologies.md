---
title: Rekommenderade topologier för communities
seo-title: Rekommenderade topologier för communities
description: Hur man hanterar användargenererat innehåll (UGC)
seo-description: Hur man hanterar användargenererat innehåll (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rekommenderade topologier för communities {#recommended-topologies-for-communities}

Från och med AEM Communities 6.1 har en unik metod använts för att hantera användargenererat innehåll (UGC) som skickats in av webbplatsbesökare (medlemmar) från publiceringsmiljön.

Den här metoden skiljer sig i grunden från hur AEM-plattformen hanterar webbplatsinnehåll som vanligtvis hanteras från författarmiljön.

AEM-plattformen använder en nodbutik som replikerar webbplatsinnehåll från författaren till publiceringen, medan AEM Communities använder en enda gemensam butik för UGC som aldrig replikeras.

För det vanliga UGC-arkivet måste du välja en [lagringsresursleverantör (SRP)](working-with-srp.md). Rekommenderade alternativ är:

* [DSRP - Resursprovider för relativ databaslagring](dsrp.md)
* [MSRP - lagringsresursprovider för MongoDB](msrp.md)
* [ASRP - Adobe Storage Resource Provider](asrp.md)

Ett annat SRP-alternativ, [JSRP - JCR Storage Resource Provider](jsrp.md), stöder inte en gemensam UGC-butik för författaren och publiceringsmiljöer med båda åtkomsten.

Kräver en gemensam lagringsplats i följande rekommenderade topologier.

>[!NOTE]
>
>För AEM Communities replikeras [aldrig](working-with-srp.md#ugc-never-replicated)UGC.
>
>När distributionen inte innehåller någon [gemensam butik](working-with-srp.md)visas bara UGC i AEM-publicerings- eller författarinstansen som den angavs för.

>[!NOTE]
>
>Mer information om AEM-plattformen finns i [Rekommenderade distributioner](../../help/sites-deploying/recommended-deploys.md) och [introduktion till AEM-plattformen](../../help/sites-deploying/data-store-config.md).

## För produktion {#for-production}

Det är viktigt att upprätta en gemensam butik för UGC, och därför är den underliggande distributionen beroende av dess förmåga att stödja en gemensam butik.

Två exempel:

1) Om den förväntade volymen av UGC är hög och en lokal MongoDB-instans är möjlig är valet [MSRP](msrp.md).

2) För optimala prestanda för sidinnehåll ger valet av en [publiceringsgrupp](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) och [ASRP](asrp.md) optimal skalning av UGC med relativt enkla åtgärder.

För båda kan distributionen baseras på valfri OAK-mikrokärna.

Om du vill välja en lämplig gemensam lagringsplats ska du noga tänka på de unika [egenskaperna](working-with-srp.md#characteristics-of-srp-options) för varje lager.

Mer information om ekormikrokernaler finns på [Rekommenderade distributioner](../../help/sites-deploying/recommended-deploys.md).

### TjärMK-publiceringsgrupp {#tarmk-publish-farm}

När topologin är en publiceringsanläggning är relevanta ämnen av betydelse

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

### Rekommenderas: DSRP, MSRP eller ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | WEBBPLATSINNEHÅLLSPOSITION | ANVÄNDARGENERERAT INNEHÅLL | LAGRINGSRESURSANORDNARE | VANLIG FÖRVARING |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| alla | JCR | MySQL | DSRP | Ja |
| alla | JCR | MongoDB | MSRP | Ja |
| alla | JCR | Adobe on Demandstorage | ASRP | Ja |

### JSRP {#jsrp}


| Distribution | WEBBPLATSINNEHÅLLSPOSITION | ANVÄNDARGENERERAT INNEHÅLL | LAGRINGSRESURSANORDNARE | VANLIG FÖRVARING |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TARMK-servergrupp (standard) | JCR | JCR | JSRP | Nej |
| Oak Cluster | JCR | JCR | JSRP | Yesfor publish environment only |

## För utveckling {#for-development}

I icke-produktionsmiljöer är [JSRP](jsrp.md) enkelt att konfigurera en utvecklingsmiljö med en författarinstans och en publiceringsinstans.

Om du väljer [ASRP](asrp.md), [DSRP](dsrp.md) eller [MSRP](msrp.md) för produktion kan du även konfigurera en liknande utvecklingsmiljö med hjälp av Adobe On-demand-lagring eller MongoDB. Se till exempel [HowTo Setup MongoDB for Demo](demo-mongo.md).

## Referenser {#references}

* [Användarsynkronisering](sync.md)

   Diskuterar synkronisering av användardata mellan publiceringsgruppinstanser.

* [Hantera användare och användargrupper](users.md)

   Diskuterar roller för användare och användargrupper i författar- och publiceringsmiljöer.

* UGC- [gemensam butik](working-with-srp.md)

   Beskriver lagring av communityinnehåll separat från webbplatsinnehåll

* [Node Stores and Data Stores](../../help/sites-deploying/data-store-config.md)

   I princip lagras webbplatsinnehållet i en nodbutik. För Assets kan ett datalager konfigureras att lagra binära data. För Communities måste en gemensam butik konfigureras för att välja SRP.

* [Lagringselement i AEM 6.3](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Beskriver implementeringarna av lagring i två noder: Tjära och MongoDB.
