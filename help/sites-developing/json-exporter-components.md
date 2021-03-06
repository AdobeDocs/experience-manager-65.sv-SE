---
title: Aktivera JSON-export för en komponent
seo-title: Aktivera JSON-export för en komponent
description: Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.
seo-description: Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---


# Aktivera JSON-export för en komponent{#enabling-json-export-for-a-component}

Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.

## Översikt {#overview}

JSON-exporten baseras på [Sling Models](https://sling.apache.org/documentation/bundles/models.html) och [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130)-ramverket (som i sin tur är beroende av [Jackson-anteckningar](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Det innebär att komponenten måste ha en Sling-modell om den behöver exportera JSON. Därför måste du följa dessa två steg för att aktivera JSON-export för alla komponenter.

* [Definiera en segmentmodell för komponenten](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anteckna gränssnittet för segmenteringsmodellen](#annotate-the-sling-model-interface)

## Definiera en segmenteringsmodell för komponenten {#define-a-sling-model-for-the-component}

Först måste en segmentmodell definieras för komponenten.

>[!NOTE]
>
>Ett exempel på hur du använder delningsmodeller finns i artikeln [Developing Sling Model Exporters in AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

Implementeringsklassen för Sling-modellen måste kommenteras med följande:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Detta garanterar att komponenten kan exporteras fristående med `.model`-väljaren och `.json`-tillägget.

Dessutom anger detta att klassen Sling Model kan anpassas till gränssnittet `ComponentExporter`.

>[!NOTE]
>
>Jackson-anteckningar anges vanligtvis inte på klassnivå för Sling Model, utan på gränssnittsnivå för Model. Detta för att säkerställa att JSON-exporten betraktas som en del av komponent-API:t.

>[!NOTE]
>
>Klasserna `ExporterConstants` och `ComponentExporter` kommer från paketet `com.adobe.cq.export.json`.

### Använda flera väljare {#multiple-selectors}

Även om det inte är ett standardanvändningsfall är det möjligt att konfigurera flera väljare förutom `model`-väljaren.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

I så fall måste `model`-väljaren vara den första väljaren och tillägget måste vara `.json`.

## Anteckna gränssnittet för segmenteringsmodellen {#annotate-the-sling-model-interface}

Modellgränssnittet bör implementera gränssnittet `ComponentExporter` (eller `ContainerExporter` om det är en behållarkomponent) för att JSON-exportramverket ska kunna ta hänsyn till.

Motsvarande Sling Model-gränssnitt ( `MyComponent`) kommenteras sedan med [Jackson-anteckningar](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) för att definiera hur det ska exporteras (serialiseras).

Modellgränssnittet måste kommenteras ordentligt för att definiera vilka metoder som ska serialiseras. Som standard kommer alla metoder som respekterar den vanliga namnkonventionen för get-ters att serialiseras och härleder sina JSON-egenskapsnamn naturligt från get-namnen. Detta kan förhindras eller åsidosättas med `@JsonIgnore` eller `@JsonProperty` för att byta namn på JSON-egenskapen.

## Exempel {#example}

Core Components har stöd för JSON-export sedan version [1.1.0 av kärnkomponenterna](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och kan användas som referens.

Ett exempel finns i Sling Model-implementeringen av Image Core-komponenten och dess kommenterade gränssnitt.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-core-wcm-components-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Relaterad dokumentation {#related-documentation}

Mer information finns i:

* Avsnittet [Innehållsfragment i användarhandboken för Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-authoring/content-fragments.md)
* [JSON-exporterare för innehållstjänster](/help/sites-developing/json-exporter.md)
* [Kärnkomponenter ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och komponenten  [Innehållsfragment](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

