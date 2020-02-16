---
title: Mappstrukturen
seo-title: Mappstrukturen
description: Hur du förstår mappstrukturen för källkoden för AEM Forms-arbetsytan så att du kan anpassa den.
seo-description: Hur du förstår mappstrukturen för källkoden för AEM Forms-arbetsytan så att du kan anpassa den.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Mappstrukturen {#understanding-the-folder-structure}

AEM Forms arbetsytekomponenter är utformade för MVC-arkitektur med Backbone. Varje komponent har en fil för:

* Modell, som innehåller affärslogik.
* Template, that is an HTML file containing interface controls.
* Visa, som fungerar som en kontrollenhetsklass för Template.

Resurserna för alla komponenter placeras i mappstrukturen som beskrivs nedan. Logga in på CRXDE Lite och bläddra till resurserna `/libs/ws/js/runtime/`.

**modeller** Innehåller modeller för stamnät.

**vyer** Innehåller vyer med ryggrad.

**-mallar** innehåller endast HTML-mallar för komponenterna.

**vägar** innehåller universella vägar. Mappen Mallar inuti vägar innehåller HTML-koden och referenserna till komponenterna.

**tjänster** Innehåller tjänstgränssnittet som anropar Adobe Experience Manager-server-API:er på REST-slutpunkten.

**util** Innehåller allmänna verktyg som kan användas av flera komponenter.

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
