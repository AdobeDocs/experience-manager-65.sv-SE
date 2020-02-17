---
title: Lägga till dynamiska Media Classic-funktioner på sidan
description: Lär dig hur du lägger till funktioner och komponenter i Dynamic Media Classic på din AEM-sida.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Lägga till dynamiska Media Classic-funktioner på sidan {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) är en värdbaserad lösning för att hantera, förbättra, publicera och leverera mediefiler till webben, mobiler, e-post och internetanslutna skärmar och för tryck.

Du kan visa AEM-resurser som publicerats i Dynamic Media Classic i olika visningsprogram:

* Zoomning
* Utfällbar
* Video
* Bildmall
* Bild

Du kan publicera digitala resurser direkt från AEM till Dynamic Media Classic och du kan publicera digitala resurser från Dynamic Media Classic till AEM.

I det här dokumentet beskrivs hur du publicerar digitala resurser från AEM till Dynamic Media Classic och vice versa. Visningsprogrammen beskrivs också i detalj. Information om hur du konfigurerar AEM för Dynamic Media Classic finns i [Integrera Dynamic Media Classic med AEM](/help/sites-administering/scene7.md).

Se även [Lägga till bildscheman](image-maps.md).

Mer information om hur du använder videokomponenter med AEM finns i [Video](video.md).

>[!NOTE]
>
>Om resurserna i Dynamic Media Classic inte visas som de ska kontrollerar du att Dynamic Media är [inaktiverat](config-dynamic.md#disabling-dynamic-media) och uppdaterar sedan sidan.

## Publicera manuellt till Dynamic Media Classic från resurser {#manually-publishing-to-scene-from-assets}

Du kan publicera digitala resurser till Dynamic Media Classic på följande sätt:

* [I det klassiska användargränssnittet från Resurskonsolen](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [I det klassiska användargränssnittet för en resurs](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [I det klassiska användargränssnittet utanför CQ-målmappen](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM publicerar till Dynamic Media Classic asynkront. När du har klickat på **[!UICONTROL Publicera]** kan det ta flera sekunder för resursen att publicera till Dynamic Media Classic.


## Dynamic Media Classic-komponenter {#scene-components}

Följande Dynamic Media Classic-komponenter är tillgängliga i AEM:

* Zoomning
* Utfällbar (zoom)
* Bildmall
* Bild
* Video

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste markeras i **[!UICONTROL designläge]** innan du använder dem.

När de är tillgängliga i **[!UICONTROL designläge]** kan du lägga till komponenterna på sidan precis som andra AEM-komponenter. Resurser som ännu inte har publicerats till Dynamic Media Classic publiceras till Dynamic Media Classic om de ligger i en synkroniserad mapp, på en sida eller med en Dynamic Media Classic-molnkonfiguration.

>[!NOTE]
>
>Om du skapar och utvecklar anpassade visningsprogram och använder Content Finder måste du lägga till parametern **[!UICONTROL allowfullscreen]** explicit.

### Meddelande om att Flash-visningsprogrammet har upphört att gälla {#flash-viewers-end-of-life-notice}

Från och med den 31 januari 2017 upphör stödet för Flash-visningsprogramplattformen med Adobe Dynamic Media Classic.

Mer information om den här viktiga förändringen finns i Vanliga frågor och svar om [användarvänligheten i Flash Viewer](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Lägga till en Dynamic Media Classic-komponent (Scene7) på en sida {#adding-a-scene-component-to-a-page}

Att lägga till en Dynamic Media Classic-komponent (Scene7) på en sida är detsamma som att lägga till en komponent på en sida. Dynamiska Media Classic-komponenter beskrivs i detalj i följande avsnitt.

**Lägga till en Dynamic Media Classic-komponent (Scene7) på en sida**

1. I AEM öppnar du sidan där du vill lägga till komponenten Dynamic Media Classic (Scene7).

1. Om det inte finns några Dynamic Media Classic-komponenter tillgängliga klickar du på **[!UICONTROL designläge]** , trycker på en komponent med en blå kant, trycker på ikonen **[!UICONTROL Överordnad]** och sedan på ikonen **[!UICONTROL Konfiguration]** . I **[!UICONTROL Parsys (Design)]** väljer du alla dynamiska Media Classic-komponenter som ska vara tillgängliga och klickar på **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Klicka på **[!UICONTROL Redigera]** för att återgå till **[!UICONTROL redigeringsläget]** .

1. Dra en komponent från Dynamic Media Classic-gruppen i sidosparken till sidan på önskad plats.

1. Klicka på ikonen **[!UICONTROL Konfiguration]** för att öppna komponenten.

1. Redigera komponenten efter behov och klicka på **[!UICONTROL OK]** för att spara ändringarna.
1. Dra bilden eller videon från innehållsläsaren till den Dynamic Media Classic-komponent som du lade till på sidan.

   >[!NOTE]
   >
   >Om du bara använder gränssnittet måste du dra och släppa bilden eller videon till den Dynamic Media Classic-komponent som du monterade på sidan. Det går inte att markera och redigera komponenten Dynamic Media Classic och sedan välja resursen.

### Lägga till interaktiva tittarupplevelser på en responsiv webbplats {#adding-interactive-viewing-experiences-to-a-responsive-website}

Responsiv design för dina resurser innebär att dina resurser anpassas beroende på var de visas. Med responsiv design kan samma resurser visas effektivt på flera enheter.

Se även [Responsiv design för webbsidor](/help/sites-developing/responsive.md).

**Lägga till en interaktiv tittarupplevelse på en responsiv webbplats**

1. Logga in på AEM och kontrollera att du har [konfigurerat Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) och att Dynamic Media Classic-komponenterna är tillgängliga.

   >[!NOTE]
   >
   >Om Dynamic Media Classic-komponenter inte är tillgängliga måste du aktivera dem [i designläge](/help/sites-authoring/default-components-designmode.md).

1. På en webbplats där **[!UICONTROL Dynamic Media Classic]** -komponenterna är aktiverade drar du en **[!UICONTROL Image]** -komponent till sidan.
1. Markera komponenten och tryck på konfigurationsikonen.
1. Justera brytpunkterna på fliken **[!UICONTROL Dynamic Media Classic Settings]** .

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Bekräfta att tittarna ändrar storlek rejält och att alla interaktioner är optimerade för datorer, surfplattor och mobiler.

### Gemensamma inställningar för alla komponenter i Dynamic Media Classic {#settings-common-to-all-scene-components}

Även om konfigurationsalternativen varierar är följande vanligt för alla [!UICONTROL komponenter i Dynamic Media Classic] :

* **[!UICONTROL Filreferens]** - Bläddra till en fil som du vill referera till. Filreferensen visar resurs-URL:en och inte nödvändigtvis den fullständiga Dynamic Media Classic-URL:en, inklusive URL-kommandon och -parametrar. Du kan inte lägga till kommandon och parametrar för dynamiska Media Classic-URL i det här fältet. De måste läggas till med motsvarande funktioner i komponenten.
* **[!UICONTROL Bredd]** - Här kan du ange bredden.
* **[!UICONTROL Höjd]** - Här kan du ange höjden.

Du anger dessa konfigurationsalternativ genom att öppna (dubbelklicka) en Dynamic Media Classic-komponent, till exempel när du öppnar en **[!UICONTROL Zoom]** -komponent:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoomning {#zoom}

HTML5 Zoom-komponenten visar en större bild när du trycker på **[!UICONTROL +]** .

Resursen har zoomverktyg längst ned. Tryck **[!UICONTROL +]** för att förstora. Tryck **[!UICONTROL -]** för att minska. Om du trycker på **[!UICONTROL x]** - eller reset-zoompilen återställs bilden till den ursprungliga storlek den importerades som. Tryck på de diagonala pilarna för att göra den i helskärmsläge. Tryck på **[!UICONTROL Redigera]** för att konfigurera komponenten. Med den här komponenten kan du konfigurera [inställningar som är gemensamma för alla [!UICONTROL Dynamic Media Classic] -komponenter](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Utfällbar {#flyout}

I den **[!UICONTROL utfällbara]** HTML5-komponenten visas resursen som en delad skärm. lämnade tillgången i den angivna storleken, till höger visas zoomdelen. Tryck på **[!UICONTROL Redigera]** för att konfigurera komponenten. Med den här komponenten kan du konfigurera [inställningar som är gemensamma för alla Dynamic Media Classic-komponenter](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Om komponenten **[!UICONTROL Flyout]** använder en anpassad storlek används den anpassade storleken och responsiv inställning av komponenten inaktiveras.
>
>Om den **[!UICONTROL utfällbara]** komponenten använder standardstorleken, enligt inställningarna i **[!UICONTROL designvyn]**, används standardstorleken och komponenten sträcks ut för att passa sidlayoutstorleken med responsiv konfiguration av komponenten aktiverad. Tänk dock på att det finns en begränsning för responsiv konfiguration av komponenten. När du använder komponenten **[!UICONTROL Flyout]** med responsiv konfiguration bör du inte använda den med full sidsträckning. I annat fall kan den **[!UICONTROL utfällbara]** sträcka sig utanför sidans högra kant.

![chlimage_1-228](assets/chlimage_1-228.png)

### Bild {#image}

Med **[!UICONTROL komponenten Dynamic Media Classic Image]** kan du lägga till Dynamic Media Classic-funktioner i dina bilder, till exempel Dynamic Media Classic-modifierare, bild- eller visningsförinställningar samt skärpa. Komponenten Dynamic Media Classic **[!UICONTROL Image]** liknar andra bildkomponenter i AEM med speciella funktioner i Dynamic Media Classic. I det här exemplet används URL-modifieraren för Dynamic Media Classic, `&op_invert=1` .

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Titel, Alt-text]** - På fliken **[!UICONTROL Avancerat]** lägger du till en titel i bilden och alternativ text för de användare som har grafik inaktiverad.

**[!UICONTROL URL, Öppna i]** - Du kan ange en resurs från för att öppna en länk. Ange **[!UICONTROL URL]** och **[!UICONTROL Öppna i]** anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Visningsförinställning]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

**[!UICONTROL Dynamic Media Classic Configuration]** - Välj den Dynamic Media Classic-konfiguration som du vill använda för att hämta aktiva bildförinställningar från SPS.

**[!UICONTROL Bildförinställning]** - Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns kan du behöva göra den synlig. Se [Hantera bildförinställningar](/help/assets/managing-image-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

**[!UICONTROL Utdataformat]** - Välj bildens utdataformat, till exempel jpeg. Beroende på vilket utdataformat du väljer kan det finnas ytterligare konfigurationsalternativ. Mer information finns i [Bästa tillvägagångssätt](/help/assets/managing-image-presets.md#image-preset-options)för bildförinställning.

**[!UICONTROL Skärpa]** - Välj hur du vill öka skärpan i bilden. Skärpeinställningen förklaras i detalj i [Bästa praxis](/help/assets/managing-image-presets.md#image-preset-options) för bildförinställningar och [Bästa tillvägagångssätt](/help/assets/assets/s7_sharpening_images.pdf)för skärpeökning.

**[!UICONTROL URL-modifierare]** - Du kan ändra bildeffekter genom att ange ytterligare Dynamic Media Classic-bildkommandon. Dessa beskrivs i [Bildförinställningar](/help/assets/managing-image-presets.md) och [Kommandoradsreferensen](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html).

**[!UICONTROL Brytpunkter]** - Om webbplatsen är responsiv bör du justera brytpunkterna. Brytpunkter måste avgränsas med kommatecken ( , ).

### Bildmall {#image-template}

[Dynamic Media Classic Image Templates](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) är lageruppbyggt Photoshop-innehåll som importerats till Dynamic Media Classic, där innehåll och egenskaper parametriserades för variabilitet. Med **[!UICONTROL bildmallskomponenten]** kan du importera bilder och ändra texten dynamiskt i AEM. Dessutom kan du konfigurera **[!UICONTROL Image-mallkomponenten]** så att värden från klientkontexten används, så att varje användare upplever bilden på ett personligt sätt.

Tryck på **[!UICONTROL Redigera]** för att konfigurera komponenten. Du kan konfigurera [inställningar som är gemensamma för alla komponenter](#settings-common-to-all-scene-components) i Dynamic Media Classic samt andra inställningar som beskrivs i det här avsnittet.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Filreferens, Bredd, Höjd]** - Se inställningar som är gemensamma för alla komponenter i ScDynamic Media Classic7.

>[!NOTE]
>
>Dynamic Media Classic URL-kommandon och -parametrar kan inte läggas till direkt i filreferensens URL. De kan bara definieras i komponentgränssnittet på panelen **[!UICONTROL Parametrar]** .

**[!UICONTROL Titel, Alt-text]** - På fliken Dynamic Media Classic Image Template lägger du till en titel i bilden och alternativ text för användare som har grafik inaktiverad.

**[!UICONTROL URL, Öppna i]** - Du kan ange en resurs från för att öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Parameterpanelen]** - När du importerar en bild fylls parametrarna i automatiskt med information från bilden. Om det inte finns något innehåll som kan ändras dynamiskt är det här fönstret tomt.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Ändra text dynamiskt {#changing-text-dynamically}

Om du vill ändra texten dynamiskt anger du ny text i fälten och klickar på **[!UICONTROL OK]**. I det här exemplet är **[!UICONTROL priset]** nu 50 dollar och frakten 99 cent.

![chlimage_1-234](assets/chlimage_1-234.png)

Texten i bilden ändras. Du kan återställa texten till det ursprungliga värdet genom att trycka på **[!UICONTROL Återställ]** bredvid fältet.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Ändra text så att värdet för en klientkontext återspeglas {#changing-text-to-reflect-the-value-of-a-client-context-value}

Om du vill länka ett fält till ett klientkontextvärde trycker du på **[!UICONTROL Välj]** för att öppna klientsnabbmenyn, markerar klientkontexten och trycker på **[!UICONTROL OK]**. I det här exemplet ändras namnet baserat på att namnet länkas till det formaterade namnet i profilen.

![chlimage_1-236](assets/chlimage_1-236.png)

Texten återspeglar namnet på den inloggade användaren. Du kan återställa texten till det ursprungliga värdet genom att klicka på **[!UICONTROL Återställ]** bredvid fältet.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Göra en länk till mallen Dynamic Media Classic Image {#making-the-scene-image-template-a-link}

1. Tryck på **[!UICONTROL Redigera]** på sidan med komponenten Dynamic Media Classic **[!UICONTROL Image Template]**.
1. I fältet **[!UICONTROL URL]** anger du den URL som användarna ska gå till när användaren trycker på bilden. I fältet **[!UICONTROL Öppna i]** väljer du om du vill att målet ska öppnas (ett nytt fönster eller samma fönster).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Tryck på **[!UICONTROL OK]**.

### Videokomponent {#video-component}

Komponenten Dynamic Media Classic **[!UICONTROL Video]** (som finns under Dynamic Media Classic i sidosparken) använder enhets- och bandbreddsidentifiering för att leverera rätt video till varje skärm. Den här komponenten är en HTML5-videospelare; det är ett enda visningsprogram som kan användas över flera kanaler.

Den kan användas för adaptiva videouppsättningar, en enda MP4-video eller en enda F4V-video.

Se [Video](s7-video.md) för mer information om hur videoklipp fungerar med integrering med Dynamic Media Classic. Se även [komponenten Dynamic Media Classic Video jämfört med komponenten](s7-video.md)Foundation Video.

![chlimage_1-239](assets/chlimage_1-239.png)

### Kända begränsningar för videokomponenten {#known-limitations-for-the-video-component}

Adobe DAM och WCM visar om en mastervideo har överförts. De visar inte följande proxyresurser:

* Dynamic Media Classic-kodade renderingar
* Dynamic Media Classic adaptive video sets

När du använder en adaptiv videouppsättning med videokomponenten Dynamic Media Classic måste du ändra storlek på komponenten så att den passar videofilens mått.

## Dynamisk Media Classic-innehållsläsare {#scene-content-browser}

Med webbläsaren Dynamic Media Classic kan du visa innehåll från Dynamic Media Classic direkt i AEM. Om du vill öppna innehållsläsaren väljer du **[!UICONTROL Dynamic Media Classic]** i det pekoptimerade användargränssnittet eller **[!UICONTROL S7]** -ikonen i det klassiska användargränssnittet i **[!UICONTROL Innehållssökning]** . Funktionen är identisk mellan båda användargränssnitten.

Om du har flera konfigurationer visar AEM som standard [standardkonfigurationen](/help/sites-administering/scene7.md#configuring-a-default-configuration). Du kan välja olika konfigurationer direkt i webbläsaren Dynamic Media Classic-innehåll i listrutan.

>[!NOTE]
>
>* Resurser som finns i ad hoc-mappen visas inte i webbläsaren Dynamic Media Classic.
>* När [Säker förhandsvisning är aktiverat](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)visas både publicerade och opublicerade resurser i Dynamic Media Classic i webbläsaren för dynamiskt media Classic-innehåll.
>* Om du inte ser ikonen **[!UICONTROL Dynamic Media Classic]** eller **[!UICONTROL S7]** som ett alternativ i webbläsaren måste du [konfigurera Dynamic Media Classic så att det fungerar med AEM](/help/sites-administering/scene7.md).
>* För video har webbläsaren Dynamic Media Classic stöd för:
   >
   >  
* Adaptiva videouppsättningar: behållare för alla videoåtergivningar som behövs för sömlös uppspelning på flera skärmar
>  * Enkel MP4-video
>  * En F4V-video


### Bläddra i det pekoptimerade användargränssnittet {#browsing-content-in-the-touch-optimized-ui}

Du kan öppna innehållsläsaren i det pekoptimerade eller klassiska användargränssnittet. För närvarande har pekoptimeringen följande begränsning:

* FXG- och Flash-resurser från Dynamic Media Classic stöds inte.

Bläddra bland dynamiskt media Classic-material genom att välja **[!UICONTROL Dynamic Media Classic]** i den tredje listrutan. Dynamic Media Classic visas inte i listan om du inte har konfigurerat Dynamic Media Classic/AEM-integrering.

>[!NOTE]
>
>* Den dynamiska Media Classic-innehållsläsaren läser in ungefär 100 resurser och sorterar dem efter namn.
>* Om du har en säker förhandsgranskningsserver angiven använder webbläsaren den förhandsvisningsservern för att återge miniatyrer och resurser.
>



![chlimage_1-240](assets/chlimage_1-240.png)

Dessutom kan du bläddra bland upplösningsinformation, storlek, dagar sedan ändringen och filnamn genom att hålla markören över resursen i webbläsaren.

![chlimage_1-241](assets/chlimage_1-241.png)

* För adaptiva videouppsättningar och mallar genereras ingen storleksinformation för miniatyrbilder.
* För adaptiva videouppsättningar genereras ingen upplösning för miniatyrbilder.

### Söka efter Dynamic Media Classic-resurser med innehållsläsaren {#searching-for-scene-assets-with-the-content-browser}

Att söka efter dynamiska mediefiler liknar att söka efter AEM-resurser, förutom att när du söker ser du en fjärrvy av resurserna i Dynamic Media Classic-systemet i stället för att importera dem direkt till AEM.

Du kan använda det klassiska användargränssnittet eller det pekoptimerade användargränssnittet för att både visa och söka efter resurser. Beroende på gränssnittet är sökningen något annorlunda.

När du söker i något av användargränssnitten kan du filtrera efter följande villkor (visas här i det pekoptimerade användargränssnittet):

**[!UICONTROL Ange nyckelord]** - Du kan söka efter resurser efter namn. När du söker efter nyckelord som du anger är det filnamnet börjar med. Om du t.ex. skriver ordet &quot;simning&quot; söker du efter alla resursfilnamn som börjar med de bokstäverna i den ordningen. Var noga med att trycka på Retur när du har skrivit in termen för att hitta resursen.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Mapp/sökväg]** - Namnet på mappen som visas baseras på den konfiguration du har valt. Du kan gå ned till lägre nivåer genom att trycka på mappikonen och välja en undermapp. Tryck sedan på bockmarkeringen för att markera den.

Om du anger ett nyckelord och väljer en mapp söker AEM igenom den mappen och eventuella undermappar. Om du inte anger några nyckelord när du söker efter, kommer endast resurserna i den mappen att visas om du väljer mappen. Inga undermappar kommer att visas.

Som standard söker AEM igenom den markerade mappen och alla undermappar.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Typ av resurs]** - Välj **[!UICONTROL Dynamic Media Classic]** om du vill bläddra i Dynamic Media Classic-innehåll. Det här alternativet är endast tillgängligt om Dynamic Media Classic har konfigurerats.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Konfiguration]** - Om du har definierat mer än en dynamisk Media Classic-konfiguration i [!UICONTROL Cloud Services]kan du välja den här. Därför ändras mappen baserat på den konfiguration du har valt.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Resurstyp]** - I webbläsaren Dynamic Media Classic kan du filtrera resultaten så att de innehåller något av följande: bilder, mallar, videor och anpassningsbara videouppsättningar. Om du inte väljer någon resurstyp söker AEM som standard igenom alla resurstyper.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* I det klassiska användargränssnittet kan du även söka efter **Flash** och **FXG**. Filtrering för dessa i det pekoptimerade användargränssnittet stöds för närvarande inte.
   >
   >
* När du söker efter video söker du efter en enskild återgivning. Resultatet returnerar den ursprungliga återgivningen (endast &amp;ast;.mp4) och den kodade återgivningen.
>* När du söker i en adaptiv videouppsättning söker du i mappen och i alla undermappar, men bara om du har lagt till ett nyckelord i sökningen. Om du inte har lagt till något nyckelord söker AEM inte igenom undermapparna.
>



**[!UICONTROL Publiceringsstatus]** - Du kan filtrera efter resurser baserat på publiceringsstatus: **[!UICONTROL Opublicerad]** eller **[!UICONTROL publicerad]**. Om du inte väljer någon **[!UICONTROL publiceringsstatus]** söker AEM som standard igenom alla publiceringsstatusar.

![chlimage_1-247](assets/chlimage_1-247.png)

