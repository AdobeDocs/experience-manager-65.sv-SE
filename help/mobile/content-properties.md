---
title: Innehållsegenskaper och noder
description: Följ den här sidan om du vill veta mer om innehållsegenskaper och noder.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---

# Innehållsegenskaper och noder {#content-properties-and-nodes}

{{ue-over-mobile}}

Artiklar, banners och samlingar representeras som cq:Pages i AEM.

De delar samma gemensamma egenskaper som finns i någon cq:Page förutom flera andra som visas nedan som representerar metadata och integreringsegenskaper för Adobe Experience Manager (AEM) Mobile On-Demand-tjänster.

I följande tabeller beskrivs innehållsegenskaperna och noderna.

## Egenskaper för gemensam integrering {#common-integration-properties}

| **Egenskapsnamn** | **Typ** | **Standardvärden eller förväntade värden** | **Beskrivning** |
|---|---|---|---|
| dps-id | Sträng |  | som tilldelats av AEM Mobile och lagras av AEM när de överförts till AEM Mobile eller importerats från AEM Mobile |
| dps-resourceType | Sträng | dps:Article | `dps:Banner` \| `dps:Collection` \| `entity type property` |
| dps-version | Sträng |  | version av AEM Mobile (ingår också i det fullständiga aemm-id:t) |
| dps-lastSynced | Datum |  | datum för senaste synkronisering/import från AEM Mobile till AEM |
| dps-lastUploaded | Datum |  | datum för senaste överföring från AEM till AEM Mobile |
| dps-lastUploadedBy | Sträng:userid |  | ID-användare som utförde den senaste överföringsbegäran från AEM till AEM Mobile |

## Egenskaper för kärnmetadata {#core-metadata-properties}

| Egenskapsnamn | Typ | Standardvärden eller förväntade värden |
|--- |--- |--- |
| dps-title | Sträng |  |
| dps-shortTitle | Sträng |  |
| dps-abstract | Sträng |  |
| dps-shortAbstract | Sträng |  |
| dps-avdelning | Sträng |  |
| dps-category | Sträng |  |
| dps-keywords | Sträng[] |  |
| dps-internalKeywords | Sträng[] |  |
| dps-prioritet | Sträng[] | Prioritet från {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Artiklar {#articles}

| **Egenskapsnamn** | **Typ** | **Standardvärden eller förväntade värden** |
|---|---|---|
| dps-author | Sträng |  |
| dps-authorURL | Sträng |  |
| dps-hideFromBrowsePage | Boolean |  |
| dps-access | Sträng | ProtectedAccess från {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Socialt** |  |  |
| dps-socialShareURL | Sträng |  |
| dps-articleText | Sträng |  |
| dps-url | Sträng |  |

### Banderoller {#banners}

| **Egenskapsnamn** | **Typ** | **Standardvärden eller förväntade värden** |
|---|---|---|
| dps-tapAction |  | Tryck på åtgärd från {webLink} |
| dps-tapActionUrl |  |  |

### Samlingar {#collections}

| Egenskapsnamn | Typ | Standardvärden eller förväntade värden |
|--- |--- |--- |
| dps-productId | Sträng |  |
| dps-readingPosition | Sträng | från {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Boolean |  |
| dps-allowDownload | Boolean |  |
| dps-openDefault | Sträng | från {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Sträng |  |

## Innehållsnoder {#content-nodes}

### Vanliga noder {#common-nodes}

| Nodnamn | Typ | Standardvärden eller förväntade värden | Beskrivning |
|--- |--- |--- |--- |
| image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### Enheter {#entities}

#### Artiklar {#articles-1}

| Nodnamn | Typ | Standardvärden för förväntade värden | Beskrivning |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### Banderoller {#banners-1}

| Nodnamn | Typ | Standardvärden för förväntade värden | Beskrivning |
|---|---|---|---|
| NA |  |  |  |

#### Samlingar {#collections-1}

| Nodnamn | Typ | Standardvärden för förväntade värden | Beskrivning |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
