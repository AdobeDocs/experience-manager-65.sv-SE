---
title: Återgivning och leverans
seo-title: Återgivning och leverans
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b

---


# Återgivning och leverans{#rendering-and-delivery}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

AEM-innehåll kan enkelt återges via [Sling-standardservrar](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) för att återge [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) och andra format.

Dessa färdiga återgivningar tar vanligtvis plats i databasen och returnerar innehållet som det är.

AEM, via Sling, har också stöd för utveckling och driftsättning av skräddarsydda försäljningsrenderare för att få full kontroll över det renderade schemat och innehållet.

Standardrenderare för innehållstjänster fyller luckan mellan färdiga Sling-standardinställningar och Anpassad utveckling som gör det möjligt att anpassa och styra många aspekter av det återgivna innehållet utan att behöva utveckla.

I följande diagram visas återgivningen av innehållstjänster.

![chlimage_1-15](assets/chlimage_1-15.png)

## Begär JSON {#requesting-json}

Använd **&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** för att begära JSON.

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
   <td><strong>Rekursion av djup (tillval</strong><br /> <br /> ) för återgivning av underordnade objekt som används vid Sling-återgivning</td>
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
   <td><p>Om excludePropertyPrefix anges<br /> innehåller detta angivna egenskaper trots att prefixet matchas,</p> <p>else (exclude properties ignore) inkluderar endast dessa egenskaper</p> </td>
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
   <td>&lt;actual_property_name&gt;,&lt;replace_property_name&gt;</td>
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
   <td>Returnera inte standardexporten för CaaS json för följande sling-resurstyper.<br /> Returnera en kundjson-export genom att återge resursen som<br /> &lt;RESOURCE&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Befintliga konfigurationer för innehållsexport {#existing-content-services-export-configs}

Content Services innehåller två exportkonfigurationer:

* default (ingen konfiguration har angetts)
* sida (för att återge webbplatssidor)

#### Standardexportkonfiguration {#default-export-configuration}

Standardexportkonfigurationen för Content Services används om en konfiguration anges i den begärda URI:n.

&lt;RESOURCE>.caas[.&lt;DEPTH-INT>].json

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
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,taggar<br /> cq:lastModified,lastModified</td>
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
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Konfiguration för sidexport {#page-export-configuration}

Den här konfigurationen utökar standardinställningen så att underordnade grupperingar inkluderas under en underordnad nod.

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### Additional Resources {#additional-resources}

Läs resurserna nedan om du vill veta mer om andra ämnen i Content Services:

* [Utveckla modeller](/help/mobile/administer-mobile-apps.md)
* [Skapa innehållstjänster](/help/mobile/develop-content-as-a-service.md)
* [Administrera innehållstjänster](/help/mobile/developing-content-services.md)

