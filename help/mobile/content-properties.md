---
title: Innehållsegenskaper och noder
seo-title: Innehållsegenskaper och noder
description: Följ den här sidan om du vill veta mer om innehållsegenskaper och noder.
seo-description: Följ den här sidan om du vill veta mer om innehållsegenskaper och noder.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Innehållsegenskaper och noder {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Artiklar, banderoller och samlingar representeras som cq:Pages in AEM.

De delar samma gemensamma egenskaper som finns i alla cq:Page, förutom flera andra som visas nedan som representerar metadata och integreringsegenskaper för Adobe Experience Manager Mobile On-Demand-tjänster (AEM).

I följande tabeller beskrivs innehållsegenskaperna och noderna.

## Egenskaper för gemensam integrering {#common-integration-properties}

| **Egenskapsnamn** | **Typ** | **Standardvärden eller förväntade värden** | **Beskrivning** |
|---|---|---|---|
| dps-id | Sträng |  | som tilldelats av AEM Mobile och lagrats av AEM när de överförts till AEM Mobile eller importerats från AEM Mobile |
| dps-resourceType | Sträng | dps:artikel | dps:Banner | dps:Samling | entitetstyp, egenskap |
| dps-version | Sträng |  | version av AEM Mobile-enhet (ingår också i det fullständiga aemm-id:t) |
| dps-lastSynced | Date |  | datum för senaste synkronisering/import från AEM Mobile till AEM |
| dps-lastUploaded | Date |  | datum för senaste överföring från AEM till AEM Mobile |
| dps-lastUploadedBy | String:userid |  | ID-användare som utförde den senaste överföringsbegäran från AEM till AEM Mobile |

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
| dps-hideFromBrowsePage | Boolesk |  |
| dps-access | Sträng | ProtectedAccess från {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
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
| dps-horizontalSwipe | Boolesk |  |
| dps-allowDownload | Boolesk |  |
| dps-openDefault | Sträng | från {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Sträng |  |

## Innehållsnoder {#content-nodes}

### Vanliga noder {#common-nodes}

| Nodnamn | Typ | Standardvärden eller förväntade värden | Beskrivning |
--- |--- |--- |--- |
| image | jcr:primärType=nt:ostrukturerad <br> sling:resourceType=foundation/components/image |  |  |

### Entities {#entities}

#### Artiklar {#articles-1}

| Nodnamn | Typ | Standardvärden för förväntade värden | Beskrivning |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primärType=nt:ostrukturerad <br> sling:resourceType=foundation/components/image |  |

#### Banderoller {#banners-1}

| Nodnamn | Typ | Standardvärden för förväntade värden | Beskrivning |
|---|---|---|---|
| NA |  |  |  |

#### Samlingar {#collections-1}

| Nodnamn | Typ | Standardvärden för förväntade värden | Beskrivning |
|--- |--- |--- |--- |
| background-image | jcr:primärType=nt:ostrukturerad <br> sling:resourceType=foundation/components/image |  |  |
