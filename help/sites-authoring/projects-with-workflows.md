---
title: Arbeta med projektarbetsflöden
seo-title: Arbeta med projektarbetsflöden
description: Det finns en mängd olika projektarbetsflöden att välja mellan.
seo-description: Det finns en mängd olika projektarbetsflöden att välja mellan.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
translation-type: tm+mt
source-git-commit: 0033dfac2540f56b3903c19f6ca19677af050db3

---


# Arbeta med projektarbetsflöden{#working-with-project-workflows}

De projektarbetsflöden som är tillgängliga från paketet innehåller följande:

* **Arbetsflöde** för projektgodkännande - Med det här arbetsflödet kan du tilldela innehåll till en användare, granska och sedan godkänna.
* **Begär start** - Ett arbetsflöde som begär start.
* **Begär landningssida** - Den här arbetsflödet begär en landningssida.
* **Begär e-post** - arbetsflöde för att begära e-post.
* **Fotofoto och produktfoto (handel)** - Mappar resurser med produkter
* **DAM Skapa och översätt kopia och DAM Skapa språkkopia** - Skapar översatta binärfiler, metadata och taggar för resurser och mappar.

Beroende på vilken projektmall du väljer finns det vissa arbetsflöden:

|  | **Enkelt projekt** | **Medieprojekt** | **Fotoprojekt för produkt** | **Översättningsprojekt** |
|---|:-:|:-:|:-:|:-:|
| Begär kopia |  | x |  |  |
| Fotofotografering |  | x | x |  |
| Fotofoto (Commerce) |  |  | x |  |
| Projektgodkännande | x |  |  |  |
| Begär start | x |  |  |  |
| Begär landningssida | x |  |  |  |
| Begär e-post | x |  |  |  |
| DAM - skapa språkkopia&amp;ast; |  |  |  | x |
| DAM Skapa och översätt språkkopia&amp;ast; |  |  |  | x |

>[!NOTE]
>
> &amp;ast; Dessa arbetsflöden startas inte från **arbetsflödespanelen** i Projekt. Se [Skapa språkkopior för resurser.](/help/sites-administering/tc-manage.md)

Stegen för att starta och slutföra arbetsflöden är desamma oavsett vilket arbetsflöde du väljer. Bara stegen ändras.

Du startar ett arbetsflöde direkt i Projekt (förutom för DAM Create Language Copy eller DAM Create och Translate Language Copy). Information om väntande uppgifter i ett projekt finns i **aktivitetspanelen** . Meddelanden om uppgifter som behöver slutföras visas bredvid användarikonen.

Mer information om hur du arbetar med arbetsflöden i AEM finns i:

* [Delta i arbetsflöden](/help/sites-authoring/workflows-participating.md)
* [Tillämpa arbetsflöden på sidor](/help/sites-authoring/workflows-applying.md)
* [Konfigurera arbetsflöden](/help/sites-administering/workflows.md)

I det här avsnittet beskrivs de arbetsflöden som är tillgängliga för projekt.

## Arbetsflödet Begär kopia {#request-copy-workflow}

Med det här arbetsflödet kan du begära ett manuskript från en användare och sedan godkänna det. Så här startar du arbetsflödet för begärandekopia:

1. I ditt medieprojekt väljer du **+** -signeringen i rutan **Arbetsflöden** och väljer **Begär kopieringsarbetsflöde**.
1. Ange en titel och en kort sammanfattning av vad du begär. Ange ett målordsantal, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![chlimage_1-325](assets/chlimage_1-321.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Uppgiften visas på **aktivitetspanelen** .

   ![chlimage_1-322](assets/chlimage_1-322.png)

## Arbetsflöde för fotografering {#product-photo-shoot-workflow}

Arbetsflödena för produktfotografering (både handel och utan handel) beskrivs i detalj i [Creative Project](/help/sites-authoring/managing-product-information.md).

## Arbetsflöde för projektgodkännande {#project-approval-workflow}

I arbetsflödet för projektgodkännande tilldelar du innehåll till en användare, granskar och godkänner sedan innehållet.

1. I det enkla projektet väljer du **`+`** signering i rutan **Arbetsflöden** och väljer **Projektgodkännandearbetsflöde**.
1. Ange en titel och välj vem du vill tilldela den till i grupplistan. Ange en beskrivning, innehållssökväg, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![chlimage_1-323](assets/chlimage_1-323.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Uppgiften visas på **aktivitetspanelen** .

   ![chlimage_1-324](assets/chlimage_1-324.png)

## Arbetsflödet Begär start {#request-launch-workflow}

Med det här arbetsflödet kan du begära att programmet startas.

1. I ditt enkla projekt väljer du **+** -signeringen i rutan **Arbetsflöden** och väljer **Begär startarbetsflöde**.
1. Ange en rubrik för startprogrammet och ange startkällans sökväg. Du kan också lägga till en beskrivning och ett live-datum, om du vill. Välj Ärv källsidans livedata eller exkludera undersidor beroende på hur du vill att startsidan ska fungera.

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. Klicka på **Skapa**. Arbetsflödet startar. **Arbetsflödet visas i listan** Arbetsflöden **(klicka på ovaler**..). på panelen **Arbetsflöden** för att komma åt den här listan).

## Begär arbetsflöde för landningssida {#request-landing-page-workflow}

Med det här arbetsflödet kan du begära en landningssida.

1. I ditt enkla projekt väljer du **+** -signeringen i rutan **Arbetsflöden** och väljer Begär arbetsflöde för landningssida.
1. Ange en rubrik för landningssidan och den överordnade sökvägen. Ange eventuellt ett live-datum eller välj en fil för landningssidan.

   ![chlimage_1-326](assets/chlimage_1-326.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Uppgiften visas på **aktivitetspanelen** .

## Begär e-postarbetsflöde {#request-email-workflow}

Med det här arbetsflödet kan du begära ett e-postmeddelande. Det är samma arbetsflöde som visas i rutan **E-post** .

1. I ditt Media- eller Simple-projekt väljer du **+** -signeringen i rutan **Arbetsflöden** och väljer **Begär e-postarbetsflöde**.
1. Ange en e-posttitel samt kampanj- och mallsökvägar. Dessutom kan du ange namn, beskrivning och live-datum.

   ![chlimage_1-327](assets/chlimage_1-327.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Uppgiften visas på **aktivitetspanelen** .

   ![chlimage_1-328](assets/chlimage_1-328.png)

## Skapa (och översätt) språkkopieringsarbetsflöde för resurser {#create-and-translate-language-copy-workflow-for-assets}

Arbetsflödena **Skapa språkkopia** och **Skapa och översätt språkkopia** beskrivs närmare i [Skapa språkkopior för resurser.](/help/assets/translation-projects.md)
