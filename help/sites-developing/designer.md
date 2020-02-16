---
title: Designer och Designer
seo-title: Designer och Designer
description: Du måste skapa en design för din webbplats och i AEM gör du det med hjälp av Designer
seo-description: Du måste skapa en design för din webbplats och i AEM gör du det med hjälp av Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Designer och Designer{#designs-and-the-designer}

>[!CAUTION]
>
>I den här artikeln beskrivs hur du skapar en webbplats baserat på det klassiska användargränssnittet. Adobe rekommenderar att du använder de senaste AEM-teknikerna för dina webbplatser enligt beskrivningen i artikeln [Komma igång med att utveckla AEM-webbplatser](/help/sites-developing/getting-started.md).

Du måste skapa en design för din webbplats och i AEM gör du det med hjälp av Designer.

>[!NOTE]
>
>Mer information om webbtillgänglighet finns i [AEM och Web Accessibility Guidelines](/help/managing/web-accessibility.md).

## Använda Designer {#using-the-designer}

Din design kan definieras i **designavsnittet** på fliken **Verktyg** :

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Här kan du skapa den struktur som krävs för att lagra designen och sedan överföra CSS och bilder som behövs.

Designen lagras under `/etc/designs`. Sökvägen till designen som ska användas för en webbplats anges med `cq:designPath` egenskapen för `jcr:content` noden.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Alla ändringar som görs på en sida i designläge bevaras under designnoden på webbplatsen och tillämpas automatiskt på alla sidor som har samma design.

## Vad du behöver {#what-you-will-need}

För att förverkliga din design behöver du:

**CSS** - Cascading Style Sheets definierar formaten för specifika områden på sidorna.
**Bilder** - Alla bilder som du använder för funktioner som bakgrunder och knappar.

### Att tänka på när du utformar din webbplats {#considerations-when-designing-your-website}

När du utvecklar en webbplats bör du lagra bilder och CSS-filer under `/etc/design/<project>` så att du kan referera till dina resurser baserat på den aktuella designen, som beskrivs i följande kodutdrag.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

Exemplet ovan ger flera fördelar:

* Komponenter kan ha olika utseende/känsla baserat på varje plats med olika designsökvägar.
* Du kan helt enkelt designa om webbplatsen genom att peka designsökvägen till en annan nod i roten av webbplatsen från `design/v1` till `design/v2.`

* `/etc/designs` och `/content` är de enda externa URL:er som webbläsaren ser för att skydda dig mot att en extern användare blir nyfiken på vad som finns under ditt `/apps` träd. Ovanstående URL-fördelar hjälper också systemadministratören att ställa in bättre säkerhet eftersom du begränsar exponeringen av resurserna till några få distinkta platser.

