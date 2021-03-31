---
title: Hantera sammansatta resurser med referenser och flera sidor
description: Lär dig hur du skapar referenser till digitala resurser inifrån [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. Använd funktionen för sidvisningsprogram för att visa enskilda underresurssidor för flersidiga filer som PDF-, INDD-, PPT-, PPTX- och AI-filer.
contentOwner: AG
role: Affärsledare, administratör
feature: Resurshantering
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# Hantera sammansatta och flersidiga resurser {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] kan identifiera om en överförd fil innehåller referenser till resurser som redan finns i databasen. Den här funktionen är endast tillgänglig för filformat som stöds. Om den överförda resursen innehåller referenser till [!DNL Experience Manager]-resurser skapas en dubbelriktad länk mellan de överförda och refererade resurserna.

Förutom att eliminera redundans kan du genom att referera till resurserna i [!DNL Adobe Creative Cloud]-program förbättra samarbetet och öka användarnas effektivitet och produktivitet.

[!DNL Experience Manager Assets] har stöd för dubbelriktade referenser. Du kan hitta refererade resurser på sidan med tillgångsinformation i den överförda filen. Dessutom kan du visa de refererande filerna på sidan med resursinformation för den refererade resursen.

Referenser tolkas utifrån sökväg, dokument-ID och instans-ID för de refererade resurserna.

## [!DNL Adobe Illustrator]: Lägg till digitala resurser som referenser  {#refai}

Du kan referera till befintliga digitala resurser inifrån en [!DNL Adobe Illustrator]-fil.

1. Hämta de digitala resurserna på det lokala filsystemet med [[!DNL Experience Manager] skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Navigera till filsystemplatsen för resursen som du vill referera till.
1. Dra resursen från den lokala mappen till [!DNL Illustrator]-filen.

1. Spara [!DNL Illustrator]-filen på den monterade enheten eller [överför](/help/assets/manage-assets.md#uploading-assets) till [!DNL Experience Manager]-databasen.

1. När arbetsflödet är klart går du till sidan med resursinformation för resursen. Referenserna till befintliga digitala resurser visas under **[!UICONTROL Dependencies]** i kolumnen **[!UICONTROL References]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. De refererade resurserna som visas under **[!UICONTROL Dependencies]** kan också refereras av andra filer än den aktuella. Om du vill visa en lista med refererande filer för en resurs klickar du på resursen i **[!UICONTROL Dependencies]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Klicka på **[!UICONTROL View Properties]** i verktygsfältet. På sidan [!UICONTROL Properties] visas listan med filer som refererar till den aktuella resursen under kolumnen **[!UICONTROL References]** på fliken **[!UICONTROL Basic]**.

   ![visa referenserna för Experience Manager Assets i kolumnen Referenser i tillgångsinformationen](assets/asset-references.png)

   *Bild: Resursreferenser i tillgångsinformation.*

## [!DNL Adobe InDesign]: Lägg till digitala resurser som referenser  {#add-aem-assets-as-references-in-adobe-indesign}

Om du vill referera till digitala resurser från en [!DNL InDesign]-fil, drar du resurserna till [!DNL InDesign]-filen eller exporterar [!DNL InDesign]-filen som ett ZIP-arkiv.

Refererade resurser finns redan i [!DNL Experience Manager Assets]. Du kan extrahera delresurser genom att [konfigurera InDesign Server](indesign.md). Inbäddade resurser i en [!DNL InDesign]-fil extraheras som delresurser.

>[!NOTE]
>
>Om [!DNL InDesign Server] är proxiderad är förhandsgranskningen för [!DNL InDesign]-filerna inbäddad i deras XMP metadata. I det här fallet krävs inte extrahering av miniatyrer uttryckligen. Om [!DNL InDesign Server] inte är proxiderad måste miniatyrbilder extraheras explicit för [!DNL InDesign]-filer.

När en INDD-fil överförs hämtas referenserna genom att resurser med egenskapen `xmpMM:InstanceID` och `xmpMM:DocumentID` hämtas i databasen.

### Skapa referenser genom att dra resurser {#create-references-by-dragging-aem-assets}

Den här proceduren liknar [hur du lägger till digitala resurser som referenser i Adobe Illustrator](#refai).

### Skapa referenser till resurser genom att exportera en ZIP-fil {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Utför stegen i [Skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md) för att skapa ett nytt arbetsflöde.
1. Använd [paketfunktionen](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) i [!DNL Adobe InDesign] för att exportera dokumentet. [!DNL Adobe InDesign] kan exportera ett dokument och de länkade resurserna som ett paket. I det här fallet innehåller den exporterade mappen en `Links`-mapp som innehåller underresurser i [!DNL InDesign]-filen. Mappen `Links` finns i samma mapp som INDD-filen.
1. Skapa en ZIP-fil och överför den till [!DNL Experience Manager]-databasen.
1. Starta `Unarchiver`-arbetsflödet.
1. När arbetsflödet är klart refereras referenserna i mappen Länkar automatiskt till underresurser. Om du vill visa en lista över refererade resurser går du till sidan med tillgångsinformation för [!DNL InDesign]-resursen och stänger [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Lägg till digitala resurser som referenser  {#refps}

1. Använd [!DNL Experience Manager]-datorprogrammet för att komma åt [!DNL Experience Manager Assets]. Hämta och visa resurserna i det lokala filsystemet. Använd funktionen [!UICONTROL Place Linked] i [!DNL Adobe Photoshop]. Se [placera resurser i skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Spara i [!DNL Photoshop]-filen på den monterade enheten eller [överför](/help/assets/manage-assets.md#uploading-assets) till [!DNL Experience Manager]-databasen.
1. När arbetsflödet är klart visas referenserna till befintliga [!DNL Experience Manager]-resurser på sidan med resursinformation.

   Om du vill visa de refererade resurserna stänger du [Rail](/help/sites-authoring/basic-handling.md#rail-selector) på sidan med resursinformation.

1. De refererade resurserna innehåller även en lista med resurser som de refereras till från. Om du vill visa en lista med refererade resurser går du till sidan med tillgångsinformation och stänger [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Resurserna i sammansatta resurser kan också refereras baserat på deras dokument-ID och instans-ID. Den här funktionen är endast tillgänglig med versionerna [!DNL Adobe Illustrator] och [!DNL Adobe Photoshop]. För andra görs en referens på grundval av den relativa sökvägen för länkade tillgångar i den huvudsakliga sammansatta tillgången, som i tidigare versioner av [!DNL Experience Manager].

## Skapa underresurser {#generate-subassets}

För resurser som stöds med flersidiga format - PDF-filer, AI-filer, [!DNL Microsoft PowerPoint]- och [!DNL Apple Keynote]-filer och [!DNL Adobe InDesign]-filer - kan [!DNL Experience Manager] generera delresurser som motsvarar varje enskild sida i den ursprungliga resursen. Dessa underresurser är länkade till *överordnad* resurs och underlättar flersidesvisning. I alla andra syften behandlas delresurserna som vanliga resurser i [!DNL Experience Manager].

Generering av delresurser är inaktiverat som standard. Så här aktiverar du generering av delresurser:

1. Logga in på [!DNL Experience Manager] som administratör. Öppna **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Välj **[!UICONTROL DAM Update Asset]**-arbetsflöde och klicka på **[!UICONTROL Edit]**.
1. Klicka på **[!UICONTROL Toggle Side Panel]** och leta upp steget **[!UICONTROL Create Sub Asset]**. Lägg till steget i arbetsflödet. Klicka på **[!UICONTROL Sync]**.

Gör något av följande om du vill generera delresurserna:

* Nya resurser: Arbetsflödet [!UICONTROL DAM Update Assets] körs på alla nya resurser som överförs till [!DNL Experience Manager]. Delresurser genereras automatiskt för nya flersidiga resurser.
* Befintliga flersidiga resurser: Kör arbetsflödet [!UICONTROL DAM Update Assets] manuellt enligt något av stegen:

   * Markera en resurs och klicka på [!UICONTROL Timeline] för att öppna den vänstra panelen. Du kan även använda kortkommandot `alt + 3`. Klicka på [!UICONTROL Start Workflow], välj [!UICONTROL DAM Update Asset], klicka på [!UICONTROL Start] och klicka på [!UICONTROL Proceed].
   * Markera en resurs och klicka på [!UICONTROL Create] > [!UICONTROL Workflow] i verktygsfältet. Välj [!UICONTROL DAM Update Asset]-arbetsflöde i popup-dialogrutan, klicka på [!UICONTROL Start] och klicka på [!UICONTROL Proceed].

Kör arbetsflödet **[!UICONTROL DAM Parse Word Documents]** för Microsoft Word-dokument. Den genererar en `cq:Page`-komponent från innehållet i Microsoft Word-dokumentet. De bilder som extraheras från dokumentet refereras från `cq:Page`-komponenten. Dessa bilder extraheras även om generering av delresurser är inaktiverat.

## Visa delresurser {#viewing-subassets}

Delresurserna visas bara om delresurserna genereras och är tillgängliga för den valda flersidiga resursen. Om du vill visa de genererade delresurserna öppnar du flersidesresursen. Klicka på ![Alternativ för att öppna den vänstra listen](assets/do-not-localize/aem_leftrail_contentonly.png) i den övre vänstra delen av sidan och klicka på **[!UICONTROL Subassets]** i listan. När du väljer **[!UICONTROL Subassets]** i listan. Du kan även använda kortkommandot `alt + 5`.

![Visa delresurser för en flersidig resurs](assets/view_subassets_simulation.gif)

## Visa sidor i en flersidig fil {#view-pages-of-a-multi-page-file}

Du kan visa en flersidig fil, till exempel PDF-, INDD-, PPT-, PPTX- och AI-filer, med hjälp av funktionen för sidvisningsprogram i [!DNL Experience Manager Assets]. Öppna en flersidig resurs och klicka på **[!UICONTROL View Pages]** i det övre vänstra hörnet på sidan. Sidvisningsprogrammet som öppnas visar sidorna för resursen och kontrollerna för att bläddra igenom och zooma varje sida.

![Visa och visa sidor för en flersidig resurs](assets/view_multipage_asset_fmr.gif)

För [!DNL InDesign] kan du extrahera sidor med [!DNL InDesign Server]. Om förhandsgranskningarna av sidorna sparas när [!DNL InDesign]-filen skapas behövs inte [!DNL InDesign Server] för sidextrahering.

Följande alternativ är tillgängliga i verktygsfältet, i den vänstra listen och i kontrollerna i sidvisningsprogrammet:

* **[!UICONTROL Desktop Actions]** för att öppna eller visa en viss underresurs med  [!DNL Experience Manager] skrivbordsappen. Se hur du [konfigurerar skrivbordsåtgärder](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) om du använder [!DNL Experience Manager]-datorprogrammet.

* **[!UICONTROL Properties]** öppnar  [!UICONTROL Properties] sidan för den specifika underresursen.

* **[!UICONTROL Annotate]** kan du göra anteckningar i den specifika underresursen. De anteckningar du använder på separata underresurser samlas in och visas tillsammans när den överordnade resursen öppnas för visning.

* **[!UICONTROL Page Overview]** visar alla delresurser samtidigt.

* **[!UICONTROL Timeline]** efter att du klickat på  ![Alternativ för att öppna vänster ](assets/do-not-localize/aem_leftrail_contentonly.png) räcke visas filens aktivitetsström.

## God praxis och begränsning {#best-practice-limitation-tips}

* Generering av delresurser kan vara mycket resurskrävande för alla [!DNL Experience Manager]-distributioner. Om du genererar delresurser när komplexa resurser överförs lägger du till steget i arbetsflödet DAM-uppdatering av resurser. Om du genererar delresurser on demand skapar du ett separat arbetsflöde för att generera delresurser. Med ett dedikerat arbetsflöde kan du hoppa över de andra stegen i arbetsflödet för DAM-uppdatering av resurser och spara beräkningsresurser.

>[!MORELIKETHIS]
>
>* [Använd Adobe Experience Manager datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Konfigurera skrivbordsåtgärder i Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Skapa länkade smarta objekt i Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Montera grafik i Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

