---
title: Personalisering och målgruppsanpassning av innehåll
seo-title: Personalisering och målgruppsanpassning av innehåll
description: Lär dig hur AEM kan skapa personaliserat innehåll
seo-description: Lär dig hur AEM kan skapa personaliserat innehåll
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Personalisering och målanpassning av innehåll {#personalization}

## Personalisering och målanpassning av innehåll {#personalization-and-content-targeting}

AEM tillhandahåller ett ramverk med verktyg för att skapa riktat innehåll och presentera personaliserade upplevelser.

## Målläge {#targeting-mode}

[Skapa riktat ](/help/sites-authoring/content-targeting-touch.md) innehåll med målinriktningsläget AEM. Målinriktningsläget och Target-komponenten tillhandahåller verktyg för att skapa innehåll för upplevelserna av era marknadsföringsaktiviteter.

## Aktiviteter {#activities}

Verksamheter definierar och organiserar era era marknadsföringssatsningar. Verksamheterna omfattar de målgrupper som ni riktar in er på och den tidsperiod under vilken målgruppsanpassningen tillämpas.

Produktkatalogen We.Retail innehåller t.ex. lärare som fokuserar på säsongsprodukter. Sommarsportsaktiviteten definierar de marknadsföringssegment som lärarna siktar på under sommarmånaderna.

Aktiviteter identifierar också [målmotorn](/help/sites-authoring/personalization.md#targeting-engine) som dina sidor använder.

Använd [aktivitetskonsolen](/help/sites-authoring/activitylib.md) för att skapa och hantera aktiviteter för dina varumärken. Du kan också skapa aktiviteter när du [redigerar riktat innehåll](/help/sites-authoring/content-targeting-touch.md).

## Upplevelser {#experiences}

För varje aktivitet definierar ni en eller flera upplevelser som identifierar målgrupperna som ni riktar in er mot. AEM gör det möjligt att styra innehållet som omfattar varje upplevelse.

Målgrupperna bygger på marknadsföringssegment som skapats i AEM eller Adobe Target. När en besökare öppnar en webbsida avgör sidlogiken vilken målgrupp de tillhör och visar det innehåll som du har skapat för den målgruppen.

En aktivitet definierar till exempel upplevelser för två olika målgrupper: kvinnor över 30 år och kvinnor under 30 år. Kvinnors sida på webbplatsen We.Retail visar olika produkter för varje upplevelse.

Ni definierar upplevelser för en aktivitet. Du kan använda [aktivitetskonsolen](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) eller [Målläge](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) för att lägga till upplevelser i en aktivitet.

## Erbjudanden {#offers}

Ett erbjudande är innehåll som visas på en plats på en sida för en upplevelse. Använd olika erbjudanden för olika upplevelser för att maximera innehållets effektivitet för era målgrupper.

Exempel: Kvinnors sida på exempelwebbplatsen We.Retail kan använda erbjudanden som den suddgummibild som visas högst upp på sidan. Ett annat erbjudande används som teaser för upplevelsen kvinna över 30 och för kvinna under 30.

Använd [Erbjudandekonsolen](/help/sites-authoring/offerlib.md) för att skapa erbjudanden som du kan använda i flera olika upplevelser. Skapa engångserbjudanden eller lägg till erbjudanden från ett erbjudandebibliotek när [du skapar riktat innehåll](/help/sites-authoring/content-targeting-touch.md).

## Målmotor {#targeting-engine}

Målmotorn är den mekanism som driver logiken för riktat innehåll. [Aktiviteter ](/help/sites-authoring/activitylib.md) är konfigurerade att använda en av två målmotorer som är tillgängliga: AEM och Adobe Target.

### AEM {#aem}

AEM har en inbyggd motor för målinriktning som bearbetar sidförfrågningar och avgör vilket innehåll som ska visas. När ni använder den AEM målgruppsmotorn begränsas ni till att använda segment som skapas i AEM för att definiera målgrupperna för era upplevelser.

### Adobe Target {#adobe-target}

Adobe Target målgruppsmotor spårar information som samlats in från sidbesök i Adobe Target.

* När ni använder den här målgruppsmotorn använder ni de segment ni importerar från Adobe Target för att definiera målgrupperna för era upplevelser.
* Aktiviteter som använder Adobe Target-motorn är [synkroniserade med Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Du kan använda den här motorn när du har [integrerat med Adobe Target](/help/sites-administering/opt-in.md).
