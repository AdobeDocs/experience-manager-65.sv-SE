---
title: JSON-exporterare för innehållstjänster
seo-title: JSON-exporterare för innehållstjänster
description: AEM Content Services är utformat för att generalisera beskrivningen och leveransen av innehåll i/från AEM, bortom fokus på webbsidor. De levererar innehåll till kanaler som inte är traditionella AEM-webbsidor med hjälp av standardiserade metoder som kan användas av alla kunder.
seo-description: AEM Content Services är utformat för att generalisera beskrivningen och leveransen av innehåll i/från AEM, bortom fokus på webbsidor. De levererar innehåll till kanaler som inte är traditionella AEM-webbsidor med hjälp av standardiserade metoder som kan användas av alla kunder.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# JSON-exporterare för innehållstjänster{#json-exporter-for-content-services}

AEM Content Services är utformat för att generalisera beskrivningen och leveransen av innehåll i/från AEM, bortom fokus på webbsidor.

De levererar innehåll till kanaler som inte är traditionella AEM-webbsidor med hjälp av standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* Enkelsidiga program
* Inbyggda mobilprogram
* andra kanaler och kontaktytor utanför AEM

Med innehållsfragment som använder strukturerat innehåll kan du tillhandahålla innehållstjänster genom att använda JSON-exporteraren för att leverera innehållet på en (y) AEM-sida i JSON-datamodellsformat. Detta kan sedan användas av dina egna program.

>[!NOTE]
>
>Funktionen som beskrivs här är tillgänglig för alla kärnkomponenter sedan [version 1.1.0 av kärnkomponenterna](https://docs.adobe.com/content/docs/en/core-components/v1.html).

## JSON-exporterare med kärnkomponenter för innehållsfragment {#json-exporter-with-content-fragment-core-components}

Med AEM JSON-exporteraren kan du leverera innehållet på en (y) AEM-sida i JSON-datamodellsformat. Detta kan sedan användas av dina egna program.

Inom AEM uppnås leveransen med suffixet

`.model.json`

1. En URL som:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Levererar innehåll som:

   ![chlimage_1-192](assets/chlimage_1-192.png)

Du kan också leverera innehållet i ett strukturerat innehållsfragment genom att specifikt rikta in det på det.

Detta görs med hela sökvägen till fragmentet (via `jcr:content`), till exempel med ett suffix som

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

Sidan kan innehålla antingen ett enda innehållsfragment eller flera komponenter av olika typer. Du kan också använda funktioner som listkomponenter för att automatiskt söka efter relevant innehåll.

* En URL som:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Levererar innehåll som:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >Ni kan [anpassa era egna komponenter](/help/sites-developing/json-exporter-components.md) för att få tillgång till och använda dessa data.

### Ytterligare information {#further-information}

Se även:

* Resurser för HTTP API

   * [Resurser för HTTP API](/help/assets/mac-api-assets.md)

* Sling Models:

   * [Sling Models - Associera en modellklass med en resurstyp sedan 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM med JSON:

   * [Hämta sidinformation i JSON-format](/help/sites-developing/pageinfo.md)

## Related Documentation {#related-documentation}

Mer information finns i:

* Avsnittet [Innehållsfragment i användarhandboken för Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modeller för innehållsfragment](/help/assets/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-authoring/content-fragments.md)
* [Aktivera JSON-export för en komponent](/help/sites-developing/json-exporter-components.md)

* [Kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och komponenten [Innehållsfragment](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

