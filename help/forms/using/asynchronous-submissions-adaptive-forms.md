---
title: Asynkron inlämning av adaptiva formulär
seo-title: Asynkron inlämning av adaptiva formulär
description: Lär dig att konfigurera asynkron överföring för adaptiva formulär.
seo-description: Lär dig att konfigurera asynkron överföring för adaptiva formulär.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---


# Asynkron sändning av adaptiva formulär{#asynchronous-submission-of-adaptive-forms}

Som standard är webbformulär konfigurerade att skicka synkront. När användare skickar ett formulär omdirigeras de i synkront skick till en bekräftelsesida, en tacksida eller en felsida om det uppstår ett överföringsfel. Moderna webbupplevelser som single page-applikationer blir dock allt populärare, där webbsidan är statisk medan klient-server-interaktion sker i bakgrunden. Du kan nu ge den här upplevelsen tillgång till adaptiva formulär genom att konfigurera asynkron överföring.

När en användare skickar in ett formulär i asynkron form plugin-program för formulärutvecklare, som omdirigering till ett annat formulär eller till ett separat avsnitt på webbplatsen. Skribenten kan också lägga in separata tjänster som att skicka data till ett annat datalager eller lägga till en anpassad analysmotor. Vid asynkron överföring fungerar ett anpassat formulär som ett program på en sida eftersom formuläret inte läses in igen eller dess URL inte ändras när de skickade formulärdata valideras på servern.

Läs vidare för mer information om asynkron överföring i adaptiva formulär.

## Konfigurera asynkron sändning {#configure}

Så här konfigurerar du asynkron sändning för ett anpassat formulär:

1. I redigeringsläget för anpassningsbara formulär markerar du objektet Formulärbehållare och trycker på ![cmpr1](assets/cmppr1.png) för att öppna dess egenskaper.
1. Aktivera **[!UICONTROL Use asynchronous submission]** i egenskapsavsnittet för **[!UICONTROL Submission]**.
1. I avsnittet **[!UICONTROL On Submit]** väljer du ett av följande alternativ för att skicka formulär.

   * **[!UICONTROL Redirect to URL]**: Omdirigerar till angiven URL eller sida när formulär skickas. Du kan ange en URL eller bläddra för att välja sökvägen till en sida i fältet **[!UICONTROL Redirect URL/Path]**.
   * **[!UICONTROL Show Message]**: Visar ett meddelande om att formulär har skickats. Du kan skriva ett meddelande i textfältet under alternativet Visa meddelande. Textfältet har stöd för RTF-formatering.

1. Tryck på ![check-button1](assets/check-button1.png) för att spara egenskaperna.

## Så här fungerar asynkron sändning {#how-asynchronous-submission-works}

AEM Forms har färdiga funktioner och felhanterare för att skicka in formulär. Hanterare är funktioner på klientsidan som körs baserat på serversvaret. När ett formulär skickas skickas data till servern för validering, som returnerar ett svar till klienten med information om om huruvida överföringen lyckades eller inte. Informationen skickas som parametrar till den relevanta hanteraren för att köra funktionen.

Dessutom kan formulärförfattare och utvecklare skriva regler på formulärnivå för att åsidosätta standardhanterare. Mer information finns i [Åsidosätta standardhanterare med regler](#custom).

Låt oss först granska serversvaret för att se om det har lyckats eller inte.

### Serversvar för lyckad sändning - händelse {#server-response-for-submission-success-event}

Strukturen för serversvaret för händelsen att överföringen lyckades är följande:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

Serversvaret vid lyckad formulärsändning innehåller:

* Typ av formulärdataformat: XML eller JSON
* Formulärdata i XML- eller JSON-format
* Markerat alternativ för omdirigering till en sida eller för att visa ett meddelande som konfigurerats i formuläret
* Sidans URL- eller meddelandeinnehåll som konfigurerats i formuläret

Hanteraren för lyckade åtgärder läser serversvaret och dirigerar därför om till den konfigurerade sidans URL eller visar ett meddelande.

### Serversvar för felhändelse för överföring {#server-response-for-submission-error-event}

Strukturen för serversvaret för en felhändelse vid överföring är följande:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

Serversvaret vid fel när formulär skickas innehåller:

* Orsak till felet, misslyckades med CAPTCHA eller validering på serversidan
* Lista över felobjekt, som innehåller SOM-uttrycket för fältet som inte kunde valideras och motsvarande felmeddelande

Felhanteraren läser serversvaret och visar därför felmeddelandet i formuläret.

## Åsidosätt standardhanterare med regler {#custom}

Formulärutvecklare och författare kan skriva regler på formulärnivå i kodredigeraren för att åsidosätta standardhanterare. Serversvaret för lyckade händelser och felhändelser visas på formulärnivå, som utvecklare kan komma åt med `$event.data` i regler.

Utför följande steg för att skriva regler i kodredigeraren för att hantera lyckade händelser och felhändelser.

1. Öppna det adaptiva formuläret i redigeringsläge, markera ett formulärobjekt och tryck på ![edit-rules1](assets/edit-rules1.png) för att öppna regelredigeraren.
1. Välj **[!UICONTROL Form]** i trädet Formulärobjekt och tryck på **[!UICONTROL Create]**.
1. Välj **[!UICONTROL Code Editor]** i listrutan för lägesval.
1. Tryck på **[!UICONTROL Edit Code]** i kodredigeraren. Tryck på **[!UICONTROL Edit]** i bekräftelsedialogrutan.
1. Välj **[!UICONTROL Successful Submission]** eller **[!UICONTROL Error in Submission]** i listrutan **[!UICONTROL Event]**.
1. Skriv en regel för den valda händelsen och tryck på **[!UICONTROL Done]** för att spara regeln.

