---
title: Resursmallar
description: Lär dig mer om tillgångsmallar i [!DNL Adobe Experience Manager Assets] och hur du använder resursmallar för att skapa marknadsföringsmaterial.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Resursmallar {#asset-templates}

Resursmallar är en speciell typ av resurser som gör det enkelt att snabbt återanvända visuellt avancerat innehåll för digitala medier och trycksaker. En resursmall består av två delar, avsnittet med fasta meddelanden och det redigerbara avsnittet.

Avsnittet med fasta meddelanden kan innehålla eget innehåll, t.ex. varumärkeslogotyp och copyrightinformation som har inaktiverats för redigering. Det redigerbara avsnittet kan innehålla visuellt och textbaserat innehåll i fält som kan redigeras för att anpassa meddelanden.

Flexibiliteten att göra begränsade redigeringar samtidigt som du skyddar globala skyltar gör resursmallarna till idealiska byggstenar för snabb innehållsanpassning och distribution som innehållsartefakter för olika funktioner. Återanvändning av innehåll bidrar till att minska kostnaderna för hantering av tryckta och digitala kanaler och ger en helhetsbild och enhetliga upplevelser i alla dessa kanaler.

Som marknadsförare kan ni lagra och hantera mallar i [!DNL Experience Manager Assets] och använda en enda basmall för att enkelt skapa flera personaliserade utskriftsupplevelser. Ni kan skapa olika typer av marknadsföringsmaterial, som broschyrer, flygblad, vykort, visitkort och så vidare, för att på ett enkelt sätt förmedla ert marknadsföringsbudskap till kunderna. Du kan också montera flersidiga utskrifter från befintliga eller nya utskrifter. Framför allt kan ni enkelt leverera både digitala och tryckta upplevelser samtidigt för att skapa en enhetlig, integrerad upplevelse för användarna.

Resursmallar är till största delen [!DNL Adobe InDesign] filer, men kompetens inom [!DNL Adobe InDesign] det är inte något hinder för att skapa fantastiska artefakter. Du behöver inte mappa fälten i din [!DNL Adobe InDesign] mall till de produktfält som du annars behöver när du skapar kataloger. Du kan redigera mallarna i WYSIWYG-läge direkt i webbgränssnittet. För [!DNL Adobe InDesign] att kunna bearbeta redigeringsändringarna måste du först konfigurera [!DNL Experience Manager Assets] för integrering med [!DNL Adobe InDesign Server].

Möjligheten att redigera [!DNL Adobe InDesign] mallar från webbgränssnittet bidrar till ett bättre samarbete mellan kreatörer och marknadsförare, samtidigt som time to market för lokala marknadsföringssatsningar minskar.

Du kan göra följande med resursmallar:

* Ändra redigerbara mallfält från webbgränssnittet
* Styr den grundläggande formateringen av text, t.ex. teckenstorlek, stil och typ på taggnivå
* Ändra bilder i mallen med hjälp av innehållsväljaren
* Förhandsgranska malländringar
* Sammanfoga flera mallfiler för att skapa en flersidig artefakt

När du väljer en mall för dina säkerheter [!DNL Experience Manager Assets] skapar en kopia av mallen som du kan redigera. Den ursprungliga mallen bevaras, vilket säkerställer att den globala signaturen förblir intakt och kan återanvändas för att stärka varumärkets enhetlighet.

Du kan exportera den uppdaterade filen i den överordnade mappen i följande format:

* INDD
* PDF
* JPG

Du kan även hämta utdata i dessa format till ditt lokala system.

## Skapa en säkerhet {#creating-a-collateral}

Tänk dig ett scenario där du vill skapa digital tryckbar information som broschyrer, flygblad och annonser för en kommande kampanj och dela med butiker globalt. Genom att skapa material som bygger på en mall kan ni leverera en enhetlig kundupplevelse över alla kanaler. Designers kan skapa kampanjmallar (en eller flera sidor) med hjälp av en kreativ lösning, som [!DNL InDesign] och överföra mallarna till [!DNL Experience Manager Assets] dig. Innan du skapar en säkerhet måste du ha en eller flera INDD-mallar överförda till och tillgängliga [!DNL Experience Manager] i förväg.

1. I [!DNL Experience Manager] gränssnittet klickar du på [!UICONTROL Resurser].

1. Välj **[!UICONTROL Mallar]** bland alternativen.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Klicka på **[!UICONTROL Skapa]** och välj sedan det material du vill skapa på menyn. Välj till exempel **[!UICONTROL Broschyr]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. ha en eller flera INDD-mallar överförda till och tillgängliga [!DNL Experience Manager] i förväg. Välj en mall för broschyren och klicka på **[!UICONTROL Nästa]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. Ange ett namn och en valfri beskrivning för broschyren.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Valfritt) Klicka på **[!UICONTROL Taggar]** och välj en eller flera taggar för broschyren. Bekräfta **[!UICONTROL valet genom att klicka på Bekräfta]** .

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. Klicka på **[!UICONTROL Skapa]**. En dialogruta bekräftar att en ny broschyr har skapats. Klicka på **[!UICONTROL Öppna]** för att öppna broschyren i redigeringsläge.

   <!--![chlimage_1-106](assets/.png) -->

   Du kan också stänga dialogrutan och navigera till mappen på mallsidan som du började med för att visa den broschyr du skapade. Typen av säkerhet visas på miniatyrbilden i kortvyn. I det här fallet visas t.ex. Broschyr på miniatyrbilden.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Redigera en säkerhet {#editing-a-collateral}

Du kan redigera en sammanställning direkt när du har skapat den. Du kan även öppna den från mallsidan eller resurssidan.

1. Gör något av följande om du vill öppna materialet för redigering:

   * Öppna den säkerhet (broschyr i det här fallet) som du skapade i steg 7 i [Skapa en säkerhet](/help/assets/asset-templates.md#creating-a-collateral).
   * Navigera från sidan Mallar till en mapp där du skapade materialet och klicka på snabbåtgärden [!UICONTROL Redigera] på miniatyrbilden av en materialet.
   * Klicka på **[!UICONTROL Redigera]** i verktygsfältet på tillgångssidan för säkerheten.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.
   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   Resurssökaren och textredigeraren visas till vänster på sidan. Textredigeraren är öppen som standard.

   Du kan använda textredigeraren för att ändra texten som ska visas i textfältet. Du kan ändra teckenstorlek, stil, färg och typ på taggnivå.

   Med resurssökaren kan du söka efter eller söka efter bilder i [!DNL Experience Manager Assets] och ersätta de redigerbara bilderna i mallen med de bilder du väljer.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   De redigerbara visas till höger. För att ett fält ska kunna redigeras i [!DNL Experience Manager Assets]måste motsvarande fält i mallen taggas i [!DNL InDesign]. De ska med andra ord markeras som redigerbara i [!DNL InDesign].

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >Se till att din [!DNL Experience Manager] instans är integrerad med en [!DNL InDesign Server] [!DNL Experience Manager Assets] så att du kan extrahera data från InDesign-mallen och göra den tillgänglig för redigering. Mer information finns i [Integrera Experience Manager Assets med InDesign Server](/help/assets/indesign.md).

1. Om du vill ändra texten i ett redigerbart fält klickar du på textfältet i listan med redigerbara fält och redigerar texten i fältet.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Du kan redigera textegenskaperna, till exempel teckensnittsstil, färg och storlek, med de alternativ som finns.

1. Klicka på **[!UICONTROL Förhandsgranska]** för att förhandsgranska textändringarna.

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. Klicka på **[!UICONTROL Resurssökaren]** om du vill byta ut en bild.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. Markera bildfältet i listan med redigerbara fält och dra sedan en önskad bild från resursväljaren till det redigerbara fältet.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Du kan också söka efter bilder med nyckelord, taggar och baserat på deras publiceringsstatus. Du kan bläddra i databasen och navigera till den önskade bildens plats [!DNL Experience Manager Assets] .

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Klicka på **[!UICONTROL Förhandsvisa]** om du vill förhandsgranska bilden.

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. Om du vill redigera en viss sida i en flersidig säkerhetssida använder du sidnavigeraren längst ned.

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Klicka på **[!UICONTROL Förhandsgranska]** i verktygsfältet om du vill förhandsgranska alla ändringar. Klicka på **[!UICONTROL Klar]** om du vill spara redigeringsändringarna för den aktuella informationen.

   >[!NOTE]
   >
   >Ikonerna Förhandsvisa och Klar är bara aktiverade när de redigerbara bildfälten i den sammansatta bilden inte har några ikoner som saknas. Om det finns saknade ikoner i din säkerhetsinformation beror det på att [!DNL Experience Manager] det inte går att matcha bilderna i [!DNL InDesign] mallen. Vanligtvis [!DNL Experience Manager] kan inte lösa bilder i följande fall:
   >
   >    * Bilder bäddas inte in i den underliggande [!DNL InDesign] mallen.
   >    * Bilderna länkas från det lokala filsystemet.
   >
   >Så här aktiverar du [!DNL Experience Manager] bildupplösning:
   >
   >    * Bädda in bilder när du skapar [!DNL InDesign] mallar (Se [Länkar och inbäddade bilder](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >    * Montera [!DNL Experience Manager] i det lokala filsystemet och mappa sedan saknade ikoner med befintliga resurser i [!DNL Experience Manager].
   >
   >Mer information om hur du arbetar med [!DNL InDesign] dokument finns i [Bästa metoder för att arbeta med InDesign-dokument i Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Om du vill generera en PDF-återgivning för broschyren väljer du alternativet Acrobat i dialogrutan och klickar sedan på **[!UICONTROL Fortsätt]**.
1. Säkerheten skapas i den mapp du började med. Om du vill visa återgivningarna öppnar du materialet och väljer **[!UICONTROL Återgivningar]** i listan GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Klicka på PDF-återgivningen i listan över återgivningar för att hämta PDF-filen. Öppna PDF-filen för att granska materialet.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Sammanfoga säkerhet {#merge-collateral}

1. I [!DNL Experience Manager] gränssnittet klickar du på [!UICONTROL Resurser] på navigeringssidan.

1. Välj **[!UICONTROL Mallar]** bland alternativen.

1. Klicka på **[!UICONTROL Skapa]** och välj **[!UICONTROL Sammanfoga]** på menyn.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. På sidan [!UICONTROL Koppla] mall klickar du på **[!UICONTROL Koppla]**.

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. Navigera till platsen för den säkerhet som du vill sammanfoga och klicka på miniatyrbilderna för den säkerhet som du vill sammanfoga för att markera dem.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Du kan också söka efter mallar från sökrutan.

   ![chlimage_1-123](assets/chlimage_1-328.png)

   Du kan bläddra genom databasen eller samlingarna och navigera till platsen för de önskade mallarna och sedan välja dem att sammanfoga. [!DNL Experience Manager Assets]

   ![chlimage_1-124](assets/chlimage_1-329.png)

   Du kan använda olika filter för att söka efter de önskade mallarna. Du kan till exempel söka efter mallar baserat på filtyp eller taggar.

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Klicka på **[!UICONTROL Nästa]** i verktygsfältet.
1. På skärmen **[!UICONTROL Förhandsgranska och ordna]** om kan du ordna om mallarna om det behövs och förhandsgranska valet av mallar som ska sammanfogas. Klicka sedan på **[!UICONTROL Nästa]** i verktygsfältet.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. Ange ett namn för säkerheten på skärmen [!UICONTROL Konfigurera mall] . Du kan också ange de taggar som du anser lämpliga. Om du vill exportera utdata i PDF-format väljer du **[!UICONTROL Acrobat (.PDF)]**. Som standard exporteras säkerheten i JPG-format och [!DNL InDesign] format. Om du vill ändra miniatyrbilden för flersidessäkerheten klickar du på **[!UICONTROL Ändra miniatyrbild]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Klicka på **[!UICONTROL Spara]** och sedan på **[!UICONTROL OK]** i dialogrutan för att stänga dialogrutan. Den flersidiga informationen skapas i den mapp du började med.

   >[!NOTE]
   >
   >Du kan inte redigera en sammanfogad säkerhet senare eller använda den för att skapa annan säkerhet.
