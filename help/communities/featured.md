---
title: Innehållsfunktion
seo-title: Innehållsfunktion
description: Funktionen Aktuellt innehåll gör att besökare på den inloggade webbplatsen kan markera innehåll
seo-description: Funktionen Aktuellt innehåll gör att besökare på den inloggade webbplatsen kan markera innehåll
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: cbb5a6bac5e9932fd36abf20d4424890080d39bf
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

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
* Konfigurationsinställningar för komponenten `Featured Content`.

## Lägga till innehåll på en sida {#adding-featured-content-to-a-page}

Om du vill lägga till en `Featured Content`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på

* `Communities / Featured Content`

och dra den till rätt plats på en sida där det aktuella innehållet ska visas.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-featured.md#essentials-for-client-side) inkluderas visas `Featured Content`-komponenten så här:

![chlimage_1-13](assets/chlimage_1-13.png)

## Konfigurerar aktuellt innehåll {#configuring-featured-content}

Markera den monterade `Featured Content`-komponenten som ska öppnas och välj ikonen `Configure` som öppnar redigeringsdialogrutan.

![chlimage_1-14](assets/chlimage_1-14.png)

![chlimage_1-15](assets/chlimage_1-15.png)

### Fliken Inställningar {#settings-tab}

Under fliken **[!UICONTROL Settings]** identifierar du innehållet som ska visas:

* **[!UICONTROL Display Name]**

   Namnet på listan med aktuellt innehåll. Till exempel `Featured Questions` eller `Featured Ideas`. Standardvärdet är `Featured Content` om inget anges.

* **[!UICONTROL Location of the Featured Content]**

   *(Obligatoriskt)* Bläddra till sidan med det innehåll som kan vara funktionellt (komponenterna på den sidan måste konfigureras för att tillåta aktuellt innehåll). Till exempel, `/content/sites/engage/en/forum`.

* **[!UICONTROL Display Limit]**

   Det maximala antalet innehåll som kan visas. Standardvärdet är 5.

## Site Visitor Experience {#site-visitor-experience}

Möjligheten att flagga innehåll som aktuellt innehåll kräver moderatorbehörighet.

När en moderator visar publicerat innehåll har de tillgång till modereringsflaggorna som innehåller den nya flaggan `Feature`.

![chlimage_1-16](assets/chlimage_1-16.png)

När modellflaggan har flaggats som en funktion blir den `Unfeature`.

Sidan som innehåller komponenten `Featured Content` kommer nu att innehålla det här inlägget.

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` är en länk till själva inlägget.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Aktuellt innehåll](essentials-featured.md) för utvecklare.

Information om hur du flaggar innehåll finns i [Moderating User Generated Content](moderate-ugc.md).
