---
title: Innehållsfunktion
seo-title: Featured Content Feature
description: Funktionen Aktuellt innehåll gör att besökare på den inloggade webbplatsen kan markera innehåll
seo-description: The Featured Content feature lets signed-in site visitors highlight content
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# Innehållsfunktion {#featured-content-feature}

## Introduktion {#introduction}

Funktionen för innehåll är ett område där besökare på den inloggade webbplatsen (community-medlemmar) i publiceringsmiljön kan markera innehåll för:

* [Bloggar](blog-feature.md)
* [Kalendrar](calendar.md)
* [Forum](forum.md)
* [Ideas](ideation-feature.md)
* [QnA](working-with-qna.md)

När innehållet har markerats som aktuellt kommer det att anges i den här komponenten, som kan placeras på specifika landningssidor eller områden som lätt fångar upp communitymedlemmens uppmärksamhet.

Möjligheten att använda innehåll kan vara tillåten eller otillåten per komponent.

I det här avsnittet av dokumentationen beskrivs:

* Lägga till aktuellt innehåll på en communitywebbplats.
* Konfigurationsinställningar för `Featured Content` -komponenten.

## Lägga till innehåll på en sida {#adding-featured-content-to-a-page}

Lägga till en `Featured Content` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Featured Content`

och dra den till rätt plats på en sida där det aktuella innehållet ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](essentials-featured.md#essentials-for-client-side) ingår så här `Featured Content` visas:

![funktionsinnehåll](assets/featuredcontent.png)

## Konfigurera aktuellt innehåll {#configuring-featured-content}

Markera den monterade `Featured Content` -komponenten som ska få åtkomst till och markera `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Fliken Inställningar {#settings-tab}

Under **[!UICONTROL Settings]** identifierar du innehållet som ska visas:

* **[!UICONTROL Display Name]**

   Namnet på listan med aktuellt innehåll. Till exempel `Featured Questions` eller `Featured Ideas`. Standard är `Featured Content` om det lämnas tomt.

* **[!UICONTROL Location of the Featured Content]**

   *(Obligatoriskt)* Bläddra till sidan med innehållet som kan vara en funktion (komponenterna på sidan måste vara konfigurerade för att tillåta aktuellt innehåll). Till exempel, `/content/sites/engage/en/forum`.

* **[!UICONTROL Display Limit]**

   Det maximala antalet innehåll som kan visas. Standardvärdet är 5.

## Site Visitor Experience {#site-visitor-experience}

Möjligheten att flagga innehåll som aktuellt innehåll kräver moderatorbehörighet.

När en moderator visar publicerat innehåll har de tillgång till modereringsflaggorna som innehåller det nya `Feature` flagga.

![webbplats-besökare-upplevelse](assets/site-visitor-experience.png)

När modellflaggan har flaggats som en funktion blir den `Unfeature`.

Sidan som innehåller `Featured Content` kommer nu att inkludera det här inlägget.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` är en länk till själva inlägget.

## Ytterligare information {#additional-information}

Mer information finns på [Innehåll](essentials-featured.md) för utvecklare.

Information om hur du flaggar innehåll finns i [Modererar användargenererat innehåll](moderate-ugc.md).
