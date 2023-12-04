---
title: Synkroniserar appen
seo-title: Synchronizing the app
description: Synkronisera AEM Forms-appen på din mobila enhet med AEM Forms-servern.
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Synkroniserar appen{#synchronizing-the-app}

## Synkroniserar appen {#synchronizing-the-app-1}

Formulären i din app hämtas från AEM Forms-servern. Formulären hämtas på flikarna Åtgärder och Forms. Utkast som skapas från formulär hämtas på fliken Utkast och utkast som skapas från uppgifter hämtas på fliken Åtgärder. För ett fristående formulär på OSGi-server hämtas formulär och utkast på flikarna Forms respektive Draft.

När du fyller i och skickar ett formulär överförs formuläret direkt till AEM Forms-servern om appen är online. Formulären hämtas från servern när appen synkroniseras. Utkasten synkroniseras emellertid direkt med servern om appen är online.

När du är online med AEM Forms-servern synkroniseras ditt program som standard var 15:e minut. Du kan dock ändra synkroniseringsfrekvensen. Du kan också när som helst synkronisera appen manuellt.

**Synkronisera appen manuellt**

Markera knappen Synkronisera ![sync-app](assets/sync-app.png) längst ned till höger på startskärmen.

**Ändra synkroniseringsfrekvensen**

1. Om du vill gå till inställningsskärmen väljer du menyknappen längst upp till vänster på startskärmen och väljer sedan **Inställningar**.
1. Välj fliken Allmänt på skärmen Inställningar.

   ![Inställningen för synkroniseringsfrekvens i fönstret Allmänna inställningar](assets/gen-settings-2.png)

1. Välj värdet till höger om synkroniseringsfrekvensen i alternativet Synkroniseringsfrekvens.
1. Välj den nya synkroniseringsfrekvensen i listrutan.

### Tekniska specifikationer {#technical-specifications}

* Den viktigaste logiken för att skicka offlineappdata till AEM Forms-servern finns i runtime/offline/util/offline.js.
* I .js-filen skickar anropet till funktionen processOfflineSubmitSavedTasks(...) de sparade/skickade uppgifterna till servern. Den hanterar även fel och konflikter i synkroniseringsprocessen. Om överföringen av en uppgift misslyckas markeras aktiviteten i programmet som misslyckad. Dessutom finns uppgiften kvar i Utkorgen.
* Funktionerna syncSubowedTask() och syncSavedTask() utför åtgärder på enskilda uppgifter.
* Anropet till funktionen processOfflineSubmitSavedTasks() initieras av uppgiftslistkomponenten efter att en användare har valt att synkronisera offlineläget med servern eller en automatisk synkronisering av bakgrundstråden.
