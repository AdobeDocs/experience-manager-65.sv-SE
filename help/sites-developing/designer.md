---
title: Designer och Designer
seo-title: Designer och Designer
description: Du måste skapa en design för webbplatsen och i AEM gör du det med hjälp av Designer
seo-description: Du måste skapa en design för webbplatsen och i AEM gör du det med hjälp av Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
translation-type: tm+mt
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Designer och designern{#designs-and-the-designer}

>[!CAUTION]
>
>I den här artikeln beskrivs hur du skapar en webbplats baserat på det klassiska användargränssnittet. Adobe rekommenderar att du utnyttjar den senaste AEM tekniken för dina webbplatser enligt beskrivningen i artikeln [Komma igång med att utveckla AEM Sites](/help/sites-developing/getting-started.md).

Designer används för att skapa en design för din webbplats med det klassiska användargränssnittet [i AEM.](/help/release-notes/touch-ui-features-status.md)

>[!NOTE]
>
>Mer information om webbtillgänglighet finns i [AEM och Web Accessibility Guidelines](/help/managing/web-accessibility.md).

## Använda Designer {#using-the-designer}

Din design kan definieras i avsnittet **designs** på fliken **Verktyg**:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Här kan du skapa den struktur som krävs för att lagra designen och sedan överföra CSS och bilder som behövs.

Designer lagras under `/apps/<your-project>`. Sökvägen till designen som ska användas för en webbplats anges med egenskapen `cq:designPath` för noden `jcr:content`.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Alla ändringar som görs på en sida i designläge bevaras under designnoden på webbplatsen och tillämpas automatiskt på alla sidor som har samma design.

## Vad du behöver {#what-you-will-need}

För att förverkliga din design behöver du:

**CSS**  - Med CSS (Cascading Style Sheets) definieras formaten för specifika områden på sidorna.
**Bilder**  - Alla bilder som du använder för funktioner som bakgrunder och knappar.

### Att tänka på när du utformar din webbplats {#considerations-when-designing-your-website}

När du utvecklar en webbplats bör du lagra bilder och CSS-filer under `/apps/<your-project>` så att du kan referera till dina resurser baserat på den aktuella designen, enligt följande kodutdrag.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

Exemplet ovan ger flera fördelar:

* Komponenter kan ha olika utseende/känsla baserat på varje plats med olika designsökvägar.
* Det är enkelt att designa om webbplatsen genom att peka designsökvägen till en annan nod i webbplatsens rot från `design/v1` till `design/v2.`

* `/etc/designs` och  `/content` är de enda externa URL:er som webbläsaren ser för att skydda dig mot att en extern användare blir nyfiken på vad som finns under ditt  `/apps` träd. Ovanstående URL-fördelar hjälper också systemadministratören att ställa in bättre säkerhet eftersom du begränsar exponeringen av resurserna till några få distinkta platser.
