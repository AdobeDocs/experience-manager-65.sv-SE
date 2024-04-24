---
title: Återgivning och leverans
description: Lär dig hur du återger Adobe Experience Manager-innehåll med Sling Default Servlets som återger JSON och andra format.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Återgivning och leverans{#rendering-and-delivery}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) kan enkelt återges med [Standardservrar för Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) för rendering [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) och andra format.

Dessa färdiga återgivningar tar vanligtvis plats i databasen och returnerar innehållet som det är.

AEM, som Sling, stöder också utveckling och driftsättning av anpassade snedstrecksrenderare för att få full kontroll över det renderade schemat och innehållet.

Standardrenderare för innehållstjänster fyller luckan mellan färdiga Sling-standardinställningar och Anpassad utveckling som gör det möjligt att anpassa och styra många aspekter av det återgivna innehållet utan att behöva utveckla.

I följande diagram visas återgivningen av innehållstjänster.

![chlimage_1-15](assets/chlimage_1-15.png)

## Begär JSON {#requesting-json}

Använd **&lt;resource.caas span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />.[&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.][&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.json** för att begära JSON.]

<table>
 <tbody>
  <tr>
   <td>RESURS</td>
   <td>en entitetsresurs under /content/entities<br /> eller <br /> en innehållsresurs under /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>VALFRITT</strong><br /> </p> <p>en exportkonfiguration hittades under /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Om det utelämnas används standardexportkonfigurationen </p> </td>
  </tr>
  <tr>
   <td>DJUP-INT</td>
   <td><strong>VALFRITT</strong><br /> <br /> djuprekursion för återgivning av underordnade objekt som används vid Sling-återgivning</td>
  </tr>
 </tbody>
</table>

## Skapa exportkonfigurationer {#creating-export-configs}

Du kan skapa exportkonfigurationer för att anpassa JSON-återgivningen.

Du kan skapa en konfigurationsnod under */apps/mobileapps/caas/exportConfigs.*

| Nodnamn | Konfigurationens namn (för återgivningsväljare) |
|---|---|
| jcr:primärType | nt:ostrukturerad |

I följande tabell visas egenskaperna för Export Configs:

<table>
 <tbody>
  <tr>
   <td><strong>Namn</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Standard (if, not set)</strong></td>
   <td><strong>Värde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Sträng[]</td>
   <td>innehåller allt</td>
   <td>sling:resourceType</td>
   <td>exkludera information för noder med angiven sling:resourceType från JSON-export</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Sträng[]</td>
   <td>utelämna ingenting</td>
   <td>sling:resourceType</td>
   <td>ta endast med information för noder med angiven sling:resourceType från JSON-export</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Sträng[]</td>
   <td>utelämna ingenting</td>
   <td>Egenskapsprefix</td>
   <td>exkludera egenskaper som börjar med angivna prefix från JSON-export</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Sträng[]</td>
   <td>utelämna ingenting</td>
   <td>Egenskapsnamn</td>
   <td>exkludera angivna egenskaper från JSON-export</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Sträng[]</td>
   <td>innehåller allt</td>
   <td>Egenskapsnamn</td>
   <td><p>if excludePropertyPrefixes set<br /> Detta omfattar angivna egenskaper trots att prefixet matchas,</p> <p>else (exclude properties ignore) inkluderar endast dessa egenskaper</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Sträng[]</td>
   <td>innehåller allt</td>
   <td>undernamn</td>
   <td>exkludera angivna underordnade från JSON-export</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Sträng[]<br /> <br /> </td>
   <td>utelämna ingenting</td>
   <td>undernamn</td>
   <td>inkludera endast angivna underordnade från JSON-export, exkludera andra</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Sträng[]<br /> <br /> </td>
   <td>ändra namn på ingenting</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>ändra namn på egenskaper med ersättningar</td>
  </tr>
 </tbody>
</table>

### Åsidosättningar av resurstypexport {#resource-type-export-overrides}

Skapa en konfigurationsnod under */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primärType | nt:ostrukturerad |

I följande tabell visas egenskaperna:

<table>
 <tbody>
  <tr>
   <td><strong>Namn</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Standard (if, not set)</strong></td>
   <td><strong>Värde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>Sträng[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Returnera inte standardexporten av CaaS json för följande sling-resurstyper.<br /> Returnera en kundjson-export genom att återge resursen som<br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### Befintliga konfigurationer för export av innehållstjänster {#existing-content-services-export-configs}

Content Services innehåller två exportkonfigurationer:

* standard (ingen konfiguration har angetts)
* sida (för att återge webbplatssidor)

#### Standardexportkonfiguration {#default-export-configuration}

Standardexportkonfigurationen för Content Services används om en konfiguration anges i den begärda URI:n.

&lt;resource>.caas[.&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>Namn</strong></td>
   <td><strong>Värde</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:beskrivning,beskrivning<br /> jcr:lastModified,lastModified<br /> cq:tags,taggar<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON Overrides</td>
   <td>grund/komponenter/bild<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Konfiguration för sidexport {#page-export-configuration}

Den här konfigurationen utökar standardinställningen så att underordnade grupperingar inkluderas under en underordnad nod.

&lt;site_page>.caas.page[.&lt;depth-int>].json

### Ytterligare resurser {#additional-resources}

Läs resurserna nedan om du vill veta mer om andra ämnen i Content Services:

* [Utveckla modeller](/help/mobile/administer-mobile-apps.md)
* [Skapa innehållstjänster](/help/mobile/develop-content-as-a-service.md)
* [Administrera innehållstjänster](/help/mobile/developing-content-services.md)
