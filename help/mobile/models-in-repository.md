---
title: Modeller i databas
seo-title: Modeller i databas
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Modeller i databas{#models-in-repository}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

En modell innehåller en uppsättning datatyper som definierar de egenskaper som till slut kommer att återges av innehållstjänster. En modell definierar också relationerna mellan andra modeller för att säkerställa dataintegriteten.

Som utvecklare bör du känna till modellstrukturen i databasen. Du kan skapa egna modeller och enheter utifrån dina appbehov.

## Skapa modelltyper {#creating-model-types}

Det finns två modelltyper som tillhandahålls av systemet under */libs/settings/mobileapps/model-types*. Om du vill åsidosätta systemmodelltyperna måste en *mobileapps/model-types* -nod skapas under konfigurationsnoden som du vill att åsidosättningen ska ske på.

Om du till exempel har skapat konfigurationer på */conf/myconf1* och */conf/myconf2* och vill åsidosätta systemmodelltyperna på *conf1* skapar du en *mobileapps/model-types* -nod under inställningarna för *conf1*.

Om du vill tillåta att datatyper läggs till i en modell måste modelltypen ha en underordnad nod med namnet &#39;scaffolding&#39; av typen &#39;cq:Page&#39; och resurstypen *wcm/scaffolding/components/scaffolding*.

Skolningssidan måste även innehålla en *dataTypesConfig* -egenskap på noden PageContent, som anger att datatyperna som skapas av den här typen kan användas.

>[!NOTE]
>
>En **ställningar** är en sida som definierar de datatyper som kan redigeras av en enhet baserat på modellen. Varje datatyp kan också konfigureras för att definiera hur fältet ska presenteras i användargränssnittet samt hur datavärdet ska bevaras.

### Konfigurera datatyper {#data-types-config}

Konfigurationsnoden för datatyper innehåller en lista med datatypsobjekt. Varje datatypsobjekt anger hur en datatyp kommer att visas i modellredigeraren samt hur den måste bevaras för eventuell återgivning av en enhet.

| **Egenskapsnamn** | **Beskrivning** |
|---|---|
| fieldIcon | klassen CoralUI-ikon som representerar datatypen |
| fieldPropResourceType | som återger alla egenskaper för konfigurering av datatypen |
| fieldProperties | flervärdeslista över egenskapskomponenter som används när fieldPropResourceType är *mobileapps/caas/gui/components/models/editor/datatypes/field* |
| fieldResourceType | resourceType för den beständiga noden för datatypen (d.v.s. komponenten som återger egenskapen i entitetsredigeraren) |
| fieldViewResourceType | -komponent som ska användas för återgivning av datatyp i modellredigeringsvyn (fieldResourceType används om den här egenskapen utelämnas) |
| fieldTitle | namnet på den datatyp som ska visas i modellredigeraren |
| multiFieldResourceType | resurstyp som ska användas på beständig nod när flera värden har valts |
| renderType | renderingsknapp för klientåtergivning |

### Konfigurationsövertäckning för datatyper {#data-types-config-overlay}

Egenskapen dataTypesConfig stöder sammanslagning av Sling-resurser. Det innebär att de datatyper som används av systemmodelltyperna (eller till och med anpassade modelltyper) kan anpassas med hjälp av överläggsnoder.

En övertäckning av */libs/settings/mobileapps/models/formbuilderconfig/datatypes* måste skapas och sedan anpassas efter behov.

En övertäckning för datatypen String kan till exempel läggas till för att ändra fieldResourceType till en anpassad komponent.

Mer information om Sling Resource Merging finns i [Använda Sling Resource Merger i AEM](/help/sites-developing/sling-resource-merger.md).

![chlimage_1-7](assets/chlimage_1-7.png)

### Datatyper {#data-types}

En modelldatatyp är en formulärkomponent som kan inkludera data som ska inkluderas när ett formulär publiceras. Datatypskomponenten kan vara så komplicerad som du vill. Ett exempel på en anpassad datatyp kan vara ett adressblock för ett visst land för att undvika att behöva återskapa det hela tiden med hjälp av primitiva datatyper.

Se &#39;/libs/mobileapps/caas/components/form/contentreference&#39; som ett exempel på en anpassad datatyp.

Alla primitiva datatyper använder befintliga Granite-formulärkomponenter. Se: [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

Alla anpassade datatyper kan sedan läggas till i en datatypskonfiguration som kan användas av modellredigeraren.

## Skapa modeller {#creating-models}

Du kan börja skapa modeller när alla önskade modelltyper och datatyper har utvecklats. Författarna kommer i slutändan att använda modeller för att skapa enheter som innehållstjänsterna använder för att återge data från.

Att skapa en modell består av att välja en tillåten modelltyp baserat på den aktuella konfigurationen och sedan ange en rubrik och beskrivning.

Mer information om hur du skapar och hanterar en modell från kontrollpanelen finns i [Skapa en modell](/help/mobile/administer-mobile-apps.md) under redigeringsavsnittet för mobilappar.

### Egenskaper för en modell {#properties-of-a-model}

I följande tabell visas egenskaperna som definierats för en modell:

| **Egenskapsnamn** | **Beskrivning** |
|---|---|
| Modelltitel | modellens namn |
| Beskrivning | beskrivning av modellen |
| Miniatyrbild | miniatyrbild av modellen |
| Modelltyp | modelltyp (det kan vara en enkel sträng eller en sökväg till en faktisk komponent) |
| Tillåtna underordnade | sökväg till en mall som kan vara underordnad den här mallen |
| Tillåtna överordnade | sökväg till en mall som kan vara överordnad den här mallen |

>[!NOTE]
>
>De *tillåtna egenskaperna för underordnade* och *tillåtna överordnade* följer samma regler som för sidmallar. Mer information finns i [Sidmallar](/help/sites-developing/page-templates-static.md).
>
>Med referens till *modelltypsegenskapen* måste alla modeller ha en överordnad typ av *mobileapps/caas/components/data/entity* , men kan ha en undertyp som gör att innehållsleveransen kan anpassas. Om du ser till att alla modelltyper är unika kan det också hjälpa klienter med innehållstjänster att skilja mellan objekt i data.

### Redigera en modell {#editing-a-model}

När du redigerar en modell öppnar du dialogrutan för ställningar som är kopplad till en modell för redigering. Skolningen är vanligtvis en underordnad nod till modellen, men den kan placeras utanför modellen om så önskas genom att ange dess sökväg med egenskapen cq:scaffolding. Detta är användbart om du vill dela samma ställningar mellan flera modeller som behöver olika egenskaper.

När modellens ställningar finns kommer modellredigeraren att återge det som finns under jcr:content/cq:dialog/content. För närvarande stöds bara en fast layout med upp till 3 kolumner av den klientbaserade formbyggmotorn. Till höger om den återgivna formulärdialogrutan finns en lista med alla datatyper som anges i datatypskonfigurationen. Du kan redigera datatyper genom att klicka på dem. Högerspåret växlar sedan till egenskapsfliken för den valda datatypen. Du kan lägga till nya datatyper genom att dra dem till förhandsvisningsytan. Om du klickar på Spara sprids ändringarna till servern. När du klickar på Avbryt stängs modellredigeraren.

>[!NOTE]
>
>Alla modeller är mallar, så de följer alla AEM-mallregler. Detta gör att du kan använda egenskaper som ** allowedParentes och *allowedChildren* . Dessa gäller när nya entiteter skapas baserat på en modell. Mallreglerna säkerställer att enheter bara kan baseras på vissa modeller beroende på deras hierarki.
>
>Mer information om hur du redigerar en modell från kontrollpanelen finns i [Skapa en modell](/help/mobile/administer-mobile-apps.md) under redigeringsavsnittet för mobilappar.

### Systemmodeller {#system-models}

Det finns två typer av fördefinierade systemmodeller för enkel återanvändning av innehåll. Dessa modeller kan inte redigeras.

**Sidmodell** Sidmodellen är en snabb metod för att återanvända befintligt innehåll från webbplatser för leverans via innehållstjänster.

resourceType för entiteter som baseras på sidmodellen är: mobileapps/caas/components/data/pages

Sökväg: Sökväg till en webbplatssida. Innehåll från den här sökvägen (och dess underordnade objekt) återges av innehållstjänsthanterare.

**Resursmodell** Med Assets-modellen kan du snabbt återanvända befintligt innehåll från Assets för leverans via innehållstjänster.

resourceType för entiteter som baseras på sidmodellen är: mobileapps/ *caas/components/data/assets.*

Resurslista: Lista med sökvägar från Assets. Varje resurs läggs till som en underordnad entitetsnod med en resourceType som är *wcm/foundation/components/image*.

>[!NOTE]
>
>Mer information om hur du använder de här mallarna för att skapa modeller från kontrollpanelen finns i [Skapa en modell](/help/mobile/administer-mobile-apps.md) under redigeringsavsnittet för mobilappar.
