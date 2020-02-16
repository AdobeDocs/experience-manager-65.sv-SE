---
title: Konfigurerar omdirigeringssida
seo-title: Konfigurerar omdirigeringssida
description: När du har fyllt i ett anpassat formulär kan användarna omdirigeras till en webbsida som formulärförfattarna kan konfigurera när de skapar formuläret.
seo-description: När du har fyllt i ett anpassat formulär kan användarna omdirigeras till en webbsida som formulärförfattarna kan konfigurera när de skapar formuläret.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Konfigurerar omdirigeringssida{#configuring-redirect-page}

Formulärförfattare kan konfigurera en sida för varje formulär som formuläranvändarna omdirigeras till efter att de har skickat in formuläret.

1. Markera en komponent i redigeringsläget, klicka på ![fältnivå](assets/field-level.png) > **Adaptiv formulärbehållare** och klicka sedan på ![cmpr](assets/cmppr.png).

1. Klicka på **Skicka** i sidlisten.

1. Ange URL-adressen till omdirigeringssidan under Tack-sidan i avsnittet Skicka.
1. Under Skicka-åtgärd kan du som alternativ konfigurera parametern som ska skickas till omdirigeringssidan för slutpunktsåtgärden Skicka till REST.

![Omdirigeringssidkonfiguration](assets/thank-you-setting-1.png)

Omdirigeringssidkonfiguration

Formulärförfattare kan använda följande parametrar som skickas till sidan Tack. Alla tillgängliga skicka-åtgärder `status` och - `owner` parametrar skickas. Förutom dessa två parametrar skickas ytterligare några parametrar för följande skicka-åtgärder:

* **Åtgärden** Lagra innehåll (borttagen): `contentPath`- sökvägen till noden i databasen där skickade data lagras - skickas.

* **Åtgärden** Lagra PDF (borttagen): `contentPath`- av skickade data och sökvägen till noden som lagrar PDF-filen i databasen - skickas.

* **Arbetsflödet** Skicka till formulär: Utdataparametrar som returneras från formulärarbetsflöden skickas.

* **Skicka till REST-slutpunkt**: Parametrar som lagts till för mappning mellan fältparametrar skickas. `status` och `owner` parametrar skickas inte i den här skicka-åtgärden. Mer information finns i [Konfigurera Skicka till REST-slutpunktsåtgärden](../../forms/using/configuring-submit-actions.md).

