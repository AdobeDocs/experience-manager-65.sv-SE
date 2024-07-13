---
title: Målgruppsinriktning för Personalization och innehåll
description: Läs om hur Adobe Experience Manager 6.5 kan skapa personaliserat innehåll.
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Målgruppsinriktning för Personalization och innehåll {#personalization}

## Målgruppsinriktning för Personalization och innehåll {#personalization-and-content-targeting}

AEM tillhandahåller ett ramverk med verktyg för att skapa riktat innehåll och presentera personaliserade upplevelser.

## Målläge {#targeting-mode}

[Skapa riktat innehåll](/help/sites-authoring/content-targeting-touch.md) med målläget AEM. Målinriktningsläget och Target-komponenten tillhandahåller verktyg för att skapa innehåll för upplevelserna av era marknadsföringsaktiviteter.

## Verksamhet {#activities}

Verksamheter definierar och organiserar era era marknadsföringssatsningar. Verksamheterna omfattar de målgrupper som ni riktar in er på och den tidsperiod under vilken målgruppsanpassningen tillämpas.

Produktkatalogen We.Retail innehåller t.ex. lärare som fokuserar på säsongsprodukter. Sommarsportsaktiviteten definierar de marknadsföringssegment som lärarna siktar på under sommarmånaderna.

Aktiviteter identifierar även den [målmotor](/help/sites-authoring/personalization.md#targeting-engine) som dina sidor använder.

Använd [aktivitetskonsolen](/help/sites-authoring/activitylib.md) för att skapa och hantera aktiviteter för dina varumärken. Du kan också skapa aktiviteter när du [skapar riktat innehåll](/help/sites-authoring/content-targeting-touch.md).

## Erfarenheter {#experiences}

För varje aktivitet definierar ni en eller flera upplevelser som identifierar målgrupperna som ni riktar in er mot. AEM gör det möjligt att styra innehållet som omfattar varje upplevelse.

Målgrupperna bygger på marknadsföringssegment som skapats i AEM eller Adobe Target. När en besökare öppnar en webbsida avgör sidlogiken vilken målgrupp de tillhör och visar det innehåll som du har skapat för den målgruppen.

En aktivitet definierar till exempel upplevelser för två olika målgrupper: kvinnor över 30 år och kvinnor under 30 år. Kvinnors sida på webbplatsen We.Retail visar olika produkter för varje upplevelse.

Ni definierar upplevelser för en aktivitet. Du kan använda [aktivitetskonsolen](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) eller [målläge](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) för att lägga till upplevelser i en aktivitet.

## Erbjudanden {#offers}

Ett erbjudande är innehåll som visas på en plats på en sida för en upplevelse. Använd olika erbjudanden för olika upplevelser för att maximera innehållets effektivitet för era målgrupper.

Exempel: Kvinnors sida på exempelwebbplatsen We.Retail kan använda erbjudanden som den suddgummibild som visas högst upp på sidan. Ett annat erbjudande används som teaser för upplevelsen kvinna över 30 och för kvinna under 30.

Använd konsolen [Erbjudanden](/help/sites-authoring/offerlib.md) för att skapa erbjudanden som du kan använda i flera olika upplevelser. Skapa engångserbjudanden eller lägg till erbjudanden från ett erbjudandebibliotek när [du redigerar målinriktat innehåll](/help/sites-authoring/content-targeting-touch.md).

## Målmotor {#targeting-engine}

Målmotorn är den mekanism som driver logiken för riktat innehåll. [Aktiviteter](/help/sites-authoring/activitylib.md) är konfigurerade att använda en av två målmotorer som är tillgängliga: AEM och Adobe Target.

### AEM {#aem}

AEM har en inbyggd motor för målinriktning som bearbetar sidförfrågningar och avgör vilket innehåll som ska visas. När ni använder den AEM målgruppsmotorn begränsas ni till att använda segment som skapas i AEM för att definiera målgrupperna för era upplevelser.

### Adobe Target {#adobe-target}

Adobe Target målgruppsmotor spårar information som samlats in från sidbesök i Adobe Target.

* När ni använder den här målgruppsmotorn använder ni de segment ni importerar från Adobe Target för att definiera målgrupperna för era upplevelser.
* Aktiviteter som använder Adobe Target-motorn är [synkroniserade med mål](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Du kan använda den här motorn när du har [integrerat med Adobe Target](/help/sites-administering/opt-in.md).
