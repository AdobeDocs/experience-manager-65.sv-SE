---
title: Avancerade URL-konfigurationer
description: Lär dig hur du anpassar URL:er för produkt- och kategorisidor. Detta gör att implementeringar kan optimera URL:er för sökmotorer och främja identifiering.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---

# Avancerade URL-konfigurationer {#url}

>[!NOTE]
>
>Sökmotoroptimering (SEO) har blivit en viktig fråga för många marknadsförare. Därför måste SEO-frågor behandlas i många AEM projekt. Se [Bästa praxis för hantering av SEO och URL](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) om du vill ha mer information.

[AEM CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components) innehåller avancerade konfigurationer för att anpassa URL:er för produkt- och kategorisidor. Många implementeringar anpassar dessa URL:er för sökmotoroptimering (SEO). Följande video visar hur du konfigurerar `UrlProvider` Service och funktioner i [Samlingsmappning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att anpassa URL:er för produkt- och kategorisidor.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Konfiguration {#configuration}

Konfigurera `UrlProvider` enligt SEO-kraven och ett projekt måste tillhandahålla en OSGI-konfiguration för konfigurationen CIF URL-provider.

>[!NOTE]
>
>Sedan version 2.0.0 av AEM CIF Core Components finns det bara fördefinierade url-format i URL-providerkonfigurationen, i stället för de format som kan konfigureras fritt från 1.x-versioner. Dessutom har användningen av väljare för att skicka data i URL-adresser ersatts med suffix.

### URL-format för produktsida {#product}

Detta konfigurerar URL:erna för produktsidorna och stöder följande alternativ:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (standard)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

Om det finns [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/product-page`
* `{{sku}}` ersätts med exempelvis produktens SKU, `VP09`
* `{{url_key}}` ersätts med produktens `url_key` egenskap, till exempel `lenora-crochet-shorts`
* `{{url_path}}` ersätts med produktens `url_path`, till exempel `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` ersätts med den markerade varianten, till exempel `VP09-KH-S`

Sedan `url_path` eftersom de fördefinierade produkt-URL-formaten är inaktuella används en produkts `url_rewrites` och välja det med de flesta bansegmenten som alternativ om `url_path` är inte tillgängligt.

Med exempeldata ser en produktvariant-URL som är formaterad med standardformatet för URL ut som `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### URL-format för kategorisida {#product-list}

Detta konfigurerar URL:erna för kategorierna eller produktlistsidorna och stöder följande alternativ:

* `{{page}}.html/{{url_path}}.html` (standard)
* `{{page}}.html/{{url_key}}.html`

Om det finns [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` ersätts med `/content/venia/us/en/products/category-page`
* `{{url_key}}` ersätts av kategoriens `url_key` property
* `{{url_path}}` ersätts av kategoriens `url_path`

Med exempeldata ovan ser en kategorisidas URL-adress formaterad med standardformatet för URL-adresser ut som `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>The `url_path` är en kombination av `url_keys` för en produkts eller kategoris överordnade och produkten eller kategorin `url_key` avgränsad med `/` snedstreck.

### Specifik kategori-/produktsida {#specific-pages}

Det går att skapa [flera kategorier och produktsidor](multi-template-usage.md) för endast en viss delmängd av kategorier eller produkter i en katalog.

The `UrlProvider` är förkonfigurerat för att generera djupa länkar till sådana sidor på instanser på författarnivå. Detta är användbart för redigerare som bläddrar på en webbplats i förhandsgranskningsläge, navigerar till en viss produkt- eller kategorisida och växlar tillbaka till redigeringsläget för att redigera sidan.

Vid publiceringsnivåinstanser å andra sidan bör katalogsidans URL-adresser hållas stabila så att de inte förlorar vinster på rankningar för sökmotorer. På grund av detta kommer instanser av publiceringsnivån inte att återge djuplänkar till specifika katalogsidor per standard. Om du vill ändra detta beteende _CIF URL Provider Specific Page Strategy_ kan konfigureras för att alltid generera särskilda sidadresser.

## Anpassade URL-format {#custom-url-format}

Om du vill ange ett anpassat URL-format som ett projekt kan implementera [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) eller [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) och registrera implementeringen som en tjänst av allmänt ekonomiskt intresse. Dessa implementeringar, om de är tillgängliga, ersätter det konfigurerade fördefinierade formatet. Om det finns flera registrerade implementeringar ersätter den med den högre rangordningen dem med den lägre rangordningen.

Implementeringarna av det anpassade URL-formatet måste implementera ett par metoder för att skapa en URL från angivna parametrar och för att tolka en URL för att returnera samma parametrar.

## Kombinera med delningskartor {#sling-mapping}

Förutom `UrlProvider`går det också att konfigurera [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) för att skriva om och bearbeta URL:er. Det AEM Archetype-projektet innehåller även [en exempelkonfiguration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) om du vill konfigurera vissa kopplingsmappningar för port 4503 (publicera) och 80 (Dispatcher).

## Kombinera med AEM Dispatcher {#dispatcher}

URL-omskrivningar kan också göras med AEM Dispatcher HTTP-server med `mod_rewrite` -modul. The [AEM Project Archettype](https://github.com/adobe/aem-project-archetype) innehåller en referens AEM Dispatcher-konfiguration som redan innehåller grundläggande [skriv om regler](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) för den genererade storleken.

## Exempel

The [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia) projektet innehåller exempelkonfigurationer som visar hur anpassade URL:er används för produkt- och kategorisidor. På så sätt kan varje projekt skapa individuella URL-mönster för produkt- och kategorisidor efter sina SEO-behov. En kombination av CIF `UrlProvider` och Samlingsmappningar enligt ovan används.

>[!NOTE]
>
>Den här konfigurationen måste justeras med den externa domän som används av projektet. Samlingsmappningarna fungerar baserat på värdnamnet och domänen. Den här konfigurationen är därför inaktiverad som standard och måste aktiveras före distributionen. Om du vill göra det byter du namn på kopplingsmappningen `hostname.adobeaemcloud.com` mapp i `ui.content/src/main/content/jcr_root/etc/map.publish/https` enligt det använda domännamnet och aktivera den här konfigurationen genom att lägga till `resource.resolver.map.location="/etc/map.publish"` till `JcrResourceResolver` projektets konfiguration.

## Ytterligare resurser

* [Referensarkiv för Venedig](https://github.com/adobe/aem-cif-guides-venia)
* [AEM resursmappning](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Samlingsmappningar](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
