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
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Använda Länk {#using-liking}

Komponenten är ett användbart verktyg som gör att användare kan uttrycka sin åsikt om ett visst innehåll, till exempel en kommentar i ett forum. `Liking` Med den här `Liking` komponenten väljer medlemmarna hjärtikonen för att visa en positiv åsikt.

## Lägga till länkning på en sida {#adding-liking-to-a-page}

Om du vill lägga till en `Liking` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på

* `Communities / Liking`

och dra den till rätt plats på en sida, t.ex. i förhållande till funktionen som användarna kan gilla.

Mer information finns i Grunderna för [communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-liking.md#essentials-for-client-side) inkluderas visas `Liking` komponenten på det här sättet.

![liking-component](assets/liking-component.png)

## Konfigurerar länk {#configuring-liking}

Markera den monterade `Liking` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

Ange de egenskaper som ska användas för att spela in gilla-markeringar på fliken **[!UICONTROL Texts & Labels]** .

![configure-läning](assets/configure-liking.png)

* **[!UICONTROL Positive Response Label]**

   (*Obligatoriskt*) Egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Negative Response Label]**

   (*Obligatoriskt*) Egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Tally Name]**

   (*Obligatoriskt*) Det interna, identifierbara egenskapsnamnet för den här instansen av en röstkomponent.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Medlemmarna kan när som helst ändra sig.

### Anonym {#anonymous}

Anonym länkning stöds inte. Besökare på webbplatsen måste registrera sig (bli medlem) och logga in för att kunna vara med.

## Additional Information {#additional-information}

Mer information finns på [sidan Liking Essentials](essentials-liking.md) för utvecklare.
