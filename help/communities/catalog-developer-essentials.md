---
title: Catalog Essentials
seo-title: Catalog Essentials
description: Katalogöversikt
seo-description: Katalogöversikt
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 3%

---

# Catalog Essentials {#catalog-essentials}

Den här sidan innehåller viktig information om hur du arbetar med katalogfunktionen på webbplatser för aktivering.

När katalogfunktionen ingår i en community-webbplats kan communitymedlemmar bläddra bland och välja aktiveringsresurser som finns listade i en katalog.

Med [ `enablement catalog`-komponenten](catalog.md) kan communitymedlemmar komma åt en katalog med [aktiveringsresurser](resources.md). Användningen av AEM taggar är en viktig del av att hantera utseendet på aktiveringsresurser i en katalog.

Se [Tagga aktiveringsresurser](tag-resources.md).

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/aktivering/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>Se <a href="catalog.md">Katalogfunktion</a></td>
  </tr>
 </tbody>
</table>

## Grundläggande för serversidan {#essentials-for-server-side}

### Katalogfunktion {#catalog-function}

En community-platsstruktur som innehåller [katalogfunktionen](functions.md#catalog-function) innehåller en konfigurerad `enablement catalog`-komponent.

### Förfilter {#pre-filters}

När en katalogfunktion har lagts till på en communitywebbplats är det möjligt att begränsa aktiveringsresurser och utbildningssökvägar som visas i katalogen genom att ange ett förfilter. Detta görs genom att ange egenskaper för platsens katalogresurs.

Använda exemplet med [självstudiekursen för aktivering](getting-started-enablement.md):

* On author
* Använda [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Till exempel [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Navigera till katalogresursen på katalogsidan

   * Till exempel, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Lägga till en underordnad filternod

   * Markera noden `catalog`
   * Välj **[!UICONTROL Create Node]**

      * Namn: `filters`
      * Typ: `nt:unstructured`
      * Välj **[!UICONTROL Save All]**

* Lägg till egenskapen `se_resource-tags` i noden `filters`

   * Välj noden `filters`
   * Lägg till en Multi-egenskap

      * Namn: `se_resource-tags`
      * Typ: Sträng
      * Värde: *&lt;ange ett [Tagg-ID](#pre-filter-tagids)>*
         * Välj **[!UICONTROL Multi]**
         * Välj **[!UICONTROL Add]**

            * I popup-dialogrutan väljer du `+` om du vill lägga till ytterligare förfiltertagg-ID:n

* Publicera communitywebbplatsen igen

![configure-catalog](assets/configure-catalog.png)

#### Förfiltrera tagg-ID:n {#pre-filter-tagids}

Förfiltret [TaggID](../../help/sites-developing/framework.md#tagid) måste exakt matcha de taggar som används för aktiveringsresurserna. Dessa är synliga i mappen `resources` för platsen som värden för egenskapen `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### Referens-API:er {#reference-apis}

* [API för aktivering](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [Rapporterings-API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API för rapporteringsanalys](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
