---
title: Gruppbearbetning
seo-title: Gruppbearbetning
description: 'null'
seo-description: 'null'
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Gruppbearbetning {#bulk-processing-operations}

## Introduktion {#introduction}

I den senaste versionen av AEM har knappen Markera alla utökats till att omfatta alla vyer: List-, kolumn- och kortvy. Knappen Markera alla markerar nu allt innehåll i en viss mapp eller samling och inte bara de resurser och sidor som är inlästa och synliga i klientens webbläsare.

Nyckelåtgärder har aktiverats för gruppåtgärden: **Flytta**, **ta bort** och **kopiera**. En ny dialogruta visar för kunderna vilka åtgärder som gruppbearbetning inte är tillgänglig för.

## Så här använder du {#how-to-use}

En ny knapp med namnet **Markera alla** har lagts till i vyerna Kort, Lista eller Kolumn. Den här knappen kan användas i alla vyer för att markera alla element i datauppsättningen.

I tidigare versioner av AEM var urvalet begränsat till vad som lästes in i klientwebbläsaren. De här nya ändringarna har införts för att undvika förvirring om hur många element en gruppåtgärd utförs på.

För närvarande har tre åtgärder lagts till i gruppbearbetning:

* Flytta
* Kopiera
* Ta bort

Stöd för fler åtgärder kommer att läggas till i framtiden.
Om du vill använda den här funktionen måste du navigera till den mapp eller samling där du vill utföra en gruppåtgärd på sidor eller på resurser.

Välj sedan en av vyerna enligt nedan:

### Kortvy {#card-view}

![](assets/unu.png)

### Massmarkering i kortvyn {#bulk-selection-in-card-view}

Resurser eller sidor kan markeras i grupp med knappen **Markera alla** överst till höger:

![](assets/doi.png) ![](assets/trei.png)

### Listvy {#list-view}

Samma sak gäller för listvyn:

![](assets/patru_modified.png)

### Massmarkering i listvyn {#bulk-selection-in-list-view}

Använd knappen **Markera alla** i listvyn eller använd kryssrutan till vänster för gruppval.

![](assets/cinci.png) ![](assets/sase.png)

### Kolumnvy {#column-view}

![](assets/sapte.png)

### Massmarkering i kolumnvyn {#bulk-selection-in-column-view}

![](assets/opt.png)

## Massaktiverade åtgärder {#bulk-enabled-operations}

Efter markeringen kan en av de tre massaktiverade åtgärderna utföras: **Flytta**, **Kopiera** eller **Ta bort**.

Här **utförs åtgärden Flytta** på de resurser som markerats ovan. I alla vyer resulterar detta i att alla resurser flyttas till den valda platsen och inte bara till de som läses in på skärmen.

![](assets/noua.png)

För andra åtgärder som inte är gruppaktiverade, **som** Hämta,visas en varning om att bara element som lästs in i webbläsaren kommer att inkluderas i åtgärden.

![](assets/zece.png)
