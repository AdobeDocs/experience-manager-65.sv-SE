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

Komponenten `Liking` är ett användbart verktyg som gör att användare kan uttrycka sin åsikt om ett visst innehåll, till exempel en kommentar i ett forum. Med komponenten `Liking` väljer medlemmarna hjärtikonen för att ange en positiv åsikt.

## Lägga till länkning på en sida {#adding-liking-to-a-page}

Om du vill lägga till en `Liking`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Liking`

Och dra den till rätt plats på en sida, till exempel i förhållande till funktionen som användarna kan gilla.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-liking.md#essentials-for-client-side) inkluderas visas `Liking`-komponenten på det här sättet.

![gillar-komponent](assets/liking-component.png)

## Konfigurerar länk {#configuring-liking}

Markera den monterade `Liking`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

Ange de egenskaper som ska användas för att spela in gilla-markeringar på fliken **[!UICONTROL Texts & Labels]**.

![configure-linking](assets/configure-liking.png)

* **[!UICONTROL Positive Response Label]**

  (*Obligatoriskt*) Egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Negative Response Label]**

  (*Obligatoriskt*) Egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Tally Name]**

  (*Obligatorisk*) Det interna, identifierbara egenskapsnamnet för den här instansen av en röstningskomponent.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Medlemmar kan när som helst ändra sina gilla-markeringar.

### Anonym {#anonymous}

Anonym länkning stöds inte. Besökare på webbplatsen måste registrera sig (bli medlem) och logga in för att kunna vara med.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Liking Essentials](essentials-liking.md) för utvecklare.
