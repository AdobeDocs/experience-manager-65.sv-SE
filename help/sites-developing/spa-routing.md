---
title: SPA
seo-title: SPA
description: För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
seo-description: För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# SPA Modellroutning{#spa-model-routing}

För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad återgivning på klientsidan (t.ex. Reaktion eller Vinkel).

## Projektroutning {#project-routing}

Appen äger routningen och implementeras sedan av projektutvecklarna. Det här dokumentet beskriver routningen som är specifik för den modell som returneras av AEM. Sidmodellens datastruktur visar den underliggande resursens URL. Det främsta projektet kan använda vilket anpassat bibliotek eller tredjepartsbibliotek som helst som tillhandahåller routningsfunktioner. När en väg förväntar sig ett fragment av modellen kan ett anrop till funktionen `PageModelManager.getData()` göras. När en modellväg har ändrats måste en händelse aktiveras för att varna avlyssningsbibliotek som t.ex. Page Editor.

## Arkitektur {#architecture}

En detaljerad beskrivning finns i avsnittet [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) i SPA.

## ModelRouter {#modelrouter}

`ModelRouter` - när den är aktiverad - kapslar in API-funktionerna för HTML5-historik `pushState` och `replaceState` för att garantera att ett visst modellfragment är förhämtat och tillgängligt. Därefter meddelas den registrerade frontkomponenten om att modellen har ändrats.

## Manuell kontra automatisk modellroutning {#manual-vs-automatic-model-routing}

`ModelRouter` automatiserar hämtning av fragment av modellen. Men som alla automatiserade verktyg har de begränsningar. Vid behov kan `ModelRouter` inaktiveras eller konfigureras att ignorera sökvägar med metaegenskaper (se avsnittet Metaegenskaper i [SPA Page Component](/help/sites-developing/spa-page-component.md)-dokumentet). Utvecklare på frontsidan kan sedan implementera sitt eget modellroutningslager genom att begära att `PageModelManager` läser in ett givet fragment av modellen med funktionen `getData()`.

>[!NOTE]
>
>För närvarande illustrerar exempelprojektet React i Web.Retail Journal det automatiserade tillvägagångssättet medan projektet Angular visar det manuella. Ett halvautomatiskt tillvägagångssätt skulle också vara ett giltigt användningsfall.

>[!CAUTION]
>
>Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar mot den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av Vanity-URL:er eller alias.

## Routningskontrakt {#routing-contract}

Den aktuella implementeringen baseras på antagandet att det SPA projektet använder API:t för HTML5-historik för routning till de olika programsidorna.

### Konfiguration {#configuration}

`ModelRouter` stöder begreppet modellroutning när den lyssnar efter `pushState`- och `replaceState`-anrop för att hämta modellfragment i förväg. Internt aktiveras `PageModelManager` för att läsa in modellen som motsvarar en angiven URL och utlöser en `cq-pagemodel-route-changed`-händelse som andra moduler kan avlyssna.

Som standard aktiveras det här beteendet automatiskt. SPA bör återge följande metaegenskap för att inaktivera den:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observera att varje väg i SPA ska motsvara en tillgänglig resurs i AEM (t.ex. &quot; `/content/mysite/mypage"`) eftersom `PageModelManager` automatiskt försöker läsa in motsvarande sidmodell när flödet har valts. Vid behov kan SPA även definiera ett &quot;blockeringslista&quot; för vägar som ska ignoreras av `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
