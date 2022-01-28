---
title: Lägga till Dynamic Media Classic-funktioner på sidor
description: Så här lägger du till Dynamic Media Classic-funktioner och -komponenter på en sida i Adobe Experience Manager.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 1%

---

# Lägga till Dynamic Media Classic-funktioner på sidor {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) är en värdbaserad lösning för att hantera, förbättra, publicera och leverera mediefiler till webben, mobiler, e-post och internetanslutna displayer samt för tryck.

Du kan visa Experience Manager-resurser som publicerats i Dynamic Media Classic i olika visningsprogram:

* Zoomning
* Utfällbar
* Video
* Bildmall
* Bild

Du kan publicera digitala resurser direkt från Experience Manager till Dynamic Media Classic och du kan publicera digitala resurser från Dynamic Media Classic till Experience Manager.

I det här dokumentet beskrivs hur du publicerar digitala resurser från Experience Manager till Dynamic Media Classic och omvänt. Visningsprogrammen beskrivs också i detalj. Mer information om hur du konfigurerar Experience Manager för Dynamic Media Classic finns i [Integrera Dynamic Media Classic med Experience Manager](/help/sites-administering/scene7.md).

Se även [Lägg till bildscheman](image-maps.md).

Mer information om hur du använder videokomponenter med Experience Manager finns i [Video](video.md).

>[!NOTE]
>
>Om Dynamic Media Classic-resurser inte visas som de ska kontrollerar du att Dynamic Media [inaktiverad](config-dynamic.md#disabling-dynamic-media) och sedan uppdatera sidan.

## Publicera manuellt till Dynamic Media Classic från resurser {#manually-publishing-to-scene-from-assets}

Du kan publicera digitala resurser till Dynamic Media Classic på följande sätt:

* [I det klassiska användargränssnittet från Resurskonsolen](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [I det klassiska användargränssnittet för en resurs](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [I det klassiska användargränssnittet utanför CQ-målmappen](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager publicerar till Dynamic Media Classic asynkront. När du har valt **[!UICONTROL Publish]**, tar det några sekunder för resursen att publicera till Dynamic Media Classic.

## Dynamic Media Classic-komponenter {#scene-components}

Följande Dynamic Media Classic-komponenter finns i Experience Manager:

* Zoomning
* Utfällbar (zoom)
* Bildmall
* Bild
* Video

>[!NOTE]
>
>Dessa komponenter är inte tillgängliga som standard och måste markeras i **[!UICONTROL Design]** före användning.

När de är tillgängliga i **[!UICONTROL Design]** I kan du lägga till komponenterna på sidan precis som andra Experience Manager-komponenter. Resurser som ännu inte har publicerats till Dynamic Media Classic publiceras till Dynamic Media Classic om de ligger i en synkroniserad mapp, på en sida eller med en Dynamic Media Classic molnkonfiguration.

>[!NOTE]
>
>Om du skapar och utvecklar anpassade visningsprogram och använder Content Finder måste du lägga till `allowfullscreen` parameter.

### Meddelande om att Flash Viewer har upphört {#flash-viewers-end-of-life-notice}

Från och med den 31 januari 2017 upphörde Adobe Dynamic Media Classic stödet för visningsprogramplattformen Flash.

### Lägga till en Dynamic Media Classic-komponent (Scene7) på en sida {#adding-a-scene-component-to-a-page}

Att lägga till en Dynamic Media Classic-komponent (Scene7) på en sida är detsamma som att lägga till en komponent på en sida. Dynamic Media Classic-komponenter beskrivs i detalj i följande avsnitt.

**Så här lägger du till en Dynamic Media Classic-komponent (Scene7) på en sida:**

1. Öppna den sida där du vill lägga till Experience Manager **[!UICONTROL Dynamic Media Classic (Scene7)]** -komponenten.

1. Om det inte finns några Dynamic Media Classic-komponenter tillgängliga väljer du **[!UICONTROL Design]** läge, markera en komponent med en blå kant, välj **[!UICONTROL Parent]** -ikonen och sedan **[!UICONTROL Configuration]** ikon. I **[!UICONTROL Parsys (Design)]**, markerar alla Dynamic Media Classic-komponenter för att göra dem tillgängliga och väljer **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Välj **[!UICONTROL Edit]** så att du kan gå tillbaka till **[!UICONTROL Edit]** läge.

1. Dra en komponent från Dynamic Media Classic-gruppen i sidosparken till sidan på önskad plats.

1. Välj **[!UICONTROL Configuration]** så att du kan öppna komponenten.

1. Redigera komponenten efter behov och markera **[!UICONTROL OK]** för att spara ändringar.
1. Dra bilden eller videon från innehållsläsaren till den Dynamic Media Classic-komponent som du har lagt till på sidan.

   >[!NOTE]
   >
   >Endast med pekskärmsgränssnittet måste du dra och släppa bilden eller videon till den Dynamic Media Classic-komponent som du monterade på sidan. Det går inte att markera och redigera Dynamic Media Classic-komponenten och sedan välja resursen.

### Lägga till en interaktiv tittarupplevelse på en responsiv webbplats {#adding-interactive-viewing-experiences-to-a-responsive-website}

Responsiv design för dina resurser innebär att dina resurser anpassas beroende på var de visas. Med responsiv design kan samma resurser visas effektivt på flera enheter.

Se även [Responsiv design för webbsidor](/help/sites-developing/responsive.md).

**Så här lägger du till en interaktiv tittarupplevelse på en responsiv webbplats:**

1. Logga in på Experience Manager och kontrollera att du har [konfigurerade Adobe Dynamic Media Classic-Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) och att Dynamic Media Classic-komponenterna är tillgängliga.

   >[!NOTE]
   >
   >Om Dynamic Media Classic-komponenterna inte är tillgängliga bör du kontrollera att [aktivera dem i designläge](/help/sites-authoring/default-components-designmode.md).

1. På en webbplats med **[!UICONTROL Dynamic Media Classic]** aktiverade komponenter, dra och **[!UICONTROL Image]** till sidan.
1. Markera komponenten och välj konfigurationsikonen.
1. I **[!UICONTROL Dynamic Media Classic Settings]** justerar du brytpunkterna.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Bekräfta att tittarna ändrar storlek rejält och att alla interaktioner är optimerade för datorer, surfplattor och mobiler.

### Gemensamma inställningar för alla Dynamic Media Classic-komponenter {#settings-common-to-all-scene-components}

Även om konfigurationsalternativen varierar är följande gemensamma för alla [!UICONTROL Dynamic Media Classic] komponenter:

* **[!UICONTROL File Reference]** - Bläddra till en fil som du vill referera till. Filreferensen visar resurs-URL:en och inte nödvändigtvis den fullständiga Dynamic Media Classic-URL:en inklusive URL-kommandon och -parametrar. Du kan inte lägga till Dynamic Media Classic URL-kommandon och -parametrar i det här fältet. I stället lägger du till dem via motsvarande funktioner i komponenten.
* **[!UICONTROL Width]** - Ange bredden.
* **[!UICONTROL Height]** - Här kan du ange höjden.

Du anger dessa konfigurationsalternativ genom att öppna (dubbelklicka) en Dynamic Media Classic-komponent, till exempel när du öppnar en **[!UICONTROL Zoom]** komponent:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoomning {#zoom}

Zoomkomponenten för HTML5 visar en större bild när du trycker på **[!UICONTROL +]** -knappen.

Resursen har zoomverktyg längst ned. Välj **[!UICONTROL +]** om du vill förstora; välj **[!UICONTROL -]** om du vill minska. Tryck på **[!UICONTROL x]** eller zoompilen återställer bilden till den ursprungliga storlek den importerades som. Markera de diagonala pilarna så att du kan göra den i helskärmsläge. Välj **[!UICONTROL Edit]** så att du kan konfigurera komponenten. Med den här komponenten kan du konfigurera [gemensamma inställningar för alla [!UICONTROL Dynamic Media Classic] komponenter](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Utfällbar {#flyout}

I HTML5 **[!UICONTROL Flyout]** komponenten visas resursen som delad skärm, lämnade tillgången i den angivna storleken, till höger visas zoomdelen. Välj **[!UICONTROL Edit]** så att du kan konfigurera komponenten. Med den här komponenten kan du konfigurera [gemensamma inställningar för alla Dynamic Media Classic-komponenter](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Om **[!UICONTROL Flyout]** -komponenten använder en anpassad storlek, sedan används den anpassade storleken och responsiv konfiguration av komponenten inaktiveras.
>
>Om **[!UICONTROL Flyout]** -komponenten använder standardstorleken, enligt **[!UICONTROL Design View]** används standardstorleken och komponenten töjs för att passa sidlayoutstorleken när responsiv installation av komponenten är aktiverad. Det finns en begränsning för responsiv konfiguration av komponenten. När du använder **[!UICONTROL Flyout]** -komponent med responsiv konfiguration ska du inte använda den med full sidsträckning. I annat fall visas **[!UICONTROL Flyout]** sträcker sig utanför sidans högra kant.

![chlimage_1-228](assets/chlimage_1-228.png)

### Bild {#image}

Dynamic Media Classic **[!UICONTROL Image]** kan du lägga till Dynamic Media Classic-funktioner i dina bilder, t.ex. Dynamic Media Classic-modifierare, bild- eller visningsförinställningar samt skärpa. Dynamic Media Classic **[!UICONTROL Image]** -komponenten liknar andra bildkomponenter i Experience Manager med speciella Dynamic Media Classic-funktioner. I det här exemplet har bilden Dynamic Media Classic URL-modifieraren, `&op_invert=1` används.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Title, Alt Text]** - I **[!UICONTROL Advanced]** lägger du till en titel i bilden och alternativ text för användare som har grafik inaktiverad.

**[!UICONTROL URL, Open in]** - Du kan ställa in en resurs från för att öppna en länk. Ange **[!UICONTROL URL]** och in **[!UICONTROL Open in]** ange om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Viewer preset]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning du söker efter inte visas måste du göra den synlig. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och omvänt.

**[!UICONTROL Dynamic Media Classic Configuration]** - Välj den Dynamic Media Classic-konfiguration som du vill använda för att hämta aktiva bildförinställningar från SPS.

**[!UICONTROL Image preset]** - Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns måste du göra den synlig. Se [Hantera bildförinställningar](/help/assets/managing-image-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och omvänt.

**[!UICONTROL Output Format]** - Välj bildens utdataformat, till exempel jpeg. Beroende på vilket utdataformat du väljer finns det ytterligare konfigurationsalternativ. Se [Bästa tillvägagångssätt för bildförinställning](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Sharpening]** - Välj hur du vill öka skärpan i bilden. Skärpa förklaras i detalj i [Bästa tillvägagångssätt för bildförinställning](/help/assets/managing-image-presets.md#image-preset-options) och [Bästa praxis för skärpa](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL URL Modifiers]** - Du kan ändra bildeffekter genom att ange ytterligare Dynamic Media Classic-bildkommandon. Dessa kommandon beskrivs i [Bildförinställningar](/help/assets/managing-image-presets.md) och [Kommandoreferens](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Breakpoints]** - Om webbplatsen är responsiv vill du justera brytpunkterna. Brytpunkter måste avgränsas med kommatecken ( , ).

### Bildmall {#image-template}

[Dynamic Media Classic-bildmallar](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) är Photoshop-innehåll i lager som importerats till Dynamic Media Classic, där innehåll och egenskaper parametriserades för variabilitet. The **[!UICONTROL Image template]** kan du importera bilder och ändra texten dynamiskt i Experience Manager. Dessutom kan du konfigurera **[!UICONTROL Image template]** -komponent för att använda värden från klientkontext, så att varje användare upplever bilden på ett personaliserat sätt.

Välj **[!UICONTROL Edit]** om du vill konfigurera komponenten. Du kan konfigurera [gemensamma inställningar för alla Dynamic Media Classic-komponenter](#settings-common-to-all-scene-components) och andra inställningar som beskrivs i det här avsnittet.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL File Reference, Width, Height]** - Se gemensamma inställningar för alla komponenter i ScDynamic Media Classic7.

>[!NOTE]
>
>Dynamic Media Classic URL-kommandon och -parametrar kan inte läggas till direkt i filreferensens URL. De kan bara definieras i komponentens användargränssnitt i **[!UICONTROL Parameter]** -panelen.

**[!UICONTROL Title, Alt Text]** - På fliken Dynamic Media Classic Image Template (Bildmall) lägger du till en titel i bilden och alternativ text för användare som har bilder inaktiverade.

**[!UICONTROL URL, Open in]** - Du kan ställa in en resurs från för att öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Parameter Panel]** - När du importerar en bild fylls parametrarna i automatiskt med information från bilden. Om det inte finns något innehåll som kan ändras dynamiskt är det här fönstret tomt.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Ändra text dynamiskt {#changing-text-dynamically}

Om du vill ändra texten dynamiskt anger du ny text i fälten och markerar **[!UICONTROL OK]**. I det här exemplet **[!UICONTROL Price]** kostar nu 50 dollar och frakten är 99 cent.

![chlimage_1-234](assets/chlimage_1-234.png)

Texten i bilden ändras. Du kan återställa texten till det ursprungliga värdet genom att trycka på **[!UICONTROL Reset]** bredvid fältet.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Ändra text så att den återspeglar värdet för ett klientkontextvärde {#changing-text-to-reflect-the-value-of-a-client-context-value}

Om du vill länka ett fält till ett klientkontextvärde väljer du **[!UICONTROL Select]** för att öppna klientsnabbmenyn väljer du klientkontext och väljer **[!UICONTROL OK]**. I det här exemplet ändras namnet baserat på att namnet länkas till det formaterade namnet i profilen.

![chlimage_1-236](assets/chlimage_1-236.png)

Texten återspeglar namnet på den inloggade användaren. Du kan återställa texten till det ursprungliga värdet genom att klicka på **[!UICONTROL Reset]** bredvid fältet.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Gör Dynamic Media Classic Image Template till en länk {#making-the-scene-image-template-a-link}

1. På sidan med Dynamic Media Classic **[!UICONTROL Image Template]** komponent, markera **[!UICONTROL Edit]**.
1. I **[!UICONTROL URL]** anger du den URL som användarna går till när användaren trycker på bilden. I **[!UICONTROL Open in]** väljer du om du vill att målet ska öppnas (ett nytt fönster eller samma fönster).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Välj **[!UICONTROL OK]**.

### Videokomponent {#video-component}

Dynamic Media Classic **[!UICONTROL Video]** -komponenten (tillgänglig från Dynamic Media Classic-delen av sidosparken) använder enhets- och bandbreddsidentifiering för att leverera rätt video till varje skärm. Den här komponenten är en videospelare för HTML5. det är ett enda visningsprogram som kan användas över flera kanaler.

Den kan användas för adaptiva videouppsättningar, en enda MP4-video eller en enda F4V-video.

Se [Video](s7-video.md) om du vill ha mer information om hur videofilmer fungerar med Dynamic Media Classic-integrering. Se även [Dynamic Media Classic Video-komponenten jämfört med Foundation Video-komponenten](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### Kända begränsningar för videokomponenten {#known-limitations-for-the-video-component}

Adobe DAM och WCM visar om en primär källvideo har överförts. De visar inte följande proxyresurser:

* Dynamic Media Classic-kodade renderingar
* Dynamic Media Classic adaptiva videouppsättningar

När du använder en adaptiv videouppsättning med videokomponenten i Dynamic Media Classic måste du ändra storlek på komponenten så att den passar videofilens mått.

## Dynamic Media Classic Content Browser {#scene-content-browser}

Med Dynamic Media Classic innehållsläsare kan du visa innehåll från Dynamic Media Classic direkt i Experience Manager. Om du vill öppna innehållsläsaren går du till **[!UICONTROL Content Finder]**, markera **[!UICONTROL Dynamic Media Classic]** i det pekoptimerade användargränssnittet eller **[!UICONTROL S7]** -ikonen i det klassiska användargränssnittet. Funktionen är identisk mellan båda användargränssnitten.

Om du har flera konfigurationer visas Experience Manager som standard [standardkonfiguration](/help/sites-administering/scene7.md#configuring-a-default-configuration). Du kan välja olika konfigurationer direkt i Dynamic Media Classic innehållsläsare i listrutan.

>[!NOTE]
>
>* Resurser i mappen on-demand visas inte i Dynamic Media Classic Content Browser.
>* När [Säker förhandsvisning är aktiverat](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), både publicerade och opublicerade resurser på Dynamic Media Classic visas i Dynamic Media Classic innehållsläsare.
>* Om du inte ser **[!UICONTROL Dynamic Media Classic]** eller **[!UICONTROL S7]** som ett alternativ i webbläsaren måste du [konfigurera Dynamic Media Classic så att det fungerar med Experience Manager](/help/sites-administering/scene7.md).
>* För video har Dynamic Media Classic Content Browser stöd för:
   >
   >   * Adaptiva videouppsättningar: behållare för alla videoåtergivningar som behövs för sömlös uppspelning på flera skärmar
   >   * Enkel MP4-video
   >   * En F4V-video


### Bläddra i det pekoptimerade användargränssnittet {#browsing-content-in-the-touch-optimized-ui}

Du kan öppna innehållsläsaren i det pekoptimerade eller klassiska användargränssnittet. För närvarande har pekoptimeringen följande begränsning:

* FXG- och Flash-resurser från Dynamic Media Classic stöds inte.

Bläddra bland Dynamic Media Classic-resurser genom att välja **[!UICONTROL Dynamic Media Classic]** från den tredje listrutan. Dynamic Media Classic visas inte i listan om du inte har konfigurerat Dynamic Media Classic/Experience Manager.

>[!NOTE]
>
>* Dynamic Media Classic innehållsläsare läser in cirka 100 resurser och sorterar dem efter namn.
>* Om du har en säker förhandsgranskningsserver angiven använder webbläsaren den förhandsvisningsservern för att återge miniatyrer och resurser.

>


![chlimage_1-240](assets/chlimage_1-240.png)

Dessutom kan du bläddra bland upplösningsinformation, storlek, dagar sedan ändringen och filnamn genom att hålla markören över resursen i webbläsaren.

![chlimage_1-241](assets/chlimage_1-241.png)

* För adaptiva videouppsättningar och mallar genereras ingen storleksinformation för miniatyrbilder.
* För adaptiva videouppsättningar genereras ingen upplösning för miniatyrbilder.

### Söka efter Dynamic Media Classic-resurser med innehållsläsaren {#searching-for-scene-assets-with-the-content-browser}

Att söka efter resurser i Dynamic Media Classic liknar att söka efter resurser i Experience Manager Assets. När du söker ser du i själva verket en fjärrvy över resurserna i Dynamic Media Classic-systemet i stället för att importera dem direkt till Experience Manager.

Du kan använda det klassiska användargränssnittet eller det pekoptimerade användargränssnittet för att både visa och söka efter resurser. Beroende på gränssnittet är sökningen något annorlunda.

När du söker i något av användargränssnitten kan du filtrera efter följande villkor (visas här i det pekoptimerade användargränssnittet):

**[!UICONTROL Enter keywords]** - Du kan söka efter resurser efter namn. När du söker efter nyckelorden som du anger är det filnamnet börjar med. Om du t.ex. skriver ordet &quot;simning&quot; söker du efter alla resursfilnamn som börjar med de bokstäverna i den ordningen. Var noga med att trycka på Retur när du har skrivit in termen för att hitta resursen.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Folder/path]** - Namnet på mappen som visas baseras på den konfiguration du har valt. Du kan gå ned till lägre nivåer genom att trycka på mappikonen och välja en undermapp. Tryck sedan på bockmarkeringen för att markera den.

Om du anger ett nyckelord och väljer en mapp söker Experience Manager igenom den mappen och eventuella undermappar. Om du inte anger några nyckelord när du söker efter, visas bara resurserna i den mappen om du markerar mappen, och inga undermappar inkluderas.

Som standard söker Experience Manager i den markerade mappen och i alla undermappar.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Type of Asset]** - Välj **[!UICONTROL Dynamic Media Classic]** om du vill bläddra i Dynamic Media Classic innehåll. Det här alternativet är bara tillgängligt om Dynamic Media Classic har konfigurerats.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuration]** - Om du har mer än en Dynamic Media Classic-konfiguration definierad i [!UICONTROL Cloud Services]väljer du den här. Därför ändras mappen baserat på den konfiguration du har valt.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Asset type]** - I Dynamic Media Classic webbläsare kan du filtrera resultaten så att de innehåller något av följande: bilder, mallar, videor och anpassningsbara videouppsättningar. Om du inte väljer någon resurstyp söker Experience Manager som standard i alla resurstyper.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* I det klassiska användargränssnittet kan du även söka efter **Flash** och **FXG**. Filtrering för de här typerna i det pekoptimerade användargränssnittet stöds inte.
>
>* När du söker efter video söker du efter en enskild återgivning. Resultatet returnerar den ursprungliga återgivningen (endast &amp;ast;.mp4) och den kodade återgivningen.
>* När du söker i en adaptiv videouppsättning söker du i mappen och i alla undermappar, men bara om du har lagt till ett nyckelord i sökningen. Om du inte har lagt till något nyckelord söker Experience Manager inte i undermapparna.

>


**[!UICONTROL Publish Status]** - Du kan filtrera efter resurser baserat på publiceringsstatus: **[!UICONTROL Unpublished]** eller **[!UICONTROL Published]**. Om du inte markerar någon **[!UICONTROL Publish Status]** söker Experience Manager som standard igenom alla publiceringsstatusar.

![chlimage_1-247](assets/chlimage_1-247.png)
