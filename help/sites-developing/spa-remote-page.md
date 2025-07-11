---
title: RemotePage-komponenten
description: RemotePage-komponenten är en anpassad sidkomponent för redigering av fjärreaktions-SPA i AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# RemotePage-komponenten {#remote-page-component}

När du bestämmer vilken nivå av integration du vill ha mellan det externa SPA-programmet och AEM är det ofta tydligt att du behöver kunna visa och redigera SPA-programmet inom AEM. RemotePage-komponenten är en anpassad sidkomponent för just detta ändamål.

{{ue-over-spa}}

## Ökning {#overview}

RemotePage-komponenten hämtar alla nödvändiga resurser från programmets genererade `asset-manifest.json` och använder den för att återge SPA i AEM.

* Med RemotePage kan du mata in skript och formatmallar för en SPA i brödtexten för en AEM Page-komponent.
* Med Virtual Front Components (Komponenter för virtuell frontend) kan du markera avsnitt som redigerbara i AEM SPA Editor.
* Tillsammans kan en SPA på en annan domän göras redigerbar i AEM.

Mer information om redigerbara externa SPA:er i AEM finns i artikeln [Redigera en extern SPA i AEM](spa-edit-external.md).

## Krav {#requirements}

* Aktivera CORS under utveckling
* Konfigurera fjärr-URL i Sidegenskaper
* Återge SPA i AEM
* Webbprogrammet måste använda ett resurmanifest som något av följande och visa en asset-manifest.json-fil i domänroten som listar alla CSS- och JS-filer som ska läsas in i en entrypoints-egenskap:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![Entrypoints](assets/asset-manifest-entrypoints.png)

* Programmet måste kunna initieras i ett `<div id="root"></div>` under body-elementet. Om en annan kod förväntas för att programmet ska kunna instansieras måste detta justeras i HTML-skripten för proxykomponenten som har en `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Begränsningar {#limitations}

* RemotePage-komponenten förväntar sig att implementeringen tillhandahåller ett tillgångsmanifest som den [ som finns här.](https://github.com/shellscape/webpack-manifest-plugin) RemotePage-komponenten har bara testats för att fungera med React Framework (och Next.js via komponenten remote-page-next) och stöder därför inte fjärrinläsning av program från andra ramverk, som Angular.
* Intern CSS som är definierad i programmets HTML-rotfil och infogad CSS på DOM-rotnoden är inte tillgänglig vid fjärråtergivning i AEM.

## Teknisk information {#technical-details}

Precis som resten av AEM SPA-projektet är RemotePage-komponenten en öppen källkod. Fullständig teknisk information om RemotePage-komponenten finns i [GitHub-databasen.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
