---
title: Konfigurerar omdirigeringssida
seo-title: Configuring redirect page
description: När du har fyllt i ett anpassat formulär kan användarna omdirigeras till en webbsida som formulärförfattarna kan konfigurera när de skapar formuläret.
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Konfigurerar omdirigeringssida{#configuring-redirect-page}

Formulärförfattare kan konfigurera en sida för varje formulär som formuläranvändarna omdirigeras till efter att de har skickat in formuläret.

1. Markera en komponent i redigeringsläget och klicka sedan på ![fältnivå](assets/field-level.png) > **Adaptiv formulärbehållare** och klicka sedan på ![cmppr](assets/cmppr.png).

1. Klicka på **Inlämning**.

1. Ange URL-adressen till omdirigeringssidan under Tack-sidan i avsnittet Skicka.
1. Under Skicka-åtgärd kan du som alternativ konfigurera parametern som ska skickas till omdirigeringssidan för slutpunktsåtgärden Skicka till REST.

![Omdirigeringssidkonfiguration](assets/thank-you-setting-1.png)

Omdirigeringssidkonfiguration

Formulärförfattare kan använda följande parametrar som skickas till sidan Tack. För alla tillgängliga inskickningsåtgärder: `status` och `owner` parametrar skickas. Förutom dessa två parametrar skickas ytterligare några parametrar för följande skicka-åtgärder:

* **Åtgärden Lagra innehåll** (utgått): `contentPath`- sökvägen till noden i databasen där skickade data lagras skickas.

* **Åtgärden Lagra PDF** (utgått): `contentPath`- av skickade data och sökvägen till noden som lagrar PDF-filen i databasen - skickas.

* **Skicka till Forms-arbetsflöde**: Utdataparametrar som returneras från formulärarbetsflöden skickas.

* **Skicka till REST-slutpunkt**: Parametrar som lagts till för mappning mellan fältparametrar skickas. `status` och `owner` parametrar skickas inte i den här skicka-åtgärden. Mer information finns i [Konfigurera åtgärden Skicka till REST-slutpunkt](../../forms/using/configuring-submit-actions.md).
