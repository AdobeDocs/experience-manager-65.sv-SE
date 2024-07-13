---
title: Funktion för innehåll
description: Funktionen Aktuellt innehåll gör att besökare på den inloggade webbplatsen kan markera innehåll
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

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
* Konfigurationsinställningar för komponenten `Featured Content`.

## Lägga till innehåll på en sida {#adding-featured-content-to-a-page}

Om du vill lägga till en `Featured Content`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Featured Content`

Dra den till en plats på en sida där det aktuella innehållet ska visas.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-featured.md#essentials-for-client-side) inkluderas visas `Featured Content`-komponenten så här:

![funktionsinnehåll](assets/featuredcontent.png)

## Konfigurera aktuellt innehåll {#configuring-featured-content}

Markera den monterade `Featured Content`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![funktionsinnehåll1](assets/featuredcontent1.png)

### Fliken Inställningar {#settings-tab}

Under fliken **[!UICONTROL Settings]** identifierar du innehållet som ska användas:

* **[!UICONTROL Display Name]**

  Namnet på listan med aktuellt innehåll. Till exempel `Featured Questions` eller `Featured Ideas`. Standardvärdet är `Featured Content` om inget anges.

* **[!UICONTROL Location of the Featured Content]**

  *(Obligatoriskt)* Bläddra till sidan som innehåller det innehåll som kan vara aktuellt (komponenterna på den sidan måste konfigureras för att tillåta aktuellt innehåll). Exempel: `/content/sites/engage/en/forum`.

* **[!UICONTROL Display Limit]**

  Det maximala antalet innehåll som kan visas. Standardvärdet är 5.

## Site Visitor Experience {#site-visitor-experience}

Möjligheten att flagga innehåll som aktuellt innehåll kräver moderatorbehörighet.

När en moderator visar publicerat innehåll har de tillgång till modereringsflaggorna som innehåller den nya `Feature`-flaggan.

![site-visitor-experience](assets/site-visitor-experience.png)

När den har flaggats som en funktion blir modereringsflaggan `Unfeature`.

Sidan som innehåller komponenten `Featured Content` innehåller nu det här inlägget.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` länkar till själva inlägget.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Aktuellt innehåll](essentials-featured.md) för utvecklare.

Information om hur du flaggar innehåll finns i [Moderering av användargenererat innehåll](moderate-ugc.md).
