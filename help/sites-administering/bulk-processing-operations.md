---
title: Gruppbearbetning
description: null
page-status-flag: never-activated
contentOwner: sarchiz
docset: aem65
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Gruppbearbetning {#bulk-processing-operations}

## Introduktion {#introduction}

I den senaste versionen av Adobe Experience Manager (AEM) har knappen Markera allt utökats till att omfatta alla vyer: list-, kolumn- och kortvyn. Knappen Markera allt markerar nu allt innehåll i en viss mapp eller samling och inte bara Assets och Sidor som är inlästa och synliga i klientens webbläsare.

Nyckelåtgärder har aktiverats för gruppåtgärden: **Flytta**, **Ta bort** och **Kopiera**. En ny dialogruta låter kunderna veta vilka åtgärder som gruppbearbetning inte är tillgänglig för.

## Använda {#how-to-use}

En ny knapp med namnet **Markera allt** har lagts till i vyerna Kort, Lista eller Kolumn. Den här knappen kan användas i alla vyer för att markera alla element i datauppsättningen.

I tidigare versioner av AEM var urvalet begränsat till vad som lästes in i klientwebbläsaren. Den nya ändringen infördes för att undvika förvirring om hur många element en gruppåtgärd utförs på.

För närvarande har tre åtgärder lagts till i gruppbearbetning:

* Flytta
* Kopiera
* Ta bort

Stöd för fler åtgärder kommer att läggas till i framtiden.
Om du vill använda den här funktionen går du till den mapp eller samling där du vill utföra en gruppåtgärd på sidor eller i Assets.

Välj sedan en av vyerna enligt nedan:

### Kortvy {#card-view}

![Kortvyn med miniatyrbilder av olika bildresurser.](assets/unu.png)

### Massmarkering i kortvyn {#bulk-selection-in-card-view}

Assets eller Sidor kan markeras gruppvis med knappen **Markera alla** längst upp till höger:

![Markera alla-knappen som visas i det övre högra hörnet i kortvyn.](assets/doi.png) ![Alla miniatyrbilder av bildresurser i kortvyn visas som markerade med bockmarkeringar.](assets/trei.png)

### Listvy {#list-view}

Samma sak gäller för listvyn:

![Alternativet Markera alla i det övre högra hörnet i listvyn är markerat.](assets/patru_modified.png)

### Massmarkering i listvyn {#bulk-selection-in-list-view}

Använd knappen **Markera allt** eller kryssrutan till vänster för gruppval i listvyn.

![Live-vyn med miniatyrbilder av bildresurser visas i vågräta rader.](assets/cinci.png) ![Listruta med miniatyrbilder av bildresurser och en kryssruta till vänster om Namn.](assets/sase.png)

### Kolumnvy {#column-view}

![Kolumnvy med miniatyrbilder av bildresurser som visas i lodräta kolumner.](assets/sapte.png)

### Massmarkering i kolumnvyn {#bulk-selection-in-column-view}

![Alla miniatyrbilder av bildresurser i kolumnvyn visas som markerade med bockmarkeringar.](assets/opt.png)

## Massaktiverade åtgärder {#bulk-enabled-operations}

Efter markeringen kan en av de tre massaktiverade åtgärderna utföras: **Flytta**, **Kopiera** eller **Ta bort**.

Här utförs åtgärden **Flytta** på den Assets som valts ovan. I alla vyer innebär detta att alla Assets flyttas till den valda platsen och inte bara till de som läses in på skärmen.

![Flytta resurser som visar en vald mapp i kolumnvyn.](assets/noua.png)

För andra åtgärder som inte är massaktiverade, till exempel **Hämta**, visas en varning om att endast element som har lästs in i webbläsaren inkluderas i åtgärden.

![Assets-vy med markerade bildresurser och popup-dialogrutan &quot;Massåtgärd stöds inte&quot;.](assets/zece.png)
