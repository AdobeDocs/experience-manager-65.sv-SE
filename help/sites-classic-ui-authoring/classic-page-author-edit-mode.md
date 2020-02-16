---
title: Komponenter för sidredigering
seo-title: Komponenter för sidredigering
description: Komponenterna är tillgängliga när du redigerar en sida på fliken Komponenter i sidosparken och i Infoga ny komponentväljare (när du dubbelklickar i området Dra komponenter eller resurser här).
seo-description: Komponenterna är tillgängliga när du redigerar en sida på fliken Komponenter i sidosparken och i Infoga ny komponentväljare (när du dubbelklickar i området Dra komponenter eller resurser här).
uuid: c353073d-d4d1-4529-b8bd-d0ca302cc9a0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9aa0521f-f321-42e9-b022-7ff968a36212
docset: aem65
translation-type: tm+mt
source-git-commit: bec587e3722c4c2e5aebd2579a2a7acbf807587a

---


# Komponenter för sidredigering{#components-for-page-authoring}

Följande komponenter är avsedda att användas vid utveckling av innehåll för en standardwebbsida. De utgör en delmängd av de komponenter som finns tillgängliga direkt för en standardinstallation av AEM.

Vissa är omedelbart tillgängliga via sidbrytaren, andra är också tillgängliga genom att aktivera/inaktivera dem i [designläge](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md) .

>[!CAUTION]
>
>I det här avsnittet behandlas endast komponenter som finns i en färdig AEM-installation.
>
>Beroende på vilken instans du har kan du ha utvecklat anpassade komponenter explicit för dina behov. De kan till och med ha samma namn som vissa av de komponenter som beskrivs här.

Komponenterna är tillgängliga när du [redigerar en sida](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) från fliken **Komponenter** i sidosparken och **Infoga ny komponent** (när du dubbelklickar i området **Dra komponenter eller resurser här** ).

Du kan markera en komponent och dra den till önskad plats på sidan och sedan [redigera innehåll och egenskaper](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties).

Komponenterna sorteras efter olika kategorier (komponentgrupper), inklusive (för sidredigering):

* [Allmänt](#general): Innehåller grundläggande komponenter som text, bilder, tabeller, diagram och så vidare.
* [Kolumner](#columns): Innehåller komponenter som behövs för att ordna innehållets layout.
* [Formulär](#formgroup): Innehåller alla komponenter som behövs för att skapa ett formulär.

## Allmänt {#general}

De allmänna komponenterna är de grundläggande komponenter som du använder för att skapa innehåll.

### Kontoobjekt {#account-item}

Du kan definiera en länk med rubrik och beskrivning.

![](do-not-localize/chlimage_1-2.png)

### Adaptiv bild {#adaptive-image}

Med komponenten Adaptive Image Foundation genereras bilder som är storleksanpassade för att passa det fönster där webbsidan öppnas. Om du vill använda komponenten anger du en bildresurs från filsystemet eller DAM. När webbsidan öppnas hämtar webbläsaren en kopia av bilden som har ändrat storlek så att den passar för det aktuella fönstret.

Följande egenskaper kan avgöra fönstrets storlek:

* Enhetsskärm: Mobila enheter visar vanligtvis webbsidor så att de sträcker sig över hela skärmen.
* Webbläsarfönsterstorlek: Användare av bärbara och stationära datorer kan ändra storlek på webbläsarfönster.

Komponenten genererar till exempel en liten bild när webbsidan öppnas på en mobiltelefon och en medelstor bild när den öppnas på en surfplatta. På en bärbar dator skapar komponenten en stor bild när sidan öppnas i en maximerad webbläsare. När webbläsarens storlek ändras för att passa en del av skärmen anpassas komponenten genom att en mindre bild visas och vyn uppdateras.

#### Bildformat som stöds {#supported-image-formats}

Du kan använda bildfiler med följande filnamnstillägg med komponenten Adaptive Image:

* .jpg
* .jpeg
* .png
* .gif **

>[!CAUTION]
>
>** Animerade .gif-filer stöds inte i AEM för adaptiva återgivningar.

#### Bildstorlekar och -kvalitet {#images-sizes-and-quality}

I följande tabell visas bredden på bilden som genereras för den angivna visningsrutans bredd. Höjden på den genererade bilden beräknas för att bibehålla en konstant proportion och inget mellanrum inträffar inuti bildkanten. Beskärning kan användas för att undvika mellanrum.

När bilden är en JPEG-bild kan visningsrutans storlek även påverka JPEG-kvaliteten. Följande JPEG-egenskaper är möjliga:

* Låg (0,42)
* Medel (0,82)
* Hög (1,00)

| Breddintervall för visningsruta (pixlar) | Bildbredd (pixlar) | JPEG-kvalitet | Målenhetstyp |
|---|---|---|---|
| width &lt;= 319 | 320 | låg |  |
| width = 320 | 320 | medium | Mobiltelefon (stående) |
| 320 &lt; bredd &lt; 481 | 480 | medium | Mobiltelefon (liggande) |
| 480 &lt; bredd &lt; 769 | 476 | hög | Tablet PC (stående) |
| 768 &lt; bredd &lt; 1025 | 620 | hög | Tablet (liggande) |
| width &lt;= 1025 | full (ursprunglig storlek) | hög | Skrivbord |

#### Egenskaper {#properties}

I dialogrutan kan du redigera egenskaper för din instans av komponenten Adaptiv bild, som många är gemensamma för den Image-komponent som den baseras på. Egenskaperna finns på två flikar:

* **Bild**

   * **Bild** Dra en bild från innehållssökaren eller klicka för att öppna ett bläddringsfönster där du kan läsa in en bild. När bilden har lästs in kan du beskära bilden, rotera den eller ta bort den. Om du vill zooma in och ut i bilden använder du bildfältet under bilden (ovanför knapparna OK och Avbryt)

   * **Beskär** en bild. Dra kanten för att beskära bilden.

   * **Rotera** Klicka på Rotera upprepade gånger tills bilden roteras som du vill.

   * **Rensa** Ta bort den aktuella bilden.

* **Avancerat**

   * **Title** The Adaptive Image component does not use this property.

   * **Alt-text** Den alternativa texten som ska användas för bilden.

   * **Länk till** komponenten Adaptiv bild använder inte den här egenskapen.

   * **Beskrivning** Komponenten Adaptiv bild använder inte den här egenskapen.

#### Utöka den adaptiva bildkomponenten {#extending-the-adaptive-image-component}

Mer information om hur du anpassar komponenten Adaptiv bild finns i [Förstå komponenten](/help/sites-developing/responsive.md#using-adaptive-images)Adaptiv bild.

### Carousel {#carousel}

Med Carousel-komponenten kan du visa bilder som är kopplade till enskilda sidor:

* en åt gången
* under en kort tid
* i den ordning du anger
* med en tidsfördröjning som du anger

Med klickbara kontroller kan användaren även bläddra igenom de visade sidorna i realtid, vid behov. Om du klickar på den sidbild som är synlig kommer du till den sidan. Carousel fungerar med andra ord som navigeringskontroll.

#### Egenskaper {#properties-1}

Dessa finns på två flikar:

* **Carousel** Här anger du hur karusellen fungerar:

   * Uppspelningshastighet Tiden i millisekunder innan nästa bild visas.
   * Övergångstid i millisekunder för övergången mellan två bildrutor.
   * Styr StilOlika alternativ finns på en listruta. Exempel: Föregående/Nästa-knappar, Överst till höger-växlar.

* **Lista** Här anger du hur sidorna ska inkluderas i Carousel:

   * **Skapa en lista med hjälp**Det finns flera sätt att skapa en sidlista - Underordnade sidor, Fast lista, Sök eller Avancerad sökning (alla beskrivs nedan).
Observera, att oavsett vilken metod du väljer, så kommer den bild som visas i Carousel att visas på de sidor som finns med i listan. Om det inte finns någon bild för en viss sida under sidans Sidegenskaper, bör du koppla en bild till sidan innan du börjar, eftersom Carousel annars visar en tom (eller nästan tom) sida. Se [Redigera sidegenskaper](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).
Beroende på vilket objekt du väljer visas en ny panel:

      * **Alternativ för underordnade sidor**

         * **Överordnad sida** Ange en bana antingen manuellt eller med väljaren. Lämna tomt om du vill använda den aktuella sidan som överordnad.
      * **Alternativ för fast lista**

         * **Sidor** Välj en lista med sidor. Använd `+` för att lägga till fler poster och upp-/nedknapparna för att justera ordningen.
      * **Alternativ för sökning**

         * **Börja i** Ange en startbana, antingen manuellt eller med väljaren.

         * **Sökfråga** Du kan ange en vanlig textsökfråga.
      * **Alternativ för avancerad sökning**

         * **Querybuilder-predikatnotation**Du kan ange en sökfråga med Querybuilder-predikatnotation. Du kan till exempel ange &quot;fulltext=Marketing&quot; om du vill att alla sidor med &quot;Marketing&quot; i innehållet ska visas i Carousel.
Se [QueryBuilder API](/help/sites-developing/querybuilder-api.md) för en fullständig diskussion om frågeuttryck och fler exempel.
   * **Ordna efter** Välj `jcr:title`, `jcr:created``cq:lastModified`eller `cq:template` från listrutan.

   * **Begränsa** det högsta antal objekt som du vill använda i Carousel; detta är valfritt.





>[!NOTE]
Du kan skapa en anpassad karusellkomponent för Adobe Experience Manager som visar digitala resurser i AEM DAM. Mer information finns i [Skapa anpassade Carousel-komponenter för Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/custom-carousel-components.html).

### Diagram {#chart}

Med diagramkomponenten kan du lägga till ett stapel-, linje- eller cirkeldiagram. AEM skapar ett diagram utifrån de data du anger. Du anger data genom att skriva direkt på fliken Data eller genom att kopiera och klistra in ett kalkylblad.

* **Data**

   * **Diagramdata** Ange diagramdata i CSV-format. I formatet för kommaseparerade värden används kommatecken (&quot;,&quot;) som fältavgränsare.

* **Avancerat**

   * **Diagramtyp** Välj från cirkeldiagram, linjediagram och stapeldiagram.

   * **Alternativ text** Alternativ text som visas i stället för diagrammet.

   * **Diagrammets** bredd i pixlar.

   * **Diagrammets höjd** i pixlar.

I följande exempel visas ett exempel på diagramdata följt av det resulterande stapeldiagrammet:

![chlimage_1-6](assets/chlimage_1-6.png) ![dc_chart_use](assets/dc_chart_use.png)

>[!NOTE]
Du kan skapa en anpassad AEM-diagramkontroll som visar data i AEM JCR. Mer information finns i [Visa Adobe Experience Manager-data i ett diagram](https://helpx.adobe.com/experience-manager/using/displaying-experience-manager-data-chart.html).

### Innehållsfragment {#content-fragment}

>[!CAUTION]
Den fullständiga funktionen för hantering av innehållsfragment är endast tillgänglig med det pekoptimerade användargränssnittet.
Komponenten Content Fragment kan visas i den klassiska användargränssnittets sidospark, men ytterligare funktioner är inte tillgängliga.

[Innehållsfragment](/help/sites-classic-ui-authoring/classic-page-author-content-fragments.md) skapas och hanteras som sidoberoende resurser. Du kan sedan använda dessa fragment och deras variationer när du redigerar innehållssidorna.

### Designimporteraren {#design-importer}

På så sätt kan du överföra en ZIP-fil som innehåller ett designpaket.

### Hämta {#download}

Komponenten Download skapar en länk på den valda webbsidan för att hämta en viss fil. Du kan antingen dra en resurs från Content Finder eller överföra en fil.

* **Hämta**

   * **Beskrivning** En kort beskrivning med nedladdningslänken.

   * **Filen** finns tillgänglig för hämtning på den slutliga webbsidan. Dra en resurs från innehållssökaren eller klicka på området för att överföra filen som ska vara tillgänglig för hämtning.

I följande exempel visas komponenten Download i Geometrixx:

![dc_download_use](assets/dc_download_use.png)

### External {#external}

Med den externa programintegrationskomponenten (**extern**) kan du bädda in externa program på din AEM-sida med hjälp av en iframe.

* **Extern**

   * **Målprogram**

      Ange URL-adressen till det webbprogram som ska integreras. till exempel:

      ```
      https://en.wikipedia.org/wiki/Main_Page
      ```

   * **Skicka parametrar**

      Markera rutan för parametrar som ska skickas till programmet när det behövs.

   * **Bredd och höjd**

      Definiera storleken på iframe

Den externa tillämpningen är integrerad i AEM-sidans styckesystem. till exempel när du använder ett Target-program av `https://en.wikipedia.org/wiki/Main_Page`:

![chlimage_1-7](assets/chlimage_1-7.png)

>[!NOTE]
Beroende på ditt sätt att arbeta är andra alternativ tillgängliga för integrering av externa program, till exempel. integreringen [av portlets](/help/sites-administering/aem-as-portal.md).

### Flash {#flash}

Med Flash-komponenten kan du läsa in en Flash-film. Du kan dra en Flash-resurs från innehållssökaren till komponenten eller använda dialogrutan:

* **Flash**

   * **Flash-film**

      Flash-filmfilen. Dra en resurs från innehållssökaren eller klicka för att öppna ett bläddringsfönster.

   * **Storlek**

      Mått i pixlar på visningsområdet där filmen finns.

* **Alternativ bild**

   En alternativ bild som ska visas

* **Avancerat**

   * **Snabbmeny**

      Anger om snabbmenyn ska visas eller döljas.

   * **Fönsterläge**

      Hur fönstret visas, till exempel ogenomskinligt, genomskinligt eller som ett distinkt (heldraget) fönster.

   * **Bakgrundsfärg**

      En bakgrundsfärg som valts i det angivna färgdiagrammet.

   * **Minimiversion**

      Den lägsta versionen av Adobe Flash Player som krävs för att köra filmen. Standardvärdet är 9.0.0.

   * **Attribut**

      Ytterligare attribut krävs.

### Bild {#image}

I bildkomponenten visas en bild och tillhörande text enligt de angivna parametrarna.

Du kan överföra en bild och sedan redigera den (t.ex. beskära, rotera, lägga till länk/titel/text).

Du kan antingen dra och släppa en bild från [Innehållssökning](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder) direkt till komponenten eller dess redigeringsdialogruta. Du kan också dubbelklicka i mitten av dialogrutan Redigera för att bläddra i det lokala filsystemet och överföra en bild. De två flikarna i dialogrutan Redigera styr också alla definitioner och ändringar av bilden:

![dc_image](assets/dc_image.png)

>[!NOTE]
Överföringens förlopp kan inte övervakas med Internet Explorer.
Internet Explorer-användare måste överföra bilden och sedan klicka på **OK** och öppna bilden igen för att se den överförda filen i förhandsgranskningen och kunna utföra ändringar (d.v.s. beskära).

>Mer information om HTML5-funktioner som används av AEM finns i avsnittet [Certifierade plattformar](/help/release-notes/release-notes.md#certifiedplatforms) .

När en bild har lästs in kan du konfigurera följande:

* **Karta**

   Om du vill mappa en bild väljer du Karta. Du kan ange hur du vill skapa bildschemat (rektangel, polygon och så vidare) och var området ska peka.

* **Beskär**

   Välj Beskär för att beskära en bild. Beskär bilden med musen.

* **Rotera**

   Om du vill rotera en bild väljer du Rotera. Använd detta upprepade gånger tills bilden roteras som du vill ha den.

* **Radera**

   Ta bort den aktuella bilden.

* **Zoomningsfält**

   Om du vill zooma in och ut i bilden använder du bildfältet under bilden (ovanför knapparna OK och Avbryt)

* **Titel**

   Bildens titel.

* **Alt-text**

   En alternativ text som kan användas när hjälpmedelsanpassat innehåll skapas.

* **Länka till**

   Skapa en länk till resurser eller andra sidor på webbplatsen.

* **Beskrivning**

   En beskrivning av bilden.

* **Storlek**

   Anger bildens höjd och bredd.

Den slutliga bilden (med **rubrik** och **beskrivning**) kan visas som:

![chlimage_1-8](assets/chlimage_1-8.png)

### Layoutbehållare {#layout-container}

>[!CAUTION]
Även om behållarkomponenten Layout är tillgänglig i det klassiska användargränssnittet är dess fullständiga funktioner bara tillgängliga i det beröringsaktiverade användargränssnittet. Mer information finns i [Responsiv layout](/help/sites-classic-ui-authoring/classic-page-author-responsive-layout.md).

### Lista {#list}

Med List-komponenten kan du konfigurera sökvillkor för att visa en lista:

* **Lista**

   * **Skapa lista med**

      Här anger du var listan ska hämta sitt innehåll. Det finns flera metoder:

   * Beroende på vilket objekt du väljer visas en ny panel:

      * **Alternativ för underordnade sidor**

         * **Underordnade till** (överordnad sida) Ange en bana antingen manuellt eller med väljaren. Lämna tomt om du vill använda den aktuella sidan som överordnad.
      * **Alternativ för fast lista**

         * **Sidor**

            Välj en lista med sidor. Använd + för att lägga till fler poster och upp-/nedknapparna för att justera ordningen.
      * **Alternativ för sökning**

         * **Starta i**

            Ange en startbana, antingen manuellt eller med väljaren.

         * **Sökfråga**

            Du kan ange en sökfråga med oformaterad text.
      * **Alternativ för avancerad sökning**

         * **Querybuilder-predikatnotation**

            Du kan ange en sökfråga med Querybuilder-predikatnotation. Du kan till exempel ange &quot;fulltext=Marketing&quot; om du vill att alla sidor med &quot;Marketing&quot; i innehållet ska visas i Carousel.

            Se [QueryBuilder API](/help/sites-developing/querybuilder-api.md) för en fullständig diskussion om frågeuttryck och fler exempel.
      * **Taggar**

         Ange **överordnad sida**, **taggar/nyckelord** och de matchningskriterier som krävs.
   * **Visa som**

      Hur du vill att objekten ska listas; innehåller länkar, lärare och nyheter.

   * **Beställ av**

      Anger om listan ska ordnas och i så fall vilka villkor som ska användas för sorteringen. Du kan ange ett villkor eller välja ett i listrutan.

   * **Gräns**

      Ange det maximala antalet objekt som ska visas i listan.

   * **Aktivera feed**

      Anger om en RSS-feed ska aktiveras för listan.

   * **Paginera efter**

      Här kan du ange hur många listobjekt som ska visas samtidigt. En lista med fler objekt än vad som angetts använder sidnumrering för att visa listan i flera delar.






I följande exempel visas en **List** -komponent på samma sätt som en lista med underordnade sidor (designen styrs av en webbplatsdesigns anpassade CSS-definitioner).

![dc_list_use](assets/dc_list_use.png)

### Inloggning {#login}

Här finns fälten Användarnamn och Lösenord.

![chlimage_1-9](assets/chlimage_1-9.png)

Du kan konfigurera:

* Logga in

   * Avsnittsetikett

      Inledande text för inmatningsfälten.

   * Etikett för användarnamn

      Text som ska etikettera användarnamnsfältet.

   * Lösenordsetikett

      Text som ska etikettera lösenordsfältet.

   * Etikett för inloggningsknapp

      Text för inloggningsknappen.

   * Omdirigera till

      Du kan ange vilken sida på webbplatsen som ska öppnas när användaren har loggat in.

* Redan inloggad

   * Knappetiketten Fortsätt

      Text som anger att användaren redan är inloggad.

### Orderstatus {#order-status}

* **Titel**

   * **Titel**

      Ange den titeltext som du vill visa.

   * **Länk**

      Ange den sida (produkt) som orderstatusen ska visas för.

   * **Typ/storlek**

      Välj ett alternativ.

![chlimage_1-10](assets/chlimage_1-10.png)

### Referens {#reference}

Med **komponenten Reference** kan du referera till text från en annan sida på AEM-webbplatsen (i den aktuella instansen). Innehållet i det refererade stycket visas sedan som om det fanns på den aktuella sidan. Innehållet uppdateras när källstycket ändras (du kan behöva uppdatera sidan).

* **Styckereferens**

   * **Referens**

      Ange sökvägen till sidan och stycket som du vill referera till (inkludera innehåll).

Om du vill ange sökvägen till ett stycke måste du lägga till ett suffix till banan (till sidan) med:

`.../jcr:content/par/<paragraph-ID>`

Exempel:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

Förutom att referera till ett visst stycke, kan sökvägen även ändras för att ange ett helt par-system. Du kan göra detta genom att lägga till sökvägen med:

`/jcr:content/par`

Exempel:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

När innehållet har konfigurerats visas det exakt som på källsidan. Det faktum att det är en referens visas bara när du öppnar komponenten för redigering:

![chlimage_1-11](assets/chlimage_1-11.png)

### Sök {#searching}

Sökkomponenten lägger till sökfunktioner på sidan.

Du kan konfigurera:

* Sök

   * **Nodtyper**

      Om sökningen ska begränsas till en viss nodtypslista de här. till exempel `cq:Page`.

   * **Sökväg att söka i**

      Ange rotsidan för grenen som du vill söka efter.

   * **Text för sökknapp**

      Namnet som visas på den faktiska sökknappen.

   * **Statistiktext**

      Texten som visas ovanför sökresultaten.

   * **Ingen resultattext**

      Om det inte finns några resultat visas den text som anges här.

   * **Stavningskontrollera text**

      Om någon skriver in en liknande term visas den här texten före termen.
Om du till exempel skriver geometrixxe visas&quot;Menade du? geometrixx&quot;.

   * **Text för liknande sidor**

      Den text som visas bredvid ett resultat för liknande sidor. Klicka på den här länken om du vill visa sidor med liknande innehåll.

   * **Text för relaterade sökningar**

      Texten som visas bredvid söker efter relaterade termer och ämnen.

   * **Text för söktender**

      Titeln ovanför de sökord som användarna anger.

   * **Resultatsidor - etikett**

      Den text som visas längst ned i listan med länkar till andra resultatsidor.

   * **Föregående etikett**

      Namnet som visas på länken till tidigare söksidor.

   * **Nästa etikett**

      Namnet som visas på länken till efterföljande söksidor.

I följande exempel visas sökkomponenten efter en sökning efter ordet *geometrixx* från rotkatalogen i en standardinstallation. Detta illustrerar också sidnumreringen av resultaten:

![dc_search_use](assets/dc_search_use.png)

I följande exempel visas en felstavad sökterm som inte är tillgänglig:

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Webbplatskarta {#sitemap}

En automatisk platskarta som (med standardinställningarna) visar alla sidor (som aktiva länkar) på den aktuella webbplatsen. Ett extrakt visar till exempel:

![dc_sitemap_use](assets/dc_sitemap_use.png)

Om det behövs kan du konfigurera:

* **Webbplatskarta**

   * **Rotsökväg**

      Sökväg som listan ska börja från.

### Bildspel {#slideshow}

Med den här komponenten kan du läsa in en serie bilder som ska visas som ett bildspel på sidan.Du kan lägga till eller ta bort bilder och tilldela varje rubrik. Under Avancerat kan du även ange storleken på visningsområdet.

Du kan konfigurera:

* **Bilder**

   * **Ny bild**

      Du kan ange ett urval av bildrutor med knapparna **Lägg till** (och **Ta bort**).

   * **Titel**

      Ange en titel om det behövs. Den här sidan läggs på lämplig sida.

* **Avancerat**

   * **Storlek**

      Ange bredd och höjd i pixlar.

Bildspelskomponenten visar sedan varje sekvens upprepade gånger, under en kort tidsperiod, innan den tonas fram till nästa bild:

![dc_slideshow_use](assets/dc_slideshow_use.png)

### Table {#table}

>[!NOTE]
Komponenten **Tabell** är baserad på [RTF-redigeraren](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md), liksom **[Text](#text)**-komponenten.
Vi rekommenderar att du använder **tabellkomponenten** för tabeller, även om de också kan skapas med komponenten **Text** .

Komponenten **Table** är förkonfigurerad så att du kan skapa, fylla i och formatera en tabell. I dialogrutan kan du konfigurera tabellen och skapa innehållet genom att antingen:

* från början
* kopiera och klistra in ett kalkylblad eller en tabell från en extern redigerare (t.ex. Excel, OpenOffice, Anteckningar).

![dc_table](assets/dc_table.png)

I följande skärmbild visas ett exempel på tabellkomponenten: designen bestäms av den platsspecifika CSS:en:

![dc_table_use](assets/dc_table_use.png)

### Tag Cloud {#tag-cloud}

I ett taggmoln visas ett grafiskt presenterat urval av de taggar som används i innehållet på webbplatsen:

![dc_tagclouduse](assets/dc_tagclouduse.png)

När du konfigurerar taggmolnkomponenten kan du ange:

* **Taggar som ska visas** varifrån taggarna som ska visas samlas in. Välj från en sida, en sida med alla underordnade eller alla taggar.

* **Sida** Välj sidan som du vill referera till.

* **Inga länkar på taggar** Anger om taggarna som visas ska fungera som länkar.

Mer information om hur du använder taggar finns i [Använda taggar](/help/sites-classic-ui-authoring/classic-feature-tags.md).

### Text {#text}

>[!NOTE]
Komponenten **Text** är baserad på [RTF-redigeraren](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md), liksom **[komponenten Table](#table)**.
Vi rekommenderar att du använder **tabellkomponenten** för tabeller, även om de också kan skapas med komponenten **Text** .

Med komponenten Text kan du ange ett textblock med en WYSIWYG-redigerare, som har funktioner från [RTF-redigeraren](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md). Med ett urval ikoner kan du formatera texten, inklusive teckensnittsegenskaper, justering, länkar, listor och indrag.

![dc_text](assets/dc_text.png)

När du öppnar fliken **Format** i dialogrutan **Redigera** kan du också ange:

* **Avstånd**
* **Textformat**

Den formaterade texten visas då på sidan; den faktiska designen beror på webbplatsens CSS:

![dc_text_use](assets/dc_text_use.png)

Mer information om komponenten Text och funktionerna i RTF-redigeraren finns på sidan [RTF-redigerare](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md) .

#### Redigering på plats {#inplace-editing}

Förutom det dialogbaserade redigeringsläget Rich Text, innehåller AEM även [Inplace Editing](/help/sites-authoring/editing-content.md), som gör det möjligt att redigera texten direkt när den visas i layouten på sidan.

### Text och bild {#text-image}

Komponenten Text och bild lägger till ett textblock och en bild. Du kan också lägga till och redigera text och bilder separat. Mer information finns i komponenterna [Text](#text) och [Bild](#image) .

![chlimage_1-12](assets/chlimage_1-12.png) ![chlimage_1-13](assets/chlimage_1-13.png)

Du kan konfigurera:

* **Komponentformat** (**format**)

   Här kan du justera bilden åt vänster eller höger. Standardvärdet är **Vänster** justerat, med bilden till vänster.

* **Bildegenskaper** (**avancerade bildegenskaper**)

   Gör att du kan ange följande:

   * **Bildresurs**

      Överför den önskade bilden.

   * **Titel**

      Blockets titel. visas med muspekaren.

   * **Alt-text**

      Alternativ text som visas om bilden inte kan visas. Om den lämnas tom används titeln.

   * **Länka till**

      Ange en målsökväg.

   * **Beskrivning**

      En beskrivning av bilden.

   * **Storlek**

      Anger bildens höjd och bredd.

I följande exempel visas en textbildskomponent som visar bilden vänsterjusterad:

![dc_textimage_use](assets/dc_textimage_use.png)

### Titel {#title}

Titelkomponenten kan antingen:

* visa den aktuella sidans namn, detta görs genom att lämna fältet Titel tomt
* visar en text som du anger i fältet Titel.

Du kan konfigurera:

* **Titel**

   Om du vill använda ett annat namn än sidrubriken anger du det här.

* **Länk**

   URI:n om titeln ska fungera som en länk.

* **Typ/storlek**

   Välj Liten eller Stor i listrutan. Liten genereras som en bild. Stor genereras som text.

I följande exempel visas en **Title** -komponent: designen bestäms av den platsspecifika CSS:n.

![dc_title_use](assets/dc_title_use.png)

### Video {#video}

Med **videokomponenten** kan du placera ett fördefinierat videoelement direkt på en sida.

Se även [Konfigurera videoprofiler](/help/sites-administering/config-video.md#configuringvideoprofiles) för användning med HTML5-element.

När du har placerat en instans av komponenten på sidan kan du konfigurera:

* Video

   * **Videoresurs**

      Överför eller släpp videomaterialet.

   * **Storlek**

      Videons ursprungliga storlek (bredd x höjd i pixlar) visas i rutorna intill Storlek (se ovan). Ange bredd- och höjddimensioner manuellt här om du vill åsidosätta videons ursprungliga dimensioner. Klicka på **OK** för att stänga dialogrutan.

>[!NOTE]
Format som stöds:
* `.mp4`
* `Ogg`
* `FLV` (Flash-video)



## Kolumner {#columns}

Kolumner är ett sätt att styra layouten för innehåll i AEM. I en standardinstallationskomponent finns det funktioner för att skapa två och/eller tre kolumner.

I följande exempel visas komponenterna 2 kolumner och 3 kolumner som används. Du kan använda platshållarna för nya komponenter:

![chlimage_1-14](assets/chlimage_1-14.png)

### 2 Columns {#columns-1}

En Column Control-komponent som har standardvärdet 2 lika med-kolumner.

### 3 Columns {#columns-2}

En Column Control-komponent som har standardvärdet 3 lika med-kolumner.

### Kolumnkontroll {#column-control}

Med komponenten Kolumnkontroll kan användarna välja hur de vill dela upp innehållet på webbsidans huvudpanel i flera kolumner. Användarna kan välja hur många kolumner som krävs (från en fördefinierad lista) och sedan skapa, ta bort eller flytta innehåll inom varje kolumn.

* **Kolumnkontroll**

   * **Kolumnlayout**

      Markera det antal kolumner som du vill återge. När varje kolumn har skapats har den en egen länk för att dra komponenter eller resurser när du lägger till innehåll.

## Form {#form}

Formulärkomponenter används för att skapa formulär som besökare kan skicka in indata i. Formulär och formulärkomponenter kan användas för att samla in information, t.ex. användarfeedback (t.ex. ett kundfrågeformulär) och användarinformation (t.ex. användarregistrering).

>[!NOTE]
Mer information om AEM Forms finns i hjälpen [för](/help/forms/home.md) AEM Forms.

Formulär byggs upp av flera olika komponenter:

* **Formulär**

   Formulärkomponenten definierar början och slutet av ett nytt formulär på en sida. Andra komponenter kan sedan placeras mellan dessa element, som tabeller, nedladdningar och så vidare.

* **Formulärfält och -element**

   Formulärfält och -element kan innehålla textrutor, alternativknappar, bilder och så vidare. Användaren slutför ofta en åtgärd i ett formulärfält, till exempel att skriva text. Mer information finns i enskilda formulärelement.

* **Profilkomponenter**

   Profilkomponenter relaterar till besökarprofiler som används för socialt samarbete och andra områden där besökaranpassning krävs.

I följande exempel visas ett exempelformulär: består av **Form** -komponenten (start och slut), med två **Form** **Text** -fält som används för inmatning, ett **Allmänt** **Text** **** -fält som används för lead-texten och en¥Submit¥-knapp.

![dc_form](assets/dc_form.png)

>[!NOTE]
Information om hur du utvecklar och anpassar formulär finns på sidan [](/help/sites-developing/developing-forms.md)Utveckla formulär. Detta inkluderar bland annat att lägga till åtgärder, begränsningar, förhandsladda fält och att använda skript för att anropa en tjänst för att utföra åtgärder.

### Inställningar som är gemensamma för (många) formulärkomponenter {#settings-common-to-many-form-components}

Även om var och en av formulärkomponenterna har olika syften, består många av liknande alternativ och parametrar.

När du konfigurerar någon av formulärkomponenterna är följande flikar tillgängliga i dialogrutan:

* **Titel och text**

   Här måste du ange grundläggande information, t.ex. formulärets rubrik och eventuell tillhörande text. Där det är lämpligt kan du även definiera annan nyckelinformation, t.ex. om fältet är flervalsbart och om det finns objekt tillgängliga för markering.

* **Startvärden**

   Gör att du kan ange ett standardvärde.

* **Begränsningar**

   Här kan du ange om ett fält är obligatoriskt och om det finns platsbegränsningar i det fältet (måste till exempel vara numeriskt).

* **Stilar**

   Anger fältets storlek och format.

>[!NOTE]
Fälten som visas varierar avsevärt beroende på den enskilda komponenten.

Dessa flikar ger dig de parametrar som behövs. dessa kan bero på den enskilda komponenttypen, men kan omfatta:

* **Titel och text**

   * **Elementnamn**

      Formulärelementets namn. Detta anger var i databasen data lagras.
Detta är ett obligatoriskt fält och får endast innehålla följande tecken:

      * alfanumeriska tecken
      * `_ . / : -`
   * **Titel**

      Titeln som visas med fältet. Om inget anges visas standardtiteln.

   * **Beskrivning**

      Gör att du kan ange ytterligare information för användaren om det behövs. I formuläret visas detta under fältet, med ett mindre teckensnitt än rubriken.

   * **Visa/dölj**

      Anger när fältet är synligt.


* **Startvärden**

   * **Standardvärde**

      Det värde som visas i fältet när formuläret öppnas. Det vill säga innan användaren har gjort några indata.

* **Begränsningar**

   * **Krävs**

      Detta beror på formulärkomponenttypen, men tillhandahåller en eller flera kryssrutor som anger att det här fältet, eller vissa delar av det här fältet, är/är obligatoriska.

   * **Nödvändigt meddelande**

      Ett meddelande som informerar användarna om att detta fält är obligatoriskt. ett obligatoriskt fält markeras med asterisk och .

   * **Begränsning**

      Vilka begränsningar som är tillgängliga för markeringen beror på formulärkomponenttypen.

   * **Begränsningsmeddelande**

      Ett meddelande som informerar användarna om vad som krävs.

* **Stilar**

   * **Storlek**

      I rader och kolumner.

   * **Bredd**

      I pixlar.

   * **CSS**

### Formulär (komponent) {#form-component}

Form-komponenten definierar både början och slutet av ett formulär med elementen **Formulärstart** och **Formulärslut** . Dessa är alltid kopplade för att säkerställa att formuläret är korrekt definierat.

![dc_form-1](assets/dc_form-1.png)

Mellan formulärets början och slut kan du lägga till formulärkomponenter som definierar de faktiska inmatningsfälten för användarna.

#### Formulärets början {#start-of-form}

Den här komponenten behövs för att definiera början på ett nytt formulär på en sida. Du kan konfigurera:

* **Formulär**

   * **Tack**

      Sidan som ska refereras till för att tacka besökarna för att de har lämnat sina synpunkter. Om formuläret lämnas tomt visas det igen när det har skickats.

   * **Starta arbetsflöde**

      Bestämmer vilket arbetsflöde som ska aktiveras när ett formulär skickas.

* **Avancerat**

   * **Åtgärdstyp**

      Ett formulär behöver en åtgärd. Åtgärden definierar den åtgärd som utlöses för körning med data som skickas av användaren (liknar action= i HTML). Vissa behöver en motsvarande **åtgärdskonfiguration**.

      En rad åtgärdstyper ingår i en AEM-standardinstallation:

      * **Kontobegäran**
      * **Skapa innehåll**
      * **Skapa lead**
      * **Skapa och uppdatera konto**
      * **E-posttjänst: Skapa prenumerant och lägg till i listan**
      * **E-posttjänst: Skicka e-post med automatisk svarare**
      * **E-posttjänst: Avbeställ användare från listan**
      * **Redigera community**
      * **Redigera resurser**
      * **Redigera arbetsflödesstyrda resurser**
      * **E-post**
      * **Information om placerad order**
      * **Profiluppdatering**
      * **Återställ lösenord**
      * **Ange lösenord**
      * **Lagra innehåll**

         Detta är standardåtgärdstypen.

      * **Lagra innehåll med överföringar**
      * **Skicka beställning**
      * **Avbeställ prenumeration**
      * **Uppdatera ordning**
   * **Formuläridentifierare**

      Formuläridentifieraren identifierar formuläret unikt. Använd formuläridentifieraren om du har flera formulär på en sida, se till att de har olika identifierare.

   * **Läs in bana**

      Sökvägen till nodegenskaper som används för att läsa in fördefinierade värden i formulärfälten.
Detta är ett valfritt fält som anger sökvägen till en nod i databasen. När den här noden har egenskaper som matchar fältnamnen förinläses motsvarande fält i formuläret med egenskapsvärdet. Om det inte finns någon matchning innehåller fältet standardvärdet.
Med **Läs in sökväg** kan du läsa in formuläret i förväg med värden i de obligatoriska fälten. Se [Förhandsladda formulärvärden](/help/sites-developing/developing-forms.md#preloading-form-values).

   * **Klientvalidering**

      Anger om klientvalidering krävs för det här formuläret (servervalidering sker *alltid* ). Detta kan du göra med **Forms Captcha** -komponenten.

   * **Typ av verifieringsresurs**

      Definierar resurstypen för formulärvalidering om du vill validera hela formuläret (i stället för enskilda fält). Om du validerar det fullständiga formuläret ska du även inkludera något av följande:

      * Ett skript för klientvalidering:

         `/apps/<myApp>/form/<myValidation>/formclientvalidation.jsp`

      * Ett skript för validering på serversidan:

         `/apps/<myApp>/form/<myValidation>/formservervalidation.jsp`
   * **Åtgärdskonfiguration**

      Vilka alternativ som är tillgängliga i **Åtgärdskonfiguration** beror på vilken **åtgärdstyp** som har valts:

      * **Kontobegäran**

         * **Skapa kontosida** Den sida som används när ett nytt konto skapas.
      * **Skapa innehåll**

         * Sökväg till innehåll Innehållssökvägen för allt innehåll som formuläret dumpar. Ange en bana som slutar med ett snedstreck `/`. Snedstrecket innebär att för varje formulärport skapas en ny nod på den angivna platsen. till exempel:
            `/forms/feedback/`

         * **Typ**

            Välj önskad typ.

         * **Formulär**

            Ange formuläret.

         * **Återge med**

            Välj önskat alternativ i listan.

         * **Resurstyp**

            Om den anges läggs den till i varje kommentar som `sling:resourceType`

         * **Visa väljare**
      * **Skapa lead**

         * **Lead läggs till i listan** Ange önskad leadlista.
      * **Skapa och uppdatera konto**

         * **Inledande grupp**

            Grupp att tilldela ny användare till.

         * **Home**

            Sida som ska visas efter slutförd inloggning.

         * **Bana**

            Sökvägen (relativ) till den plats där det nya kontot skapas och lagras.

         * **Visa data...**

            Klicka på den här knappen för att komma åt information om formulärresultat i gruppredigeraren. Härifrån kan du exportera informationen till en `.tsv` (tabbseparerad) fil (som exempelvis kan användas i ett Excel-kalkylblad).
      * **E-post**

         * **Från**

            Ange den e-postadress som e-postmeddelandet ska komma från.

         * **Mailto**

            Ange den eller de e-postadresser som formuläret ska skickas till.

         * **CC**

            Ange e-postadress(er) för CC.

         * **BCC**

            Ange e-postadressen/adresserna för den grundläggande kontrollCC-profilen.

         * **Ämne**

            Ange ett ämne för e-postmeddelandet.
      * **Återställ lösenord**

         * **Ändra lösenordssida**

            Sidan som används när lösenordet ändras.
      * **Lagra innehåll**

         * **Innehållsbana**

            Innehållssökvägen för allt innehåll som formuläret dumpar. Ange en bana som slutar med ett snedstreck `/`. Snedstrecket innebär att för varje formulärport skapas en ny nod på den angivna platsen. till exempel:
            `/forms/feedback/`

         * **Visa data...**

            Klicka på den här knappen för att komma åt information om formulärresultat i gruppredigeraren. Härifrån kan du exportera informationen till en .tsv-fil (tabbseparerad) (som exempelvis kan användas i ett Excel-kalkylblad).
      * **Lagra innehåll med överföringar**

         Detta har samma alternativ som **Lagra innehåll**.

      * **Avbeställ prenumeration**

         * **Lead kommer att tas bort från den här listan**

            Ange önskad leadlista.










#### Formulärets slut {#end-of-form}

Detta markerar formulärets slut. Du kan konfigurera:

* **Formulärslut**

   * **Visa Skicka-knapp**

      Anger om en Skicka-knapp ska visas eller inte.

   * **Skicka namn**

      En identifierare om du använder flera skicka-knappar i ett formulär.

   * **Skicka titel**

      Namnet som visas på knappen, till exempel Skicka eller Skicka.

   * **Visa knappen Återställ**

      Markera kryssrutan för att visa knappen Återställ.

   * **Återställ titel**

      Namnet som visas på knappen Återställ.

   * **Beskrivning**

      Information som visas under knappen.

### Kontonamn {#account-name}

Detta gör att användaren kan ange ett kontonamn:

![dc_form_account_name](assets/dc_form_accountname.png)

### Adress {#address}

Detta gör att du kan lägga till ett internationellt adressfält med följande format:

![dc_form_adressfield](assets/dc_form_addressfield.png)

Komponenten är konfigurerad för omedelbar användning, men du kan ändra konfigurationen om det behövs. Du kan till exempel lägga till begränsningar för de enskilda elementen i adressen. Om du lämnar fält tomma används standardinställningarna.

### Captcha {#captcha}

Captcha-komponenten kräver att användaren skriver en alfanumerisk sträng som den visas på skärmen. Strängen ändras vid varje uppdatering.

![dc_form_captcha](assets/dc_form_captcha.png)

Du kan konfigurera olika parametrar för den här komponenten, inklusive ett meddelande som visas när captcha-strängen är ogiltig.

### Kryssrutegrupp {#checkbox-group}

Med en kryssruta kan du skapa en lista med en av flera kryssrutor, som flera kan markeras samtidigt.

![dc_form_checkbox_groupuse](assets/dc_form_checkboxgroupuse.png)

Du kan ange olika parametrar, inklusive rubrik, beskrivning och elementnamn. Med knapparna + och - kan du lägga till eller ta bort objekt och sedan placera dem med upp- och nedpilarna.

>[!NOTE]
Med **Objekt Läs in sökväg** kan du förhandsladda kryssrutegrupplistan med värden.
Se [Förhandsladda formulärfält med flera värden](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Kreditkortsinformation {#credit-card-details}

På så sätt kan du ange de fält som behövs för att ange kreditkortsinformation. Du kan konfigurera det för att ange vilka typer av kort som accepteras och vilken information som krävs (till exempel säkerhetskod).

![chlimage_1-15](assets/chlimage_1-15.png)

### Listruta {#dropdown-list}

En nedrullningsbar lista kan konfigureras så att du kan använda ett intervall av värden för markering:

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

Du kan ange en titel och vilka objekt som ska visas i listan. Med knapparna + och - kan du lägga till eller ta bort listobjekten och sedan placera dem med knapparna Upp och Ned. Du kan ange om användarna ska kunna markera flera objekt i listan och alla objekt som ska väljas automatiskt första gången de öppnar listan (startvärden).

>[!NOTE]
Med **Objekt Läs in sökväg** kan du läsa in listrutan med värden i förväg.
Se [Förhandsladda formulärfält med flera värden](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Filöverföring {#file-upload}

Komponenten för filöverföring ger användaren en funktion för att välja och överföra en fil.

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
Du kan skapa en anpassad överföringskomponent för att överföra filer till en Sling-server. Mer information finns i [Överföra filer till Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/uploading-files-aem1.html).

### Dolt fält {#hidden-field}

Med den här komponenten kan du skapa ett dolt fält. Dessa kan användas för olika ändamål. t.ex. när du behöver utföra en åtgärd efter att du har skickat formuläret eller när dolda data krävs vid efterbearbetning.

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
Du kan också anpassa formuläret för att visa eller dölja specifika formulärkomponenter enligt värdet i andra fält i formuläret. Att ändra synligheten för ett formulärfält är användbart när fältet bara behövs under specifika förhållanden.
Se [Visa och dölja formulärkomponenter](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components).

### Bildknapp {#image-button}

Med en bildknapp kan du skapa en knapp med din egen bild och text:

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### Bildöverföring {#image-upload}

Bildöverföringskomponenten ger användaren en mekanism för att välja och överföra en bildfil.

![dc_form_imageupload](assets/dc_form_imageupload.png)

### Länkfält {#link-field}

I länkfältet kan användaren ange en URL:

![dc_form_link](assets/dc_form_link.png)

Det används oftast för kalenderhändelsematerialet, där det används för URL-/länkfältet för en händelse.

### Lösenordsfält {#password-field}

Detta används för att tillåta användaren att ange sitt lösenord:

![dc_form_password](assets/dc_form_password.png)

### Återställ lösenord {#password-reset}

Den här komponenten ger användaren två fält för:

* inmatning av ett lösenord
* upprepade inmatningar av lösenordet för att kontrollera att inmatningen är korrekt.

Med standardinställningarna visas komponenten som:

![dc_password_reset](assets/dc_password_reset.png)

### Grupp med alternativknappar {#radio-group}

En alternativknappsgrupp ger dig en lista över en eller flera kryssrutor, där bara en av kryssrutorna kan markeras vid en viss tidpunkt.

Du kan ange elementnamnet tillsammans med en titel och en beskrivning Med knapparna + och - kan du lägga till eller ta bort objekt, placera dem med upp- och nedpilarna och ange ett standardvärde om det behövs:

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
Om du använder **Objekt Läs in bana** kan du förhandsladda gruppen med värden.
Se [Förhandsladda formulärfält med flera värden](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Submit Button {#submit-button}

Med den här komponenten kan du skapa en skicka-knapp med antingen standardtexten:

![dc_form_submit_button](assets/dc_form_submitbutton.png)

Eller med egen text:

![dc_form_submit_button_use](assets/dc_form_submitbuttonuse.png)

### Märkordsfält {#tags-field}

I det här fältet kan du välja taggar:

![dc_form_tags_use](assets/dc_form_tags_use.png)

Du kan ange olika parametrar, inklusive namnutrymmen som kan användas med hjälp av fliken Specialtecken:

* **Taggfält**

   * **Tillåtna namnutrymmen**

      * **Geometrixx utomhus**
      * **Arbetsflöde**
      * **Forum**
      * **Arkivfotografier**
      * **Geometrixx Media**
      * **Standardtaggar**
      * **Marknadsföring**
      * **Resursegenskaper**
   * **Bredd i pixlar**
   * **Popup-storlek**


### Textfält {#text-field}

Standardtextfältet kan konfigureras till den storlek du vill ha och med ditt eget lead i ett meddelande:

![dc_form_text](assets/dc_form_text.png)

### Skicka-knappar för arbetsflöde {#workflow-submit-button-s}

På så sätt kan du skapa en Skicka-knapp som kan användas i ett arbetsflöde.

![chlimage_1-16](assets/chlimage_1-16.png)
