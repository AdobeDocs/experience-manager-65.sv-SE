---
title: SPA
seo-title: SPA Model Routing
description: För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
seo-description: For single page applications in AEM, the app is responsible for the routing. This document describes the routing mechanism, the contract, and options available.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# SPA{#spa-model-routing}

För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad rendering på klientsidan (till exempel React eller Angular).

## Projektdirigering {#project-routing}

Appen äger routningen och implementeras sedan av projektutvecklarna. Det här dokumentet beskriver routningen som är specifik för den modell som returneras av AEM. Sidmodellens datastruktur visar den underliggande resursens URL. Det främsta projektet kan använda vilket anpassat bibliotek eller tredjepartsbibliotek som helst som tillhandahåller routningsfunktioner. När en väg förväntar sig ett fragment av modellen, anropar du `PageModelManager.getData()` kan göras. När en modellväg har ändrats måste en händelse aktiveras för att varna avlyssningsbibliotek som t.ex. Page Editor.

## Arkitektur {#architecture}

En detaljerad beskrivning finns i [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) i SPA.

## ModelRouter {#modelrouter}

The `ModelRouter` - när det är aktiverat - kapslar in API-funktioner för händelser i HTML5 `pushState` och `replaceState` för att garantera att ett visst fragment av modellen är förhämtat och tillgängligt. Därefter meddelas den registrerade frontkomponenten om att modellen har ändrats.

## Manuell kontra automatisk modellroutning {#manual-vs-automatic-model-routing}

The `ModelRouter` automatiserar hämtning av fragment av modellen. Men som alla automatiserade verktyg har de begränsningar. Vid behov `ModelRouter` kan inaktiveras eller konfigureras för att ignorera sökvägar med hjälp av metaegenskaper (se avsnittet Metaegenskaper i [SPA](/help/sites-developing/spa-page-component.md) -dokument). Utvecklare kan sedan implementera sitt eget modellroutningslager genom att begära `PageModelManager` för att läsa in ett givet fragment av modellen med `getData()` funktion.

>[!NOTE]
>
>The [We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) Exempel på React-projekt illustrerar det automatiserade tillvägagångssättet medan det manuella Angularna illustrerar det. Ett halvautomatiskt tillvägagångssätt skulle också vara ett giltigt användningsfall.

>[!CAUTION]
>
>Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar på den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av Vanity-URL:er eller alias.

## Routningskontrakt {#routing-contract}

Den aktuella implementeringen baseras på antagandet att det SPA projektet använder historik-API:t HTML5 för routning till de olika programsidorna.

### Konfiguration {#configuration}

The `ModelRouter` stöder begreppet modellroutning när det avlyssnar `pushState` och `replaceState` anropar för att hämta modellfragment i förväg. Internt aktiveras `PageModelManager` för att läsa in den modell som motsvarar en angiven URL och utlöser en `cq-pagemodel-route-changed` -händelse som andra moduler kan lyssna på.

Som standard aktiveras det här beteendet automatiskt. SPA bör återge följande metaegenskap för att inaktivera den:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Observera att varje väg i SPA ska motsvara en tillgänglig resurs i AEM (till exempel &quot; `/content/mysite/mypage"`) sedan `PageModelManager` försöker automatiskt att läsa in motsvarande sidmodell när flödet har valts. Vid behov kan SPA även definiera en &quot;blockeringslista&quot; av rutter som ska ignoreras av `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
