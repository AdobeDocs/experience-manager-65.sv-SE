---
title: Anpassa sidredigering
seo-title: Customizing Page Authoring
description: AEM innehåller olika mekanismer som gör att du kan anpassa sidredigeringsfunktionerna
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 273836ad0afd6466eac437bf7711e7dbabc1d5e9
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 0%

---

# Anpassa sidredigering{#customizing-page-authoring}

>[!CAUTION]
>
>I det här dokumentet beskrivs hur du anpassar sidredigering i det moderna, pekaktiverade användargränssnittet och det gäller inte det klassiska användargränssnittet.

AEM innehåller olika mekanismer som gör att du kan anpassa sidredigeringsfunktionen (och [konsolerna](/help/sites-developing/customizing-consoles-touch.md)) för redigeringsinstansen.

* Clientlibs

   Med Clientlibs kan du utöka standardimplementeringen för att få nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder. När du anpassar kan du skapa ett eget klientlib under `/apps.` Det nya klientlib måste:

   * är beroende av redigeringsklientlib `cq.authoring.editor.sites.page`
   * ingå i lämplig `cq.authoring.editor.sites.page.hook`-kategori

* Övertäckningar

   Övertäckningar baseras på noddefinitioner och gör att du kan täcka över standardfunktionerna (i `/libs`) med din egen anpassade funktion (i `/apps`). När du skapar en övertäckning krävs inte en 1:1-kopia av originalet, eftersom [sling-resurskonfusion](/help/sites-developing/sling-resource-merger.md) tillåter arv.

>[!NOTE]
>
>Mer information finns i [JS-dokumentationsuppsättningen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

De kan användas på många sätt för att utöka sidredigeringsfunktionen i AEM. En markering beskrivs nedan (på en hög nivå).

>[!NOTE]
>
>Mer information finns i:
>
>* Använda och skapa [klientlibs](/help/sites-developing/clientlibs.md).
>* Använda och skapa [övertäckningar](/help/sites-developing/overlays.md).
>* [Granit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Struktur för det AEM Touch-aktiverade ](/help/sites-developing/touch-ui-structure.md) användargränssnittet för information om de strukturella områden som används för sidredigering.

>
>Det här avsnittet behandlas också i [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html)-sessionen - [Anpassning av användargränssnittet för AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html).

>[!CAUTION]
>
>Du ***får*** inte ändra något i `/libs`-sökvägen.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
>
>Den rekommenderade metoden för konfiguration och andra ändringar är:
>
>1. Återskapa önskat objekt (t.ex. som det finns i `/libs`) under `/apps`
>1. Gör ändringar i `/apps`


## Lägg till nytt lager (läge) {#add-new-layer-mode}

När du redigerar en sida finns det olika [lägen](/help/sites-authoring/author-environment-tools.md#page-modes) tillgängliga. Dessa lägen implementeras med [lager](/help/sites-developing/touch-ui-structure.md#layer). Dessa ger åtkomst till olika typer av funktioner för samma sidinnehåll. Standardlagren är: redigera, förhandsgranska, kommentera, utveckla och målinrikta.

### Exempel på lager: Live Copy-status {#layer-example-live-copy-status}

En AEM standardinstans innehåller MSM-lagret. Detta ger åtkomst till data som är relaterade till [hantering av flera platser](/help/sites-administering/msm.md) och markerar dem i lagret.

För att se hur det fungerar kan du redigera en [webbsida (eller någon annan live-kopia) och välja läget **Live Copy Status**.](/help/sites-developing/we-retail-globalized-site-structure.md)

MSM-lagerdefinitionen (som referens) finns i:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Kodexempel {#code-sample}

Detta är ett exempelpaket som visar hur du skapar ett nytt lager (läge), som är ett nytt lager för MSM-vyn.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-new-layer-mode-projekt i GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Lägg till ny markeringskategori i resursläsaren {#add-new-selection-category-to-asset-browser}

Resursläsaren visar resurser av olika typer/kategorier (t.ex. bilder, dokument osv.). Resurserna kan också filtreras efter dessa tillgångskategorier.

### Kodexempel {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` är ett exempelpaket som visar hur du lägger till en ny grupp i tillgångssökaren. Det här exemplet ansluter till den allmänna dataströmmen för [Flickr](https://www.flickr.com) och visar dem på sidopanelen.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-assetfinder-flickr-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtreringsresurser {#filtering-resources}

När användaren redigerar sidor måste han eller hon ofta välja bland resurser (t.ex. sidor, komponenter, resurser osv.). Detta kan vara en lista som författaren till exempel måste välja ett objekt från.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Om till exempel [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui)-komponenten används för att låta användaren välja sökvägen till en viss resurs, kan sökvägarna som visas filtreras på följande sätt:

* Implementera det anpassade predikatet genom att implementera gränssnittet [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Ange ett namn för predikatet och referera det namnet när du använder `pathbrowser`.

Mer information om hur du skapar ett anpassat predikat finns i [den här artikeln](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementering av ett anpassat predikat genom implementering av gränssnittet `com.day.cq.commons.predicate.AbstractNodePredicate` fungerar även i det klassiska användargränssnittet.
>
>I [den här kunskapsbasartikeln](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) finns ett exempel på hur du implementerar ett anpassat predikat i det klassiska användargränssnittet.

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

            Definierar vilken typ av infogad redigerare som ska användas när redigeringen på plats aktiveras för den komponenten. t.ex. `text`, `textimage`, `image`, `title`.

1. Ytterligare konfigurationsinformation om redigeraren kan konfigureras med en `config`-nod som innehåller konfigurationer samt en annan `plugin`-nod som innehåller nödvändig konfigurationsinformation för plugin-programmet.

   Följande är ett exempel på hur du definierar bildproportioner för bildbeskärningsplugin-programmet för bildkomponenten. Observera att beskärningsproportionerna flyttades till helskärmsredigeraren på grund av risken för mycket begränsad skärmstorlek och att de bara kan ses där.

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
   >Observera att i AEM beskärningsproportioner, som anges av egenskapen `ratio`, definieras som **height/width**. Detta skiljer sig från den vanliga definitionen av bredd/höjd och görs av äldre kompatibilitetsskäl. Redigeringsanvändarna kommer inte att vara medvetna om några skillnader förutsatt att du definierar egenskapen `name` tydligt eftersom detta visas i användargränssnittet.

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

`aem-authoring-extension-inplace-editor` är ett exempelpaket som visar hur du skapar en ny redigerare på plats i AEM.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-inplace-editor-projekt i GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Konfigurera flera redigerare på plats {#configuring-multiple-in-place-editors}

Det går att konfigurera en komponent så att den har flera redigerare på plats. När flera redigerare på plats har konfigurerats kan du välja rätt innehåll och öppna rätt redigerare. Mer information finns i [Configuring Multiple In-Place Editors](/help/sites-developing/multiple-inplace-editors.md)-dokumentationen.

## Lägg till en ny sidåtgärd {#add-a-new-page-action}

Om du vill lägga till en ny sidåtgärd i sidverktygsfältet, till exempel en **Gå tillbaka till platser** (konsol)-åtgärd.

### Kodexempel {#code-sample-3}

`aem-authoring-extension-header-backtosites` är ett exempelpaket som visar hur du skapar en anpassad åtgärd i sidhuvudsfältet för att hoppa tillbaka till webbplatskonsolen.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-header-backtosites-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Anpassa arbetsflödet för begäran om aktivering {#customizing-the-request-for-activation-workflow}

Det färdiga arbetsflödet, **Begär aktivering**:

* Visas automatiskt på rätt meny när en innehållsförfattare **inte har** rätt replikeringsbehörighet, men **inte har** medlemskap i DAM-användare och författare.

* I annat fall visas ingenting eftersom replikeringsrättigheterna har tagits bort.

Om du vill ha ett anpassat beteende vid en sådan aktivering kan du täcka över arbetsflödet **Begär aktivering**:

1. I `/apps`-övertäckningen **Platser**-guiden:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Detta åsidosätter den vanliga förekomsten av:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Uppdatera [arbetsflödesmodellen](/help/sites-developing/workflows-models.md) och relaterade konfigurationer/skript efter behov.
1. Ta bort rättigheten till [ `replicate`-åtgärden](/help/sites-administering/security.md#actions) från alla lämpliga användare för alla relevanta sidor, om du vill att det här arbetsflödet ska utlösas som en standardåtgärd när någon av användarna försöker publicera (eller replikera) en sida.
