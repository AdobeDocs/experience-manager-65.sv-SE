---
title: Mappstrukturen
seo-title: Mappstrukturen
description: Hur du förstår mappstrukturen för källkoden för arbetsytan i AEM Forms så att du kan anpassa den.
seo-description: Hur du förstår mappstrukturen för källkoden för arbetsytan i AEM Forms så att du kan anpassa den.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Mappstrukturen {#understanding-the-folder-structure}

AEM Forms arbetsytekomponenter är utformade för MVC-arkitektur med Backbone. Varje komponent har en fil för:

* Modell, som innehåller affärslogik.
* Template, that is an HTML file containing interface controls.
* Visa, som fungerar som en kontrollenhetsklass för Template.

Resurserna för alla komponenter placeras i mappstrukturen som beskrivs nedan. Om du vill komma åt resurserna loggar du in på CRXDE Lite och bläddrar till `/libs/ws/js/runtime/`.

**** modelsInnehåller stammodeller.

**** vyerInnehåller vyer med ryggrad.

**** templatesInnehåller endast HTML-mallarna för komponenterna.

**route** Innehåller universella vägar. Mappen Mallar inuti vägar innehåller HTML-koden och referenserna till komponenterna.

**** servicesInnehåller tjänstgränssnittet för att anropa Adobe Experience Manager server-API:er på REST-slutpunkten.

**utilInnehåller allmänna** verktyg som kan användas av flera komponenter.
