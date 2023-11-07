---
title: Responsiv layout för dina innehållssidor
description: Med Adobe Experience Manager kan du förverkliga en responsiv layout för dina sidor.
uuid: 4db45d78-9fca-4251-b504-ae3481fd9a8b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 668d1a8a-c757-4c9f-833f-e5dada4d0384
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 6%

---

# Responsiv layout{#responsive-layout}

AEM kan du använda en responsiv layout för dina sidor med **Layoutbehållare** -komponenten.

Detta ger ett styckesystem där du kan placera komponenter i ett responsivt rutnät. Rutnätet kan ändra layouten beroende på enhetens/fönstrets storlek och format. Komponenten används tillsammans med [**Layout** läge](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode), vilket gör att du kan skapa och redigera din responsiva layout beroende på enhet.

Layoutbehållaren:

* Tillhandahåller vågrät fäst mot rutnät, tillsammans med möjligheten att placera komponenter i rutnätet sida vid sida och definiera när de ska komprimeras/omformas.
* Använder fördefinierade brytpunkter (till exempel för telefon, surfplatta och så vidare) för att du ska kunna definiera önskat beteende för innehåll för relaterade enheter/orientering.

   * Du kan till exempel anpassa komponentstorleken eller om komponenten kan visas på särskilda enheter.

* Kan kapslas så att kolumnkontroll tillåts.

Användaren kan sedan se hur innehållet återges för specifika enheter med emulatorn.

>[!CAUTION]
>
>Även om Layout Container-komponenten är tillgänglig i det klassiska användargränssnittet är dess fullständiga funktioner bara tillgängliga och stöds i det beröringsaktiverade användargränssnittet.

AEM realiserar responsiv layout för dina sidor med en kombination av mekanismer:

* [**Layoutbehållare**](#adding-a-layout-container-and-its-content-edit-mode) komponent

  Den här komponenten är tillgänglig i [komponentwebbläsare](/help/sites-authoring/author-environment-tools.md#components-browser) och har ett rutnätsstyckesystem där du kan lägga till och placera komponenter i ett responsivt rutnät. Den kan också anges som standardstyckesystem på sidan.

* [**Layoutläge**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

  När layoutbehållaren är placerad på sidan kan du använda **Layout** läge för att placera innehåll i det responsiva rutnätet.

* [**Emulator**](#selecting-a-device-to-emulate)
På så sätt kan du skapa och redigera responsiva webbplatser som ändrar layouten beroende på enhetens/fönstrets storlek genom att ändra komponenternas storlek interaktivt. Användaren kan sedan se hur innehållet återges med emulatorn.

Med dessa responsiva rutnätsmekanismer kan du:

* Använd brytpunkter för att definiera olika innehållslayouter baserat på enhetens bredd (relaterat till enhetstyp och orientering).
* Använd samma brytpunkter och innehållslayouter för att se till att innehållet är anpassat till storleken på webbläsarfönstret på skrivbordet.
* Använd vågrät fäst mot rutnät för att placera komponenter i rutnätet, ändra storlek efter behov och definiera när de ska komprimeras/omformas så att de ligger sida vid sida eller ovanför/nedanför.
* Dölj komponenter för specifika enhetslayouter.
* Uppnå kolumnkontroll.

Beroende på vilket projekt du arbetar med kan Layoutbehållaren användas som standardstyckesystem för sidorna eller som en komponent som kan läggas till på sidan via komponentwebbläsaren (eller båda).

>[!NOTE]
>
>Adobe tillhandahåller [GitHub-dokumentation](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) av den responsiva layouten som en referens som kan ges till gränssnittsutvecklare så att de kan använda det AEM rutnätet utanför AEM, till exempel när de skapar statiska HTML-modeller för en framtida AEM.

>[!NOTE]
>
>Användningen av ovanstående mekanismer aktiveras av mallens konfiguration. Se [Konfigurera responsiv layout](/help/sites-administering/configuring-responsive-layout.md) för ytterligare information.

## Layoutdefinitioner, enhetsemulering och brytpunkter {#layout-definitions-device-emulation-and-breakpoints}

När du skapar webbplatsinnehåll vill du se till att innehållet visas på rätt sätt för den enhet som används för att visa det.

Med AEM kan du definiera layouter beroende på enhetens bredd:

* Med emulatorn kan du emulera dessa layouter på en mängd olika enheter. Förutom enhetstypen är orienteringen vald av **Rotera enhet** kan påverka den markerade brytpunkten när bredden ändras.
* Brytpunkter är de punkter som skiljer layoutdefinitionerna åt.

   * De definierar effektivt den maximala bredden (i pixlar) för alla enheter med en viss layout.
   * Brytpunkterna är vanligtvis giltiga för ett urval enheter, beroende på vilken bredd de visas på.
   * Intervallet för en brytpunkt sträcker sig åt vänster till nästa brytpunkt.
   * Du kan inte markera brytpunkten specifikt. Om du väljer en enhet och orientering väljs automatiskt rätt brytpunkt.

Enheten **Skrivbord**, som inte har någon specifik bredd, relaterar till standardbrytpunkten (d.v.s. allt ovanför den senast konfigurerade brytpunkten).

>[!NOTE]
>
>Det skulle vara möjligt att definiera brytpunkter för varje enskild enhet, men detta skulle drastiskt öka den insats som krävs för att definiera och underhålla layout.

När du använder emulatorn väljer du en specifik enhet för emulerings- och layoutdefinition och den relaterade brytpunkten markeras också. Alla layoutändringar du gör gäller för andra enheter som brytpunkten gäller för, dvs. enheter som är placerade till vänster om den aktiva brytpunktsmarkören, men före nästa brytpunktsmarkör.

När du t.ex. väljer enheten **iPhone 6 Plus** (definierat med en bredd på 540 pixlar) för emulering och layout, brytpunkten **Telefon** (definierat som 768 pixlar) aktiveras också. Alla layoutändringar du gör för **IPHONE 6** kommer att gälla för andra enheter enligt **Telefoner** brytpunkt, som **IPHONE 5** (definierat som 320 pixlar).

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## Välja en enhet som ska emuleras {#selecting-a-device-to-emulate}

1. Öppna den sida du vill redigera. Till exempel:

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. Välj **Emulator** ikonen i det övre verktygsfältet:

   ![Emulator](do-not-localize/screen_shot_2018-03-23at084256.png)

1. Emulatorverktygsfältet öppnas.

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   Emulatorverktygsfältet innehåller ytterligare layoutalternativ:

   * **Rotera enhet** - Du kan rotera en enhet från lodrät (stående) orientering till vågrät (liggande) orientering och tvärtom.

     ![Rotera enhet](do-not-localize/screen_shot_2018-03-23at084612.png) ![Rotera enhet](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **Välj enhet** - Definiera en specifik enhet som ska emuleras från en lista (mer information finns i nästa steg)

     ![Välj enhet](do-not-localize/screen_shot_2018-03-23at084743.png)

1. Om du vill välja en specifik enhet som ska emuleras kan du antingen:

   * Använd ikonen Välj enhet och välj i en nedrullningsbar väljare.
   * Tryck/klicka på enhetsindikatorn i emulatorns verktygsfält.

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. När en viss enhet har valts kan du:

   * Se den aktiva markören för den valda enheten, till exempel **iPad.**
   * Se den aktiva markören för lämplig [brytpunkt](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) som **Tablet.**

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * Den blå prickade linjen representerar *vika* för den valda enheten (här en **IPHONE 6**).

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * Flödet kan också betraktas som sidradbrytningen (ska inte blandas ihop med [brytpunkter](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)) för innehållet. Detta visas för att underlätta för användaren att visa vilken del av innehållet som kommer att visas på enheten före rullning.
   * Flödets linje visas inte om höjden på den enhet som emuleras är högre än skärmstorleken.
   * Flödet visas för författarens bekvämlighet och visas inte på den publicerade sidan.

## Lägga till en layoutbehållare och dess innehåll (redigeringsläge) {#adding-a-layout-container-and-its-content-edit-mode}

A **Layoutbehållare** är ett styckesystem som

* Innehåller andra komponenter.
* Definierar layouten.
* Svar på ändringar.

>[!NOTE]
>
>Om den inte redan är tillgänglig **Layoutbehållare** måste anges explicit [aktiverad för ett styckesystem/en styckesida](/help/sites-administering/configuring-responsive-layout.md) (till exempel genom att använda [**Design** läge](/help/sites-authoring/default-components-designmode.md)).

1. **Layoutbehållaren** är tillgänglig som en standardkomponent i [komponentläsaren](/help/sites-authoring/author-environment-tools.md#components-browser). Härifrån kan du dra den till önskad plats på sidan och sedan ser du platshållaren **Dra komponenter hit**.
1. Du kan sedan lägga till komponenter i layoutbehållaren. De här komponenterna innehåller det faktiska innehållet:

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## Markera och vidta åtgärder på en layoutbehållare (redigeringsläge) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Precis som med andra komponenter kan du markera och sedan vidta åtgärder för (klippa ut, kopiera, ta bort) en layoutbehållare (när de är **Redigera** läge):

>[!CAUTION]
>
>När en layoutbehållare är ett styckesystem tas både layoutstödrastret och alla komponenter (och deras innehåll) som finns i behållaren bort om komponenten tas bort.

1. Om du för musen över eller trycker på platshållaren för stödrastret visas åtgärdsmenyn.

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   Du måste välja **Överordnad** alternativ.

   ![Överordnat alternativ](do-not-localize/screen_shot_2018-03-23at085417.png)

1. Om layoutkomponenten är kapslad väljer du **Överordnad** Med det här alternativet visas en listruta där du kan välja den kapslade layoutbehållaren eller dess överordnade behållare.

   När du för musen över behållarnamnen i listrutan visas deras konturer på sidan.

   * Den lägsta kapslade layoutbehållaren kontureras i svart.
   * Den näst lägsta kapslade layoutbehållaren kommer att vara i mörkgrått.
   * Varje efterföljande behållare blir en ljusare nyans av grått.

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. Då markeras hela stödrastret med dess innehåll. Åtgärdsverktygsfältet visas, där du kan välja en åtgärd som t.ex. **Ta bort.**

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## Definiera layouter (layoutläget) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Du kan definiera en separat layout för varje [brytpunkt](#layout-definitions-device-emulation-and-breakpoints) (enligt emulerad enhetstyp och orientering).

Om du vill konfigurera layouten för ett responsivt rutnät som implementeras med layoutbehållaren måste du använda **Layout** läge.

**Layout** kan startas på två sätt.

* Genom att använda [lägesmenyn i verktygsfältet](/help/sites-authoring/author-environment-tools.md#page-modes) och välja **layoutläget**

   * Välj **layoutläget** på samma sätt som du växlar till **redigeringsläget** eller **målinriktningsläget**.
   * **Layoutläget** är beständigt och du lämnar inte **layoutläget** förrän du väljer ett annat läge med lägesväljaren.

* När [redigera en enskild komponent.](/help/sites-authoring/editing-content.md#edit-component-layout)

   * Genom att använda **Layout** på komponentens snabbåtgärdsmeny kan du växla till **Layout** läge.
   * **Layout** läget kvarstår när komponenten redigeras och återgår till **Redigera** när fokus ändras till en annan komponent.

I layoutläget kan du utföra olika åtgärder på ett rutnät:

* Ändra storlek på innehållskomponenterna med de blå punkterna. Storleksändring fästs alltid mot stödrastret. När du ändrar storlek visas bakgrundsstödrastret som stöd för justering:

  ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

  >[!NOTE]
  >
  >Proportionerna och proportionerna bevaras när komponenter som **Bilder** storleksändras.

* Klicka/peka på en innehållskomponent så kan du göra följande i verktygsfältet:

   * **Överordnad**

     Gör att du kan markera hela layoutbehållarkomponenten för att utföra en åtgärd i sin helhet.

   * **Flyt till ny rad**

     Komponenten flyttas till en ny rad, beroende på vilket utrymme som är tillgängligt i rutnätet.

   * **Dölj komponent**

     Komponenten blir osynlig (den kan återställas från verktygsfältet i layoutbehållaren).

  ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* I **Layout** läge där du kan trycka/klicka på **Dra komponenter hit** om du vill markera hela komponenten. Då visas verktygsfältet för det här läget.

  Verktygsfältet har olika alternativ beroende på layoutkomponentens läge och vilka komponenter som hör till det. Till exempel:

   * **Överordnad** - Markera den överordnade komponenten.

     ![Överordnad](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **Visa dolda komponenter** - Visa alla eller enskilda komponenter. Siffran visar hur många dolda komponenter det finns för närvarande. Räknaren visar hur många komponenter som är dolda.

     ![Visa dolda komponenter](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **Återställ brytpunktslayout** - Återgå till standardlayout. Det innebär att ingen anpassad layout kommer att användas.

     ![Återställ brytpunktslayout](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **Flyt till ny rad** - Flytta komponenten uppåt en position om avstånd tillåter.

     ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **Dölj komponent** - Dölj den aktuella komponenten.

     ![Dölj komponent](do-not-localize/screen_shot_2018-03-23at090834.png)

     >[!NOTE]
     >
     >I exemplet ovan är åtgärderna float och hide tillgängliga eftersom den här layoutbehållaren är kapslad i en överordnad layoutbehållare.

   * **Visa komponenter**
Välj de överordnade komponenterna för att visa åtgärdsverktygsfältet med **Visa dolda komponenter** alternativ. I det här exemplet är två komponenter dolda.

     ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

  Om du väljer alternativet **Visa dolda komponenter** visas de dolda komponenterna i blått i sina ursprungliga positioner.

  ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

  Markera **Återställ alla** visar alla dolda komponenter.
