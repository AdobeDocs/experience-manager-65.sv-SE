---
title: Introduktion till [!DNL Adobe Experience Manager Assets].
description: Lär dig vad som är digital resurshantering, användningsexempel och [!DNL Adobe Experience Manager Asset] erbjudande.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---


# Om [!DNL Adobe Experience Manager Assets] som en DAM-lösning {#administering-assets}

[!DNL Assets] är ett DAM-verktyg (Digital Asset Management) som är en integrerad del av  [!DNL Experience Manager] plattformen och gör det möjligt för företaget att hantera och distribuera digitala resurser. Användare i en hel organisation kan hantera, lagra och få tillgång till många typer av digitalt material som bilder, videor, dokument, ljudklipp, 3D-filer och multimedia för användning på webben, i tryck och för digital distribution.

## Vad är Digital Asset Management? {#what-is-digital-asset-management}

[!DNL Assets] erbjuder företagsövergripande delning och distribution av en organisations viktigaste digitala resurser. Användare i en hel organisation kan lagra, hantera och komma åt digitala resurser som bilder, grafik, ljud, video och dokument via ett webbgränssnitt (eller en CIFS- eller WebDAV-mapp).

[!DNL Assets] kan du  [!DNL Experience Manager] göra följande:

* Lägg in och dela bilder, dokument, ljudfiler och videofiler i en mängd olika filformat.
* Hantera resurser genom att gruppera dem efter taggar, ljusbord eller stjärnor (dina favoriter). Lägg till anteckningar i resurser.
* Sök efter resurser genom att söka efter filnamn, den fullständiga texten i dokument och genom att söka efter datum, dokumenttyp och taggar.
* Lägg till eller redigera metadatainformation för resurser. Metadata versionshanteras automatiskt tillsammans med motsvarande resurs. Du kan importera eller exportera metadata för resurser.
* Utför bildredigeringsfunktioner som skalning och lägga till bildfilter. Importera och exportera flera digitala resurser samtidigt med en WebDAV- eller CIFS-mapp.
* Använd arbetsflöden och meddelanden för att möjliggöra gemensam bearbetning och hämtning av alla typer av resurser och hantera åtkomsträttigheter till resurser.

### [!DNL Experience Manager Assets] är integrerat med  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] är helt integrerat med  [!DNL Sites] och fungerar smidigt för alla användningsområden. När du skapar webbsidor kan till exempel [!DNL Sites]-författarna hitta och använda de digitala resurserna via Innehållssökning. Användargränssnittet för [!DNL Assets] är detsamma som för [!DNL Sites]. Mer information finns i [översikt över platser](/help/sites-authoring/page-authoring.md).

Det grundläggande användargränssnittet är samma som för [!DNL Sites]. Mer information finns i [Översikt över platserna](/help/sites-authoring/page-authoring.md).

### Digital Asset Management jämfört med bildkomponenten {#digital-asset-management-versus-image-component}

När du avgör om en bild ska placeras i DAM-databasen eller om bildkomponenten ska användas, bör du tänka på bildens livscykel:

* Om bilden har samma livscykel som sidan använder du Image Component (Bildkomponent).
* Om bilden har en separat livscykel, till exempel om du använder bilden två gånger eller utanför WCM, använder du [!DNL Assets].

## Vad är digitala resurser? {#what-are-digital-assets}

En resurs är ett digitalt dokument, en bild, en video eller ett ljud (eller en del av ett) som kan ha flera återgivningar och kan ha underresurser (t.ex. lager i en Photoshop-fil, bilder i en PowerPoint-fil, sidor i en PDF-fil, filer i en ZIP-fil).

En resurs är i stort sett en binär resurs plus metadata plus återgivningar plus underresurser. Mer information finns i [DAM Performance Guide](/help/sites-deploying/assets-performance-sizing.md).

>[!CAUTION]
>
>Överföring och/eller redigering av en stor mängd resurser (särskilt bilder) kan påverka prestandan för din [!DNL Experience Manager]-distribution.

### [!DNL Experience Manager Assets] terminologi  {#aem-assets-terminology}

När du arbetar med digitala resurser i [!DNL Experience Manager] måste du förstå följande terminologi:

* **Samling**: En samling resurser, antingen baserat på fysisk plats (mapp), gemensamma egenskaper (sparad sökmapp) eller användarval (lightbox-mappar).

* **** [!DNL Assets] Metadata. till exempel författare, förfallodatum, DRM-information (Digital Rights Management) och så vidare. Metadata är under åtkomstkontroll. [!DNL Assets] har stöd för följande vanliga metadatascheman:

   * Dublin Core: inklusive författare, beskrivning, datum, ämne och så vidare.
   * IPTC: inklusive händelse, modell, plats och så vidare.
   * WCM: inkluderar sidegenskaper, [!UICONTROL On Time] och [!UICONTROL Off Time], och så vidare.

* **Taggning**:  [!DNL Assets] kan taggas och klassificeras. Se [ordna resurser](/help/assets/organize-assets.md).

* **Återgivningar**: En återgivning är den binära representationen av en resurs. [!DNL Assets] har alltid en primär representation - den överförda filen. De kan ha valfritt antal ytterligare representationer som skapas, till exempel genom anpassade arbetsflödessteg eller när en resurs överförs. Återgivningar kan ha en annan storlek, med en annan upplösning, med en vattenstämpel eller någon annan förändrad egenskap.

* **Versioner**: Versionshantering skapar en ögonblicksbild av digitala resurser vid en viss tidpunkt. Du kan återställa resurser till tidigare versioner. Se [versionshantering i Resurser](manage-assets.md#asset-versioning).

* **Deltillgångar**: Delresurser är resurser som utgör en resurs, till exempel lager i en  [!DNL Adobe Photoshop] fil eller sidor i en PDF-fil. I [!DNL Assets] kan du hantera delresurser på samma sätt som du hanterar resurser.

### Så här arbetar du med resurser {#how-to-work-with-assets}

Du utför en åtgärd på en resurs eller samling. Funktionsmakron kan skapa och ändra resurser, samlingar och återgivningar. Många av de grundläggande åtgärder du utför på resurser - överföra, ta bort, uppdatera, spara underresurser - utlöser förkonfigurerade arbetsflöden. Dessa aktiveras automatiskt i [!DNL Assets] och beskrivs i detalj i [!DNL Assets]-mediehanterare.

De uppgifter du kan utföra med dessa förkonfigurerade arbetsflöden:

* Spara resursen i eller ta bort resursen från databasen.
* Extrahera och spara metadata för resursen; de enskilda metadataobjekten sparas som XMP.
* Generera återgivningar och miniatyrbilder för resursen. inklusive automatisk storleksändring och beskärning vid behov.
* Omkoda tillgången där det behövs. Video för mobil- och webbanvändning omkodas till exempel med 24 bildrutor per sekund, och video hämtas med 30 bildrutor per sekund. Ljud för mobil- och webbanvändning omkodas med 128 kbit/s, ljud för nedladdning med 192 kbit/s.

Du kan förstås även använda arbetsflöden manuellt. En lista över standardarbetsflöden finns i [Resursmediehanterare](/help/assets/media-handlers.md).

## [!DNL Experience Manager Assets] och  [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

Mer information om skillnaderna finns i [Assets and MediaLibrary](/help/assets/medialibrary.md).
