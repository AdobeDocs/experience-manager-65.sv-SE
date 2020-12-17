---
title: Lägga till Scene7-funktioner på din sida
seo-title: Lägga till Scene7-funktioner på din sida
description: Adobe Scene7 är en värdbaserad lösning för att hantera, förbättra, publicera och leverera mediefiler för webben, mobiler, e-post och internetanslutna displayer samt tryck.
seo-description: Adobe Scene7 är en värdbaserad lösning för att hantera, förbättra, publicera och leverera mediefiler för webben, mobiler, e-post och internetanslutna displayer samt tryck.
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
translation-type: tm+mt
source-git-commit: 863c3292d272ba4c80a80645262919e55870a437
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 1%

---


# Lägga till Scene7-funktioner på din sida{#adding-scene-features-to-your-page}

[Adobe Scene7](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html)  är en värdbaserad lösning för att hantera, förbättra, publicera och leverera mediefiler för webben, mobiler, e-post och internetanslutna displayer samt tryck.

Du kan visa Experience Manager-resurser som publicerats i Scene7 i olika visningsprogram:

* Zoomning
* Utfällbar
* Video
* Bildmall
* Bild

Du kan publicera digitala resurser direkt från Experience Manager till Scene7 och du kan publicera digitala resurser från Scene7 till Experience Manager.

I det här dokumentet beskrivs hur du publicerar digitala resurser från Experience Manager till Scene7 och vice versa. Visningsprogrammen beskrivs också i detalj. Mer information om hur du konfigurerar Experience Manager för Scene7 finns i [Integrera Scene7 med Experience Manager](/help/sites-administering/scene7.md).

Se även [Lägga till bildscheman](/help/assets/image-maps.md).

Mer information om hur du använder videokomponenter med Experience Manager finns i:

* [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Om Scene7-resurser inte visas som de ska kontrollerar du att Dynamic Media är [inaktiverat](/help/assets/config-dynamic.md#disabling-dynamic-media) och uppdaterar sedan sidan.

## Publicera manuellt till Scene7 från Assets {#manually-publishing-to-scene-from-assets}

Du kan publicera digitala resurser till Scene7 antingen från Assets-konsolen i det klassiska användargränssnittet eller direkt från resursen.

>[!NOTE]
>
>Experience Manager publicerar till Scene7 asynkront. När du har klickat på **Publish** kan det ta flera sekunder innan resursen publiceras till Scene7.


### Publicera från Resurskonsolen {#publishing-from-the-assets-console}

Så här publicerar du till Scene7 från Resurskonsolen om resurserna finns i en målmapp i Scene7:

1. Klicka på **Digital Assets** i det klassiska användargränssnittet i Experience Manager för att komma åt den digitala resurshanteraren.

1. Markera resursen (eller resurserna) eller mappen i målmappen som du vill publicera till Scene7, högerklicka och välj **Publicera till Scene7**. Du kan också välja **Publicera till Scene7** på **Verktyg-menyn**.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Gå till Scene7 och bekräfta att resurserna är tillgängliga.

   >[!NOTE]
   >
   >Om resurserna inte finns i en synkroniserad Scene7-mapp är **Publicera till Scene7** på båda menyerna synliga men inaktiverade.

### Publicera från en resurs {#publishing-from-an-asset}

Du kan publicera en resurs manuellt så länge som resursen finns inuti den synkroniserade Scene7-mappen.

>[!NOTE]
>
>Om resursen inte finns i Scene7 synkroniserade mapp visas inte länken till **Publicera till Scene7**.

Så här publicerar du till Scene7 direkt från en digital resurs:

1. I Experience Manager klickar du på **Digital Assets** för att öppna den digitala resurshanteraren.

1. Dubbelklicka för att öppna en resurs.

1. Välj **Publicera till Scene7** i rutan Resursinformation.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. Länken ändras till **Publicerar ...** och sedan **Publicerad**. Gå till Scene7 och bekräfta att resursen är tillgänglig.

   >[!NOTE]
   >
   >Om resursen inte publiceras korrekt på Scene7 ändras länken till **Publiceringen misslyckades**. Om resursen redan har publicerats till Scene7, läses länken **Publicera igen till Scene7**. Med publicering kan du göra ändringar i en resurs i Experience Manager och publicera om dem.

### Publicera resurser utanför CQ-målmappen {#publishing-assets-from-outside-the-cq-target-folder}

Adobe rekommenderar att du bara publicerar resurser till Scene7 från resurser i Scene7 målmapp. Men om du behöver överföra resurser från en mapp utanför målmappen kan du ändå göra det genom att överföra dem till en **ad-hoc**-mapp på Scene7.

Det gör du genom att först konfigurera molnkonfigurationen för sidan där resursen ska visas. Sedan lägger du till en Scene7-komponent på sidan och drar och släpper en resurs på komponenten. När sidegenskaperna har ställts in för den sidan visas en **Publicera på Scene7**-länk, som när den är markerad utlöser överföring till Scene7.

>[!NOTE]
>
>Resurser som finns i ad hoc-mappen visas inte i Scene7 Content Browser.

Så här publicerar du resurser som finns utanför CQ-målmappen:

1. I Experience Manager i det klassiska användargränssnittet klickar du på **Webbplatser** och navigerar till den webbsida där du vill lägga till en digital resurs som ännu inte har publicerats i Scene7. (Normala sidarvsregler gäller.)

1. Klicka på ikonen **Sida** i sidsparken och klicka på **Sidegenskaper**.

1. Klicka på **Cloud Services** och klicka på **Lägg till tjänster** och välj **Scene7**.
1. I listrutan **Adobe Scene7** väljer du önskad konfiguration och klickar på **OK**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Lägg till en Scene7-komponent på önskad plats på webbsidan.
1. Dra en digital resurs från innehållssökaren till komponenten. Du ser en länk till **Kontrollera Scene7 Publication Status**.

   >[!NOTE]
   >
   >Om den digitala resursen finns i CQ-målmappen visas ingen länk till **Check Scene7 Publication Status**. Resurserna placeras bara i komponenten.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Klicka på **Kontrollera Scene7 Publication Status**. Om resurserna inte publiceras publicerar Experience Manager resursen till Scene7. När resursen har överförts finns den i ad hoc-mappen. Som standard finns ad hoc-mappen i **name_of_the_company/CQ5_adhoc**. Du kan [konfigurera detta, om det behövs](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Om resursen inte finns i en synkroniserad Scene7-mapp och det inte finns någon Scene7-molnkonfiguration kopplad till den aktuella sidan, kommer överföringen att misslyckas.

## Scene7 Components {#scene-components}

Följande Scene7-komponenter finns i Experience Manager:

* Zoomning
* Utfällbar (zoom)
* Bildmall
* Bild
* Video

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste markeras i designläge innan du använder.

När de har gjorts tillgängliga i designläge kan du lägga till komponenterna på sidan precis som andra Experience Manager-komponenter. Resurser som ännu inte har publicerats till Scene7 publiceras till Scene7 om de ligger i en synkroniserad mapp, på en sida eller med en Scene7 molnkonfiguration.

>[!NOTE]
>
>Om du skapar och utvecklar anpassade S7-visningsprogram och använder Content Finder måste du lägga till parametern **allowfullscreen** explicit.

### Meddelande om att Flash Viewer har upphört {#flash-viewers-end-of-life-notice}

Från och med den 31 januari 2017 kommer Adobe Scene7 officiellt att stödja visningsprogrammet för Flash.

Mer information om den här viktiga ändringen finns i [Vanliga frågor om användarutgånget i Flash Viewer](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Lägga till en Scene7-komponent på en sida {#adding-a-scene-component-to-a-page}

Att lägga till en Scene7-komponent på en sida är detsamma som att lägga till en komponent på en sida. Scene7-komponenter beskrivs i detalj i följande avsnitt.

Så här lägger du till en Scene7-komponent/ett visningsprogram på en sida i det klassiska användargränssnittet:

1. Öppna den sida i Experience Manager där du vill lägga till Scene7-komponenten.

1. Om det inte finns några Scene7-komponenter tillgängliga klickar du på linjalen i sidosparken för att gå in i **designläget**, på **Redigera**-parsysen och markerar alla **Scene7**-komponenter för att göra dem tillgängliga.

1. Gå tillbaka till **redigeringsläget** genom att klicka på pennan i sidosparken.

1. Dra en komponent från **Scene7**-gruppen i sidosparken till den önskade platsen på sidan.

1. Klicka på **Redigera** för att öppna komponenten.

1. Redigera komponenten efter behov och klicka på **OK** för att spara ändringarna.

### Lägga till interaktiva tittarupplevelser på en responsiv webbplats {#adding-interactive-viewing-experiences-to-a-responsive-website}

Responsiv design för dina resurser innebär att dina resurser anpassas beroende på var de visas. Med responsiv design kan samma resurser visas effektivt på flera enheter.

Så här lägger du till en interaktiv visningsupplevelse på en responsiv webbplats i det klassiska användargränssnittet:

1. Logga in på Experience Manager och kontrollera att du har [konfigurerade Adobe Scene7-Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) och att Scene7-komponenterna är tillgängliga.

   >[!NOTE]
   >
   >Om Scene7 WCM-komponenter inte är tillgängliga måste du aktivera dem i designläge.

1. På en webbplats där Scene7-komponenterna är aktiverade drar du ett **Image**-visningsprogram till sidan.
1. Redigera komponenten och justera brytpunkterna på fliken **Scene7 Settings**.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Bekräfta att tittarna ändrar storlek rejält och att alla interaktioner är optimerade för datorer, surfplattor och mobiler.

### Inställningar som är gemensamma för alla Scene7-komponenter {#settings-common-to-all-scene-components}

Även om konfigurationsalternativen varierar är följande vanligt för alla Scene7-komponenter:

* **Filreferens** - Bläddra till en fil som du vill referera till. Filreferensen visar resurs-URL:en och inte nödvändigtvis den fullständiga Scene7-URL:en inklusive URL-kommandon och -parametrar. Du kan inte lägga till Scene7 URL-kommandon och -parametrar i det här fältet. De måste läggas till med motsvarande funktioner i komponenten.
* **Bredd**  - Ange bredden.
* **Höjd**  - Här kan du ange höjden.

Du anger dessa konfigurationsalternativ genom att öppna (dubbelklicka) en Scene7-komponent, till exempel när du öppnar en **Zooma**-komponent:

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoomning {#zoom}

HTML5 Zoom-komponenten visar en större bild när du trycker på +-knappen.

Resursen har zoomverktyg längst ned. Klicka på **+** för att förstora. Klicka på **-** för att minska. Om du klickar på **x** eller på zoompilen återställs bilden till den ursprungliga storlek den importerades som. Klicka på de diagonala pilarna för att göra helskärmspilen. Klicka på **Redigera** för att konfigurera komponenten. Med den här komponenten kan du konfigurera [inställningar som är gemensamma för alla Scene7-komponenter](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-3.png)

### Flyout {#flyout}

I den utfällbara HTML5-komponenten visas resursen som en delad skärm. lämnade tillgången i den angivna storleken, till höger visas zoomdelen. Klicka på **Redigera** för att konfigurera komponenten. Med den här komponenten kan du konfigurera [inställningar som är gemensamma för alla Scene7-komponenter](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Om den utfällbara komponenten använder en anpassad storlek, används den anpassade storleken och responsiv konfiguration av komponenten inaktiveras.
>
>Om den utfällbara komponenten använder standardstorleken, enligt inställningarna i designvyn, används standardstorleken och komponenten sträcks ut för att passa sidlayoutstorleken med responsiv inställning för komponenten aktiverad. Tänk dock på att det finns en begränsning för responsiv konfiguration av komponenten. När du använder den utfällbara komponenten med responsiv konfiguration bör du inte använda den med full sidsträckning. I annat fall kan den utfällbara menyn sträcka sig utanför sidans högra kant.

![chlimage_1-53](assets/chlimage_1-53.png)

### Bild {#image}

Med Scene7 Image-komponenten kan du lägga till Scene7-funktioner i dina bilder, t.ex. Scene7-modifierare, bild- eller visningsförinställningar samt skärpa. Scene7-bildkomponenten liknar andra bildkomponenter i Experience Manager med speciella Scene7-funktioner. I det här exemplet används Scene7 URL-modifieraren **&amp;op_invert=1**.

![](do-not-localize/chlimage_1-4.png)

**Titel, Alt-** textLägg till en titel i bilden och alternativ text på fliken Avancerat för användare som har inaktiverat grafik.

**URL, Öppna** iDu kan ange en resurs från för att öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

![chlimage_1-54](assets/chlimage_1-54.png)

**Förinställning** för visningsprogramVälj en befintlig förinställning för visningsprogram i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se Hantera förinställningar för visningsprogram. Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

**Scene7** ConfigurationVälj den Scene7-konfiguration som du vill använda för att hämta aktiva bildförinställningar från SPS.

**BildförinställningVälj en** befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns kan du behöva göra den synlig. Se Hantera bildförinställningar. Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

**UtdataformatVälj** bildens utdataformat, till exempel jpeg. Beroende på vilket utdataformat du väljer kan det finnas ytterligare konfigurationsalternativ. Mer information finns i Bästa tillvägagångssätt för förinställda bilder.

**** SkärpaVälj hur du vill öka skärpan i bilden. Skärpa förklaras i detalj i Bästa praxis för bildförinställningar och Bästa praxis för skärpa.

**URL-** modifierareDu kan ändra bildeffekter genom att ange ytterligare S7-bildkommandon. Dessa beskrivs i Bildförinställningar och Kommandoreferensen.

**BrytpunkterOm webbplatsen är responsiv** vill du justera brytpunkterna. Brytpunkter måste avgränsas med kommatecken (,).

### Bildmall {#image-template}

[Scene7 Image-](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) mallar är Photoshop-innehåll i lager som importerats till Scene7, där innehåll och egenskaper parametriserats för variabilitet. Med komponenten **Bildmallen** kan du importera bilder och ändra texten dynamiskt i Experience Manager. Dessutom kan du konfigurera **Image-mallen**-komponenten så att värden från klientkontexten används, så att varje användare upplever bilden på ett personligt sätt.

Klicka på **Redigera** för att konfigurera komponenten. Du kan konfigurera [inställningar som är gemensamma för alla Scene7-komponenter](/help/sites-administering/scene7.md#settingscommontoallscene7components) samt andra inställningar som beskrivs i det här avsnittet.

![chlimage_1-55](assets/chlimage_1-55.png)

**Filreferens, Bredd,** HöjdSe inställningar som är gemensamma för alla Scene7-komponenter.

>[!NOTE]
>
>Scene7 URL-kommandon och -parametrar kan inte läggas till direkt i filreferensens URL. De kan bara definieras i komponentgränssnittet på panelen **Parameter**.

**Titel, Alt-** textPå fliken Scene7-bildmall lägger du till en titel i bilden och alternativ text för användare som har bilder inaktiverade.

**URL, Öppna** iDu kan ange en resurs från för att öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

![chlimage_1-56](assets/chlimage_1-56.png)

**Parameterpanelen** När du importerar en bild fylls parametrarna i automatiskt med information från bilden. Om det inte finns något innehåll som kan ändras dynamiskt är det här fönstret tomt.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Ändra text dynamiskt {#changing-text-dynamically}

Om du vill ändra texten dynamiskt anger du ny text i fälten och klickar på **OK**. I det här exemplet är **Price** nu $50 och frakten 99 cent.

![chlimage_1-58](assets/chlimage_1-58.png)

Texten i bilden ändras. Du kan återställa texten till det ursprungliga värdet genom att klicka på **Återställ** bredvid fältet.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Ändra text så att den återspeglar värdet för ett klientkontextvärde {#changing-text-to-reflect-the-value-of-a-client-context-value}

Om du vill länka ett fält till ett klientkontextvärde klickar du på **Välj** för att öppna klientsnabbmenyn, markerar klientkontexten och klickar på **OK**. I det här exemplet ändras namnet baserat på att namnet länkas till det formaterade namnet i profilen.

![chlimage_1-60](assets/chlimage_1-60.png)

Texten återspeglar namnet på den inloggade användaren. Du kan återställa texten till det ursprungliga värdet genom att klicka på **Återställ** bredvid fältet.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Göra Scene7-bildmallen till en länk {#making-the-scene-image-template-a-link}

Så här gör du Scene7-bildmallskomponenten till en klickbar länk:

1. Klicka på **Redigera** på sidan med Scene7-bildmallskomponenten.
1. I fältet **URL** anger du den URL som användarna går till när de klickar på bilden. I fältet **Öppna i** väljer du om du vill att målet ska öppnas (ett nytt fönster eller samma fönster).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Klicka på **OK**.

### Videokomponent {#video-component}

Komponenten Scene7 **Video** (tillgänglig från Scene7-delen av sidosparken) använder enhets- och bandbreddsidentifiering för att visa rätt video för varje skärm. Den här komponenten är en HTML5-videospelare; det är ett enda visningsprogram som kan användas över flera kanaler.

Den kan användas för adaptiva videouppsättningar, en enda MP4-video eller en enda F4V-video.

Se [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) om du vill ha mer information om hur videofilmer fungerar med Scene7-integrering. Se även hur [komponenten **Scene7 video** jämförs med komponenten **video**](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Kända begränsningar för videokomponenten {#known-limitations-for-the-video-component}

Adobe DAM och WCM visar om en primär källvideo har överförts. De visar inte följande proxyresurser:

* Scene7-kodade renderingar
* Scene7 adaptiva videouppsättningar

När du använder en adaptiv videouppsättning med videokomponenten i Scene7 måste komponentens storlek ändras så att den passar videofilens mått.

## Scene7 Content Browser {#scene-content-browser}

Med Scene7 innehållsläsare kan du visa innehåll från Scene7 direkt i Experience Manager. Om du vill komma åt innehållsläsaren väljer du **Scene7** i det pekoptimerade användargränssnittet eller **S7**-ikonen i det klassiska användargränssnittet. Funktionen är identisk mellan båda användargränssnitten.

Om du har flera konfigurationer visar Experience Manager som standard [standardkonfigurationen](/help/sites-administering/scene7.md#configuring-a-default-configuration). Du kan välja olika konfigurationer direkt i Scene7 innehållsläsare i listrutan.

>[!NOTE]
>
>* Resurser som finns i ad hoc-mappen visas inte i Scene7 innehållsläsare.
>* När [Säker förhandsvisning är aktiverat](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) visas både publicerade och opublicerade resurser på Scene7 i Scene7 innehållsläsare.
>* Om du inte ser **Scene7** eller **S7**-ikonen som ett alternativ i webbläsaren måste du [konfigurera Scene7 så att det fungerar med Experience Manager](/help/sites-administering/scene7.md).
>* För video har Scene7 Content Browser stöd för:
   >   * Adaptiva videouppsättningar: behållare för alla videoåtergivningar som behövs för sömlös uppspelning på flera skärmar
   >   * Enkel MP4-video
   >   * En F4V-video


### Bläddrar i innehåll {#browsing-content-in-the-classic-ui}

Bläddra bland innehåll i Scene7 genom att klicka på fliken **S7**.

Du kan ändra konfigurationen som du använder genom att välja konfigurationen. Mapparna ändras beroende på vilken konfiguration du väljer.

![chlimage_1-64](assets/chlimage_1-64.png)

Precis som med Innehållssökaren för Resurser kan du söka efter resurser och filtrera resultat. Till skillnad från Assets Finder börjar filnamnet **när du anger ett nyckelord på fliken** S7 **med &lt;a2/>strängen som du angav, i stället för** som innehåller **nyckelordet i filnamnet.**

Som standard visas resurser efter filnamn. Du kan också filtrera resultat efter resurstyp.

>[!NOTE]
>
>För video har Scene7 Content Browser of WCM stöd för:
>
>* Adaptiva videouppsättningar: behållare för alla videoåtergivningar som behövs för sömlös uppspelning på flera skärmar
>* Enkel MP4-video
>* En F4V-video

>



### Söka efter Scene7-resurser med innehållsläsaren {#searching-for-scene-assets-with-the-content-browser}

Att söka efter Scene7-resurser liknar att söka efter Experience Manager-resurser, förutom att när du söker ser du en fjärrvy över resurserna i Scene7-systemet i stället för att importera dem direkt till Experience Manager.

Du kan använda det klassiska användargränssnittet eller det pekoptimerade användargränssnittet för att både visa och söka efter resurser. Beroende på gränssnittet är sökningen något annorlunda.

När du söker i något av användargränssnitten kan du filtrera efter följande villkor (visas här i det pekoptimerade användargränssnittet):

**Ange** nyckelordDu kan söka efter resurser efter namn. När du söker efter nyckelord som du anger är det filnamnet börjar med. Om du till exempel skriver ordet &quot;simning&quot; söker du efter alla resursfilnamn som börjar med de bokstäverna i den ordningen. Var noga med att klicka på Ange när du har skrivit in termen för att hitta resursen.

![chlimage_1-65](assets/chlimage_1-65.png)

**Mapp/** sökväg Namnet på mappen som visas baseras på den konfiguration du har valt. Du kan gå ned till lägre nivåer genom att klicka på mappikonen och välja en undermapp. Markera sedan kryssrutan för att markera den.

Om du anger ett nyckelord och väljer en mapp söker Experience Manager igenom den mappen och eventuella undermappar. Om du inte anger några nyckelord när du söker efter, kommer endast resurserna i den mappen att visas om du väljer mappen. Inga undermappar kommer att visas.

Som standard söker Experience Manager i den markerade mappen och i alla undermappar.

![chlimage_1-66](assets/chlimage_1-66.png)

**Typ av** resursVälj Scene7 för att bläddra i Scene7-innehåll. Det här alternativet är bara tillgängligt om Scene7 har konfigurerats.

![chlimage_1-67](assets/chlimage_1-67.png)

**** KonfigurationOm fler än en Scene7-konfiguration har definierats i Cloud Services kan du välja den här. Därför ändras mappen baserat på den konfiguration du har valt.

![chlimage_1-68](assets/chlimage_1-68.png)

**ResurstypI** webbläsaren Scene7 kan du filtrera resultaten så att de innehåller något av följande: bilder, mallar, videor och anpassningsbara videouppsättningar. Om du inte väljer någon resurstyp söker Experience Manager som standard igenom alla resurstyper.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* I det klassiska användargränssnittet kan du även söka efter **Flash** och **FXG**. Filtrering för dessa i det pekoptimerade användargränssnittet stöds för närvarande inte.
   >
   >
* När du söker efter video söker du efter en enskild återgivning. Resultatet returnerar den ursprungliga återgivningen (endast *.mp4) och den kodade återgivningen.
* När du söker i en adaptiv videouppsättning söker du i mappen och i alla undermappar, men bara om du har lagt till ett nyckelord i sökningen. Om du inte har lagt till något nyckelord söker Experience Manager inte igenom undermapparna.



**Publiceringsstatus** Du kan filtrera efter resurser baserat på publiceringsstatus: Opublicerad eller publicerad. Om du inte väljer någon publiceringsstatus söker Experience Manager som standard igenom alla publiceringsstatusar.

![chlimage_1-70](assets/chlimage_1-70.png)
