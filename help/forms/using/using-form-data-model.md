---
title: Använd formulärdatamodell
seo-title: Use form data model
description: Lär dig hur du använder formulärdatamodell för att skapa och arbeta med adaptiva formulär och interaktiv kommunikation.
seo-description: Learn how to use form data model to create and work with adaptive forms and interactive communications.
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
feature: Form Data Model
exl-id: 9a73a643-7ad4-49aa-a971-08d52679158d
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 0%

---

# Använd formulärdatamodell{#use-form-data-model}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model.html) |
| AEM 6.5 | Den här artikeln |


![hero-image](do-not-localize/data-integration.png)

Med AEM Forms dataintegrering kan ni använda olika backend-datakällor för att skapa en formulärdatamodell som du kan använda som schema i olika adaptiva formulär och interaktiva kommunikationsarbetsflöden. Det kräver att du konfigurerar datakällor och skapar formulärdatamodell som baseras på datamodellsobjekt och tjänster som är tillgängliga i datakällor. Mer information finns i följande:

* [AEM Forms dataintegrering](../../forms/using/data-integration.md)
* [Konfigurera datakällor](../../forms/using/configure-data-sources.md)
* [Skapa formulärdatamodell](../../forms/using/create-form-data-models.md)
* [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md)

En formulärdatamodell är ett tillägg till JSON-schema som du kan använda för att:

* [Skapa anpassningsbara formulär och fragment](#create-af)
* [Skapa interaktiv kommunikation och byggstenar som text, listor och villkorsfragment](#create-ic)
* [Förgranska interaktiv kommunikation med exempeldata](#preview-ic)
* [Förifyll anpassningsbara formulär och interaktiv kommunikation](#prefill)
* [Skriv in data från anpassningsbara formulär i datakällor](#write-af)
* [Anropa tjänster med anpassningsbara formulärregler](#invoke-services)

## Skapa anpassningsbara formulär och fragment {#create-af}

Du kan [anpassningsbara formulär](../../forms/using/creating-adaptive-form.md) och [adaptiva formulärfragment](../../forms/using/adaptive-form-fragments.md) baserat på en formulärdatamodell. Gör så här om du vill använda en formulärdatamodell när du skapar ett adaptivt formulär eller adaptivt formulärfragment:

1. På fliken Formulärmodell på skärmen Lägg till egenskaper väljer du **[!UICONTROL Form Data Model]** i **[!UICONTROL Select From]** listruta.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Tryck för att expandera **[!UICONTROL Select Form Data Model]**. Alla tillgängliga formulärdatamodeller visas.

   Välj en från datamodell.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Endast adaptiva formulärfragment**) Du kan skapa ett adaptivt formulärfragment baserat på endast ett datamodellsobjekt i en formulärdatamodell. Expandera **[!UICONTROL Form Data Model Definitions]** nedrullningsbar meny. Den visar alla datamodellsobjekt i den angivna formulärdatamodellen. Markera ett datamodellsobjekt i listan.

   ![create-af-3](assets/create-af-3.png)

När det adaptiva formuläret eller adaptiva formulärfragment som baseras på en formulärdatamodell har skapats, visas formulärdatamodellsobjekt i **[!UICONTROL Data Model Objects]** i Content Browser i adaptive form editor.

>[!NOTE]
>
>För ett adaptivt formulärfragment visas endast det datamodellsobjekt som valts vid redigeringen och tillhörande datamodellsobjekt på fliken Datamodellsobjekt.

![data-model-objects-tab](assets/data-model-objects-tab.png)

Du kan dra och släppa datamodellsobjekt till det adaptiva formuläret eller fragmentet för att lägga till formulärfält. De tillagda formulärfälten behåller metadataegenskaperna och bindningen med datamodellens objektegenskaper. Bindningen ser till att fältvärdena uppdateras i motsvarande datakällor när formuläret skickas och förifylls när formuläret återges.

## Skapa interaktiv kommunikation {#create-ic}

Du kan skapa en interaktiv kommunikation baserad på en formulärdatamodell som du kan använda för att förifylla interaktiv kommunikation med data från konfigurerade datakällor. Dessutom kan byggstenarna i en interaktiv kommunikation, som text, lista och villkorsdokumentfragment, baseras på en formulärdatamodell.

Du kan välja en formulärdatamodell när du skapar en interaktiv kommunikation eller ett dokumentfragment. Följande bild visar fliken Allmänt i dialogrutan Skapa interaktiv kommunikation.

![create-ic](assets/create-ic.png)

Fliken Allmänt i dialogrutan Skapa interaktiv kommunikation

Mer information finns i:

[Skapa interaktiv kommunikation](../../forms/using/create-interactive-communication.md)

[Text i interaktiv kommunikation](/help/forms/using/texts-interactive-communications.md)

[Villkor i interaktiv kommunikation](/help/forms/using/conditions-interactive-communications.md)

[Listfragment](/help/forms/using/lists.md)

## Förhandsgranska med exempeldata {#preview-ic}

Med formulärdatamodellens redigerare kan du generera och redigera exempeldata för datamodellsobjekt i formulärdatamodellen. Du kan använda dessa data för att förhandsgranska och testa interaktiv kommunikation och anpassningsbara formulär. Du måste generera exempeldata innan du förhandsgranskar enligt beskrivningen i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md#sample).

Så här förhandsgranskar du en interaktiv kommunikation med exempelformulärdata:

1. Navigera AEM författarinstansen till **[!UICONTROL Forms > Forms & Documents]**.
1. Välj en interaktiv kommunikation och tryck **[!UICONTROL Preview]** i verktygsfältet för att markera **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, eller **[!UICONTROL Both Channels]** för att förhandsgranska interaktiv kommunikation.
1. I förhandsgranskningen [*kanal*] se till att **[!UICONTROL Test Data of Form Data Model]** är markerat och tryck **[!UICONTROL Preview]**.

Den interaktiva kommunikationen öppnas med förfyllda exempeldata.

![webbförhandsvisning](assets/web-preview.png)

Om du vill förhandsgranska ett adaptivt formulär med exempeldata öppnar du det adaptiva adaptiva formuläret i redigeringsläge och trycker på **[!UICONTROL Preview]**.

## Förifyll med formulärdatamodelltjänst {#prefill}

AEM Forms tillhandahåller förifyllningstjänsten för formulärdatamodell som är färdig att användas och som du kan aktivera för adaptiva formulär och interaktiv kommunikation baserat på formulärdatamodell. förifyllningstjänsten frågar efter datakällor för datamodellobjekt i det adaptiva formuläret och interaktiv kommunikation och fyller i data i förväg när formuläret eller kommunikationen återges.

Om du vill aktivera förifyllningstjänsten för formulärdatamodellen för ett adaptivt formulär öppnar du egenskaperna för den adaptiva formulärbehållaren och väljer **[!UICONTROL Form Data Model Prefill service]** från **[!UICONTROL Prefill Service]** nedrullningsbar meny i dragspelsfliken Grundläggande. Spara sedan egenskaperna.

![prefill-service](assets/prefill-service.png)

Om du vill konfigurera förifyllningstjänsten för formulärdatamodell i en interaktiv kommunikation kan du välja förifyllningstjänst för formulärdatamodell i listrutan Förifyll tjänst när du skapar den eller senare genom att ändra egenskaperna.

![edit-ic-props](assets/edit-ic-props.png)

Dialogrutan Redigera egenskaper för en interaktiv kommunikation

## Skriv data från anpassade formulär till datakällor {#write-af}

När en användare skickar ett formulär baserat på en formulärdatamodell kan du konfigurera formuläret så att det skriver skickade data för ett datamodellsobjekt till sina datakällor. AEM Forms tillhandahåller [Skicka-åtgärd för formulärdatamodell](../../forms/using/configuring-submit-actions.md), som finns att tillgå direkt för anpassningsbara formulär baserade på en formulärdatamodell. Den skriver skickade data för ett datamodellsobjekt i sin datakälla.

Om du vill konfigurera skickaåtgärden för formulärdatamodellen öppnar du egenskaper för adaptiv formulärbehållare och väljer **[!UICONTROL Submit using Form Data Model]** från listrutan Skicka åtgärd under dragspelsfliken. Bläddra och välj sedan ett datamodellsobjekt på **[!UICONTROL Name of the data model object to submit]** nedrullningsbar meny. Spara egenskaperna.

När formuläret skickas skrivs data för det konfigurerade datamodellobjektet till respektive datakälla.

![inlämning av data](assets/data-submission.png)

Du kan också skicka formulärbilagor till en datakälla med hjälp av objektegenskapen för binär datamodell. Gör följande för att skicka bilagor till en JDBC-datakälla:

1. Lägg till ett datamodellsobjekt som innehåller en binär egenskap i formulärdatamodellen.
1. Dra-och-släpp **[!UICONTROL File Attachment]** från komponentwebbläsaren till det adaptiva formuläret.
1. Tryck för att markera den tillagda komponenten och tryck på ![settings_icon](assets/settings_icon.png) om du vill öppna egenskapsgranskaren för komponenten.
1. I fältet Bindningsreferens trycker du på ![foldersearch_18](assets/foldersearch_18.png) och navigera till den binära egenskap som du lade till i formulärdatamodellen. Konfigurera andra egenskaper efter behov.

   Tryck ![check-button](assets/check-button.png) för att spara egenskaperna. Bilagefältet är nu bundet till den binära egenskapen för formulärdatamodellen.

1. Aktivera i delen Skicka i egenskaperna för den adaptiva formulärbehållaren **[!UICONTROL Submit Form Attachments]**. Den bifogade filen i fältet för binära egenskaper skickas till datakällan när formuläret skickas.

## Anropa tjänster i anpassningsbara formulär med hjälp av regler {#invoke-services}

I ett anpassningsbart formulär baserat på en formulärdatamodell kan du [skapa regler](../../forms/using/rule-editor.md) för att anropa tjänster som konfigurerats i formulärdatamodellen. The **[!UICONTROL Invoke Services]** -åtgärden i en regel listar alla tillgängliga tjänster i formulärdatamodellen och låter dig välja in- och utdatafält för tjänsten. Du kan också använda **Ange värde** regeltyp som anropar en datamodelltjänst för formulär och ställer in värdet för ett fält på utdata som returneras av tjänsten.

I följande regel anropas till exempel en get-tjänst som tar Employee Id som indata och de returnerade värdena fylls i i motsvarande fält för beroende ID, efternamn, förnamn och kön i formuläret.

![invoke-service](assets/invoke-service.png)

Dessutom kan du använda `guidelib.dataIntegrationUtils.executeOperation` API för att skriva ett JavaScript i kodredigeraren för regelredigeraren. API-information finns i [API för att anropa datamodelltjänst för formulär](/help/forms/using/invoke-form-data-model-services.md).
