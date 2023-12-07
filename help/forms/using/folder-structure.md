---
title: Mappstrukturen
description: Så här förstår du mappstrukturen för källkoden för arbetsytan i AEM Forms för att anpassa.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Mappstrukturen {#understanding-the-folder-structure}

AEM Forms arbetsytekomponenter är utformade för MVC-arkitektur med Backbone. Varje komponent har en fil för:

* Modell, som innehåller affärslogik.
* Template, that is an HTML file containing interface controls.
* Visa, som fungerar som en kontrollenhetsklass för Template.

Resurserna för alla komponenter placeras i mappstrukturen som beskrivs nedan. Om du vill komma åt resurserna loggar du in på CRXDE Lite och bläddrar till `/libs/ws/js/runtime/`.

**modeller** Innehåller ryggradsmodeller.

**vyer** Innehåller vyer för ryggraden.

**mallar** Innehåller bara komponenternas HTML-mallar.

**rutter** Innehåller universella vägar. Mappen Mallar inuti vägar innehåller HTML-koden och referenserna till komponenterna.

**tjänster** Innehåller tjänstgränssnitt för att anropa Adobe Experience Manager server-API:er på REST-slutpunkten.

**util** Innehåller allmänna verktyg som kan användas av flera komponenter.
