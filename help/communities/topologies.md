---
title: Rekommenderade topologier för communities
description: Hur man hanterar användargenererat innehåll (UGC)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Rekommenderade topologier för communities {#recommended-topologies-for-communities}

Från och med AEM Communities 6.1 har ett unikt tillvägagångssätt använts för att hantera användargenererat innehåll (UGC) som skickats in av webbplatsbesökare (medlemmar) från publiceringsmiljön.

Den här metoden skiljer sig i grunden från hur den AEM plattformen hanterar webbplatsinnehåll som vanligtvis hanteras från författarmiljön.

Den AEM plattformen använder ett nodarkiv som replikerar webbplatsinnehåll från författaren till publiceringen, medan AEM Communities använder en gemensam lagringsplats för UGC som aldrig replikeras.

För det gemensamma UGC-arkivet måste du välja en [lagringsresursleverantör (SRP)](working-with-srp.md). Rekommenderade alternativ är:

* [DSRP - Resursprovider för relativ databaslagring](dsrp.md)
* [MSRP - lagringsresursprovider för MongoDB](msrp.md)
* [ASRP - Adobe lagringsresursleverantör](asrp.md)

Ett annat SRP-alternativ, [JSRP - JCR-lagringsresursprovidern](jsrp.md), stöder inte en gemensam UGC-butik för författaren och publiceringsmiljöer för båda åtkomsten.

Kräver en gemensam lagringsplats i följande rekommenderade topologier.

>[!NOTE]
>
>För AEM Communities replikeras [UGC aldrig](working-with-srp.md#ugc-never-replicated).
>
>När distributionen inte innehåller någon [gemensam lagringsplats](working-with-srp.md) visas bara UGC i den AEM publicerings- eller författarinstansen som den angavs för.
>

>[!NOTE]
>
>Mer information om den AEM plattformen finns i [Rekommenderade distributioner](../../help/sites-deploying/recommended-deploys.md) och [Introduktion till den AEM plattformen](../../help/sites-deploying/data-store-config.md).

## För produktion {#for-production}

Det är viktigt att upprätta en gemensam butik för UGC, och därför är den underliggande distributionen beroende av dess förmåga att stödja en gemensam butik.

Två exempel:

1. Om den förväntade volymen av UGC är hög och en lokal MongoDB-instans är möjlig är alternativet [MSRP](msrp.md).

1. För optimala prestanda för sidinnehåll ger valet av en [publiceringsgrupp](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) och [ASRP](asrp.md) optimal skalning av UGC med relativt enkla åtgärder.

För båda kan distributionen baseras på valfri OAK-mikrokärna.

Om du vill välja en lämplig gemensam lagringsplats bör du tänka på de unika [egenskaperna](working-with-srp.md#characteristics-of-srp-options) för varje.

Mer information om Oak mikrokernaler finns på [Rekommenderade distributioner](../../help/sites-deploying/recommended-deploys.md).

### TaMK Publish Farm {#tarmk-publish-farm}

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

I icke-produktionsmiljöer är det enkelt att konfigurera en utvecklingsmiljö med en författarinstans och en publiceringsinstans i [JSRP](jsrp.md) .

Om du väljer [ASRP](asrp.md), [DSRP](dsrp.md) eller [MSRP](msrp.md) för produktion, går det också att konfigurera en liknande utvecklingsmiljö med hjälp av Adobe on-demand-lagring eller MongoDB. Se till exempel [HowTo Setup MongoDB for Demo](demo-mongo.md).

## Referenser {#references}

* [Användarsynkronisering](sync.md)

  Diskuterar synkronisering av användardata mellan publiceringsgruppinstanser.

* [Hantera användare och användargrupper](users.md)

  Diskuterar roller för användare och användargrupper i författar- och publiceringsmiljöer.

* UGC [gemensam butik](working-with-srp.md)

  Beskriver lagring av communityinnehåll separat från webbplatsinnehåll.

* [Node Stores and Data Stores](../../help/sites-deploying/data-store-config.md)

  I princip lagras webbplatsinnehållet i en nodbutik. För Assets kan ett datalager konfigureras för att lagra binära data. För Communities måste en gemensam butik konfigureras för att välja SRP.

* [Lagringselement](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Beskriver implementeringarna av lagring med två noder: tar och MongoDB.
