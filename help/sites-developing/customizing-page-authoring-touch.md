---
title: Anpassa sidredigering
description: I Adobe Experience Manager (AEM) finns olika sätt att anpassa sidredigeringsfunktionerna.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---

# Anpassa sidredigering{#customizing-page-authoring}

>[!CAUTION]
>
>I det här dokumentet beskrivs hur du anpassar sidredigering i det moderna, pekaktiverade användargränssnittet och det gäller inte det klassiska användargränssnittet.

I Adobe Experience Manager (AEM) finns olika sätt att anpassa sidredigeringsfunktionerna (och [konsoler](/help/sites-developing/customizing-consoles-touch.md)) i din redigeringsinstans.

* Clientlibs

  Med Clientlibs kan du utöka standardimplementeringen för att få nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder. När du anpassar kan du skapa en egen klientlib under `/apps.` Den nya klientlib måste:

   * är beroende av redigeringsklientlib `cq.authoring.editor.sites.page`
   * vara en del av `cq.authoring.editor.sites.page.hook` kategori

* Övertäckningar

  Övertäckningar baseras på noddefinitioner och gör att du kan täcka över standardfunktionerna (i `/libs`) med din egen anpassade funktionalitet (i `/apps`). När du skapar en övertäckning krävs ingen 1:1-kopia av originalet, eftersom [sammanslagning av säljresurser](/help/sites-developing/sling-resource-merger.md) tillåter arv.

>[!NOTE]
>
>Mer information finns i [JS-dokumentationsuppsättning](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

De kan användas på många sätt för att utöka sidredigeringsfunktionen i AEM. En markering beskrivs nedan (på en hög nivå).

>[!NOTE]
>
>Mer information finns i följande:
>
>* Använda och skapa [klientlibs](/help/sites-developing/clientlibs.md).
>* Använda och skapa [övertäckningar](/help/sites-developing/overlays.md).
>* [Granit](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Struktur för det AEM användargränssnittet med pekskärm](/help/sites-developing/touch-ui-structure.md) om du vill ha information om de strukturella områden som används för sidredigering.
>


>[!CAUTION]
>
>***Gör inte*** ändra något i `/libs` bana.
>
>Orsaken är att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du installerar en snabbkorrigering eller ett funktionspaket).
>
>Den rekommenderade metoden för konfiguration och andra ändringar är:
>
>1. Återskapa önskat objekt (d.v.s. som det finns i `/libs`) under `/apps`
>1. Gör ändringar i `/apps`

## Lägg till nytt lager (läge) {#add-new-layer-mode}

När du redigerar en sida finns det olika [lägen](/help/sites-authoring/author-environment-tools.md#page-modes) tillgängliga. Dessa lägen implementeras med [lager](/help/sites-developing/touch-ui-structure.md#layer). Dessa ger åtkomst till olika typer av funktioner för samma sidinnehåll. Standardlagren är: redigera, förhandsgranska, kommentera, utveckla och målinrikta.

### Exempel på lager: Live Copy-status {#layer-example-live-copy-status}

En AEM standardinstans innehåller MSM-lagret. Detta ger åtkomst till data relaterade till [hantering av flera webbplatser](/help/sites-administering/msm.md) och markerar det i lagret.

Om du vill se hur det fungerar kan du redigera [We.Retail Language copy](/help/sites-developing/we-retail-globalized-site-structure.md) sida (eller någon annan live-kopia-sida) och markera **Live Copy-status** läge.

MSM-lagerdefinitionen (som referens) finns i:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Kodexempel {#code-sample}

Detta är ett exempelpaket som visar hur du skapar ett lager (läge), som är ett nytt lager för MSM-vyn.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-new-layer-mode-projekt i GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Lägg till ny markeringskategori i resursläsaren {#add-new-selection-category-to-asset-browser}

Resursläsaren visar resurser av olika typer/kategorier (till exempel bilder och dokument). Resurserna kan också filtreras efter dessa tillgångskategorier.

### Kodexempel {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` är ett exempelpaket som visar hur du lägger till en grupp i tillgångssökaren. Det här exemplet ansluter till [Flickr](https://www.flickr.com)Det offentliga flödet och visar dem på sidopanelen.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-assetfinder-flickr-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtreringsresurser {#filtering-resources}

När användaren redigerar sidor måste han eller hon ofta välja bland resurser (till exempel sidor, komponenter och resurser). Detta kan vara en lista där författaren måste välja ett objekt.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Om [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granit](/help/sites-developing/touch-ui-concepts.md#granite-ui) -komponenten används för att användaren ska kunna välja sökvägen till en viss resurs. Sökvägarna kan filtreras på följande sätt:

* Implementera det anpassade predikatet genom att implementera [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html) gränssnitt.
* Ange ett namn för predikatet och referera det namnet när du använder `pathbrowser`.

Mer information om hur du skapar ett anpassat predikat finns i [den här artikeln](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementera ett anpassat predikat genom att implementera `com.day.cq.commons.predicate.AbstractNodePredicate` -gränssnittet fungerar även i det klassiska användargränssnittet.
>
>Se [den här kunskapsbasartikeln](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) som ett exempel på implementering av ett anpassat predikat i det klassiska användargränssnittet.

## Lägg till ny åtgärd i ett komponentverktygsfält {#add-new-action-to-a-component-toolbar}

Varje komponent (vanligtvis) har ett verktygsfält som ger tillgång till en rad åtgärder som kan vidtas för den komponenten.

### Kodexempel {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` är ett exempelpaket som visar hur du skapar en anpassad verktygsfältåtgärd för att återge komponenter.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-toolbar-screenshot project på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Lägg till ny lokal redigerare {#add-new-in-place-editor}

### Standardredigerare på plats {#standard-in-place-editor}

I en vanlig AEM-installation:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Innehåller definitioner av de olika redigeringsprogrammen som är tillgängliga.

1. Det finns en anslutning mellan redigeraren och varje resurstyp (som i komponenten) som kan använda den:

   * `cq:inplaceEditing`

     till exempel:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * egenskap: `editorType`

           Definierar vilken typ av infogad redigerare som används när redigeringen på plats aktiveras för den komponenten. till exempel `text`, `textimage`, `image`, `title`.

1. Ytterligare konfigurationsinformation om redigeraren kan konfigureras med en `config` nod som innehåller konfigurationer och en `plugin` nod som innehåller nödvändig konfigurationsinformation för plugin-programmet.

   Följande är ett exempel på hur du definierar bildproportioner för bildbeskärningsplugin-programmet för bildkomponenten. På grund av den begränsade skärmstorleken har beskärningsproportionerna flyttats till helskärmsredigeraren och kan bara ses där.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >AEM beskärningsproportioner, enligt inställningen i `ratio` egenskap, definieras som **höjd/bredd**. Detta skiljer sig från den vanliga definitionen av bredd/höjd och görs av kompatibilitetsskäl. Redigeringsanvändarna kommer inte att vara medvetna om några skillnader förutsatt att du definierar `name` egenskapen tydligt eftersom detta är vad som visas i användargränssnittet.

#### Skapa en ny lokal redigerare {#creating-a-new-in-place-editor}

Så här implementerar du en ny redigerare på plats (i klientlib):

>[!NOTE]
>
>Se till exempel:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementera:

   * `setUp`
   * `tearDown`

1. Registrera redigeraren (inkluderar konstruktorn):

   * `editor.register`

1. Ange anslutningen mellan redigeraren och alla resurstyper (som i komponenten) som kan använda den.

#### Kodexempel för att skapa en ny lokal redigerare {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` är ett exempelpaket som visar hur du skapar en redigerare på plats i AEM.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-inplace-editor-projekt i GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Konfigurera flera redigerare på plats {#configuring-multiple-in-place-editors}

Det går att konfigurera en komponent så att den har flera redigerare på plats. När flera redigerare på plats har konfigurerats kan du välja rätt innehåll och öppna rätt redigerare. Se [Konfigurera flera redigerare på plats](/help/sites-developing/multiple-inplace-editors.md) mer information.

## Lägg till en ny sidåtgärd {#add-a-new-page-action}

Lägga till en ny sidåtgärd i verktygsfältet, till exempel en **Tillbaka till platser** (konsol).

### Kodexempel {#code-sample-3}

`aem-authoring-extension-header-backtosites` är ett exempelpaket som visar hur du skapar en anpassad åtgärd i sidhuvudsfältet för att hoppa tillbaka till webbplatskonsolen.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-header-backtosites-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Anpassa arbetsflödet för begäran om aktivering {#customizing-the-request-for-activation-workflow}

färdiga arbetsflöden, **Aktiveringsbegäran**:

* Visas automatiskt på rätt meny när en innehållsförfattare **har inte** rätt replikeringsrättigheter, men **har** medlemskap för DAM-användare och författare.

* I annat fall visas ingenting eftersom replikeringsrättigheter har tagits bort.

Om du vill ha ett anpassat beteende för en sådan aktivering kan du täcka över **Aktiveringsbegäran** arbetsflöde:

1. I `/apps` överlägg **Webbplatser** guide:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Detta åsidosätter den vanliga förekomsten av:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Uppdatera [arbetsflödesmodell](/help/sites-developing/workflows-models.md) och relaterade konfigurationer/skript efter behov.
1. Ta bort höger till [`replicate` åtgärd](/help/sites-administering/security.md#actions) från alla lämpliga användare för alla relevanta sidor, om du vill att det här arbetsflödet ska utlösas som en standardåtgärd när någon av användarna försöker publicera (eller replikera) en sida.
