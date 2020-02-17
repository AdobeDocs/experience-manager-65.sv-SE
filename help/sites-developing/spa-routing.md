---
title: SPA-modellroutning
seo-title: SPA-modellroutning
description: För program med en sida i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
seo-description: För program med en sida i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA-modellroutning{#spa-model-routing}

För program med en sida i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.

>[!NOTE]
>
>SPA-redigeraren är den rekommenderade lösningen för projekt som kräver SPA-ramverksbaserad rendering på klientsidan (t.ex. React eller Angular).

## Projektdirigering {#project-routing}

Appen äger routningen och implementeras sedan av projektutvecklarna. I det här dokumentet beskrivs routningen som är specifik för den modell som returneras av AEM-servern. Sidmodellens datastruktur visar den underliggande resursens URL. Det främsta projektet kan använda vilket anpassat bibliotek eller tredjepartsbibliotek som helst som tillhandahåller routningsfunktioner. När en väg förväntar sig ett fragment av modellen kan ett anrop till `PageModelManager.getData()` funktionen göras. När en modellväg har ändrats måste en händelse aktiveras för att varna avlyssningsbibliotek som t.ex. Page Editor.

## Arkitektur {#architecture}

En detaljerad beskrivning finns i avsnittet [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) i SPA-designdokumentet.

## ModelRouter {#modelrouter}

När `ModelRouter` det här alternativet är aktiverat kapslar det in API-funktioner för HTML5-historik `pushState` och `replaceState` för att garantera att ett visst modellfragment är förhämtat och tillgängligt. Därefter meddelas den registrerade frontkomponenten om att modellen har ändrats.

## Manuell kontra automatisk modellroutning {#manual-vs-automatic-model-routing}

Funktionen `ModelRouter` automatiserar hämtning av fragment av modellen. Men som alla automatiserade verktyg har de begränsningar. Vid behov `ModelRouter` kan sökvägarna inaktiveras eller konfigureras så att de ignoreras med metaegenskaper (se avsnittet Metaegenskaper i [SPA Page Component](/help/sites-developing/spa-page-component.md) -dokumentet). Utvecklare kan sedan implementera sitt eget modellroutningslager genom att begära `PageModelManager` att ett visst fragment av modellen ska läsas in med `getData()` funktionen.

>[!NOTE]
>
>För närvarande illustrerar exempelprojektet React i Web.Retail Journal det automatiserade tillvägagångssättet medan projektet Angular visar det manuella. Ett halvautomatiskt tillvägagångssätt skulle också vara ett giltigt användningsfall.

>[!CAUTION]
>
>Den aktuella versionen av det `ModelRouter` enda stödet för användning av URL:er som pekar på den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av Vanity-URL:er eller alias.

## Routningskontrakt {#routing-contract}

Den aktuella implementeringen baseras på antagandet att SPA-projektet använder API:t för HTML5-historik för routning till de olika programsidorna.

### Konfiguration {#configuration}

Den `ModelRouter` stöder begreppet modellroutning när den lyssnar efter `pushState` och `replaceState` anropar för att hämta modellfragment i förväg. Internt aktiveras en funktion för `PageModelManager` att läsa in den modell som motsvarar en viss URL och utlöser en `cq-pagemodel-route-changed` händelse som andra moduler kan lyssna på.

Som standard aktiveras det här beteendet automatiskt. Om du vill inaktivera den bör SPA återge följande metaegenskap:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observera att alla vägar i SPA bör motsvara en tillgänglig resurs i AEM (t.ex. &quot; `/content/mysite/mypage"`) eftersom användaren `PageModelManager` automatiskt försöker att läsa in motsvarande sidmodell när flödet har valts. Vid behov kan SPA även definiera en&quot;svart lista&quot; med vägar som ska ignoreras av `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
