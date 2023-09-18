---
title: Funktion för innehåll
description: Funktionen Aktuellt innehåll gör att besökare på den inloggade webbplatsen kan markera innehåll
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# Funktion för innehåll {#featured-content-feature}

## Introduktion {#introduction}

Funktionen för innehåll är ett område där besökare (community-medlemmar) på den inloggade webbplatsen kan markera innehåll för:

* [Bloggar](blog-feature.md)
* [Kalendrar](calendar.md)
* [Forum](forum.md)
* [Ideas](ideation-feature.md)
* [QnA](working-with-qna.md)

När innehållet har markerats som aktuellt listas det i den här komponenten, som kan placeras på specifika landningssidor eller områden som lätt fångar samhällets uppmärksamhet.

Möjligheten att använda innehåll kan vara tillåten eller otillåten per komponent.

I det här avsnittet av dokumentationen beskrivs:

* Lägga till aktuellt innehåll på en communitywebbplats.
* Konfigurationsinställningar för `Featured Content` -komponenten.

## Lägga till innehåll på en sida {#adding-featured-content-to-a-page}

Lägga till en `Featured Content` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Featured Content`

Dra den till en plats på en sida där det aktuella innehållet ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](essentials-featured.md#essentials-for-client-side) ingår så här `Featured Content` visas:

![funktionsinnehåll](assets/featuredcontent.png)

## Konfigurera aktuellt innehåll {#configuring-featured-content}

Markera den monterade `Featured Content` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Fliken Inställningar {#settings-tab}

Under **[!UICONTROL Settings]** identifierar du innehållet som ska visas:

* **[!UICONTROL Display Name]**

  Namnet på listan med aktuellt innehåll. Till exempel: `Featured Questions` eller `Featured Ideas`. Standard är `Featured Content` om det lämnas tomt.

* **[!UICONTROL Location of the Featured Content]**

  *(Obligatoriskt)* Bläddra till sidan som innehåller det innehåll som kan vara aktuellt (komponenterna på den sidan måste vara konfigurerade för att tillåta aktuellt innehåll). Till exempel, `/content/sites/engage/en/forum`.

* **[!UICONTROL Display Limit]**

  Det maximala antalet innehåll som kan visas. Standardvärdet är 5.

## Site Visitor Experience {#site-visitor-experience}

Möjligheten att flagga innehåll som aktuellt innehåll kräver moderatorbehörighet.

När en moderator visar publicerat innehåll har de tillgång till modereringsflaggorna som innehåller det nya `Feature` flagga.

![webbplats-besökare-upplevelse](assets/site-visitor-experience.png)

När den har flaggats som en funktion blir modereringsflaggan `Unfeature`.

Sidan som innehåller `Featured Content` ingår nu detta inlägg.

![site-visitor-experience1](assets/site-visitor-experience1.png)

The `Read More` länkar till själva inlägget.

## Ytterligare information {#additional-information}

Mer information finns på [Innehåll](essentials-featured.md) för utvecklare.

Information om hur du flaggar innehåll finns i [Modererar användargenererat innehåll](moderate-ugc.md).
