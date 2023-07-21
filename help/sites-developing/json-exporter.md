---
title: JSON-exporterare för innehållstjänster
description: AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor. De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 2%

---

# JSON-exporterare för innehållstjänster{#json-exporter-for-content-services}

AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor.

De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* [Enkelsidiga program](spa-walkthrough.md)
* Inbyggda mobilprogram
* andra kanaler och kontaktpunkter externt för AEM

Med innehållsfragment som använder strukturerat innehåll kan du tillhandahålla innehållstjänster genom att använda JSON-exporteraren för att leverera innehållet på alla AEM sidor i JSON-datamodellformat. Den här metoden kan sedan användas av dina egna program.

>[!NOTE]
>
>Funktionen som beskrivs här är tillgänglig för alla kärnkomponenter eftersom [version 1.1.0 av kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

## JSON-exporterare med kärnkomponenter för innehållsfragment {#json-exporter-with-content-fragment-core-components}

Med den AEM JSON-exporteraren kan du leverera innehållet på alla AEM sidor i JSON-datamodellformat. Den här metoden kan sedan användas av dina egna program.

Inom AEM uppnås leveransen med väljaren `model` och `.json` tillägg.

`.model.json`

1. En URL som:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Levererar innehåll som:

   ![chlimage_1-192](assets/chlimage_1-192.png)

Du kan också leverera innehållet i ett strukturerat innehållsfragment genom att specifikt rikta in det på det.

Använd hela sökvägen till fragmentet (med hjälp av `jcr:content`). till exempel med ett suffix som

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
  >Du kan [anpassa era egna komponenter](/help/sites-developing/json-exporter-components.md) för att få tillgång till och använda dessa data.

  >[!NOTE]
  >
  >Även om det inte är en standardimplementering [flera väljare stöds,](json-exporter-components.md#multiple-selectors) men `model` måste vara först.

### Ytterligare information {#further-information}

Se även:

* HTTP API för Assets

   * [HTTP API för Assets](/help/assets/mac-api-assets.md)

* Sling Models:

   * [Sling Models - Associera en modellklass med en resurstyp sedan 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM med JSON:

   * [Hämta sidinformation i JSON-format](/help/sites-developing/pageinfo.md)

## Relaterad dokumentation {#related-documentation}

Mer information finns i:

* The [Avsnittet Innehållsfragment i användarhandboken för Assets](/help/assets/content-fragments/content-fragments.md)

* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-authoring/content-fragments.md)
* [Aktivera JSON-export för en komponent](/help/sites-developing/json-exporter-components.md)

* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och [Innehållsfragmentkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
