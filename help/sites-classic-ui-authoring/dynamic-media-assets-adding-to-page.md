---
title: Lägga till Dynamic Media-resurser på sidor
seo-title: Lägga till Dynamic Media-resurser på sidor
description: Om du vill lägga till de dynamiska mediefunktionerna i resurser som du använder på dina webbplatser kan du lägga till Dynamic Media-komponenten eller Interactive Media-komponenten direkt på sidan.
seo-description: Om du vill lägga till de dynamiska mediefunktionerna i resurser som du använder på dina webbplatser kan du lägga till Dynamic Media-komponenten eller Interactive Media-komponenten direkt på sidan.
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 2%

---


# Lägga till Dynamic Media-resurser på sidor{#adding-dynamic-media-assets-to-pages}

Om du vill lägga till Dynamic Media-funktionalitet i resurser som du använder på dina webbplatser kan du lägga till komponenten **[!UICONTROL Dynamic Media]** eller **[!UICONTROL Interactive Media]** direkt på sidan. Det gör du genom att aktivera läget [!UICONTROL Design] och aktivera de dynamiska mediekomponenterna. Sedan kan du lägga till komponenterna på sidan och lägga till resurser i komponenterna. Komponenterna för dynamiska media och interaktiva media är smarta - de vet om du lägger till en bild eller en video och de tillgängliga alternativen ändras i enlighet med detta.

Du lägger till dynamiska medieresurser direkt på sidan om du använder AEM som WCM-fil.

>[!NOTE]
>
>Bildscheman är tillgängliga direkt för karusellbanderoller.

## Lägga till en Dynamic Media-komponent på en sida {#adding-a-dynamic-media-component-to-a-page}

Att lägga till komponenten [!UICONTROL Dynamic Media] eller [!UICONTROL Interactive Media] på en sida är detsamma som att lägga till en komponent på en sida. Komponenterna [!UICONTROL Dynamic Media] och [!UICONTROL Interactive Media] beskrivs i detalj i följande avsnitt.

Så här lägger du till en Dynamic Media-komponent/ett visningsprogram på en sida:

1. Öppna AEM sidan där du vill lägga till Dynamic Media-komponenten.
1. Om ingen Dynamic Media-komponent är tillgänglig klickar du på linjalen i [!UICONTROL Sidekick] för att gå in i **[!UICONTROL Design]**-läget, klickar på **[!UICONTROL Edit]**-parsysen och väljer **[!UICONTROL Dynamic Media]** för att göra Dynamic Media-komponenterna tillgängliga.

   >[!NOTE]
   >
   >Mer information finns i [Konfigurera komponenter i designläge](/help/sites-authoring/default-components-designmode.md).

1. Gå tillbaka till läget **[!UICONTROL Edit]** genom att klicka på pennikonen i [!UICONTROL Sidekick].
1. Dra **[!UICONTROL Dynamic Media]**- eller **[!UICONTROL Interactive Media]**-komponenten från **[!UICONTROL Other]**-gruppen i sidesparken till sidan på önskad plats.
1. Klicka på **[!UICONTROL Edit]** för att öppna komponenten.
1. [Redigera ](#dynamic-media-component) komponenterna efter behov och klicka  **[!UICONTROL OK]** för att spara ändringarna.

## Dynamic Media Components {#dynamic-media-components}

[!UICONTROL Dynamic Media] och  [!UICONTROL Interactive Media] är tillgängliga i  [!UICONTROL Sidekick] under  **[!UICONTROL Dynamic Media.]** Du använder  **[!UICONTROL Interactive Media]** komponenten för alla interaktiva resurser som interaktiv video, interaktiva bilder eller karuselluppsättningar. Använd komponenten **[!UICONTROL Dynamic Media]** för alla andra dynamiska mediekomponenter.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste markeras i designläge innan du använder. [När de har gjorts tillgängliga i designläge](/help/sites-authoring/default-components-designmode.md) kan du lägga till komponenterna på sidan på samma sätt som andra AEM.

### Dynamic Media-komponent {#dynamic-media-component}

Dynamic Media-komponenten är smart - beroende på om du lägger till en bild eller en video finns det olika alternativ. Komponenten har stöd för bildförinställningar, bildbaserade visningsprogram som bilduppsättningar, snurra, blandade medieuppsättningar och video. Dessutom är visningsprogrammet responsivt. Skärmstorleken ändras alltså automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-baserade.

>[!NOTE]
>
>När du lägger till komponenten [!UICONTROL Dynamic Media] och **[!UICONTROL Dynamic Media Settings]** är tom eller du inte kan lägga till en resurs på rätt sätt bör du kontrollera följande:
>
>* Du har [aktiverat Dynamic Media](/help/assets/config-dynamic.md). Dynamic Media är inaktiverat som standard.
>* Bilden har en pyramidformad fil. Bilder som importerats innan dynamiska medier har aktiverats har ingen pyramiddiff-fil.

>



#### När du arbetar med bilder {#when-working-with-images}

Med [!UICONTROL Dynamic Media]-komponenten kan du lägga till dynamiska bilder, inklusive bilduppsättningar, snurra och blandade medieuppsättningar. Du kan zooma in, zooma ut och, om tillämpligt, vrida en bild i en snurra eller välja en bild från en annan typ av uppsättning.

Du kan också konfigurera visningsförinställningen, bildförinställningen eller bildformatet direkt i komponenten. Om du vill göra en bild responsiv kan du antingen ange brytpunkter eller använda en responsiv bildförinställning.

![chlimage_1-72](assets/chlimage_1-72a.png)

Du kan redigera följande Dynamic Media-inställningar genom att klicka på **[!UICONTROL Edit]** i komponenten och sedan på fliken **[!UICONTROL Dynamic Media Settings]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Som standard är Dynamic Media-bildkomponenten adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten på fliken **[!UICONTROL Advanced]** med egenskaperna **[!UICONTROL Width]** och **[!UICONTROL Height]**.

**[!UICONTROL Viewer preset]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

Det här är det enda tillgängliga alternativet om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar. De visningsförinställningar som visas är också smarta - endast relevanta visningsprogramförinställningar visas.

**[!UICONTROL Image preset]** - Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns kan du behöva göra den synlig. Se [Hantera bildförinställningar](/help/assets/managing-image-presets.md). Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL Image Modifiers]** - Du kan ändra bildeffekter genom att ange ytterligare bildkommandon. Dessa beskrivs i [Hantera bildförinställningar](/help/assets/managing-viewer-presets.md) och [Kommandoreferens](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL Breakpoints]** - Om du använder den här resursen på en responsiv webbplats måste du lägga till sidbrytpunkter. Bildbrytpunkter måste avgränsas med kommatecken (,). Det här alternativet fungerar när ingen höjd eller bredd har definierats i en bildförinställning.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

Du kan redigera följande [!UICONTROL Advanced Settings] genom att klicka på **[!UICONTROL Edit]** i komponenten.

**[!UICONTROL Title]** - Ändra bildens titel.

**[!UICONTROL Alt Text]** - Lägg till en titel i bilden för de användare som har inaktiverat grafik.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL URL, Open in]** - Du kan ställa in en resurs från för att öppna en länk. Ange **[!UICONTROL URL]** och **[!UICONTROL Open in]** för att ange om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

**[!UICONTROL Width and Height]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar dessa värden tomma anpassas resursen.

#### När du arbetar med video {#when-working-with-video}

Använd [!UICONTROL Dynamic Media]-komponenten för att lägga till dynamisk video på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

![chlimage_1-74](assets/chlimage_1-74a.png)

Du kan redigera följande [!UICONTROL Dynamic Media Settings] genom att klicka på **[!UICONTROL Edit]** i komponenten.

>[!NOTE]
>
>Som standard är videokomponenten i Dynamic Media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten med **[!UICONTROL Width]** och **[!UICONTROL Height]** på fliken **[!UICONTROL Advanced]**.

**[!UICONTROL Viewer preset]** - Välj en befintlig förinställning för visningsprogrammet för video i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

Du kan redigera följande [!UICONTROL Advanced]-inställningar genom att klicka på **[!UICONTROL Edit]** i komponenten.

**[!UICONTROL Title]** - Ändra videons titel.

**[!UICONTROL Width and Height]** - Ange värdet i pixlar om du vill att videon ska ha en fast storlek. Om du lämnar dessa värden tomma blir de anpassningsbara.

#### Så här levererar du säker video {#how-to-delivery-secure-video}

När du installerar [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480) i AEM 6.2 kan du kontrollera om en video levereras via en säker SSL-anslutning (HTTPS) eller en osäker anslutning (HTTP). Som standard ärvs videoleveransprotokollet automatiskt från inbäddningswebbsidans protokoll. Om webbsidan läses in via HTTPS levereras videon också via HTTPS. Och tvärtom, om webbsidan finns på HTTP, levereras videon via HTTP. I de flesta fall är standardbeteendet bra och du behöver inte göra några konfigurationsändringar. Du kan dock åsidosätta det här standardbeteendet genom att lägga till `VideoPlayer.ssl=on` i slutet av en URL-sökväg eller i listan med andra parametrar för visningsprogramkonfiguration i ett inbäddat kodfragment, för att framtvinga en säker videoleverans.

Mer information om säker videoleverans och användning av konfigurationsattributet `VideoPlayer.ssl` i URL-sökvägen finns i [Säker videoleverans](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) i referenshandboken för visningsprogram. Förutom Video Viewer finns säker videoutgång för visningsprogram för Mixed Media och Interactive Video.

### Interaktiv mediakomponent {#interactive-media-component}

Komponenten Interactive Media är till för de resurser som har interaktivitet i dem, till exempel hotspot-områden eller bildscheman. Om du har en interaktiv bild, interaktiv video eller karusellbanderoll använder du komponenten **[!UICONTROL Interactive Media]**.

Komponenten [!UICONTROL Interactive Media] är smart - beroende på om du lägger till en bild eller en video har du olika alternativ. Dessutom är visningsprogrammet responsivt. Skärmstorleken ändras alltså automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-baserade.

![chlimage_1-75](assets/chlimage_1-75a.png)

Du kan redigera följande **[!UICONTROL General]**-inställningar genom att klicka på **[!UICONTROL Edit]** i komponenten.

**[!UICONTROL Viewer preset]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Förinställningar för visningsprogram måste publiceras innan de kan användas. Se Hantera förinställningar för visningsprogram.

**[!UICONTROL Title]** - Ändra videons titel.

**[!UICONTROL Width and Height]** - Ange värdet i pixlar om du vill att videon ska ha en fast storlek. Om du lämnar dessa värden tomma blir de anpassningsbara.

Du kan redigera följande **[!UICONTROL Add To Cart]**-inställningar genom att klicka på **[!UICONTROL Edit]** i komponenten.

**[!UICONTROL Show Product Asset]** - Som standard är det här värdet valt. Produktresursen visar en bild av produkten enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktresursen.

**[!UICONTROL Show Product Price]** - Som standard är det här värdet valt. Produktpriset visar priset för artikeln enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktpriset.

**[!UICONTROL Show Product Form]** - Som standard är det här värdet inte markerat. Produktformuläret innehåller alla produktvarianter som storlek och färg. Avmarkera kryssrutan om du inte vill visa produktvarianterna.
