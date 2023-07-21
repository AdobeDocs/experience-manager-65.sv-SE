---
title: Aktivera JSON-export för en komponent
description: Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Aktivera JSON-export för en komponent{#enabling-json-export-for-a-component}

Komponenter kan anpassas för att generera JSON-export av deras innehåll baserat på ett modellramverk.

## Översikt {#overview}

JSON-exporten baseras på [Sling Models](https://sling.apache.org/documentation/bundles/models.html)och på [Export av försäljningsmodell](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) som i sig förlitar sig på [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Det innebär att komponenten måste ha en Sling-modell om den måste exportera JSON. Följ därför de här två stegen för att aktivera JSON-export för alla komponenter.

* [Definiera en segmentmodell för komponenten](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anteckna gränssnittet för segmenteringsmodellen](#annotate-the-sling-model-interface)

## Definiera en delningsmodell för komponenten {#define-a-sling-model-for-the-component}

Först måste en segmentmodell definieras för komponenten.

>[!NOTE]
>
>Ett exempel på hur du använder modeller finns i [Utveckla export av försäljningsmodeller i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en).

Implementeringsklassen för Sling-modellen måste kommenteras med följande:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Detta garanterar att komponenten kan exporteras fristående med `.model` väljaren och `.json` tillägg.

Dessutom anger detta att klassen Sling Model kan anpassas till `ComponentExporter` gränssnitt.

>[!NOTE]
>
>Jackson-anteckningar anges inte på klassnivå för Sling Model, utan på gränssnittsnivå för Model. Detta för att säkerställa att JSON-exporten betraktas som en del av komponent-API:t.

>[!NOTE]
>
>The `ExporterConstants` och `ComponentExporter` klasserna kommer från `com.adobe.cq.export.json` paket.

### Använda flera väljare {#multiple-selectors}

Även om det inte är ett standardanvändningsfall är det möjligt att konfigurera flera väljare förutom `model` väljare.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

I sådana fall gäller dock att `model` väljaren måste vara den första väljaren och tillägget måste vara `.json`.

## Anteckna gränssnittet för segmenteringsmodellen {#annotate-the-sling-model-interface}

Modellgränssnittet bör implementera `ComponentExporter` gränssnitt (eller `ContainerExporter`, om det finns en behållarkomponent).

Motsvarande Sling Model-gränssnitt ( `MyComponent`) kommenteras sedan med [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) för att definiera hur den ska exporteras (serialiseras).

Modellgränssnittet måste vara korrekt kommenterat för att definiera vilka metoder som ska serialiseras. Som standard serialiseras alla metoder som respekterar den vanliga namnkonventionen för get-ters och hämtar JSON-egenskapsnamnen naturligt från get-namnen. Detta kan förhindras eller åsidosättas med `@JsonIgnore` eller `@JsonProperty` för att byta namn på JSON-egenskapen.

## Exempel {#example}

Core Components har stöd för JSON-export sedan lanseringen [1.1.0 av kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och kan användas som referens.

Ett exempel finns i Sling Model-implementeringen av Image Core-komponenten och dess kommenterade gränssnitt.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-core-wcm-components-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Relaterad dokumentation {#related-documentation}

Mer information finns i följande:

* The [Avsnittet Innehållsfragment i användarhandboken för Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
* [Skapa med innehållsfragment](/help/sites-authoring/content-fragments.md)
* [JSON-exporterare för innehållstjänster](/help/sites-developing/json-exporter.md)
* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och [Innehållsfragmentkomponent](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
