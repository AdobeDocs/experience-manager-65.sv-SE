---
title: Visa sidanalysdata
seo-title: Visa sidanalysdata
description: Använd data från sidanalys för att mäta hur effektivt deras sidinnehåll är
seo-description: Använd data från sidanalys för att mäta hur effektivt deras sidinnehåll är
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Visa sidanalysdata{#seeing-page-analytics-data}

Använd sidanalysdata för att mäta hur effektivt sidinnehållet är.

## Analyser visas från konsolen {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Sidanalysdata visas i [listvyn](/help/sites-authoring/basic-handling.md#list-view) i webbplatskonsolen. När sidorna visas i listformat är följande kolumner tillgängliga som standard:

* Sidvyer
* Unika besökare
* Tid på sidan

Varje kolumn visar ett värde för den aktuella rapporteringsperioden och anger också om värdet har ökat eller minskat sedan den föregående rapporteringsperioden. De data du ser uppdateras var tolfte timme.

>[!NOTE]
>
>[Konfigurera importintervallet](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) om du vill ändra uppdateringsperioden.

1. Öppna konsolen **Platser**; till exempel [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. Klicka på eller tryck på ikonen längst till höger i verktygsfältet för att välja **listvy** (den ikon som visas beror på den [aktuella vyn](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Återigen, längst till höger i verktygsfältet (övre högra hörnet), klicka eller tryck på ikonen och välj sedan **Visa inställningar**. Dialogrutan **Konfigurera kolumner** öppnas. Gör nödvändiga ändringar och bekräfta med **Uppdatera**.

   ![aa-04](assets/aa-04.png)

### Välja rapporteringsperiod {#selecting-the-reporting-period}

Välj den rapporteringsperiod för vilken analysdata visas på webbplatskonsolen:

* Data för de senaste 30 dagarna
* Data för de senaste 90 dagarna
* Årets data

Den aktuella rapportperioden visas i verktygsfältet i webbplatskonsolen (till höger i det övre verktygsfältet). Använd listrutan för att välja önskad rapporteringsperiod.
![aa-05](assets/aa-05.png)

### Konfigurera tillgängliga datakolumner {#configuring-available-data-columns}

Medlemmar i användargruppen analytics-administrators kan konfigurera konsolen Sites så att författare kan se extra analyskolumner.

>[!NOTE]
>
>När ett sidträd innehåller underordnade sidor som är kopplade till olika Adobe Analytics molnkonfigurationer, kan du inte konfigurera tillgängliga datakolumner för sidorna.

1. I listvyn använder du vyväljarna (höger om verktygsfältet), väljer **Visa inställningar** och sedan **Lägg till anpassade analysdata**.

   ![aa-15](assets/aa-15.png)

1. Markera de mätvärden som du vill visa för författare i webbplatskonsolen och klicka sedan på **Lägg till**.

   Kolumnerna som visas hämtas från Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Öppnar innehållsinsikter från webbplatser {#opening-content-insights-from-sites}

Öppna [Content Insight](/help/sites-authoring/content-insights.md) från Sites-konsolen för att utforska sidans effektivitet ytterligare.

1. I webbplatskonsolen väljer du den sida som du vill se innehållsinsikter för.
1. Klicka på ikonen Analytics (Analyser) och Recommendations () i verktygsfältet.

   ![](do-not-localize/chlimage_1-16a.png)

## Synliga analyser från sidredigeraren (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Detta visas om [Activity Map har konfigurerats](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) för din webbplats.

>[!NOTE]
>
>Data för Activity Map hämtas från Adobe Analytics.

När din webbplats har [konfigurerats för Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md) kan du använda [mode Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) för att visa relevanta data. Till exempel:

![aa-07](assets/aa-07.png)

### Åtkomst till Activity Map {#accessing-the-activity-map}

När du har valt läget [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) uppmanas du att ange dina inloggningsuppgifter för Adobe Analytics.

![aa-03](assets/aa-03.png)

Det flytande verktygsfältet **Analytics** visas; här kan du:

* ändra verktygsfältets format med hjälp av dubbelpilarna (**>>**)
* Växla sidinformation (ögonikon)
* Konfigurera inställningar för Activity Map (cog-ikon)
* Välj den analys som ska visas (olika nedrullningsbara väljare)
* Avsluta Activity Map och stäng verktygsfältet (x)

![aa-09](assets/aa-09.png)

### Välja den analys som ska visas {#selecting-the-analytics-to-show}

Du kan välja vilka analysdata som ska visas och hur de ska visas med hjälp av de olika kriterierna:

* **Standard**/**Live**

* händelsetyp
* användargrupp
* **Bubblor**/**Övertoning**/**Gainers &amp; Losers**/**Av**

* period som ska visas

![aa-13](assets/aa-13.png)

### Konfigurera Activity Map {#configuring-the-activity-map}

Använd ikonen **Visa inställningar** för att öppna dialogrutan **Activity Map-inställningar**.

![aa-04-1](assets/aa-04-1.png)

Dialogrutan **Inställningar för Activity Map** innehåller ett antal alternativ på tre flikar:

![aa-06](assets/aa-06.png)

* Allmänt

   * Report Suite
   * Sidnamn
   * Språk:
   * Etikettövertäckningar med
   * Teckenstorlek för etikett
   * Övertoningsfärg
   * Bubbelfärg
   * Färgövertoning baserad på
   * Genomskinlighet för övertoning

* Standard

   * Visning (typ och antal länkar)
   * Dölj övertäckningar för länkar som inte fått några träffar

* Live

   * Visa överkant (täljare eller förlorare)
   * Exkludera nederkant %
   * Automatisk uppdatering (data och period)

