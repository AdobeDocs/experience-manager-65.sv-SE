---
title: Uppgraderar anpassade sökformulär
seo-title: Uppgraderar anpassade sökformulär
description: I den här artikeln beskrivs de justeringar som krävs efter en uppgradering för att de anpassade sökformulären ska fungera.
seo-description: I den här artikeln beskrivs de justeringar som krävs efter en uppgradering för att de anpassade sökformulären ska fungera.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uppgraderar anpassade sökformulär{#upgrading-custom-search-forms}

I AEM 6.2 har platsen där anpassade sökformulär lagras i databasen ändrats. När de uppgraderas flyttas de från sin plats i 6.1 på:

* /apps/cq/gui/content/facets

till en ny plats under:

* /conf/global/settings/cq/search/facets

Därför krävs manuella justeringar efter en uppgradering för att formulären ska fortsätta att fungera.

Detta gäller både nya sökformulär och anpassade standardformulär.

Mer information finns i dokumentationen om [sökansikten](/help/assets/search-facets.md).

## Ändra egenskapen resourceType {#changing-the-resourcetype-property}

Om inget annat anges kräver de flesta justeringar som måste göras efter uppgraderingen att du ändrar egenskapen `sling:resourceType` för de konfigurerade anpassade sökformulären. Detta behövs så att egenskapen pekar på rätt plats för återgivningsskriptet.

Du kan ändra egenskapen genom att göra följande:

1. Öppna CRXDE Lite genom att gå till `https://server:port/crx/de/index.jsp`
1. Bläddra till platsen för noden som behöver justeras, enligt vad som anges i listan med [anpassade sökformulär](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) nedan.
1. Klicka på noden. Klicka på och ändra egenskapen **sling:resourceType** i den högra egenskapspanelen.
1. Spara ändringarna genom att trycka på knappen **Spara alla** .

## Lista med anpassade sökformulär {#list-of-custom-search-forms}

Här nedan hittar du en lista över alla anpassade sökformulär och de ändringar de behöver efter uppgraderingen. De hänvisar till namnen i `/conf/global/settings/cq/search/facets/sites/items`.

### Fulltextpredikat med nodnamnet &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1</td>
   <td>fulltext</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpreates/fulltextpredikate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

I AEM 6.1 ingick standardpredikatet för fulltext i sökformuläret. I 6.2 har fulltextfältet ersatts av OmniSearch. Det här predikatet hoppas över programmatiskt och kan tas bort.

**** Åtgärd: Ta bort noden helt.

### Andra fulltextpredikat {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökningen från i 6.1</td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpreates/fulltextpredikate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpreates/fulltextpredikate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Förutsägelser för sökvägsläsare {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpreates/pathpredikate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpreates/pathpredate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Förutsägelser för taggar {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>taggar</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpreates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpreates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera **resourceType** -egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan).

### Sidstatuspredikat {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

Sidstatus har ersatts med två alternativ för egenskapspredikat, en för publicering och en för LiveCopy-status.

**Åtgärder:**

* Ta bort `pagestatuspredicate` noden
* Kopiera nod

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * to `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Kopiera nod

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * to `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Se till att du anger `listOrder` egenskapen för `analyticspredicate` noden till &quot;**8**&quot;. Detta behövs för att undvika konflikter.

### Förutsägelser för datumintervall {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Resurstyp i 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpreates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpreates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Dolt filter {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>type</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Inget att justera.

### Analytics Predicate {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Intervallpredikering {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

>[!NOTE]
>
>Obs! I motsats till 6.1 återges inte längre en tagg i sökfältet av intervallpredikatet.

### Egenskapspredikat för alternativ {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Slider-intervallpredikat {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Komponentpredikat {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/component/spredicate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/componentPredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Författarpredikat {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/userpredikate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/userpreate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Mallar - predikat {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nod/noder i standardsökformuläret i 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Resurstyp i 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpreates/templatesPredikate</p> </td>
  </tr>
  <tr>
   <td>Resurstyp i 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpreates/templatesPredikate</p> </td>
  </tr>
 </tbody>
</table>

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

## Resursadministratörssökväg {#assets-admin-search-rail}

Nedan visas namnen i `/conf/global/settings/dam/search/facets/assets/items`

### Fulltextpredikat med nodnamnet &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nod/noder i standardsökformuläret i 6.1 | fulltext |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/fulltextpredikate |
| Resurstyp i 6.2 | n/a |

I 6.1 ingick standardpredikatet för fulltext i sökformuläret. I 6.2 har fulltextfältet ersatts av OmniSearch. Det här predikatet hoppas över programmatiskt och kan tas bort.

**** Åtgärd: Ta bort noden ovan.

### Förutsägelser för sökvägsläsare {#path-browser-predicates-1}

| Nod/noder i standardsökformuläret i 6.1 | patbrowser |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/pathbrowserpredikate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/pathbrowserpredikate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Mime Type Predicates {#mime-type-predicates}

| Nod/noder i standardsökformuläret i 6.1 | mimeType |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpredikates/optionspredicate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/optionspredicate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; på samma sätt som i 6.2 ovan).

### Filstorleksprognoser {#file-size-predicates}

| Nod/noder i standardsökformuläret i 6.1 | filesize |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/filesizepredicate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/sliderangepredicate |

**** Åtgärd: Justera `resourceType` enligt anvisningarna i 6.2 ovan.

### Predikat för senast ändrade resurs {#asset-last-modified-predicates}

| Nod/noder i standardsökformuläret i 6.1 | assetlastmodifiedpredikat |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/assetlastmodifiedpredikate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/assetlastmodifiedpredicate |

Åtgärd: Justera egenskapen resourceType (lägg till &quot;/coral&quot; på samma sätt som i 6.2-platsen som anges ovan).

### Publicera predikat {#publish-predicate}

| Nod/noder i standardsökformuläret i 6.1 | publicera |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/publishpredikate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/publishate |

**Åtgärder:**

*  Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

* Lägg till en `optionPaths` egenskap (av typen String) med värdet: `/libs/dam/options/predicates/publish`

* Lägg till `singleSelect` egenskap med booleskt värde `true`.

### Statusprognoser {#status-predicates}

| Nod/noder i standardsökformuläret i 6.1 | status |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpredikates/optionspredicate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/optionspredicate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

### Förutsägelser för förfallostatus {#expiry-status-predicates}

| Nod/noder i standardsökformuläret i 6.1 | förfallostatus |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/expirredassetpredikate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/expirredassetpredikate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

### Giltighetspredikat för metadata {#metadata-validity-predicates}

| Nod/noder i standardsökformuläret i 6.1 | metadata |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpredikates/optionspredicate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/optionspredicate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

### Klassificeringsprognoser {#rating-predicates}

| Nod/noder i standardsökformuläret i 6.1 | värdering |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/ratingpredikate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/sliderangepredicate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

### Orienteringspredikat {#orientation-predicate}

| Nod/noder i standardsökformuläret i 6.1 | orientation |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/tagsfilterpredikate |
| Resurstyp i 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpreates/tagspredicate |

**Åtgärder:**

*  Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

* Lägg till en `fieldLabel` egenskap med samma värde som `text` egenskapen på samma nod.

* Lägg till en `emptyText` egenskap med samma värde som `text` egenskapen på samma nod.

* Lägg till en `rootPath` egenskap med samma värde som `optionPaths` egenskapen på samma nod.

### Formatpredikat {#style-predicate}

| Nod/noder i standardsökformuläret i 6.1 | style |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpreates/tagsfilterpredikate |
| Resurstyp i 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpreates/tagspredicate |

**Åtgärder:**

*  Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

* Lägg till en `fieldLabel` egenskap med samma värde som `text` egenskapen på samma nod.

* Lägg till en `emptyText` egenskap med samma värde som `text` egenskapen på samma nod.

* Lägg till en `rootPath` egenskap med samma värde som `optionPaths` egenskapen på samma nod.

### Videoformatsprognoser {#video-format-predicates}

| Nod/noder i standardsökformuläret i 6.1 | videoFormat |
|---|---|
| Resurstyp i 6.1 | dam/gui/components/admin/customsearch/searchpredikates/optionspredicate |
| Resurstyp i 6.2 | dam/gui/coral/components/admin/customsearch/searchpreates/optionspredicate |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)

### Förutsägelse av huvudtillgång {#mainasset-predicate}

| Nod/noder i standardsökformuläret i 6.1 | huvudtillgång |
|---|---|
| Resurstyp i 6.1 | granite/ui/components/foundation/form/hidden |
| Resurstyp i 6.2 | granite/ui/components/coral/foundation/form/hidden |

**** Åtgärd: Justera `resourceType` egenskapen (lägg till &quot;**/coral**&quot; som i 6.2-positionen ovan)
