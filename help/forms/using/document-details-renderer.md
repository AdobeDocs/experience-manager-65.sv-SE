---
title: Dokumentinformation för återgivning
seo-title: Document details for renderer
description: Konceptuell information om hur renderingar fungerar i AEM Forms arbetsyta för att återge de olika formulär och filtyper som stöds.
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Dokumentinformation för återgivning {#document-details-for-renderer}

## Introduktion {#introduction}

I AEM Forms-arbetsytan stöds flera formulärtyper sömlöst. Bland dessa finns:

* PDF forms (XDP/Acroform/platt PDF)
* Nya HTML-formulär
* Bilder
* Tredjepartsprogram (till exempel Korrespondenshantering)

I det här dokumentet förklaras hur dessa renderare fungerar när det gäller semantisk anpassning/återanvändning av komponenter, så att kundens krav uppfylls utan att renderingen bryts. Även om AEM Forms arbetsyta tillåter användargränssnitt/semantiska ändringar rekommenderar vi att återgivningslogiken för olika formulärtyper inte ändras, annars kan resultatet bli oförutsägbart. Det här dokumentet är avsett som vägledning/kunskap för att ge stöd för återgivning av samma formulär, med samma arbetsytekomponenter i olika portaler, och inte för att ändra själva återgivningslogiken.

## PDF forms {#pdf-forms}

PDF forms återges av `PdfTaskForm View`.

När ett XDP-formulär återges som PDF, `FormBridge` JavaScript™ läggs till av tjänsten FormsAugmenter. Denna JavaScript™ (i PDF) hjälper dig att utföra åtgärder som att skicka formulär, spara formulär eller ta formulär offline.

I AEM Forms-arbetsytan kommunicerar PDFTaskForm-vyn med `FormBridge`javascript, via en mellanhand HTML närvarande `/lc/libs/ws/libs/ws/pdf.html`. Flödet är:

**PDFTaskForm view - pdf.html**

kommunicerar med `window.postMessage` / `window.attachEvent('message')`

Den här metoden är standardmetoden för kommunikation mellan en överordnad bildruta och en iframe. De befintliga händelseavlyssnarna från tidigare öppnade PDF forms tas bort innan en ny läggs till. Denna rensning tar även hänsyn till växlingen mellan fliken Formulär och fliken Historik i vyn med aktivitetsinformation.

**pdf.html - `FormBridge`javascript inuti den renderade PDF**

kommunicerar med `pdfObject.postMessage` / `pdfObject.messageHandler`

Den här metoden är standardmetoden för kommunikation med ett PDFJavaScript från en HTML. PdfTaskForm-vyn hanterar även PDF som platt och återger den tydligt.

>[!NOTE]
>
>Du bör inte ändra pdf.html / innehållet i PDF-vyn TaskForm.

## New HTML Forms {#new-html-forms}

Nya HTML-formulär återges i vyn NewHTMLTaskForm.

När ett XDP-formulär återges som HTML med det mobila formulärpaketet som distribueras på CRX, läggs även ytterligare `FormBridge`JavaScript i formuläret, som visar olika metoder för att spara och skicka formulärdata.

Detta JavaScript skiljer sig från det som anges i PDF forms ovan, men har ett liknande syfte.

>[!NOTE]
>
>Du bör inte ändra innehållet i vyn NewHTMLTaskForm.

## Flex Forms och stödlinjer {#flex-forms-and-guides}

Flex Forms återges av SWFTaskForm och stödlinjer återges av HTMLTaskForm-vyer.

I AEM Forms-arbetsytan kommunicerar dessa vyer med det aktuella SWF som utgör Flex-formuläret/-guiden med hjälp av en mellanhand som är SWF i `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

Kommunikationen sker med `swfObject.postMessage` / `window.flexMessageHandler`.

Detta protokoll definieras av `WsNextAdapter.swf`. Befintliga `flexMessageHandlers`i fönsterobjekt tas tidigare öppnade SWF-formulär bort innan ett nytt läggs till. Logiken tar också hänsyn till växlingen mellan fliken Formulär och fliken Historik i vyn med uppgiftsdetaljer. `WsNextAdapter.swf` används för att utföra olika formuläråtgärder som att spara eller skicka.

>[!NOTE]
>
>Du bör inte ändra `WSNextAdapter.swf` eller innehållet i vyn SwfTaskForm/HtmlTaskForm.

## Tredjepartsprogram (till exempel Korrespondenshantering) {#third-party-applications-for-example-correspondence-management}

Tredjepartsprogram återges med vyn ExtAppTaskForm.

**Tredjepartsprogram för AEM Forms arbetsytekommunikation**

AEM Forms arbetsyta lyssnar på `window.global.postMessage([Message],[Payload])`

[Meddelande] kan vara en sträng som anges som `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`i `runtimeMap`. Tredjepartsprogram måste använda det här gränssnittet för att meddela AEM Forms-arbetsytan efter behov. Det är obligatoriskt att använda det här gränssnittet eftersom AEM Forms-arbetsytan måste känna till att när uppgiften skickas så att den kan rensa upp aktivitetsfönstret.

**AEM Forms arbetsyta till kommunikation med program från tredje part**

Om direktåtgärdsknapparna för AEM Forms-arbetsytan visas anropas `window.[External-App-Name].getMessage([Action])`, där `[Action]` läses från `routeActionMap`. Tredjepartsprogrammet måste lyssna på det här gränssnittet och sedan meddela AEM Forms via `postMessage ()` API.

Ett Flex-program kan till exempel definiera `ExternalInterface.addCallback('getMessage', listener)` för att stödja denna kommunikation. Om tredjepartsprogrammet vill hantera formulärskickning med sina egna knappar, bör du ange `hideDirectActions = true() in the runtimeMap` och du kan hoppa över den här avlyssnaren. Denna konstruktion är alltså valfri.

Du kan läsa mer om integrering av tredjepartsprogram med avseende på Correspondence Management på [Integrera korrespondenshantering i AEM Forms arbetsyta](/help/forms/using/integrating-correspondence-management-html-workspace.md).
