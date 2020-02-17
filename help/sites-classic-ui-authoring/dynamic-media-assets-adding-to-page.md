---
title: Lägga till dynamiska medieresurser på sidor
seo-title: Lägga till dynamiska medieresurser på sidor
description: Om du vill lägga till funktionen för dynamiska medier i resurser som du använder på dina webbplatser kan du lägga till komponenten Dynamiska media eller Interaktiva media direkt på sidan.
seo-description: Om du vill lägga till funktionen för dynamiska medier i resurser som du använder på dina webbplatser kan du lägga till komponenten Dynamiska media eller Interaktiva media direkt på sidan.
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Lägga till dynamiska medieresurser på sidor{#adding-dynamic-media-assets-to-pages}

Om du vill lägga till funktionaliteten Dynamic Media i resurser som du använder på dina webbplatser kan du lägga till komponenten **[!UICONTROL Dynamic Media]** eller **[!UICONTROL Interactive Media]** direkt på sidan. Det gör du genom att gå in i [!UICONTROL designläge] och aktivera de dynamiska mediekomponenterna. Sedan kan du lägga till de här komponenterna på sidan och lägga till resurser i komponenten. Komponenterna för dynamiska media och interaktiva media är smarta - de vet om du lägger till en bild eller en video och de tillgängliga alternativen ändras i enlighet med detta.

Du lägger till dynamiska medieresurser direkt på sidan om du använder AEM som WCM.

>[!NOTE]
>
>Bildscheman är tillgängliga direkt för karusellbanderoller.

## Lägga till en Dynamic Media-komponent på en sida {#adding-a-dynamic-media-component-to-a-page}

Att lägga till komponenten [!UICONTROL Dynamic Media] eller [!UICONTROL Interactive Media] på en sida är detsamma som att lägga till en komponent på en sida. Komponenterna [!UICONTROL Dynamic Media] och [!UICONTROL Interactive Media] beskrivs i detalj i följande avsnitt.

Så här lägger du till en komponent/ett visningsprogram för dynamiska media på en sida:

1. Öppna sidan där du vill lägga till komponenten Dynamic Media i AEM.
1. Om ingen Dynamic Media-komponent är tillgänglig klickar du på linjalen i [!UICONTROL sidosparken] för att gå till **[!UICONTROL designläget]** , klickar på **[!UICONTROL Redigera]** parsys och väljer **[!UICONTROL Dynamiska media]** för att göra Dynamic Media-komponenterna tillgängliga.

   >[!NOTE]
   >
   >Mer information finns i [Konfigurera komponenter i designläge](/help/sites-authoring/default-components-designmode.md) .

1. Gå tillbaka till **[!UICONTROL redigeringsläget]** genom att klicka på pennikonen i [!UICONTROL sidosparken].
1. Dra **[!UICONTROL komponenten Dynamic Media]** eller **[!UICONTROL Interactive Media]** från gruppen **[!UICONTROL Annan]** i sidosparken till den önskade platsen.
1. Klicka på **[!UICONTROL Redigera]** för att öppna komponenten.
1. [Redigera komponenten](#dynamic-media-component) efter behov och klicka på **[!UICONTROL OK]** för att spara ändringarna.

## Dynamiska mediakomponenter {#dynamic-media-components}

[!UICONTROL Dynamic Media] och [!UICONTROL Interactive Media] finns i [!UICONTROL Sidekick] under **[!UICONTROL Dynamic Media]**. Du använder komponenten **[!UICONTROL Interactive Media]** för interaktiva resurser som interaktiv video, interaktiva bilder eller karuselluppsättningar. Använd komponenten **[!UICONTROL Dynamic Media]** för alla andra dynamiska mediekomponenter.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste markeras i designläge innan du använder. [När de är tillgängliga i designläge](/help/sites-authoring/default-components-designmode.md)kan du lägga till komponenterna på sidan på samma sätt som andra AEM-komponenter.

### Dynamic Media-komponent {#dynamic-media-component}

Komponenten Dynamic Media är smart - beroende på om du lägger till en bild eller en video finns det olika alternativ. Komponenten har stöd för bildförinställningar, bildbaserade visningsprogram som bilduppsättningar, snurra, blandade medieuppsättningar och video. Dessutom är visningsprogrammet responsivt. Skärmstorleken ändras alltså automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-baserade.

>[!NOTE]
>
>När du lägger till komponenten [!UICONTROL Dynamic Media] och **[!UICONTROL Dynamiska mediainställningar]** är tomma eller du inte kan lägga till en resurs på rätt sätt bör du kontrollera följande:
>
>* Du har [aktiverat Dynamic Media](/help/assets/config-dynamic.md). Dynamiska media är inaktiverat som standard.
>* Bilden har en pyramidformad fil. Bilder som importerats innan dynamiska medier aktiverats har ingen pyramiddiff-fil.
>



#### När du arbetar med bilder {#when-working-with-images}

Med [!UICONTROL komponenten Dynamic Media] kan du lägga till dynamiska bilder, inklusive bilduppsättningar, snurra och blandade medieuppsättningar. Du kan zooma in, zooma ut och, om tillämpligt, vrida en bild i en snurra eller välja en bild från en annan typ av uppsättning.

Du kan också konfigurera visningsförinställningen, bildförinställningen eller bildformatet direkt i komponenten. Om du vill göra en bild responsiv kan du antingen ange brytpunkter eller använda en responsiv bildförinställning.

![chlimage_1-72](assets/chlimage_1-72a.png)

Du kan redigera följande dynamiska mediainställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten och sedan på fliken **[!UICONTROL Dynamiska mediainställningar]** .

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Som standard är bildkomponenten för dynamiska media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten på fliken **[!UICONTROL Avancerat]** med egenskaperna **[!UICONTROL Bredd]** och **[!UICONTROL Höjd]** .

**[!UICONTROL Visningsförinställning]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

Det här är det enda tillgängliga alternativet om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar. De visningsförinställningar som visas är också smarta - endast relevanta visningsprogramförinställningar visas.

**[!UICONTROL Bildförinställning]** - Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns kan du behöva göra den synlig. Se [Hantera bildförinställningar](/help/assets/managing-image-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL Bildmodifierare]** - Du kan ändra bildeffekter genom att ange ytterligare bildkommandon. Dessa beskrivs i [Hantera bildförinställningar](/help/assets/managing-viewer-presets.md) och i [Kommandoreferensen](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html).

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL Brytpunkter]** - Om du använder den här resursen på en responsiv webbplats måste du lägga till sidbrytpunkter. Bildbrytpunkter måste avgränsas med kommatecken (,). Det här alternativet fungerar när ingen höjd eller bredd har definierats i en bildförinställning.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

Du kan redigera följande [!UICONTROL avancerade inställningar] genom att klicka på **[!UICONTROL Redigera]** i komponenten.

**[!UICONTROL Titel]** - Ändra bildens titel.

**[!UICONTROL Alt Text]** - Lägg till en titel i bilden för de användare som har grafik inaktiverad.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL URL, Öppna i]** - Du kan ange en resurs från för att öppna en länk. Ange **[!UICONTROL URL]** och **[!UICONTROL Öppna i]** för att ange om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL Bredd och Höjd]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar dessa värden tomma anpassas resursen.

#### När du arbetar med video {#when-working-with-video}

Använd komponenten [!UICONTROL Dynamic Media] för att lägga till dynamisk video på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

![chlimage_1-74](assets/chlimage_1-74a.png)

Du kan redigera följande [!UICONTROL dynamiska mediainställningar] genom att klicka på **[!UICONTROL Redigera]** i komponenten.

>[!NOTE]
>
>Som standard är videokomponenten för dynamiska media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten med **[!UICONTROL Bredd]** och **[!UICONTROL Höjd]** på fliken **[!UICONTROL Avancerat]** .

**[!UICONTROL Förinställning]** för visningsprogram - Välj en befintlig förinställning för visningsprogram i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

Du kan redigera följande [!UICONTROL avancerade] inställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

**[!UICONTROL Titel]** - Ändra videons titel.

**[!UICONTROL Bredd och Höjd]** - Ange värdet i pixlar om du vill att videon ska ha en fast storlek. Om du lämnar dessa värden tomma blir de anpassningsbara.

#### Leverera säker video {#how-to-delivery-secure-video}

När du installerar [FP-13480](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)i AEM 6.2 kan du styra om en video levereras via en säker SSL-anslutning (HTTPS) eller en osäker anslutning (HTTP). Som standard ärvs videoleveransprotokollet automatiskt från inbäddningswebbsidans protokoll. Om webbsidan läses in via HTTPS levereras videon också via HTTPS. Och tvärtom, om webbsidan finns på HTTP, levereras videon via HTTP. I de flesta fall är standardbeteendet bra och du behöver inte göra några konfigurationsändringar. Du kan dock åsidosätta det här standardbeteendet genom att lägga `VideoPlayer.ssl=on` till i slutet av en URL-sökväg eller i listan med andra konfigurationsparametrar för visningsprogrammet i ett inbäddat kodfragment för att framtvinga säker videoleverans.

Mer information om säker videoleverans och användning av konfigurationsattributet i URL-sökvägen finns i `VideoPlayer.ssl` Säker videoleverans [](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_video_viewer_20_securevideodelivery.html) i referenshandboken för visningsprogram. Förutom Video Viewer finns säker videoutgång för visningsprogram för Mixed Media och Interactive Video.

### Interaktiv mediakomponent {#interactive-media-component}

Komponenten Interactive Media är till för de resurser som har interaktivitet i dem, till exempel hotspot-områden eller bildscheman. Om du har en interaktiv bild, interaktiv video eller karusellbanderoll använder du komponenten **[!UICONTROL Interactive Media]** .

Komponenten [!UICONTROL Interaktiva media] är smart - beroende på om du lägger till en bild eller en video har du olika alternativ. Dessutom är visningsprogrammet responsivt. Skärmstorleken ändras alltså automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-baserade.

![chlimage_1-75](assets/chlimage_1-75a.png)

Du kan redigera följande **[!UICONTROL allmänna]** inställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

**[!UICONTROL Visningsförinställning]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Förinställningar för visningsprogram måste publiceras innan de kan användas. Se Hantera förinställningar för visningsprogram.

**[!UICONTROL Titel]** - Ändra videons titel.

**[!UICONTROL Bredd och Höjd]** - Ange värdet i pixlar om du vill att videon ska ha en fast storlek. Om du lämnar dessa värden tomma blir de anpassningsbara.

Du kan redigera följande inställningar för **[!UICONTROL Lägg till i kundvagnen** genom att klicka på **[!UICONTROL Redigera]** i komponenten.

**[!UICONTROL Visa produktresurs]** - Som standard är det här värdet valt. Produktresursen visar en bild av produkten enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktresursen.

**[!UICONTROL Visa produktpris]** - Som standard är det här värdet valt. Produktpriset visar priset för artikeln enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktpriset.

**[!UICONTROL Visa produktformulär]** - Som standard är det här värdet inte valt. Produktformuläret innehåller alla produktvarianter som storlek och färg. Avmarkera kryssrutan om du inte vill visa produktvarianterna.
