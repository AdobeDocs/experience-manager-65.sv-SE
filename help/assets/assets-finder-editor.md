---
title: Skapa och konfigurera sidor för Resursredigeraren
description: Lär dig hur du skapar anpassade sidor i Resursredigeraren och redigerar flera resurser samtidigt.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Skapa och konfigurera sidor för Resursredigeraren {#creating-and-configuring-asset-editor-pages}

I det här dokumentet beskrivs följande:

* Därför ska du skapa anpassade resursredigeringssidor.
* Skapa och anpassa resursredigeringssidor, dvs. WCM-sidor, där du kan visa och redigera metadata samt utföra åtgärder på resursen.
* Så här redigerar du flera resurser samtidigt.

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 OOTB samples. -->

>[!NOTE]
>
>Resursresurs är tillgänglig som en referensimplementering med öppen källkod. Se Kommentarer för [resursdelning](https://adobe-marketing-cloud.github.io/asset-share-commons/). Det stöds inte officiellt.

## Varför skapa och konfigurera sidor i Resursredigeraren? {#why-create-and-configure-asset-editor-pages}

Digital Asset Management används i allt fler scenarier. När man går över från en småskalig lösning för en liten användargrupp yrkesutbildade användare - till exempel fotografer eller taxonomier - till större och mer mångsidiga användargrupper - t.ex. affärsanvändare, WCM-författare, journalister osv. - kan det kraftfulla användargränssnittet i Adobe Experience Manager (AEM) Assets för professionella användare tillhandahålla för mycket information och intressenter börja begära specifika användargränssnitt eller applikationer för att få tillgång till de digitala resurser som är relevanta för dem.

Dessa resurscentrerade program kan vara enkla fotogallerier i ett intranät där medarbetarna kan ladda upp bilder från mässor eller ett presscenter på en offentlig webbplats, till exempel i Geometrixx. Tillgångscentrerade tillämpningar kan även omfatta kompletta lösningar som kundvagnar, kassor och verifieringsprocesser.

Att skapa ett resurscentrerat program blir i stor utsträckning en konfigurationsprocess som inte kräver kodning, bara kunskap om användargrupper och deras behov samt kunskap om de metadata som används. Resurscentrerade program som skapats med AEM Resurser kan utökas: med måttlig kodningsansträngning kan återanvändbara komponenter för att söka, visa och ändra resurser skapas.

Ett resurscentrerat program i AEM består av en tillgångsredigeringssida, som kan användas för att få en detaljerad vy över en viss resurs. På en resursredigeringssida kan du även redigera metadata, förutsatt att användaren som använder resursen har de behörigheter som krävs.

## Skapa och konfigurera en resursdelningssida {#creating-and-configuring-an-asset-share-page}

Du kan anpassa DAM Finder-funktionen och skapa sidor som har alla funktioner du behöver, som kallas resursdelningssidor. Om du vill skapa en ny resursdelningssida lägger du till sidan med hjälp av mallen Geometrixx Asset Share och sedan anpassar du de åtgärder som användare kan utföra på den sidan, avgör hur tittarna ser resurserna och avgör hur användarna kan skapa sina frågor.

Här är några exempel på hur du kan skapa en anpassad resursdelningssida:

* Presscenter för journalister
* Bildsökningsmotor för interna företagsanvändare
* Bilddatabas för webbplatsanvändare
* Media Tagging Interface for metadata editors

### Skapa en resursdelningssida {#creating-an-asset-share-page}

Om du vill skapa en ny resursdelningssida kan du antingen skapa den när du arbetar på webbplatser eller från den digitala resurshanteraren.

>[!NOTE]
>
>När du skapar en resursdelningssida från **Nytt** i den digitala resurshanteraren skapas som standard en resursvisare och resursredigerare automatiskt.

Så här skapar du en ny resursdelningssida i **webbplatskonsolen** :

1. Gå till den plats där du vill skapa en resursdelningssida på fliken **Webbplatser** och klicka på **Ny**.

1. Markera sidan **Resursresurs** och klicka på **Skapa**. Den nya sidan skapas och resursdelningssidan visas på fliken **Webbplatser** .

![dam8](assets/dam8.png)

Grundsidan som skapas med hjälp av mallen för resursdelning i Geometrixx DAM ser ut så här:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

Om du vill anpassa sidan Resursdelning använder du element från sidosparken och redigerar även egenskaper för frågebyggaren. Sidan **Geometrixx Press Center** är en anpassad version av en sida som är baserad på den här mallen:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

Så här skapar du en ny resursdelningssida via den digitala resurshanteraren:

1. I den digitala resurshanteraren väljer du **Ny resurs i** Ny **resurs**.
1. Ange namnet på resursdelningssidan i **Rubrik**. Om du vill kan du ange ett namn för URL:en.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Dubbelklicka på resursdelningssidan för att öppna den och konfigurera sidan.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   När du skapar en resursdelningssida från **Nytt** skapas som standard ett resursvisningsprogram och en resursredigerare automatiskt.

#### Anpassa funktionsmakron {#customizing-actions}

Du kan avgöra vilka åtgärder användare kan utföra på valda digitala resurser från ett urval av fördefinierade åtgärder.

Så här lägger du till åtgärder på sidan Resursresurs:

1. På sidan Resursresurs som du vill anpassa klickar du på **Åtgärder** i sidosparken.

Följande åtgärder är tillgängliga:

![assetshare2](assets/assetshare2.bmp)

| Åtgärd | Beskrivning |
|---|---|
| [!UICONTROL Ta bort åtgärd] | Användare kan ta bort de markerade resurserna. |
| [!UICONTROL Hämta åtgärd] | Tillåter användare att hämta valda resurser till sina datorer. |
| [!UICONTROL Ljuslådeåtgärd] | Sparar resurser i en&quot;ljuslåda&quot; där du kan utföra andra åtgärder på dem. Detta är praktiskt när du arbetar med resurser på flera sidor. Ljuslådan kan också användas som kundvagn för resurser. |
| [!UICONTROL Flytta åtgärd] | Användarna kan flytta resursen till en annan plats |
| [!UICONTROL Taggåtgärd] | Tillåter användare att lägga till taggar i markerade resurser |
| [!UICONTROL Visa resursåtgärd] | Öppnar resursen i tillgångsredigeraren för användarmanipulering. |

1. Dra lämplig åtgärd till området **Åtgärder** på sidan. När du gör det skapas en knapp som används för att utföra åtgärden.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Bestämma hur sökresultat visas {#determining-how-search-results-are-presented}

Du bestämmer hur resultaten ska visas i en fördefinierad lista med objektiv.

Så här ändrar du hur sökresultat visas:

1. Klicka på Sök på sidan Resursresurs som du vill anpassa.

![chlimage_1](assets/assetshare3.png)

1. Dra lämplig lins till sidans övre mitt. I Press Center finns objekten redan tillgängliga. Användarna kan visa sökresultaten genom att trycka på motsvarande objektivikon.

Följande linser är tillgängliga:

| Lins | Beskrivning |
|---|---|
| **[!UICONTROL List Lens]** | Visar resurserna i en lista med detaljer. |
| **[!UICONTROL Mosaik]** | Presenterar resurser på ett mosaiskt sätt. |

#### Mosaik {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Anpassa Query Builder {#customizing-the-query-builder}

Med frågebyggaren kan du ange söktermer och skapa innehåll för sidan Resursdelning. När du redigerar frågebyggaren kan du även bestämma hur många sökresultat som ska visas per sida, vilken resursredigerare som ska öppnas när du dubbelklickar på en resurs, vilken sökväg frågan söker i och anpassar nodtyper.

Så här anpassar du frågeverktyget:

1. På sidan Resursresurs som du vill anpassa klickar du på **Redigera** i frågeverktyget. Fliken **Allmänt** öppnas som standard.
1. Välj antalet resultat per sida, sökvägen till resursredigeraren (om du har en anpassad resursredigerare) och åtgärdstiteln.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Klicka på fliken **Banor** . Ange en eller flera sökvägar som sökningen ska köras på. Dessa sökvägar skrivs över om användaren använder Banor-predikatet.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Ange en annan nodtyp, om du vill.

1. I URL **-fältet i** Query Builder kan du åsidosätta eller omsluta frågebyggaren och ange de nya webbadresserna med den befintliga frågebyggarkomponenten. I fältet **Feed-URL** kan du även åsidosätta feed-URL:en.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. I fältet **Text** anger du den text som du vill ska visas för resultat och sidnummer. Klicka på **OK** när du är klar med ändringarna.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Lägg till predikat {#adding-predicates}

AEM Resurser innehåller ett antal predikat som du kan lägga till på sidan Resursdelning. På så sätt kan användarna begränsa sökningarna ytterligare. I vissa fall kan de åsidosätta en frågebyggarparameter (till exempel parametern Path).

Så här lägger du till predikat:

1. På sidan Resursresurs som du vill anpassa klickar du på **Sök**.

![assetshare3](assets/assetshare3.png)

1. Dra lämpliga predikat till sidan Resursresurs under frågebyggaren. Då skapas rätt fält.

![assetshare4](assets/assetshare4.bmp)

Följande predikat är tillgängliga:

| Förutse | Beskrivning |
|---|---|
| **[!UICONTROL Datumpredikat]** | Tillåter användare att söka efter resurser som har ändrats före och efter vissa datum. |
| **[!UICONTROL Alternativ - predikat]** | Webbplatsägaren kan ange en egenskap att söka efter (som i egenskapspredikatet, till exempel cq:tags) och ett innehållsträd att fylla i alternativen från (till exempel taggträdet). Då genereras en lista med alternativ där användarna kan välja de värden (taggar) som den valda egenskapen (taggegenskap) ska ha. Med det här predikatet kan du skapa listkontroller som listan över taggar, filtyper, bildorienteringar och så vidare. Det passar bra för en fast uppsättning alternativ. |
| **[!UICONTROL Banförutsägelse]** | Tillåter användare att definiera sökvägen och undermapparna, om så önskas. |
| **[!UICONTROL Egenskapspredikat]** | Webbplatsägaren anger en egenskap att söka efter, t.ex. tiff:ImageLength, och användaren kan sedan ange ett värde, t.ex. 800. Då returneras alla bilder som är 800 pixlar höga. Användbart predikat om egenskapen kan ha godtyckliga värden. |

Mer information finns i [predikatet Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. Dubbelklicka på predikatet om du vill konfigurera det ytterligare. När du t.ex. öppnar Förutsägande av sökväg måste du tilldela rotsökvägen.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)

## Skapa och konfigurera en resursredigeringssida {#creating-and-configuring-an-asset-editor-page}

Du anpassar resursredigeraren för att avgöra hur användare kan visa och redigera digitala resurser. För att göra detta skapar du en ny resursredigeringssida och anpassar sedan vyerna och de åtgärder som användarna kan utföra på den sidan.

>[!NOTE]
>
>Om du vill lägga till anpassade fält i DAM-resursredigeraren lägger du till nya cq:Widget-noder i `/apps/dam/content/asseteditors.`

### Skapa en resursredigeringssida {#creating-the-asset-editor-page}

När du skapar sidan Resursredigerare kan det vara bra att skapa sidan direkt under sidan Resursdelning.

Så här skapar du en resursredigeringssida:

1. Gå till den plats där du vill skapa en resursredigeringssida på fliken **Webbplatser** och klicka på **Ny**.
1. Välj **Geometrixx Resursredigerare** och klicka på **Skapa**. Den nya sidan skapas och sidan visas på fliken **Webbplatser** .

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

Grundsidan som skapas med hjälp av mallen Geometrixx Asset Editor ser ut så här:

![assetshare5](assets/assetshare5.bmp)

Om du vill anpassa resursredigeringssidan använder du element från sidosparken. Sidan Resursredigeraren som öppnas från **Geometrixx Press Center** är en anpassad version av en sida som är baserad på den här mallen:

![assetshare6](assets/assetshare6.bmp)

#### Ange att en resursredigerare ska öppnas från en resursdelningssida {#setting-which-asset-editor-opens-from-an-asset-share-page}

När du har skapat den anpassade resursredigeringssidan måste du se till att när du dubbelklickar på resurser som den anpassade resursresursen du skapade öppnar resurserna på den anpassade redigeringssidan.

Så här anger du sidan Resursredigeraren:

1. På sidan Resursresurs klickar du på **Redigera** bredvid Frågebyggaren.

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. Klicka på fliken **Allmänt** om den inte redan är markerad.

1. I fältet **Sökväg till resursredigeraren** anger du sökvägen till den resursredigerare som du vill att sidan Resursdelning ska öppna resurser i och klickar på **OK**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### Lägg till komponenterna i Resursredigeraren {#adding-asset-editor-components}

Du bestämmer vilken funktionalitet en resursredigerare har genom att lägga till komponenter på sidan.

Så här lägger du till komponenterna för redigering av resurser:

1. På sidan Resursredigeraren som du vill anpassa väljer du **Resursredigeraren** i sidosparken. Alla tillgängliga komponenterna för redigeringsprogrammet för resurser visas.

>[!NOTE]
>
>Vad du kan anpassa beror på vilka komponenter som är tillgängliga. Om du vill aktivera komponenter går du till designläge och markerar de komponenter som du behöver ha aktiverade.

1. Dra komponenterna från sidosparken till resursredigeraren och gör eventuella ändringar i komponentdialogrutorna. Komponenterna beskrivs i följande tabell och beskrivs i de detaljerade instruktionerna som följer.

>[!NOTE]
>
>När du utformar resursredigeringssidan skapar du komponenter som är skrivskyddade eller redigerbara. Användarna vet att ett fält kan redigeras om en bild av en penna visas i den komponenten. Som standard är de flesta komponenter skrivskyddade.

| Komponent | Beskrivning |
|---|---|
| **[!UICONTROL Metadataformulär]och[!UICONTROL metadatatextfält]** | Gör att du kan lägga till ytterligare metadata för en resurs och utföra en åtgärd, som att skicka, för den resursen. |
| **[!UICONTROL Deltillgångar]** | Gör att du kan anpassa underresurser. |
| **Taggar** | Tillåter användare att markera och lägga till taggar i en resurs. |
| **[!UICONTROL Miniatyrbild]** | Visar en miniatyrbild av resursen, dess filnamn och låter dig lägga till en alternativ text. Du kan även lägga till resursredigeringsåtgärder här. |
| **[!UICONTROL Titel]** | Visar resursens titel, som kan anpassas. |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### Metadataformulär och textfält - Konfigurera komponenten Visa metadata {#metadata-form-and-text-field-configuring-the-view-metadata-component}

Metadataformuläret är ett formulär som innehåller en start- och slutåtgärd. däremellan anger du **textfält** . Mer information om hur du arbetar med formulär finns i [Formulär](/help/sites-authoring/default-components-foundation.md#form-component) .

1. Skapa en startåtgärd genom att klicka på **Redigera** i formulärets startdel. Om du vill kan du ange en Box-titel. Som standard är rutans rubrik **Metadata**. Markera kryssrutan Klientvalidering om du vill att Java-script-klientkoden ska genereras för validering.

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. Skapa en slutåtgärd genom att klicka på **Redigera** i formulärets slutområde. Du kan till exempel skapa en **Skicka** -knapp som tillåter användare att skicka metadataändringar. Du kan också lägga till en **återställningsknapp** som återställer metadata till det ursprungliga läget.

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. Dra metadatatextfält mellan **Formulärstart** och **Formulärslut** till formuläret. Användare fyller i metadata i dessa textfält som de kan skicka eller slutföra en annan åtgärd på.

1. Dubbelklicka på fältnamnet, till exempel **Titel** , för att öppna metadatafältet och göra ändringar. På fliken **Allmänt** i fönstret **Redigera komponent** definierar du namnutrymmet och fältetiketten samt typ, till exempel `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

Mer information om hur du ändrar namnutrymmen i metadataformuläret finns i [Anpassa och utöka AEM-resurser](/help/assets/extending-assets.md) .

1. Klicka på fliken **Begränsningar** . Här kan du välja om ett fält är obligatoriskt och vid behov lägga till begränsningar.

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. Klicka på fliken **Visa** . Här kan du ange en ny bredd och ett nytt antal rader för metadatafältet. Markera kryssrutan **Fältet är skrivskyddat** om du vill tillåta användare att redigera metadata.

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

Följande är ett exempel på ett metadataformulär med olika fält:

![chlimage_1-162](assets/chlimage_1-390.png)

På sidan Resursredigeraren kan användare sedan ange värden i metadatafälten (om de är redigerbara) och utföra slutåtgärden (till exempel skicka ändringarna).

#### Deltillgångar {#sub-assets}

I delresurskomponenten kan du visa och välja delresurser. Du kan bestämma vilka namn som ska visas under [huvudresursen](/help/assets/assets.md#what-are-digital-assets) och underresurserna.

![screen_shot_2012-04-23at24025pm](assets/screen_shot_2012-04-23at24025pm.png)

Dubbelklicka på delresurskomponenten för att öppna dialogrutan med delresurser där du kan ändra rubrikerna för huvudresursen och eventuella delresurser. Standardvärdena visas under motsvarande fält.

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

Följande är ett exempel på en ifylld delresurskomponent:

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

Om du till exempel markerar en underresurs bör du tänka på hur komponenten visar rätt sida och ruttiteln ändras från underresurser till syskon.

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### Taggar {#tags}

Komponenten Tags är en komponent där användare kan tilldela befintliga taggar till en resurs, vilket gör det enklare att ordna och hämta den senare. Du kan göra den här komponenten skrivskyddad, så användarna kan inte lägga till taggar, utan bara visa dem.

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

Dubbelklicka på taggkomponenten för att öppna dialogrutan Taggar där du kan ändra titeln från Taggar, om du vill, och där du kan välja de tilldelade namnutrymmena. Om du vill göra det här fältet redigerbart avmarkerar du kryssrutan **[!UICONTROL Dölj redigering]** . Som standard är taggar redigerbara.

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

Om användare kan redigera taggar kan de klicka på pennan för att lägga till taggar genom att välja dem i listrutan Taggar.

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

Följande är en ifylld tagg-komponent:

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### Miniatyrbild {#thumbnail}

Miniatyrkomponenten är den plats där den valda miniatyrbilden visas (för många av formaten extraheras miniatyrbilden automatiskt). Komponenten visar dessutom filnamnet och de [åtgärder som du kan ändra](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

Dubbelklicka på miniatyrkomponenten för att öppna dialogrutan med miniatyrbilder där du kan ändra alternativ text. Som standard används miniatyrbilden för alternativ text som **Klicka för att hämta** resursen.

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

Följande är ett exempel på en fylld miniatyrkomponent:

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### Titel {#title}

Rubrikkomponenten visar resursens namn och en beskrivning.

![chlimage_1-163](assets/chlimage_1-391.png)

Som standard är den i skrivskyddat läge, så användare kan inte redigera den. Dubbelklicka på komponenten och avmarkera kryssrutan **Dölj redigeringsknapp** om du vill göra den redigerbar. Ange dessutom en titel för flera resurser.

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

Om du kan redigera titeln kan du lägga till en titel och en beskrivning genom att klicka på pennan för att öppna fönstret **Resursegenskaper** . Dessutom kan du aktivera och inaktivera resursen genom att välja datum och tid.

När användare redigerar titeln genom att klicka på pennikonen kan de ändra **titel**, **beskrivning** och ange **På** - och **Av-tider** för att aktivera och inaktivera resursen.

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

Följande är ett exempel på en ifylld Title-komponent:

![chlimage_1-164](assets/chlimage_1-392.png)

#### Lägg till resursredigeringsåtgärder {#adding-asset-editor-actions}

Du kan avgöra vilka åtgärder användare kan utföra på valda digitala resurser från ett urval av fördefinierade åtgärder.

Så här lägger du till åtgärder på sidan Resursredigeraren:

1. På sidan Resursredigeraren som du vill anpassa klickar du på **Resursredigeraren** i sidosparken.

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

Följande åtgärder är tillgängliga:

| Åtgärd | Beskrivning |
|---|---|
| [!UICONTROL Hämta] | Tillåter användare att hämta valda resurser till sina datorer. |
| [!UICONTROL Redigerare] | Tillåter användare att redigera en bild (interaktiv redigering) |
| [!UICONTROL Ljuslåda] | Sparar resurser i en&quot;ljuslåda&quot; där du kan utföra andra åtgärder på dem. Detta är praktiskt när du arbetar med resurser på flera sidor. |
| [!UICONTROL Låsning] | Tillåter användare att låsa en resurs. Den här funktionen är inte aktiverad som standard och måste aktiveras i komponentlistan. |
| [!UICONTROL Referenser] | Klicka här för att visa på vilka sidor resursen används. |
| [!UICONTROL Versionshantering] | Gör att du kan skapa och återställa versioner av en resurs. |

1. Dra lämplig åtgärd till området **Åtgärder** på sidan. När du gör det skapas en knapp som används för att utföra åtgärden.

![chlimage_1-165](assets/chlimage_1-393.png)

## Flera redigeringsresurser med sidan Resursredigeraren {#multi-editing-assets-with-the-asset-editor-page}

Med AEM Assets kan du ändra flera resurser samtidigt. När du har valt resurser kan du ändra deras:

* Taggar
* Metadata

Så här gör du om du vill redigera flera resurser på sidan Resursredigeraren:

1. Öppna sidan Geometrixx **Press Center** :
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. Välj resurser:

   * i Windows: `Ctrl + click` varje tillgång.
   * på Mac: `Cmd + click` varje tillgång.
   Så här väljer du en rad resurser: klicka på den första resursen och sedan på `Shift + click` den sista resursen.

1. Klicka på **Redigera metadata** i fältet **Åtgärder** (vänster del av sidan).
1. Sidan Geometrixx **Press Center Asset Editor** öppnas på en ny flik. Resursernas metadata visas enligt följande:

   * En tagg som inte gäller för alla resurser utan bara för ett fåtal, visas i kursiv stil.
   * En tagg som gäller för alla resurser visas med ett vanligt teckensnitt.
   * Andra metadata än taggar: värdet för fältet visas bara om det är samma för alla markerade resurser.

1. Klicka på **Hämta** för att hämta en zip-fil som innehåller resursens ursprungliga återgivningar.
1. Klicka på pennikonen bredvid fältet **Taggar** för att redigera taggarna:

   * En tagg som inte gäller för alla resurser, men bara för ett fåtal har en grå bakgrund.
   * En tagg som gäller för alla resurser har en vit bakgrund.
   Du kan:

   * Klicka på **x** -ikonen för att ta bort taggen för alla resurser.
   * Klicka på **+** -ikonen för att lägga till taggen i alla resurser.
   * Klicka på **pilen** och välj en tagg för att lägga till en ny tagg till alla resurser.
   Klicka på **OK** för att skriva ändringarna i formuläret. Rutan bredvid fältet **Taggar** markeras automatiskt.

1. Redigera beskrivningsfältet. Ange det till exempel till:

   `This is a common description`

   När ett fält redigeras skrivs de befintliga värdena för de valda resurserna över när formuläret skickas.

   Obs! kryssrutan bredvid fältet markeras automatiskt när fältet redigeras.

1. Klicka på **Uppdatera metadata** för att skicka formuläret och spara ändringarna för alla resurser.

   Obs! endast markerade metadata ändras.
