---
title: Använda Länk
description: Lär dig hur du lägger till och konfigurerar komponenten Länka så att användare kan uttrycka en åsikt om ett visst innehåll, till exempel en kommentar.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Använda Länk {#using-liking}

The `Liking` -komponenten är ett användbart verktyg som gör att användare kan uttrycka sin åsikt om en viss del av innehållet, till exempel en kommentar i ett forum. Med `Liking` -komponenten väljer medlemmarna hjärtikonen för att ange en positiv åsikt.

## Lägga till länkning på en sida {#adding-liking-to-a-page}

Lägga till en `Liking` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Liking`

Och dra den till rätt plats på en sida, till exempel i förhållande till funktionen som användarna kan gilla.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](essentials-liking.md#essentials-for-client-side) ingår så här `Liking` visas.

![liking-component](assets/liking-component.png)

## Konfigurerar länk {#configuring-liking}

Markera den monterade `Liking` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

Under **[!UICONTROL Texts & Labels]** anger du de egenskaper som används för att spela in gilla-markeringar.

![configure-läning](assets/configure-liking.png)

* **[!UICONTROL Positive Response Label]**

  (*Obligatoriskt*) Egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Negative Response Label]**

  (*Obligatoriskt*) Egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Tally Name]**

  (*Obligatoriskt*) Det interna, identifierbara egenskapsnamnet för den här instansen av en röstkomponent.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Medlemmar kan när som helst ändra sina gilla-markeringar.

### Anonym {#anonymous}

Anonym länkning stöds inte. Besökare på webbplatsen måste registrera sig (bli medlem) och logga in för att kunna vara med.

## Ytterligare information {#additional-information}

Mer information finns på [Länka viktiga](essentials-liking.md) för utvecklare.
