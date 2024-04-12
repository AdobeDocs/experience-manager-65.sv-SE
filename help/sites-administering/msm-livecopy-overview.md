---
title: Översiktskonsol för Live Copy
description: Lär dig grunderna i Live Copy Overview Console.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Översiktskonsol för Live Copy{#live-copy-overview-console}

The **Live Copy - översikt** gör att du kan:

* Visa/hantera arv på en webbplats:

   * Visa det blå trädet och motsvarande Live-kopia-struktur, tillsammans med deras arvsstatus
   * Ändra arvsstatus, till exempel göra uppehåll, återuppta
   * Visa egenskaper för utkast och live-kopia

* Utför utrullningsåtgärder

## Öppna Live Copy-översikt {#opening-the-live-copy-overview}

Du kan öppna Live-kopieringsöversikt från:

* [Panelen Referenser till en översiktssida (Sites console)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Egenskaper för en ritningssida](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Öppna Live Copy-översikt - referenser för en designsida {#opening-live-copy-overview-references-for-a-blueprint-page}

The **Live Copy - översikt** kan öppnas från **Referenser** sidpanelen på **Webbplatser** konsol:

1. I **Webbplatser** konsol, [navigera till din ritningssida och markera den](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna **[Referenser](/help/sites-authoring/basic-handling.md#references)** panel och markera **Live-kopior**.

   ![Referenspanelen - Live-kopior](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >Du kan också öppna Referenser först och sedan välja en plan.

1. Välj **Live Copy - översikt** om du vill visa och använda översikten över alla live-kopior som hör till den valda planen.
1. Använd **Stäng** för att avsluta och återgå till **Webbplatser** konsol.

### Öppna Live Copy-översikt - egenskaper för en designsida {#opening-live-copy-overview-properties-of-a-blueprint-page}

The **Live Copy - översikt** kan öppnas när du visar egenskaper för en ritningssida:

1. Öppna **Egenskaper** för lämplig ritningssida.
1. Öppna **Blueprint** -fliken - **Live Copy - översikt** visas i det övre verktygsfältet:

   ![Fliken Utskrift - Live-kopia - översikt](assets/chlimage_1-360.png)

1. Välj **Live Copy - översikt** om du vill visa och använda översikten över alla live-kopior som hör till den aktuella planen.

   >[!NOTE]
   >
   >Mer information finns även i artikeln i kunskapsbasen [LiveCycle-statusmeddelande - uppdaterad/grön/synkroniserad](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. Använd **Stäng** för att avsluta och återgå till **Webbplatser** konsol.

## Använda Live Copy-översikt {#using-the-live-copy-overview}

The **Live Copy - översikt** kan även användas för att utföra åtgärder på live-kopian:

1. Öppna **Live Copy - översikt**.
1. Välj önskad skiss- eller Live copy-sida - verktygsfältet uppdateras för att visa tillgängliga åtgärder. The [funktionsmakron](/help/sites-administering/msm.md#terms-used) beroende på om du väljer en [skiss](#actions-for-a-blueprint-page) eller [live copy](#actions-for-a-live-copy-page) sida:

### Åtgärder för en designsida {#actions-for-a-blueprint-page}

När du väljer en ritningssida är följande åtgärder tillgängliga:

![Markerad skiss - tillgängliga åtgärder](assets/chlimage_1-361.png)

* Redigera

   * Öppna ritningssidan för redigering.

* [Utrullning](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Utför en utrullning för att föra över ändringar från källan till livecopy.

### Åtgärder för en Live Copy-sida {#actions-for-a-live-copy-page}

När du väljer en live-kopieringssida är följande åtgärder tillgängliga:

![Live copy page selected - actions available](assets/chlimage_1-362.png)

* Redigera

   * Öppna kopieringssidan för redigering.

* [Relationsstatus](#relationship-status)

   * Visa information om status och arv.

* [Synkronisera](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Synkronisera en live-kopia för att dra ändringar från källan till livecopy.

* [Återställ](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Återställ en live-kopieringssida om du vill ta bort alla arvsannulleringar och återställa sidan till samma läge som källsidan.

* [Gör uppehåll](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Inaktiverar tillfälligt relationen mellan en live-kopia och dess planeringssida.

* [Återuppta](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * Med Fortsätt kan du återskapa en pausad relation.

* [Koppla loss](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Tar permanent bort den aktiva relationen mellan en live-kopia och dess designsida.

## Relationsstatus {#relationship-status}

The **Relationsstatus** konsolen har två flikar med en rad funktioner:

* [Statusinformation för relation](#relationship-status-information)
* [Live Copy-information](#live-copy-information)

### Statusinformation för relation {#relationship-status-information}

På den här fliken finns detaljerad information om statusen för relationen mellan ritningen och den aktiva kopian:

![Statusinformation för relation](assets/chlimage_1-363.png)

### Live Copy-information {#live-copy-information}

På den här fliken kan du visa och redigera konfigurationen av live-kopian:

![Live copy-information](assets/chlimage_1-364.png)
