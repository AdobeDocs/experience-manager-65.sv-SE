---
title: Använda Länk
seo-title: Använda Länk
description: Lägga till och konfigurera komponenten Länka
seo-description: Lägga till och konfigurera komponenten Länka
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# Använda Länk {#using-liking}

Komponenten är ett användbart verktyg som gör att användare kan uttrycka sin åsikt om ett visst innehåll, till exempel en kommentar i ett forum. `Liking` Med den här `Liking` komponenten väljer medlemmarna hjärtikonen för att visa en positiv åsikt.

## Lägga till länkning på en sida {#adding-liking-to-a-page}

Om du vill lägga till en `Liking` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på:

* `Communities / Liking`

och dra den till rätt plats på en sida, t.ex. i förhållande till funktionen som användarna kan gilla.

Mer information finns i Grunderna för [communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-liking.md#essentials-for-client-side) inkluderas visas `Liking` komponenten på det här sättet.

![chlimage_1-93](assets/chlimage_1-93.png)

## Konfigurerar länk {#configuring-liking}

Markera den monterade `Liking` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-94](assets/chlimage_1-94.png)

Under fliken **[!UICONTROL Texter och etiketter]** anger du vilka egenskaper som ska användas för att spela in gilla-markeringar.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL Etikett för positivt svar]**

   (*Obligatoriskt*) Egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Etikett för negativt svar]**

   (*Obligatoriskt*) Egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Namn]**

   (*Obligatoriskt*) Det interna, identifierbara egenskapsnamnet för den här instansen av en röstkomponent.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Medlemmarna kan när som helst ändra sig.

### Anonym {#anonymous}

Anonym länkning stöds inte. Besökare på webbplatsen måste registrera sig (bli medlem) och logga in för att kunna vara med.

## Additional Information {#additional-information}

Mer information finns på [sidan Liking Essentials](essentials-liking.md) för utvecklare.
