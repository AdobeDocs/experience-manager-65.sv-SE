---
title: Använd formulärdatamodell
seo-title: Använd formulärdatamodell
description: Lär dig hur du använder formulärdatamodell för att skapa och arbeta med adaptiva formulär och interaktiv kommunikation.
seo-description: Lär dig hur du använder formulärdatamodell för att skapa och arbeta med adaptiva formulär och interaktiv kommunikation.
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Använd formulärdatamodell{#use-form-data-model}

![](do-not-localize/data-integeration.png)

Med dataintegrering med AEM Forms kan du använda olika backend-datakällor för att skapa en formulärdatamodell som du kan använda som schema i olika adaptiva formulär och interaktiva kommunikationsarbetsflöden. Det kräver att du konfigurerar datakällor och skapar formulärdatamodell som baseras på datamodellsobjekt och tjänster som är tillgängliga i datakällor. Mer information finns i följande:

* [Integrering av AEM Forms-data](../../forms/using/data-integration.md)
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

Du kan skapa [anpassningsbara formulär](../../forms/using/creating-adaptive-form.md) och [anpassningsbara formulärfragment](../../forms/using/adaptive-form-fragments.md) baserat på en formulärdatamodell. Gör följande om du vill använda en formulärdatamodell när du skapar ett adaptivt formulär eller adaptivt formulärfragment:

1. På fliken Formulärmodell på skärmen Lägg till egenskaper väljer du **[!UICONTROL Formulärdatamodell]** i listrutan **[!UICONTROL Välj från]** .

   ![create-af-1-1](assets/create-af-1-1.png)

1. Tryck för att expandera **[!UICONTROL Välj formulärdatamodell]**. Alla tillgängliga formulärdatamodeller visas.

   Välj en från datamodell.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (Endast **** adaptiva formulärfragment) Du kan skapa ett adaptivt formulärfragment baserat på endast ett datamodellsobjekt i en formulärdatamodell. Expandera **[!UICONTROL formulärdatamodelldefinitioner]** . Den visar alla datamodellsobjekt i den angivna formulärdatamodellen. Markera ett datamodellsobjekt i listan.

   ![create-af-3](assets/create-af-3.png)

När det adaptiva formuläret eller adaptiva formulärfragment som baseras på en formulärdatamodell har skapats, visas formulärdatamodellsobjekt på fliken **[!UICONTROL Datamodellsobjekt]** i innehållsläsaren i en adaptiv formulärredigerare.

>[!NOTE] {graybox=&quot;true&quot;}
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

Med redigeraren för formulärdatamodell kan du generera och redigera exempeldata för datamodellsobjekt i formulärdatamodellen. Du kan använda dessa data för att förhandsgranska och testa interaktiv kommunikation och anpassningsbara formulär. Du måste generera exempeldata innan du förhandsgranskar enligt beskrivningen i [Arbeta med formulärdatamodellen](../../forms/using/work-with-form-data-model.md#sample).

Så här förhandsgranskar du en interaktiv kommunikation med exempeldata för formulärdatamodell:

1. På AEM-författarinstansen går du till **[!UICONTROL Formulär > Formulär och dokument]**.
1. Välj en interaktiv kommunikation och tryck på **[!UICONTROL Förhandsgranska]** i verktygsfältet för att välja **[!UICONTROL Webbkanal]**, **[!UICONTROL Utskriftskanal]** eller **[!UICONTROL Båda kanaler]** för att förhandsgranska den interaktiva kommunikationen.
1. Kontrollera att [*Testa data för formulärdatamodellen*] är markerat i dialogrutan Förhandsgranska **[!UICONTROL kanal]** och tryck sedan på **[!UICONTROL Förhandsgranska]**.

Den interaktiva kommunikationen öppnas med förfyllda exempeldata.

![webbförhandsvisning](assets/web-preview.png)

Om du vill förhandsgranska ett adaptivt formulär med exempeldata öppnar du det adaptiva adaptiva adaptiva formuläret i redigeringsläge och trycker på **[!UICONTROL Förhandsgranska]**.

## Förifyll med formulärdatamodelltjänst {#prefill}

AEM Forms tillhandahåller förifyllningstjänsten för formulärdatamodeller som är färdig att användas, som du kan aktivera för adaptiva formulär och interaktiv kommunikation baserat på formulärdatamodell. förifyllningstjänsten frågar efter datakällor för datamodellobjekt i det adaptiva formuläret och interaktiv kommunikation och fyller i data i förväg när formuläret eller kommunikationen återges.

Om du vill aktivera förifyllningstjänsten för formulärdatamodellen för ett adaptivt formulär öppnar du egenskaperna för den adaptiva formulärbehållaren och väljer tjänsten **[!UICONTROL Förifyll]** formulärdatamodell i listrutan **[!UICONTROL Förifyll tjänst]** i dragspelet Grundläggande. Spara sedan egenskaperna.

![prefill-service](assets/prefill-service.png)

Om du vill konfigurera förifyllningstjänsten för formulärdatamodell i en interaktiv kommunikation kan du välja förifyllningstjänst för formulärdatamodell i listrutan Förifyll tjänst när du skapar den eller senare genom att ändra egenskaperna.

![edit-ic-props](assets/edit-ic-props.png)

Dialogrutan Redigera egenskaper för en interaktiv kommunikation

## Skriv data från anpassade formulär till datakällor {#write-af}

När en användare skickar ett formulär baserat på en formulärdatamodell kan du konfigurera formuläret så att det skriver skickade data för ett datamodellsobjekt till sina datakällor. För att uppnå detta tillhandahåller AEM Forms en åtgärd [för att skicka](../../forms/using/configuring-submit-actions.md)formulärdatamodell, som bara finns att tillgå när det gäller anpassningsbara formulär baserade på en formulärdatamodell. Den skriver skickade data för ett datamodellsobjekt i sin datakälla.

Om du vill konfigurera skickaåtgärden för formulärdatamodellen öppnar du egenskaper för adaptiv formulärbehållare och väljer **[!UICONTROL Skicka med formulärdatamodell]** i listrutan Skicka åtgärd under dragspelsfliken. Bläddra och välj sedan ett datamodellsobjekt i **[!UICONTROL namnet på datamodellsobjektet som ska skickas]** . Spara egenskaperna.

När formuläret skickas skrivs data för det konfigurerade datamodellobjektet till respektive datakälla.

![inlämning av data](assets/data-submission.png)

Du kan också skicka formulärbilagor till en datakälla med hjälp av objektegenskapen för binär datamodell. Gör följande för att skicka bilagor till en JDBC-datakälla:

1. Lägg till ett datamodellsobjekt som innehåller en binär egenskap i formulärdatamodellen.
1. I det adaptiva formuläret drar och släpper du komponenten **[!UICONTROL Bifogad fil]** från komponentwebbläsaren till det adaptiva formuläret.
1. Tryck för att markera den tillagda komponenten och tryck på ![settings_icon](assets/settings_icon.png) för att öppna egenskapsläsaren för komponenten.
1. I fältet Bindningsreferens trycker du på ![foldersearch_18](assets/foldersearch_18.png) och navigerar till den binära egenskap som du har lagt till i formulärdatamodellen. Konfigurera andra egenskaper efter behov.

   Tryck på ![bockknappen](assets/check-button.png) för att spara egenskaperna. Bilagefältet är nu bundet till den binära egenskapen för formulärdatamodellen.

1. Aktivera Skicka **[!UICONTROL formulärbilagor]** i avsnittet Skicka i egenskaperna för den adaptiva formulärbehållaren. Den bifogade filen i fältet för binära egenskaper skickas till datakällan när formuläret skickas.

## Anropa tjänster i anpassningsbara formulär med hjälp av regler {#invoke-services}

I ett adaptivt formulär som baseras på en formulärdatamodell kan du [skapa regler](../../forms/using/rule-editor.md) för att anropa tjänster som konfigurerats i formulärdatamodellen. Åtgärden **[!UICONTROL Anropa tjänster]** i en regel listar alla tillgängliga tjänster i formulärdatamodellen och gör att du kan välja in- och utdatafält för tjänsten. Du kan också använda regeltypen **Ange värde** för att anropa en formulärdatamodelltjänst och ställa in värdet för ett fält på utdata som returneras av tjänsten.

I följande regel anropas till exempel en get-tjänst som tar Employee Id som indata och de returnerade värdena fylls i i motsvarande fält för beroende ID, efternamn, förnamn och kön i formuläret.

![invoke-service](assets/invoke-service.png)

Dessutom kan du använda API:t för att skriva ett JavaScript i kodredigeraren för regelredigeraren. `guidelib.dataIntegrationUtils.executeOperation` API-information finns i [API för att anropa datamodellstjänsten](/help/forms/using/invoke-form-data-model-services.md)för formulär.
