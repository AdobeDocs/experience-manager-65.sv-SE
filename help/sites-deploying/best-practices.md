---
title: Distribuera bästa praxis
seo-title: Distribuera bästa praxis
description: Driftsätta och underhålla bästa praxis.
seo-description: Driftsätta och underhålla bästa praxis.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Distribuera bästa praxis{#deploying-best-practices}

Bästa tillvägagångssätt för att driftsätta eller underhålla AEM på det mest effektiva och effektiva sättet. Den här växande ämneslistan innehåller en rad olika områden i AEM.

Följande områden har dokumentation om användning och underhåll av bästa metoder och rekommendationer:

* [OAK](#oak)
* [Communities](#communities)
* [UI](#ui)
* [Prestanda](#performance)

Mer information om hur du administrerar, utvecklar och redigerar finns i följande:

* [Administrera metodtips](/help/sites-administering/administer-best-practices.md)
* [Utveckla bästa praxis](/help/sites-developing/best-practices.md)
* [Bästa tillvägagångssätt](/help/sites-authoring/best-practices.md)

Specifika dokument beskrivs och länkas till i de tabeller som följer.

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) är ett skalbart och prestandabaserat hierarkiskt innehållsarkiv som utgör grunden för AEM.

<table>
 <tbody>
  <tr>
   <td><p>Skalbarhet, prestanda och katastrofåterställning</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Prestanda och skalbarhet</a></td>
   <td>Innehåller en rapport om den tekniska flexibiliteten, höga prestanda och funktioner för återställning efter ljudkatastrof</td>
  </tr>
  <tr>
   <td>Rekommenderade OAK-distributioner</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Rekommenderade driftsättningar</a></td>
   <td>Beskriver distributionsscenarier</td>
  </tr>
  <tr>
   <td>Mongo topologi</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Bästa praxis för Mongo-topologi</a></td>
   <td>Beskriver mongo-topologi - när du ska använda vilken topologi.</td>
  </tr>
  <tr>
   <td>Alternativ för datalagring</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Konfigurera nod- och datalager</a></td>
   <td>I det här dokumentet förklaras de bästa sätten att lagra binära data och innehållsnoder. Innehåller information om hur du använder datalagret Amazon S3.</td>
  </tr>
  <tr>
   <td>Sök i OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Metodtips för frågor och indexering</a><br /> </td>
   <td>Beskriver de bästa sätten att indexera innehåll.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities förenklar framtagning och hantering av lokala communityn. Bästa tillvägagångssätt för AEM Communities beskrivs här:

[Community Content Store](/help/communities/working-with-srp.md) - Diskuterar den nya funktionen för delad lagring av användargenererat innehåll (UGC) och överväganden för val av underliggande [topologi](/help/communities/topologies.md).

[Rekommenderade distributioner för communities](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Beskriver de rekommenderade distributionerna för Communities. |

## UI {#ui}

De bästa sätten att använda användargränssnittet beskrivs här:

[Rekommendationer för användargränssnitt för kunder](/help/sites-deploying/ui-recommendations.md)

AEM har för närvarande två gränssnitt: klassiskt och pekoptimerat gränssnitt i samma version. Därför måste kunderna fatta ett beslut om vilken användning som ska ske under projektets genomförande. Det här dokumentet är avsett att hjälpa till att hitta rätt alternativ.

## Prestanda {#performance}

De bästa metoderna för prestandaanvändning listas här:

<table>
 <tbody>
  <tr>
   <td>Bästa metoder för kvalitetssäkring</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Bästa metoder för kvalitetssäkring</a></td>
   <td>En standardiserad översikt över problem med att definiera ett testkoncept specifikt för prestandatester i din <em>publiceringsmiljö</em> . Detta är främst av intresse för kvalitetstekniker, projektledare och systemadministratörer.</td>
  </tr>
  <tr>
   <td>Använda Dispatcher med ett CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Använda Dispatcher med ett CDN</a></td>
   <td>Ett leveransnätverk (CDN), som Akamai Edge Delivery eller Amazon Cloud Front, levererar innehåll från en plats nära slutanvändaren.</td>
  </tr>
  <tr>
   <td>Prestandaoptimering</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Prestandaoptimering</a></td>
   <td>Ett viktigt problem är den tid det tar för er webbplats att svara på besökarnas förfrågningar.</td>
  </tr>
  <tr>
   <td>Prestandatestning</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Bästa metoder för prestandatestning</a></td>
   <td>Beskriver de bästa sätten att köra prestandatester på en AEM-distribution.<br /> </td>
  </tr>
 </tbody>
</table>

