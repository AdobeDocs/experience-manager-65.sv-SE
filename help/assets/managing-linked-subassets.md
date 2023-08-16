---
title: Hantera sammansatta resurser med referenser och flera sidor
description: Lär dig hur du skapar referenser till digitala resurser inifrån [!DNL Adobe InDesign], [!DNL Adobe Illustrator]och [!DNL Adobe Photoshop]. Använd funktionen för sidvisningsprogram för att visa enskilda underresurssidor för flersidiga filer som PDF, INDD, PPT, PPTX och AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 0%

---

# Hantera sammansatta och flersidiga resurser {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] kan identifiera om en överförd fil innehåller referenser till resurser som redan finns i databasen. Den här funktionen är endast tillgänglig för filformat som stöds. Om den överförda resursen innehåller referenser till [!DNL Experience Manager] resurser skapas en dubbelriktad länk mellan de överförda och refererade resurserna.

Förutom att eliminera redundans kan du referera till resurserna i [!DNL Adobe Creative Cloud] applikationerna förbättrar samarbetet och ökar användarnas effektivitet och produktivitet.

[!DNL Experience Manager Assets] har stöd för dubbelriktade referenser. Du kan hitta refererade resurser på sidan med tillgångsinformation i den överförda filen. Dessutom kan du visa de refererande filerna på sidan med resursinformation för den refererade resursen.

Referenser tolkas utifrån sökväg, dokument-ID och instans-ID för de refererade resurserna.

## [!DNL Adobe Illustrator]: Lägg till digitala resurser som referenser {#refai}

Du kan referera till befintliga digitala resurser inifrån en [!DNL Adobe Illustrator] -fil.

1. Använda [[!DNL Experience Manager] datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), hämtar de digitala resurserna i det lokala filsystemet. Navigera till filsystemplatsen för resursen som du vill referera till.
1. Dra resursen från den lokala mappen till [!DNL Illustrator] -fil.

1. Spara [!DNL Illustrator] till den monterade enheten, eller [ladda upp](/help/assets/manage-assets.md#uploading-assets) till [!DNL Experience Manager] databas.

1. När arbetsflödet är klart går du till sidan med tillgångsinformation för resursen. Referenserna till befintliga digitala resurser listas under **[!UICONTROL Dependencies]** i **[!UICONTROL References]** kolumn.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. De refererade resurserna som visas under **[!UICONTROL Dependencies]** kan också refereras av andra filer än den aktuella. Om du vill visa en lista med refererade filer för en resurs klickar du på resursen i listan under **[!UICONTROL Dependencies]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Klicka på **[!UICONTROL View Properties]** i verktygsfältet. I [!UICONTROL Properties] sidan visas listan med filer som refererar till den aktuella resursen under **[!UICONTROL References]** kolumn i **[!UICONTROL Basic]** -fliken.

   ![visa referenserna för Experience Manager Assets i kolumnen Referenser i tillgångsinformationen](assets/asset-references.png)

   *Bild: Resursreferenser i resursinformation.*

## [!DNL Adobe InDesign]: Lägg till digitala resurser som referenser {#add-aem-assets-as-references-in-adobe-indesign}

Referera till digitala resurser inifrån en [!DNL InDesign] filen, dra resurser till [!DNL InDesign] eller exportera [!DNL InDesign] som ett ZIP-arkiv.

Refererade resurser finns redan i [!DNL Experience Manager Assets]. Du kan extrahera delresurser med [konfigurera InDesign Server](indesign.md). Inbäddade resurser i en [!DNL InDesign] filen extraheras som delresurser.

>[!NOTE]
>
>Om [!DNL InDesign Server] är proxiderad, [!DNL InDesign] filer förhandsgranskas inbäddat i deras XMP metadata. I det här fallet krävs inte extrahering av miniatyrer uttryckligen. Om [!DNL InDesign Server] är inte proxiderad, miniatyrbilder måste extraheras explicit för [!DNL InDesign] filer.

När en INDD-fil överförs hämtas referenserna genom att resurser som har `xmpMM:InstanceID` och `xmpMM:DocumentID` i databasen.

### Skapa referenser genom att dra resurser {#create-references-by-dragging-aem-assets}

Den här proceduren liknar [lägga till digitala resurser som referenser i Adobe Illustrator](#refai).

### Skapa referenser till resurser genom att exportera en ZIP-fil {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Utför stegen i [Skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md) för att skapa ett nytt arbetsflöde.
1. Använd [Paketfunktion](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) av [!DNL Adobe InDesign] för att exportera dokumentet. [!DNL Adobe InDesign] kan exportera ett dokument och de länkade resurserna som ett paket. I det här fallet innehåller den exporterade mappen en `Links` mapp som innehåller delresurser i [!DNL InDesign] -fil. The `Links` finns i samma mapp som INDD-filen.
1. Skapa en ZIP-fil och överför den till [!DNL Experience Manager] databas.
1. Starta `Unarchiver` arbetsflöde.
1. När arbetsflödet är klart refereras referenserna i mappen Länkar automatiskt till underresurser. Om du vill visa en lista över refererade resurser går du till sidan med tillgångsinformation på sidan [!DNL InDesign] resurs och stäng [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Lägg till digitala resurser som referenser {#refps}

1. Använd [!DNL Experience Manager] datorprogram som du kommer åt [!DNL Experience Manager Assets]. Hämta och visa resurserna i det lokala filsystemet. Använd [!UICONTROL Place Linked] funktionalitet i [!DNL Adobe Photoshop]. Se [placera resurser i datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Spara som [!DNL Photoshop] till den monterade enheten eller [ladda upp](/help/assets/manage-assets.md#uploading-assets) till [!DNL Experience Manager] databas.
1. När arbetsflödet är klart refererar referenserna till befintliga [!DNL Experience Manager] resurser visas på sidan med tillgångsinformation.

   Om du vill visa de refererade resurserna stänger du [Rail](/help/sites-authoring/basic-handling.md#rail-selector) på sidan med tillgångsinformation.

1. De refererade resurserna innehåller även en lista med resurser som de refereras till från. Om du vill visa en lista med refererade resurser går du till sidan med tillgångsinformation och stänger dialogrutan [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Resurserna i sammansatta resurser kan också refereras baserat på deras dokument-ID och instans-ID. Den här funktionen är tillgänglig med [!DNL Adobe Illustrator] och [!DNL Adobe Photoshop] endast versioner. För andra görs en referens på grundval av den relativa sökvägen för länkade tillgångar i den huvudsakliga sammansatta tillgången, som i tidigare versioner av [!DNL Experience Manager].

## Skapa delresurser {#generate-subassets}

För resurser som stöds i flersidiga format - PDF-filer, AI-filer, [!DNL Microsoft PowerPoint] och [!DNL Apple Keynote] filer, och [!DNL Adobe InDesign] filer — [!DNL Experience Manager] kan generera delresurser som motsvarar varje enskild sida i den ursprungliga tillgången. Dessa delresurser är länkade till *parent* och underlätta flersidig visning. I alla andra syften behandlas deltillgångarna som normala tillgångar i [!DNL Experience Manager].

Generering av delresurser är inaktiverat som standard. Så här aktiverar du generering av delresurser:

1. Logga in [!DNL Experience Manager] som administratör. Öppna **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Välj **[!UICONTROL DAM Update Asset]** och klicka **[!UICONTROL Edit]**.
1. Klicka **[!UICONTROL Toggle Side Panel]** och hitta **[!UICONTROL Create Sub Asset]** steg. Lägg till steget i arbetsflödet. Klicka på **[!UICONTROL Sync]**.

Gör något av följande om du vill generera delresurserna:

* Nya resurser: [!UICONTROL DAM Update Assets] arbetsflödet körs på alla nya resurser som överförs till [!DNL Experience Manager]. Delresurser genereras automatiskt för nya flersidiga resurser.
* Befintliga flersidiga resurser: Kör manuellt [!UICONTROL DAM Update Assets] arbetsflöde som följer något av stegen:

   * Markera en resurs och klicka på [!UICONTROL Timeline] för att öppna den vänstra panelen. Du kan även använda kortkommandot `alt + 3`. Klicka [!UICONTROL Start Workflow], markera [!UICONTROL DAM Update Asset], klicka [!UICONTROL Start]och klicka [!UICONTROL Proceed].
   * Markera en resurs och klicka på [!UICONTROL Create] > [!UICONTROL Workflow] i verktygsfältet. Välj i popup-dialogrutan [!UICONTROL DAM Update Asset] arbetsflöde, klicka [!UICONTROL Start]och klicka [!UICONTROL Proceed].

För Microsoft Word-dokument gäller följande: **[!UICONTROL DAM Parse Word Documents]** arbetsflöde. Det genererar en `cq:Page` från innehållet i Microsoft Word-dokumentet. De bilder som extraheras från dokumentet refereras från `cq:Page` -komponenten. Dessa bilder extraheras även om underresursgenerering är inaktiverad.

>[!NOTE]
>
>I [!UICONTROL Create Sub Asset Process - Step Properties] in [!UICONTROL Process Arguments]kan du ange antalet underresurser som [!DNL Experience Manager] genererar. Standardvärdet är 5. Om du vill generera alla underordnade resurser lämnar du fältet tomt. Om fältet har negativ genereras inga delresurser.

## Visa delresurser {#viewing-subassets}

Delresurserna visas bara om delresurserna genereras och är tillgängliga för den valda flersidiga resursen. Om du vill visa de genererade delresurserna öppnar du flersidesresursen. Klicka på i det övre vänstra området på sidan ![Alternativ för att öppna vänster räl](assets/do-not-localize/aem_leftrail_contentonly.png) och klicka **[!UICONTROL Subassets]** från listan. När du väljer **[!UICONTROL Subassets]** från listan. Du kan även använda kortkommandot `alt + 5`.

![Visa delresurser för en flersidig resurs](assets/view_subassets_simulation.gif)

## Visa sidor i en flersidig fil {#view-pages-of-a-multi-page-file}

Du kan visa en flersidig fil, t.ex. PDF, INDD, PPT, PPTX och AI, med hjälp av sidvisningsprogrammet i [!DNL Experience Manager Assets]. Öppna en flersidig resurs och klicka på **[!UICONTROL View Pages]** från det övre vänstra hörnet på sidan. Sidvisningsprogrammet som öppnas visar sidorna för resursen och kontrollerna för att bläddra igenom och zooma varje sida.

![Visa och visa sidor för en flersidig resurs](assets/view_multipage_asset_fmr.gif)

För [!DNL InDesign]kan du extrahera sidor med [!DNL InDesign Server]. Om förhandsgranskningar av sidor sparas under [!DNL InDesign] skapar sedan [!DNL InDesign Server] krävs inte för sidextrahering.

Följande alternativ är tillgängliga i verktygsfältet, i den vänstra listen och i kontrollerna i Page Viewer:

* **[!UICONTROL Desktop Actions]** för att öppna eller visa en viss underresurs med [!DNL Experience Manager] datorprogram. Se hur man [konfigurera skrivbordsåtgärder](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) om du använder [!DNL Experience Manager] datorprogram.

* **[!UICONTROL Properties]** öppnar [!UICONTROL Properties] sidan för den specifika underresursen.

* **[!UICONTROL Annotate]** gör att du kan anteckna den specifika underresursen. De anteckningar du använder på separata underresurser samlas in och visas tillsammans när den överordnade resursen öppnas för visning.

* **[!UICONTROL Page Overview]** visar alla delresurser samtidigt.

* **[!UICONTROL Timeline]** från vänster ratt efter klickning ![Alternativ för att öppna vänster räl](assets/do-not-localize/aem_leftrail_contentonly.png) visar filens aktivitetsström.

## God praxis och begränsning {#best-practice-limitation-tips}

* Generering av delresurser kan vara mycket resurskrävande för alla [!DNL Experience Manager] distribution. Om du genererar delresurser när komplexa resurser överförs lägger du till steget i arbetsflödet DAM-uppdatering av resurser. Om du genererar delresurser on demand skapar du ett separat arbetsflöde för att generera delresurser. Med ett dedikerat arbetsflöde kan du hoppa över de andra stegen i arbetsflödet för DAM-uppdatering av resurser och spara beräkningsresurser.

>[!MORELIKETHIS]
>
>* [Använd Adobe Experience Manager datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Konfigurera skrivbordsåtgärder i Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Skapa länkade smarta objekt i Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Montera grafik i Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)
