---
title: Lägga till dynamiska medieresurser på sidor
description: Lägga till komponenter för dynamiska media på en sida i AEM
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
translation-type: tm+mt
source-git-commit: 202e4d5d0e3fa285b9973e4709a02ca77ccb6e71

---


# Adding Dynamic Media Assets to Pages{#adding-dynamic-media-assets-to-pages}

Om du vill lägga till Dynamic Media-funktionen i resurser som används på era webbplatser kan du lägga till komponenten **dynamiska medier**, **interaktiva medier**, **panoramamedier** eller **360-videomedier** direkt på sidan. Det gör du genom att gå in i layoutläget och aktivera Dynamic Media-komponenterna. Sedan kan du lägga till komponenterna på sidan och lägga till resurser i komponenterna. Dynamic Media-komponenterna är smarta – de känner av om du lägger till en bild eller en video och konfigurationsalternativen ändras i enlighet med detta.

Du lägger till Dynamic Media-resurser direkt på sidan om du använder AEM som innehållshanteringssystem. Om ni använder en annan leverantör för innehållshanteringssystemet kan ni antingen [länka](/help/assets/linking-urls-to-yourwebapplication.md) eller [bädda in](/help/assets/embed-code.md) resurserna. Om du har en responsiv webbplats hos en extern leverantör läser du [Leverera optimerade bilder till en responsiv webbplats](/help/assets/responsive-site.md).

>[!NOTE]
>
>Du måste publicera resurser innan du lägger till dem på sidor i AEM. See [Publishing Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md).

## Lägga till en Dynamic Media-komponent på en sida {#adding-a-dynamic-media-component-to-a-page}

Att lägga till en Dynamic Media-, Interactive Media-, Panoramic Media- eller Video 360 Media-komponent på en sida är detsamma som att lägga till en komponent på en sida. Komponenterna för dynamiska media beskrivs i följande avsnitt.

1. Öppna sidan där du vill lägga till komponenten Dynamic Media i AEM.
1. Tryck på ikonen **[!UICONTROL Komponenter]** i den vänstra rutan och filtrera sedan efter Dynamic Media.

   Om det inte finns några Dynamic Media-komponenter tillgängliga måste du aktivera eller aktivera Dynamic Media-komponenterna. Mer information finns i [Redigera sidmallar](/help/sites-authoring/templates.md#editing-templates-template-authors) .

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Dra en **[!UICONTROL Dynamic Media]** -komponent och släpp den på önskad plats på sidan.

   I exemplet nedan används **[!UICONTROL Video 360 Media]** -komponenten.

   ![6_5_360video_wcmComponentdrag](assets/6_5_360video_wcmcomponentdrag.png)

1. Håll muspekaren direkt på komponenten. När komponenten är omgiven av en blå ruta trycker du en gång för att visa komponentens verktygsfält. Tryck på ikonen **[!UICONTROL Konfiguration (skiftnyckel)]** .

   ![6_5_360video_wcmComponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Beroende på vilken Dynamic Media-komponent du släppte på sidan öppnas en konfigurationsdialogruta. [Ange komponentens alternativ](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) efter behov.

   I exemplet nedan visas dialogrutan Dynamic Media **[!UICONTROL Video 360 Media]** Component (Media-komponent) och de alternativ som är tillgängliga i listrutan Viewer Preset (Visningsförinställning).

   ![Video 360 Media-komponent](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media Video 360 Media-komponenten.

1. När du är klar, nära dialogrutans övre högra hörn, trycker du på bockmarkeringen för att spara ändringarna.

## Lokalisera dynamiska mediakomponenter {#localizing-dynamic-media-components}

Du kan lokalisera komponenter för dynamiska media på ett av två sätt:

* Within a web page in Sites, open **[!UICONTROL Properties]** and select the **[!UICONTROL Advanced]** tab. Välj språk för lokalisering.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* Välj önskad sida eller sidgrupp i platsväljaren. Tryck på **[!UICONTROL Egenskaper]** och välj fliken **[!UICONTROL Avancerat]** . Välj språk för lokalisering.

   >[!NOTE]
   >
   >Observera att inte alla språk som är tillgängliga på menyn **[!UICONTROL Språk]** har tilldelats tokens.

## Dynamiska mediakomponenter {#dynamic-media-components}

Dynamiska mediekomponenter är tillgängliga när du trycker på ikonen **[!UICONTROL Komponenter]** och sedan filtrerar på **[!UICONTROL Dynamic Media]**.

De dynamiska mediakomponenterna som är tillgängliga omfattar följande:

* **[!UICONTROL Dynamiska media]** - Använd för exempelvis bilder, video, e-kataloger och snurra.
* **[!UICONTROL Interaktiva media]** - Använd för interaktiva resurser som interaktiv video, interaktiva bilder eller karuselluppsättningar.
* **[!UICONTROL Panoramabilder]** - Används för panoramabilder eller panoramabilder från VR.
* **[!UICONTROL Video 360 Media]** - Använd för 360-video och 360-VR-videomaterial.

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste göras tillgängliga via mallredigeraren innan du använder dem. [När de har gjorts tillgängliga](/help/sites-authoring/templates.md#editing-templates-template-authors)i mallredigeraren kan du lägga till komponenterna på sidan på samma sätt som andra AEM-komponenter.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Dynamic Media-komponent {#dynamic-media-component}

Komponenten Dynamic Media är smart. Beroende på om du lägger till en bild eller en video har du olika alternativ. Komponenten har stöd för bildförinställningar, bildbaserade visningsprogram som bilduppsättningar, snurra, blandade medieuppsättningar och video. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av komponenten Dynamic Media används på samma sida.
>* Varje instans använder samma resurstyp.
>
>
Tänk på att det inte går att tilldela olika visningsprogramförinställningar till varje Dynamic Media-komponent på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla komponenter för dynamiska media som använder resurser av samma typ på sidan.

När du lägger till komponenten Dynamic Media och **[!UICONTROL Dynamiska mediainställningar]** är tomma eller du inte kan lägga till en resurs på rätt sätt ska du kontrollera följande:

* Du har [aktiverat Dynamic Media](/help/assets/config-dynamic.md). Dynamiska media är inaktiverat som standard.
* Bilden har en pyramidformad fil. Bilder som importerats innan dynamiska medier aktiverats har ingen pyramiddiff-fil.

#### När du arbetar med bilder {#when-working-with-images}

Med komponenten Dynamic Media kan du lägga till dynamiska bilder, inklusive bilduppsättningar, snurpuppsättningar och blandade medieuppsättningar. Du kan zooma in, zooma ut och, om tillämpligt, vrida en bild i en snurra eller välja en bild från en annan typ av uppsättning.

Du kan också konfigurera visningsförinställningen, bildförinställningen eller bildformatet direkt i komponenten. Om du vill göra en bild responsiv kan du antingen ange brytpunkter eller använda en responsiv bildförinställning.

Du *måste* redigera följande dynamiska mediainställningar genom att trycka på ikonen **[!UICONTROL Redigera]** i komponenten och sedan på **[!UICONTROL Dynamiska mediainställningar]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Som standard är Dynamic Media-bildkomponenten adaptiv. If you want to make it a fixed size, set it in the component in the **[!UICONTROL Advanced]** tab with the **[!UICONTROL Width]** and **[!UICONTROL Height]**.

* **[!UICONTROL Visningsförinställning]**- Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kan du behöva göra den synlig. Se Hantera förinställningar för visningsprogram. Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

   Det här är det enda tillgängliga alternativet om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar. De visningsförinställningar som visas är också smarta - endast relevanta visningsprogramförinställningar visas.

* **[!UICONTROL Modifierare]** för visningsprogram - Modifierare för visningsprogram har formen av namn=värde-par med en &amp;-avgränsare och du kan ändra visningsprogram enligt anvisningarna i referenshandboken för visningsprogram. Ett exempel på en visningsmodifierare är `posterimage=img.jpg&caption=text.vtt,1` som ställer in en annan bild för videominiatyrbilden och kopplar en undertextningsfil till videon.

* **[!UICONTROL Bildförinställning]**- Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns kan du behöva göra den synlig. Se Hantera bildförinställningar. Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Bildmodifierare]**- Du kan använda bildeffekter genom att ange ytterligare bildkommandon. Dessa beskrivs i Bildförinställningar och i Referens för bildserverkommando.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Brytpunkter]**- Om du använder den här resursen på en responsiv webbplats måste du lägga till bildbrytpunkter. Bildbrytpunkter måste avgränsas med kommatecken (,). Det här alternativet fungerar när ingen höjd eller bredd har definierats i en bildförinställning.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

   You can edit the following Advanced Settings by tapping **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Titel]**- Ändra bildens titel.

* **[!UICONTROL Alt Text]**- Lägg till en titel i bilden för de användare som har inaktiverat grafik.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL URL, Öppna i]**- Du kan ange att en resurs ska öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.


#### När du arbetar med video {#when-working-with-video}

Använd komponenten Dynamic Media för att lägga till dynamisk video på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

![chlimage_1-173](assets/chlimage_1-540.png)

Du måste redigera följande dynamiska mediainställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

>[!NOTE]
>
>Som standard är videokomponenten för dynamiska media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten med **[!UICONTROL Bredd]** och **[!UICONTROL Höjd]** på fliken **[!UICONTROL Avancerat]** .

* **[!UICONTROL Viewer preset**- Välj en befintlig förinställning för visningsprogrammet för video i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se Hantera förinställningar för visningsprogram.

* **[!UICONTROL Viewer modifiers**- Viewer modifiers har formen av name=value-par med en &amp;-avgränsare och du kan ändra visningsprogram enligt riktlinjerna i referenshandboken för Adobe Viewer. Ett exempel på en visningsmodifierare är `posterimage=img.jpg&caption=text.vtt,1`

   Med visningsmodifierare kan du till exempel göra följande:

   * Associera en bildtextfil med en video: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_caption.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_caption.html)
   * Associera en navigeringsfil med en video: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_navigation.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_navigation.html)
   You can edit the following Advanced Settings by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Title**- Ändra videons titel.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

#### När du arbetar med smart beskärning {#when-working-with-smart-crop}

Använd komponenten Dynamic Media för att lägga till bildresurser för smart beskärning på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

Se även [Bildprofiler](/help/assets/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

Du måste redigera följande dynamiska mediainställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

>[!NOTE]
>
>Som standard är Dynamic Media-bildkomponenten adaptiv. If you want to make it a fixed size, set it in the component in the **[!UICONTROL Advanced]** tab with the **[!UICONTROL Width]** and **[!UICONTROL Height]**.

* **[!UICONTROL Bildmodifierare]**- Du kan använda bildeffekter genom att ange ytterligare bildkommandon. Dessa beskrivs i Bildförinställningar och i Referens för bildserverkommando.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

   You can edit the following Advanced Settings by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Titel]**- Ändra titeln på bilden för smart beskärning.

* **[!UICONTROL Alt Text]**- Lägg till en titel i den smarta beskärningsbilden för de användare som har inaktiverat grafik.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL URL, Öppna i]**- Du kan ange att en resurs ska öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

### Interaktiv mediakomponent {#interactive-media-component}

Komponenten Interactive Media är till för de resurser som har interaktivitet i dem, till exempel hotspot-områden eller bildscheman. Om du har en interaktiv bild, interaktiv video eller karusellbanderoll använder du komponenten **[!UICONTROL Interactive Media]** .

Komponenten Interactive Media är smart. Beroende på om du lägger till en bild eller en video har du olika alternativ. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av komponenten Interactive Media används på samma sida.
>* Varje instans använder samma resurstyp.
>
>
Tänk på att det inte går att tilldela olika visningsprogramförinställningar till varje interaktiv mediekomponent på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla interaktiva mediekomponenter som använder resurser av samma typ på sidan.

![chlimage_1-174](assets/chlimage_1-541.png)

You can edit the following **[!UICONTROL General]** settings by tapping **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Visningsförinställning]**- Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Förinställningar för visningsprogram måste publiceras innan de kan användas. Se Hantera förinställningar för visningsprogram.

* **[!UICONTROL Titel]**- Ändra videons titel.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

   You can edit the following **[!UICONTROL Add To Cart]** settings by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Visa produktresurs]**- Som standard är det här värdet valt. Produktresursen visar en bild av produkten enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktresursen.

* **[!UICONTROL Visa produktpris]**- Som standard är det här värdet valt. Produktpriset visar priset för artikeln enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktpriset.

* **[!UICONTROL Visa produktformulär]**- Som standard är det här värdet inte valt. Produktformuläret innehåller alla produktvarianter som storlek och färg. Avmarkera kryssrutan om du inte vill visa produktvarianterna.

### Panoramamakomponent {#panoramic-media-component}

Komponenten för panoramamedia är avsedd för resurser som är sfäriska panoramabilder. Sådana bilder ger en 360-gradig visningsupplevelse av ett rum, en egenskap, en plats eller ett landskap. För att en bild ska kvalificeras som ett sfäriskt panorama måste den ha antingen ett ELLER båda av följande:

* Proportionerna 2:1.
* Taggad med nyckelorden `equirectangular` eller (`spherical` + `panorama`) eller (`spherical` + `panoramic`). Se [Använda taggar](/help/sites-authoring/tags.md).

Both the aspect ratio and keyword criteria apply to panoramic assets for the asset details page and the **[!UICONTROL Panoramic Media]** WCM component.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av **[!UICONTROL panoramakomponenten]** används på samma sida.
>* Varje instans använder samma resurstyp.
>
>
Be aware that assigning a different viewer preset to each **[!UICONTROL Panoramic Media]** component on that page is not supported.
>
>Du kan dock använda samma visningsförinställning för alla panoramakomponenter som använder resurser av samma typ på sidan.

![panoramabild-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

Du kan redigera följande inställning genom att trycka på **[!UICONTROL Konfigurera]** i komponenten.

* **[!UICONTROL Förinställning]** för visningsprogram - Välj ett befintligt visningsprogram i listrutan med förinställningar för visningsprogram.

Om den visningsförinställning du söker efter inte visas kontrollerar du att den är publicerad. Du måste publicera förinställningarna för visningsprogrammet innan du kan använda dem. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

### Video 360 Media Component {#video-media-component}

Använd **[!UICONTROL Video 360 Media]** -komponenten för att återge ekvirektangulär video på din webbsida för att få en engagerande upplevelse av ett rum, en egenskap, plats, landskap eller läkarvård.

Vid uppspelning på en platt skärm har användaren kontroll över betraktningsvinkeln. uppspelning på mobila enheter utnyttjar vanligtvis de inbyggda gyroskopiska kontrollerna.

Visningsprogrammet har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Du kan redigera följande inställning genom att trycka på **[!UICONTROL Konfigurera]** i komponenten.

* **[!UICONTROL Förinställning]** för visningsprogram - Välj ett befintligt visningsprogram i listrutan med förinställningar för visningsprogram. Använd Video360VR för slutanvändare som använder virtuella verklighetsglasögon. Innehåller grundläggande videouppspelningskontroller och funktioner för sociala medier. Använd Video360_social som innehåller grundläggande videouppspelningskontroller. Videoåtergivning sker i stereoläge. Manuell vypunktskontroll är inaktiverad men gyroskopisk kontroll är aktiverad. Det finns inga funktioner för sociala medier.

Om den visningsförinställning du söker efter inte visas kontrollerar du att den är publicerad. Du måste publicera förinställningarna för visningsprogrammet innan du kan använda dem. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

### Använda HTTP/2 för att leverera Dynamic Media-resurser {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](/help/assets/http2.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.

>[!MORELIKETHIS]
>
>* [Använda videospelaren i AEM Dynamic Media](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-player-feature-video-use.html)
>* [Använda interaktiv video med AEM Dynamic Media](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-interactive-video-feature-video-use.html)
>* [Så här fungerar resursvisningsprogrammet med AEM Dynamic Media](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-viewer-feature-video-understand.html)
>* [Använda anpassade videominiatyrer med AEM Dynamic Media](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Färghantering med AEM Dynamic Media](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-color-management-technical-video-setup.html)
>* [Använda bildskärpa med AEM Dynamic Media](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-image-sharpening-feature-video-use.html)

