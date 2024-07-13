---
title: Designa hjälpmedelsförberedda HTML5-formulär
description: HTML5-formulär använder hjälpmedelsstandarden ARIA HTML5. Dessa formulär har stöd för fliknavigering och är certifierade att vara kompatibla med vanliga skärmläsare.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Designa hjälpmedelsförberedda HTML5-formulär {#designing-accessible-html-forms}

HTML5-formulär använder hjälpmedelsstandarden ARIA HTML5 för att generera hjälpmedelsförberedda HTML-formulär. De här formulären har stöd för tabbnavigering (utom Mozilla FireFox) och är certifierade som kompatibla med vanliga skärmläsare. Om du vill generera ett HTML5-formulär med bra hjälpmedelsfunktioner utformar du XFA-formulärmallen baserat på vissa grundläggande riktlinjer för design. Riktlinjerna för designen omfattar konfiguration av rätt tabbordning och tillhandahållande av innehållet i Tala text för varje formulärkontroll. AEM Forms Designer stöder inställningen av dessa formulärkontrollsattribut för att skapa ett PDF och HTML5-formulär som är tillgängligt.

*Obs! Fliknavigeringen omfattar inte skyddade fält, t.ex. beräkningsfält som visar summan av värden. För att skärmläsaren ska kunna läsa värdet för ett skyddat fält placerar du ett tomt skrivskyddat fält ovanpå eller bredvid det skyddade fältet. Tilldela det skyddade fältets värde till det nya skrivskyddade fältet. Skärmläsaren eller fliknavigeringen kan välja det här skrivskyddade fältet och tala ut det som värdet för det skyddade fältet.*

AEM Forms Designer innehåller flera alternativ för att tala text som kan skickas till skärmläsare. För varje objekt i ett formulär kan användaren ange en av flera inställningar för skärmläsartexten:

* Anpassad uppläsningstext, som kan ställas in med paletten Tillgänglighet. Författare kan kommentera namnen på knappar och fält och deras syfte.
* Verktygstips som du kan ange på paletten Tillgänglighet.
* Bildtexter för fält i formuläret.
* Namn på objekt, enligt vad som anges i alternativet Namn på fliken Bindning.

![hjälpmedel](assets/accessibility.png)

Om det finns flera alternativ som funktionsbeskrivning, Reader-text och bildtext på en formulärkontroll använder Reader på skärmen endast en av dessa egenskaper. Standardordningen är Reader, funktionsbeskrivning, bildtext och namn för anpassad skärm. Du kan åsidosätta standardordningen med alternativet **Företräde** på Reader på paletten Tillgänglighet.
