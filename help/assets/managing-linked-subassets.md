---
title: Hantera sammansatta resurser med referenser och flersidiga resurser i Adobe Experience Manager.
description: Lär dig hur du skapar referenser till digitala resurser från Adobe InDesign, Adobe Illustrator och Adobe Photoshop. Använd funktionen för sidvisningsprogram för att visa enskilda underresurssidor för flersidiga filer som PDF-, INDD-, PPT-, PPTX- och AI-filer.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 790efeaff6c8cf7e60104601e08955180dbb9600

---


# Hantera sammansatta och flersidiga resurser {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] kan identifiera om en överförd fil innehåller referenser till resurser som redan finns i databasen. Den här funktionen är endast tillgänglig för filformat som stöds. Om den överförda resursen innehåller referenser till Experience Manager-resurser skapas en dubbelriktad länk mellan de överförda och refererade resurserna.

Förutom att eliminera redundans kan du förbättra samarbetet och öka användarnas effektivitet och produktivitet genom att referera till resurserna i Adobe Creative Cloud-programmen.

[!DNL Experience Manager Assets] har stöd för dubbelriktade referenser. Du kan hitta refererade resurser på sidan med tillgångsinformation i den överförda filen. Dessutom kan du visa de refererande filerna på sidan med resursinformation för den refererade resursen.

Referenser tolkas utifrån sökväg, dokument-ID och instans-ID för de refererade resurserna.

## Lägg till digitala resurser som referenser i [!DNL Adobe Illustrator]{#refai}

Du kan referera till befintliga digitala resurser inifrån en [!DNL Adobe Illustrator] fil.

1. Hämta digitala resurser till det lokala filsystemet med hjälp av [Experience Manager-datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html). Navigera till filsystemplatsen för resursen som du vill referera till.
1. Dra resursen från den lokala mappen till [!DNL Illustrator] filen.

1. Spara [!DNL Illustrator] filen på den monterade enheten eller [överför](/help/assets/managing-assets-touch-ui.md#uploading-assets) den till Experience Manager-databasen.

1. När arbetsflödet är klart går du till sidan med resursinformation för resursen. Referenserna till befintliga digitala resurser visas under **[!UICONTROL Beroenden]** i kolumnen **[!UICONTROL Referenser]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. De refererade resurserna som visas under **[!UICONTROL Beroenden]** kan också refereras av andra filer än den aktuella. Om du vill visa en lista med referensfiler för en resurs klickar du på resursen under **[!UICONTROL Beroenden]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Klicka på **[!UICONTROL Visa egenskaper]** i verktygsfältet. På sidan [!UICONTROL Egenskaper] visas listan med filer som refererar till den aktuella resursen under kolumnen **[!UICONTROL Referenser]** på fliken **[!UICONTROL Grundläggande]** .

   ![visa referenserna för Experience Manager Assets i kolumnen Referenser i resursinformationen](assets/asset-references.png)

   *Bild: Resursreferenser i tillgångsinformation*

## Lägg till digitala resurser som referenser i [!DNL Adobe InDesign]{#add-aem-assets-as-references-in-adobe-indesign}

Om du vill referera till digitala resurser från en [!DNL InDesign] fil drar du resurserna till [!DNL InDesign] filen eller exporterar [!DNL InDesign] filen som ett ZIP-arkiv.

Refererade resurser finns redan i [!DNL Experience Manager Assets]. Du kan extrahera delresurser genom att [konfigurera InDesign Server](indesign.md). Inbäddade resurser i en [!DNL InDesign] fil extraheras som delresurser.

>[!NOTE]
>
>Om bilden [!DNL InDesign Server] [!DNL InDesign] är en proxy bäddas förhandsvisningen in i filernas XMP-metadata. I det här fallet krävs inte extrahering av miniatyrer uttryckligen. Om [!DNL InDesign Server] filen inte är proxiderad måste miniatyrbilder extraheras explicit för [!DNL InDesign] filer.

### Skapa referenser genom att dra resurser {#create-references-by-dragging-aem-assets}

Den här proceduren liknar hur du [lägger till digitala resurser som referenser i Adobe Illustrator](#refai).

### Skapa referenser till resurser genom att exportera en ZIP-fil {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Utför stegen i [Skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md) för att skapa ett nytt arbetsflöde.
1. Använd funktionen Packa i för [!DNL Adobe InDesign] att exportera dokumentet. [!DNL Adobe InDesign] kan exportera ett dokument och de länkade resurserna som ett paket. I det här fallet innehåller den exporterade mappen en länkmapp som innehåller underresurser i [!DNL InDesign] filen.
1. Skapa en ZIP-fil och överför den till [!DNL Experience Manager] databasen.
1. Starta `Unarchiver` arbetsflödet.
1. När arbetsflödet är klart refereras referenserna i mappen Länkar automatiskt till underresurser. Om du vill visa en lista med refererade resurser går du till sidan med tillgångsinformation för [!DNL InDesign] resursen och stänger [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## Lägg till digitala resurser som referenser i [!DNL Adobe Photoshop]{#refps}

1. Använd [!DNL Experience Manager] skrivbordsappen för att komma åt [!DNL Experience Manager Assets]. Hämta och visa resurserna i det lokala filsystemet. Använd funktionen [!UICONTROL Montera länkad] i [!DNL Adobe Photoshop]. Se [placera resurser i skrivbordsappen](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Spara som [!DNL Photoshop] fil till den monterade enheten eller [överför](/help/assets/managing-assets-touch-ui.md#uploading-assets) till [!DNL Experience Manager] databasen.
1. När arbetsflödet är klart visas referenserna till befintliga [!DNL Experience Manager] resurser på sidan med resursinformation.

   Om du vill visa de refererade resurserna stänger du [Rail](/help/sites-authoring/basic-handling.md#rail-selector) på sidan med tillgångsinformation.

1. De refererade resurserna innehåller även en lista med resurser som de refereras till från. Om du vill visa en lista med refererade resurser går du till sidan med tillgångsinformation och stänger [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Resurserna i sammansatta resurser kan också refereras baserat på deras dokument-ID och instans-ID. Den här funktionaliteten finns endast för [!DNL Adobe Illustrator] och [!DNL Adobe Photoshop] versioner. För andra görs en referens på grundval av den relativa sökvägen för länkade tillgångar i den huvudsakliga sammansatta tillgången, som i tidigare versioner av [!DNL Experience Manager].

## Skapa delresurser {#generate-subassets}

För resurser som stöds i flersidiga format - PDF-filer, AI-filer [!DNL Microsoft PowerPoint] , [!DNL Apple Keynote] filer och [!DNL Adobe InDesign] filer - [!DNL Experience Manager] kan du generera delresurser som motsvarar varje enskild sida i den ursprungliga resursen. Dessa delresurser är länkade till den *överordnade* resursen och underlättar flersidesvisning. I alla andra syften behandlas deltillgångarna som normala tillgångar i [!DNL Experience Manager].

Generering av delresurser är inaktiverat som standard. Så här aktiverar du generering av delresurser:

1. Logga in på Experience Manager som administratör. Öppna **[!UICONTROL Verktyg > Arbetsflöde > Modeller]**.
1. Välj arbetsflöde för **[!UICONTROL DAM-uppdatering av resurser]** och klicka på **[!UICONTROL Redigera]**.
1. Klicka på **[!UICONTROL Växla sidopanel]** och leta upp steget **[!UICONTROL Skapa underresurs]** . Lägg till steget i arbetsflödet. Klicka på **[!UICONTROL Synkronisera]**.

Gör något av följande om du vill generera delresurserna:

* Nya resurser: Arbetsflödet för [!UICONTROL DAM-uppdatering av resurser] körs på alla nya resurser som överförs till [!DNL Experience Manager]. Delresurser genereras automatiskt för nya flersidiga resurser.
* Befintliga flersidiga resurser: Kör arbetsflödet [!UICONTROL DAM Update Assets] manuellt enligt något av följande:

   * Markera en resurs och klicka på [!UICONTROL Tidslinje] för att öppna den vänstra panelen. Du kan också använda kortkommandot `alt + 3`. Klicka på [!UICONTROL Starta arbetsflöde], välj [!UICONTROL DAM-uppdateringsresurs], klicka på [!UICONTROL Start]och sedan på [!UICONTROL Fortsätt].
   * Markera en resurs och klicka på [!UICONTROL Skapa > Arbetsflöde] i verktygsfältet. I popup-dialogrutan väljer du arbetsflöde för [!UICONTROL DAM-uppdatering av resurs] , klickar på [!UICONTROL Start]och sedan på [!UICONTROL Fortsätt].

För Microsoft Word-dokument gäller att du ska köra arbetsflödet **[!UICONTROL DAM-tolka Word-dokument]** . Det genererar en `cq:Page` komponent från innehållet i Microsoft Word-dokumentet. De bilder som extraheras från dokumentet refereras från `cq:Page` komponenten. Dessa bilder extraheras även om generering av delresurser är inaktiverat.

## Visa delresurser {#viewing-subassets}

Delresurserna visas bara om delresurserna genereras och är tillgängliga för den valda flersidiga resursen. Om du vill visa de genererade delresurserna öppnar du flersidesresursen. Klicka på ikonen ![för](assets/do-not-localize/aem_leftrail_contentonly.png) vänsterkant i det övre vänstra området på sidan och klicka på **[!UICONTROL Delresurser]** i listan. När du väljer **[!UICONTROL Delresurser]** i listan. Du kan också använda kortkommandot `alt + 5`.

![Visa delresurser för en flersidig resurs](assets/view_subassets_simulation.gif)

## Visa sidor i en flersidig fil {#view-pages-of-a-multi-page-file}

Du kan visa en flersidig fil, till exempel PDF-, INDD-, PPT-, PPTX- och AI-filer, med hjälp av funktionen för sidvisning i [!DNL Experience Manager Assets]. Öppna en flersidig resurs och klicka på **[!UICONTROL Visa sidor]** i det övre vänstra hörnet på sidan. Sidvisningsprogrammet som öppnas visar sidorna för resursen och kontrollerna för att bläddra igenom och zooma varje sida.

![Visa och visa sidor för en flersidig resurs](assets/view_multipage_asset_fmr.gif)

Du kan till [!DNL InDesign]exempel extrahera sidor med [!DNL InDesign Server]. Om förhandsvisningarna av sidorna sparas när [!DNL InDesign] filen skapas [!DNL InDesign Server] behövs inte för sidextraheringen.

Följande alternativ är tillgängliga i verktygsfältet, i den vänstra listen och i kontrollerna i sidvisningsprogrammet:

* **[!UICONTROL Skrivbordsåtgärder]** för att öppna eller visa en viss underresurs med [!DNL Experience Manager] datorprogrammet. Se hur du [konfigurerar skrivbordsåtgärder](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) om du använder [!DNL Experience Manager] datorprogrammet.

* **[!UICONTROL Alternativet Egenskaper]** öppnar sidan [!UICONTROL Egenskaper] för den specifika underresursen.

* **[!UICONTROL Alternativet Anteckna]** gör att du kan anteckna i den specifika underresursen. De anteckningar du använder på separata underresurser samlas in och visas tillsammans när den överordnade resursen öppnas för visning.

* **[!UICONTROL Alternativet Sidöversikt]** visar alla delresurser samtidigt.

* **[!UICONTROL Alternativet Tidslinje]** i den vänstra listen när du har klickat på ikonen ![för](assets/do-not-localize/aem_leftrail_contentonly.png) vänster spår visas filens aktivitetsström.

>[!MORELIKETHIS]
>
>* [Använd datorprogrammet Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)
>* [Konfigurera skrivbordsåtgärder i Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Skapa länkade smarta objekt i Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Montera bilder i Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)