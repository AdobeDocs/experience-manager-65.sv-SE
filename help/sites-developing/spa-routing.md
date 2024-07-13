---
title: SPA
description: För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# SPA{#spa-model-routing}

För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad klientåtergivning (till exempel React eller Angular).

## Projektdirigering {#project-routing}

Appen äger routningen och implementeras sedan av projektutvecklarna. Det här dokumentet beskriver routningen som är specifik för den modell som returneras av AEM. Sidmodellens datastruktur visar den underliggande resursens URL. Det främsta projektet kan använda vilket anpassat bibliotek eller tredjepartsbibliotek som helst som tillhandahåller routningsfunktioner. När en väg förväntar sig ett fragment av modellen kan ett anrop till funktionen `PageModelManager.getData()` göras. När en modellväg har ändrats måste en händelse aktiveras för att varna avlyssningsbibliotek som t.ex. Page Editor.

## Arkitektur {#architecture}

En detaljerad beskrivning finns i avsnittet [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) i SPA.

## ModelRouter {#modelrouter}

`ModelRouter` - när den är aktiverad - kapslar in HTML5 History API-funktionerna `pushState` och `replaceState` för att garantera att ett visst modellfragment är förhämtat och tillgängligt. Därefter meddelas den registrerade frontkomponenten om att modellen har ändrats.

## Manuell kontra automatisk modellroutning {#manual-vs-automatic-model-routing}

`ModelRouter` automatiserar hämtning av fragment av modellen. Men som alla automatiserade verktyg har de begränsningar som behövs. Vid behov kan `ModelRouter` inaktiveras eller konfigureras för att ignorera sökvägar med hjälp av metaegenskaper (se avsnittet Metaegenskaper i [SPA Page Component](/help/sites-developing/spa-page-component.md) -dokumentet). Utvecklare på klientsidan kan sedan implementera sitt eget modellroutningslager genom att begära att `PageModelManager` läser in ett givet fragment av modellen med funktionen `getData()`.

>[!NOTE]
>
>Exempelprojektet [We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) visar det automatiserade tillvägagångssättet medan det manuella Angularna visas i projektet. Ett halvautomatiskt tillvägagångssätt skulle också vara ett giltigt användningsfall.

>[!CAUTION]
>
>Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar mot den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av Vanity-URL:er eller alias.

## Routningskontrakt {#routing-contract}

Den aktuella implementeringen baseras på antagandet att det SPA projektet använder historik-API:t HTML5 för routning till de olika programsidorna.

### Konfiguration {#configuration}

`ModelRouter` stöder begreppet modellroutning när det lyssnar efter `pushState` - och `replaceState` -anrop för att hämta modellfragment i förväg. Internt aktiveras `PageModelManager` för att läsa in modellen som motsvarar en angiven URL och en `cq-pagemodel-route-changed` -händelse som andra moduler kan lyssna på utlöses.

Som standard aktiveras det här beteendet automatiskt. SPA bör återge följande metaegenskap för att inaktivera den:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Observera att varje väg i SPA ska motsvara en tillgänglig resurs i AEM (till exempel `/content/mysite/mypage"`) eftersom `PageModelManager` automatiskt försöker läsa in motsvarande sidmodell när flödet har valts. Om det behövs kan SPA även definiera ett &quot;blockeringslista&quot; av vägar som ska ignoreras av `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
