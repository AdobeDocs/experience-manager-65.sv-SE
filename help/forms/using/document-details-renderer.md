---
title: Dokumentinformation för återgivning
seo-title: Dokumentinformation för återgivning
description: Konceptuell information om hur renderingar fungerar på arbetsytan i AEM Forms för att återge de olika formulär och filtyper som stöds.
seo-description: Konceptuell information om hur renderingar fungerar på arbetsytan i AEM Forms för att återge de olika formulär och filtyper som stöds.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Dokumentinformation för återgivning {#document-details-for-renderer}

## Introduktion {#introduction}

På arbetsytan i AEM Forms stöds flera formulärtyper sömlöst. Bland dessa finns:

* PDF forms (XDP/Acroform/platta PDF-filer)
* Nya HTML-formulär
* Bilder
* Tredjepartsprogram (till exempel Korrespondenshantering)

I det här dokumentet förklaras hur dessa renderare fungerar när det gäller semantisk anpassning/återanvändning av komponenter, så att kundens krav uppfylls utan att renderingen bryts. Även om arbetsytan i AEM Forms tillåter användargränssnitt/semantiska ändringar rekommenderar vi att återgivningslogiken för olika formulärtyper inte ändras, annars kan resultatet bli oförutsägbart. Det här dokumentet är avsett som vägledning/kunskap för att ge stöd för återgivning av samma formulär, med samma arbetsytekomponenter i olika portaler, och inte för att ändra själva återgivningslogiken.

## PDF forms {#pdf-forms}

PDF forms återges av `PdfTaskForm View`.

När ett XDP-formulär återges som PDF läggs ett `FormBridge` JavaScript™ till av tjänsten FormsAugmenter. Denna JavaScript™ (i PDF-formuläret) hjälper dig att utföra åtgärder som att skicka formulär, spara formulär eller ta formulär offline.

I arbetsytan AEM Forms kommunicerar PDFTaskForm-vyn med `FormBridge`javascript, via en mellanliggande HTML-kod som finns på `/lc/libs/ws/libs/ws/pdf.html`. Flödet är:

**PDFTaskForm view - pdf.html**

Kommunicerar med `window.postMessage` / `window.attachEvent('message')`

Den här metoden är standardmetoden för kommunikation mellan en överordnad bildruta och en iframe. De befintliga händelseavlyssnarna från tidigare öppnade PDF forms tas bort innan en ny läggs till. Denna rensning tar även hänsyn till växlingen mellan fliken Formulär och fliken Historik i vyn med aktivitetsinformation.

**pdf.html -`FormBridge`javascript inuti den återgivna PDF-filen**

Kommunicerar med `pdfObject.postMessage` / `pdfObject.messageHandler`

Den här metoden är standardmetoden för kommunikation med ett PDFJavaScript från en HTML-kod. Vyn PdfTaskForm hanterar också platta PDF-filer och återger dem enkelt.

>[!NOTE]
>
>Du bör inte ändra pdf.html / innehållet i PDF-vyn TaskForm.

## Nya HTML-formulär {#new-html-forms}

Nya HTML-formulär återges i vyn NewHTMLTaskForm.

När ett XDP-formulär återges som HTML med det mobila formulärpaketet som distribueras på CRX, läggs även ytterligare `FormBridge`JavaScript till i formuläret, som visar olika metoder för att spara och skicka formulärdata.

Detta JavaScript skiljer sig från det som anges i PDF forms ovan, men har ett liknande syfte.

>[!NOTE]
>
>Du bör inte ändra innehållet i vyn NewHTMLTaskForm.

## Flex-formulär och -guider {#flex-forms-and-guides}

Flex-formulär återges av SWfTaskForm och stödlinjer återges av HTMLTaskForm-vyer.

På arbetsytan i AEM Forms kommunicerar dessa vyer med den faktiska SWF-filen som utgör Flex-formuläret/stödlinjen med hjälp av en mellanliggande SWF-fil som finns på `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

Kommunikationen sker med `swfObject.postMessage` / `window.flexMessageHandler`.

Detta protokoll definieras av `WsNextAdapter.swf`. Det befintliga `flexMessageHandlers`fönsterobjektet, från tidigare öppnade SWF-formulär, tas bort innan ett nytt läggs till. Logiken tar också hänsyn till växlingen mellan fliken Formulär och fliken Historik i vyn med uppgiftsdetaljer. `WsNextAdapter.swf` används för att utföra olika formuläråtgärder som att spara eller skicka.

>[!NOTE]
>
>Vi rekommenderar inte att du ändrar `WSNextAdapter.swf` eller ändrar innehållet i vyn SwfTaskForm / HtmlTaskForm.

## Tredjepartsprogram (till exempel Korrespondenshantering) {#third-party-applications-for-example-correspondence-management}

Tredjepartsprogram återges med vyn ExtAppTaskForm.

**Tredjepartsprogram för AEM Forms arbetsytekommunikation**

Arbetsytan i AEM Forms lyssnar på `window.global.postMessage([Message],[Payload])`

[Meddelande] kan vara en sträng som anges som `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`i `runtimeMap`. Tredjepartsprogram måste använda det här gränssnittet för att meddela AEM Forms arbetsytan efter behov. Det är obligatoriskt att använda det här gränssnittet eftersom arbetsytan i AEM Forms måste veta att när uppgiften skickas så att den kan rensa upp aktivitetsfönstret.

**AEM Forms arbetsyta till kommunikation med program från tredje part**

Om direktåtgärdsknapparna för arbetsytan i AEM Forms är synliga anropas `window.[External-App-Name].getMessage([Action])`där [ `Action]` läses från `routeActionMap`. Tredjepartsprogrammet måste lyssna på det här gränssnittet och sedan meddela AEM Forms via `postMessage ()` API.

En Flex-applikation kan till exempel definiera `ExternalInterface.addCallback('getMessage', listener)` som stöd för den här kommunikationen. Om tredjepartsprogrammet vill hantera formulärskickning med sina egna knappar, bör du ange `hideDirectActions = true() in the runtimeMap` och du kan hoppa över den här avlyssnaren. Denna konstruktion är alltså valfri.

Du kan läsa mer om integrering av tredjepartsprogram med avseende på Correspondence Management på arbetsytan [Integrating Correspondence Management i AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
