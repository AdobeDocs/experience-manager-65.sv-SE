---
title: Arbeta med projektarbetsflöden
seo-title: Working with Project Workflows
description: Det finns en mängd olika projektarbetsflöden att välja mellan.
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---


# Arbeta med projektarbetsflöden {#working-with-project-workflows}

De projektarbetsflöden som är tillgängliga från paketet innehåller följande:

* **Arbetsflöde för projektgodkännande** - Med det här arbetsflödet kan du tilldela innehåll till en användare, granska och sedan godkänna.
* **Begär start** - Ett arbetsflöde som begär en start.
* **Begär landningssida** - Det här arbetsflödet begär en landningssida.
* **Begär e-post** - Arbetsflöde för att begära e-post.
* **Fotofotografering och fotografering av produkter (handel)** - Mappar resurser med produkter
* **DAM Skapa och översätt kopia och DAM Skapa språkkopia** - Skapar översatta binärfiler, metadata och taggar för resurser och mappar.

Beroende på vilken projektmall du väljer finns det vissa arbetsflöden:

|   | **Enkelt projekt** | **Medieprojekt** | **Fotoprojekt för produkt** | **Översättningsprojekt** |
|---|:-:|:-:|:-:|:-:|
| Begär kopia |  | x |  |  |
| Fotofotografering |  | x | x |  |
| Fotofoto (Commerce) |  |  | x |  |
| Projektgodkännande | x |  |  |  |
| Begär start | x |  |  |  |
| Begär landningssida | x |  |  |  |
| Begär e-post | x |  |  |  |
| DAM - skapa &amp;språkkopia; |  |  |  | x |
| DAM Skapa och översätt &amp;språkkopia; |  |  |  | x |

>[!NOTE]
>
>&amp;ast; dessa arbetsflöden startas inte från **Arbetsflöde** sida vid sida i projekt. Se [Skapa språkkopior för resurser.](/help/sites-administering/tc-manage.md)

Stegen för att starta och slutföra arbetsflöden är desamma oavsett vilket arbetsflöde du väljer. Bara stegen ändras.

Du startar ett arbetsflöde direkt i Projekt (förutom för DAM Create Language Copy eller DAM Create och Translate Language Copy). Information om utestående uppgifter i ett projekt finns i **Uppgifter** platta. Meddelanden om uppgifter som behöver slutföras visas bredvid användarikonen.

Mer information om hur du arbetar med arbetsflöden i AEM finns i följande dokument:

* [Delta i arbetsflöden](/help/sites-authoring/workflows-participating.md)
* [Tillämpa arbetsflöden på sidor](/help/sites-authoring/workflows-applying.md)
* [Konfigurera arbetsflöden](/help/sites-administering/workflows.md)

I det här avsnittet beskrivs de arbetsflöden som är tillgängliga för projekt.

## Begär kopieringsarbetsflöde {#request-copy-workflow}

Med det här arbetsflödet kan du begära ett manuskript från en användare och sedan godkänna det. Så här startar du arbetsflödet för begärandekopia:

1. I ett medieprojekt trycker eller klickar du på nedåtpilen längst upp till höger på **Arbetsflöden** sida vid sida och markera **Starta arbetsflöde**.
1. Välj **Begär kopia** och klicka **Nästa**.
1. Ange ett manuskriptnamn och en kort sammanfattning av vad du begär. Ange ett målordsantal, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![Arbetsflödet Begär kopia](assets/project-request-copy-workflow.png)

1. Klicka **Skicka**.

Arbetsflödet startar. Uppgiften visas på **Uppgifter** kort.

## Arbetsflöde för fotografering {#product-photo-shoot-workflow}

The **Fotofotografering** arbetsflöden (både handel och utan handel) beskrivs i detalj i dokumentet [Kreativa projekt](/help/sites-authoring/managing-product-information.md)

## Arbetsflöde för projektgodkännande {#project-approval-workflow}

I **Projektgodkännande** arbetsflöde kan du tilldela innehåll till en användare, granska och sedan godkänna innehållet.

1. I ett enkelt projekt: tryck eller klicka på nedåtpilen längst upp till höger i **Arbetsflöden** sida vid sida och markera **Starta arbetsflöde**.
1. Välj **Arbetsflöde för projektgodkännande** och klicka **Nästa**.
1. Ange en titel och välj vem du vill tilldela den till. Ange en beskrivning, innehållssökväg, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![Arbetsflöde för projektgodkännande](assets/project-approval-workflow.png)

1. Klicka **Skicka**.

Arbetsflödet startar. Uppgiften visas på **Uppgifter** kort.

## Begär startarbetsflöde {#request-launch-workflow}

Med det här arbetsflödet kan du begära en start.

1. I ett enkelt projekt: tryck eller klicka på nedåtpilen längst upp till höger i **Arbetsflöden** sida vid sida och markera **Starta arbetsflöde**.
1. Välj **Begär startarbetsflöde** och klicka **Nästa**.
1. Ange en rubrik för startprogrammet och ange startkällans sökväg. Du kan också lägga till en beskrivning och ett live-datum, om du vill. Välj Ärv källsidans livedata eller exkludera undersidor beroende på hur du vill att startsidan ska fungera.

   ![Begär startarbetsflöde](assets/project-request-launch-workflow.png)

1. Klicka **Skicka**.

Arbetsflödet startar. Arbetsflödet visas i **Arbetsflöden** lista.

## Begär arbetsflöde för landningssida {#request-landing-page-workflow}

Med det här arbetsflödet kan du begära en landningssida.

1. I ett enkelt projekt: tryck eller klicka på nedåtpilen längst upp till höger i **Arbetsflöden** sida vid sida och markera **Starta arbetsflöde**.
1. Välj **Begär landningssida** och klicka **Nästa**.
1. Ange en rubrik för landningssidan och den överordnade sökvägen. Ange eventuellt ett live-datum eller välj en fil för landningssidan.

   ![Begär arbetsflöde för landningssida](assets/project-request-landing-page-workflow.png)

1. Klicka **Skicka**.

Arbetsflödet startar. Uppgiften visas på **Uppgifter** kort.

## Begär e-postarbetsflöde {#request-email-workflow}

Med det här arbetsflödet kan du begära ett e-postmeddelande. Det är samma arbetsflöde som visas i **E-post** platta.

1. I ett enkelt projekt: tryck eller klicka på nedåtpilen längst upp till höger i **Arbetsflöden** sida vid sida och markera **Starta arbetsflöde**.
1. Välj **Begär e-post** och klicka **Nästa**.
1. Ange en e-posttitel samt kampanj- och mallsökvägar. Dessutom kan du ange namn, beskrivning och live-datum.

   ![Begär e-postarbetsflöde](assets/project-request-email-workflow.png)

1. Klicka **Skicka**.

Arbetsflödet startar. Uppgiften visas på **Uppgifter** kort.

## Skapa (och översätt) språkkopieringsarbetsflöde för resurser {#create-and-translate-language-copy-workflow-for-assets}

The **Skapa språkkopia** och **Skapa och översätta språkkopia** arbetsflöden beskrivs i detalj i dokumentet [Skapa språkkopior för resurser.](/help/assets/translation-projects.md)
