---
title: Använda SOM-uttryck i adaptiva former
seo-title: Använda SOM-uttryck i adaptiva former
description: Lär dig hur du extraherar SOM-uttryck för en panel i ett adaptivt formulär.
seo-description: Lär dig hur du extraherar SOM-uttryck för en panel i ett adaptivt formulär.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Använda SOM-uttryck i adaptiva former{#using-som-expressions-in-adaptive-forms}

Anpassningsbara formulär modelleras som AEM Page, som representeras som JCR-innehållsstruktur i AEM-databasen. Nyckelelementet i innehållsstrukturen är noden guideContainer. Under guideContainer finns det rootPanel som kan innehålla kapslade paneler och fält.

Du kan använda en skriptobjektmodell (SOM) för att referera till värden, egenskaper och metoder i en viss dokumentobjektmodell (DOM). En DOM organiserar minnesobjekt och egenskaper i en trädhierarki. A SOM expression references Fields/Draw elements and panels.

Följande bild visar en nodstruktur som ett adaptivt formulär översätter till när du lägger till komponenter i ett formulär. Du kan till exempel lägga till en panel i rotpanelen och en alternativknapp i panelen som omvandlas till DOM vid körning. SOM-uttrycket för alternativknappsfältet i adaptiv form anges som `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![DOM-träd](assets/hierarchy.png)

DOM-träd

A SOM expression for any element in an adaptive form is prefix by `guide[0].guide1[0]`. Positionen för en komponent i nodstrukturhierarkin används för att härleda dess SOM-uttryck.

![DOM-träd med två alternativknappar](assets/hierarchy_radio_button.png)

DOM-träd med två alternativknappar

SOM-uttrycket ändras när du ändrar positionen för alternativknapparna i det adaptiva formuläret. I redigeringsläget kan du visa SOM-uttrycket för ett fält eller element i AEM Forms med alternativet Visa SOM-uttryck. Alternativet visas på panelen och när du högerklickar på fältet eller elementet.

![Extrahera SOM-uttryck i en adaptiv form](assets/som-expressions.png)

Extrahera SOM-uttryck i en adaptiv form

I paneler kan du komma åt funktionen från panelens verktygsfält. Funktionen underlättar skriptning för formulärförfattare som vill anpassa formulär.

![Extrahera SOM-uttryck med panelens verktygsfält](assets/som-expression.png)

Extrahera SOM-uttryck med panelens verktygsfält

Vissa API:er i [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.md) använder SOM-uttrycket för ett element. Om du till exempel vill ge fokus till ett visst fält i en adaptiv form skickar du motsvarande SOM-uttryck till `getFocus`API:t i `guideBridge`.

