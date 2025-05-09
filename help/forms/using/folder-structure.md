---
title: Mappstrukturen
description: Så här förstår du mappstrukturen för källkoden för arbetsytan i AEM Forms för att anpassa.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Mappstrukturen {#understanding-the-folder-structure}

AEM Forms arbetsytekomponenter är utformade för MVC-arkitektur med Backbone. Varje komponent har en fil för:

* Modell, som innehåller affärslogik.
* Template, that is an HTML file containing interface controls.
* Visa, som fungerar som en kontrollenhetsklass för Template.

Resurserna för alla komponenter placeras i mappstrukturen som beskrivs nedan. Logga in på CRXDE Lite och bläddra till `/libs/ws/js/runtime/` om du vill komma åt resurserna.

**modeller** innehåller ryggrad-modeller.

**vyer** innehåller vyer med ryggrad.

**mallar** innehåller endast HTML-mallarna för komponenterna.

**vägar** innehåller universella vägar. Mappen Mallar inuti vägar innehåller HTML-koden och referenserna till komponenterna.

**services** Innehåller tjänstgränssnittet för att anropa Adobe Experience Manager server-API:er på REST-slutpunkten.

**util** Innehåller allmänna verktyg som kan användas av flera komponenter.
