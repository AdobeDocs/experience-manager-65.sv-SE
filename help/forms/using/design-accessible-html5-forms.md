---
title: Utforma hjälpmedelsförberedda HTML5-formulär
seo-title: Utforma hjälpmedelsförberedda HTML5-formulär
description: HTML5-formulär använder hjälpmedelsstandarden ARIA HTML5. Dessa formulär har stöd för fliknavigering och är certifierade att vara kompatibla med vanliga skärmläsare.
seo-description: HTML5-formulär använder hjälpmedelsstandarden ARIA HTML5. Dessa formulär har stöd för fliknavigering och är certifierade att vara kompatibla med vanliga skärmläsare.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Utforma hjälpmedelsförberedda HTML5-formulär {#designing-accessible-html-forms}

HTML5-formulär använder hjälpmedelsstandarden ARIA HTML5 för att generera hjälpmedelsförberedda HTML-formulär. De här formulären har stöd för tabbnavigering (utom Mozilla FireFox) och är certifierade som kompatibla med vanliga skärmläsare. Om du vill generera ett HTML5-formulär med bra hjälpmedelsfunktioner utformar du XFA-formulärmallen baserat på vissa grundläggande riktlinjer för design. Riktlinjerna för designen omfattar konfiguration av rätt tabbordning och tillhandahållande av innehållet i Tala text för varje formulärkontroll. AEM Forms Designer stöder inställningen av dessa formulärkontrollsattribut för att generera ett tillgängligt PDF- och HTML5-formulär.

*Obs!Fliknavigering omfattar inte skyddade fält, t.ex. beräkningsfält som visar summan av värden. För att skärmläsaren ska kunna läsa värdet för ett skyddat fält placerar du ett tomt skrivskyddat fält ovanpå eller bredvid det skyddade fältet. Tilldela det skyddade fältets värde till det nya skrivskyddade fältet. Skärmläsaren eller fliknavigeringen kan välja det här skrivskyddade fältet och tala ut det som värdet för det skyddade fältet.*

AEM Forms Designer innehåller ett antal alternativ för att tala text som kan skickas till skärmläsare. För varje objekt i ett formulär kan användaren ange en av flera inställningar för skärmläsartexten:

* Anpassad uppläsningstext, som kan ställas in med paletten Tillgänglighet. Författare kan kommentera namnen på knappar och fält samt deras syfte.
* Verktygstips som du kan ange på paletten Tillgänglighet.
* Bildtexter för fält i formuläret.
* Namn på objekt, enligt alternativen Namn på fliken Bindning.

![hjälpmedel](assets/accessibility.png)

Om det finns flera alternativ som funktionsbeskrivning, Reader-text och bildtext på en formulärkontroll använder Reader på skärmen endast en av dessa egenskaper. Standardordningen är Reader, funktionsbeskrivning, bildtext och namn för anpassad skärm. Du kan åsidosätta standardordningen med alternativet Skärmprioritet **Reader** på paletten Tillgänglighet.
