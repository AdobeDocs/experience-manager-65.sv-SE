---
title: RemotePage-komponenten
description: RemotePage-komponenten är en anpassad sidkomponent för redigering av SPA för fjärreaktion i AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# RemotePage-komponenten {#remote-page-component}

När du bestämmer vilken nivå av integration du vill ha mellan dina externa SPA och AEM är det ofta tydligt att du måste kunna visa och redigera SPA inom AEM. RemotePage-komponenten är en anpassad sidkomponent för just detta ändamål.

## Översikt {#overview}

RemotePage-komponenten hämtar alla nödvändiga resurser från programmets genererade `asset-manifest.json` och använder detta för att återge SPA i AEM.

* Med RemotePage kan du mata in skript och formatmallar för en SPA i brödtexten för en AEM Page-komponent.
* Med Virtual Front Components kan du markera avsnitt som redigerbara AEM redigeraren.
* Tillsammans kan en SPA på en annan domän göras redigerbar i AEM.

Se artikeln [Redigera en extern SPA i AEM](spa-edit-external.md) om du vill ha mer information om redigerbara, externa SPA i AEM.

## Krav {#requirements}

* Aktivera CORS under utveckling
* Konfigurera fjärr-URL i Sidegenskaper
* Återge SPA i AEM
* Webbprogrammet måste använda ett resurmanifest som något av följande och visa en asset-manifest.json-fil i domänroten som listar alla CSS- och JS-filer som ska läsas in i en entrypoints-egenskap:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![Entrypoints](assets/asset-manifest-entrypoints.png)

* Programmet måste kunna initieras i en `<div id="root"></div>` under body-elementet. Om en annan kod förväntas för att programmet ska kunna instansieras måste detta justeras i enlighet med HTML-skripten för den proxykomponent som har en `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Begränsningar {#limitations}

* RemotePage-komponenten förväntar sig att implementeringen tillhandahåller ett tillgångsmanifest som den [hittades här.](https://github.com/shellscape/webpack-manifest-plugin) RemotePage-komponenten har bara testats för att fungera med React Framework (och Next.js via komponenten remote-page-next) och stöder därför inte fjärrinläsning av program från andra ramverk, till exempel Angular.
* Intern CSS som är definierad i programmets rotfil och infogad CSS på DOM-rotnoden är inte tillgänglig vid fjärråtergivning i AEM.

## Teknisk information {#technical-details}

Precis som resten av AEM SPA är RemotePage-komponenten öppen källkod. Mer information om RemotePage-komponenten finns i [finns i GitHub-databasen.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
