---
title: Begränsningar för redigerare
seo-title: Editor Limitations
description: Redigeraren i det beröringsaktiverade användargränssnittet använder övertäckningar för att interagera med innehåll som begränsas i en iframe. Den här interaktionen skapar vissa begränsningar i både användningen av redigeraren och för utvecklare.
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Begränsningar för redigerare{#editor-limitations}

Redigeraren i det beröringsaktiverade användargränssnittet använder övertäckningar för att interagera med innehåll som begränsas i en iframe. Den här interaktionen skapar vissa begränsningar i både användningen av redigeraren och för utvecklare. På den här sidan sammanfattas dessa begränsningar och lösningar eller tillfälliga lösningar ges där det är möjligt.

## Funktionsbegränsningar {#functional-limitations}

En författare kan stöta på följande funktionella begränsningar när han eller hon använder redigeraren för att skapa sidor.

### Länkar som inte är aktiva {#links-not-active}

När [redigera en sida](/help/sites-authoring/editing-content.md), är länkar inte aktiva.

* [Växla till **Förhandsgranska** läge](/help/sites-authoring/editing-content.md#preview-mode) för att navigera med hjälp av länkarna i ditt innehåll.

### Strukturera sidor {#structure-pages}

Sidor kan inte namnges `structure`. Sidor med namn `structure` går inte att redigera i sidredigeraren.

## CSS-begränsningar {#css-limitations}

En utvecklare kan stöta på följande begränsningar när det gäller redigerarens interaktion med CSS.

### Absolut positionerade element {#absolutely-positioned-elements}

Absolut positionerade element kan orsaka problem i positionen för deras övertäckning.

* Om det inträffar måste du kontrollera att dimensionerna för det absolut placerade elementet är korrekta eftersom redigeraren kommer att skapa en övertäckning med exakt samma dimensioner.

### vh Enheter {#vh-units}

`vh` enheter stöds inte eftersom iframe-höjden måste justeras automatiskt av AEM.

### Fasta bakgrundsbilder {#fixed-background-images}

Fasta bakgrundsbilder kanske inte visas som fasta vid bläddring eftersom de är inbäddade i en iframe.

* Markera **Visa sidan som publicerad** i sidhuvudsfältets åtgärder visas sidan korrekt.

### 100 % höjd {#height}

Höjden 100 % stöds inte för en sidas body-element.

* Du kan komma runt problemet om du vill implementera en helskärmsbrödtext genom att&quot;sträcka ut&quot; body-elementet enligt följande:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Komprimera marginal {#margin-collapsing}

Problem med att komprimera marginaler visas om det första underordnade elementet i body-elementet har en marginal.

* Lösningen är att lägga till ett klarfix på body-elementnivån enligt följande:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
