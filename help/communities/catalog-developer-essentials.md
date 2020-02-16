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
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Catalog Essentials {#catalog-essentials}

Den här sidan innehåller viktig information om hur du arbetar med katalogfunktionen på webbplatser för aktivering.

När katalogfunktionen ingår i en community-webbplats kan communitymedlemmar bläddra bland och välja aktiveringsresurser som finns listade i en katalog.

Komponenten [ gör att communitymedlemmar kan komma åt en katalog med `enablement catalog` aktiveringsresurser](catalog.md) [](resources.md). Användningen av AEM-taggar är en viktig del i hanteringen av utseendet på aktiveringsresurser i en katalog.

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

En community-platsstruktur som innehåller [katalogfunktionen](functions.md#catalog-function)innehåller en konfigurerad `enablement catalog` komponent.

### Förfilter {#pre-filters}

När en katalogfunktion har lagts till på en communitywebbplats är det möjligt att begränsa aktiveringsresurser och utbildningssökvägar som visas i katalogen genom att ange ett förfilter. Detta görs genom att ange egenskaper för platsens katalogresurs.

Använda exemplet med [självstudiekursen](getting-started-enablement.md):

* On author
* Använda [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Till exempel [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Navigera till katalogresursen på katalogsidan

   * Exempel, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Lägga till en underordnad filternod

   * Markera `catalog`noden
   * Välj **[!UICONTROL Skapa nod]**

      * Namn: `filters`
      * Typ: `nt:unstructured`
   * Välj **[!UICONTROL Spara alla]**


* Lägg till `se_resource-tags` egenskap till `filters` noden

   * Markera `filters` noden
   * Lägg till en Multi-egenskap

      * Namn: `se_resource-tags`
      * Typ:Sträng
      * Värde: *&lt;ange ett[tagg-ID](#pre-filter-tagids)>*
      * Markera **[!UICONTROL flera]**
      * Välj **[!UICONTROL Lägg till]**

         * I popup-dialogrutan väljer du `+` att lägga till ytterligare förfiltertagg-ID:n

* Publicera communitywebbplatsen igen

![chlimage_1-189](assets/chlimage_1-189.png)

#### Förfiltrera tagg-ID:n {#pre-filter-tagids}

Förfiltreringen av [TagID:n](../../help/sites-developing/framework.md#tagid) måste exakt matcha de taggar som används i aktiveringsresurserna. Dessa är synliga som egenskapens värden i platsens `resources` mapp `se_resource-tags`.

![chlimage_1-190](assets/chlimage_1-190.png)

### Referens-API:er {#reference-apis}

* [API för aktivering](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [Rapporterings-API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API för rapporteringsanalys](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

