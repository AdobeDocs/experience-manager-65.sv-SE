---
title: Om AEM Assets
description: Läs om vad som är digital resurshantering, användningsexempel och Adobes AEM Asset-erbjudande
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Administrera resurser {#administering-assets}

Resurser är ett DAM-verktyg (Digital Asset Management) som är helt integrerat med AEM-plattformen och som gör att ditt företag kan dela och distribuera digitala resurser. Användare i en hel organisation kan hantera, lagra och komma åt bilder, videor, dokument, ljudklipp och multimedia som Flash-filer för användning på webben, i tryck och för digital distribution.

## Vad är Digital Asset Management? {#what-is-digital-asset-management}

Resurser ger möjlighet till företagsövergripande delning och distribution av en organisations viktigaste digitala resurser. Användare i en hel organisation kan lagra, hantera och komma åt digitala resurser som bilder, grafik, ljud, video och dokument via ett webbgränssnitt (eller en CIFS- eller WebDAV-mapp).

AEM Assets är väl integrerat i AEM och gör följande:

* Lägg in och dela bilder, dokument, ljudfiler och videofiler i en mängd olika filformat.
* Hantera resurser genom att gruppera dem efter taggar, ljusbord eller stjärnor (dina favoriter). Lägg till anteckningar i resurser.
* Sök efter resurser genom att söka efter filnamn, den fullständiga texten i dokument och genom att söka efter datum, dokumenttyp och taggar.
* Lägg till eller redigera metadatainformation för resurser. Metadata versionshanteras automatiskt tillsammans med motsvarande resurs. Du kan importera eller exportera metadata för resurser.
* Utför bildredigeringsfunktioner som skalning och lägga till bildfilter. Importera och exportera flera digitala resurser samtidigt med en WebDAV- eller CIFS-mapp.
* Använd arbetsflöden och meddelanden för att möjliggöra gemensam bearbetning och hämtning av alla typer av resurser och hantera åtkomsträttigheter till resurser.

### AEM Assets är helt integrerat i CQ WCM {#aem-assets-fully-integrated-in-cq-wcm}

AEM Assets är helt integrerat med CQ WCM och funktionalitet finns med hjälp av DAM-ikonen:

![screen_shot_2012-04-17at15946pm](assets/screen_shot_2012-04-17at15946pm.png) ![screen_shot_2012-04-17at20100pm](assets/screen_shot_2012-04-17at20100pm.png)

Resurser som hanteras i CQ DAM kan sedan nås via innehållshanteraren i WCM:

![screen_shot_2012-04-17at20214pm](assets/screen_shot_2012-04-17at20214pm.png)

>[!NOTE]
>
>Den grundläggande GUI-hanteringen är densamma som resten av WCM. Mer information finns i [Översikt över GUI-konsolen](/help/sites-authoring/page-authoring.md) .

### Digital Asset Management jämfört med bildkomponent {#digital-asset-management-versus-image-component}

När du avgör om en bild ska läggas in i AEM Resurser eller användas som AEM Image-komponent bör du överväga bildens livscykel:

* Om bilden har samma livscykel som sidan använder du Image Component (Bildkomponent).
* Om bilden har en separat livscykel, till exempel om du använder bilden två gånger eller utanför WCM, använder du AEM Resurser.

## Vad är digitala resurser? {#what-are-digital-assets}

En resurs är ett digitalt dokument, en bild, en video eller ett ljud (eller en del av ett) som kan ha flera återgivningar och kan ha underresurser (t.ex. lager i en Photoshop-fil, bilder i en PowerPoint-fil, sidor i en PDF-fil, filer i en ZIP-fil).

En resurs är i stort sett en binär resurs plus metadata plus återgivningar plus underresurser. Mer information finns i [DAM-prestandaguiden](/help/sites-deploying/assets-performance-sizing.md) .

>[!CAUTION]
>
>Överföring och/eller redigering av en stor mängd resurser (särskilt bilder) kan påverka CQ-instansens prestanda.

### AEM Assets-terminologi {#aem-assets-terminology}

När du arbetar med digitala resurser i AEM måste du förstå följande terminologi:

* **Samling** En samling resurser, antingen baserat på fysisk plats (mapp), gemensamma egenskaper (sparad sökmapp) eller användarval (lightbox-mappar).

* **Metadatatillgångar** har metadata. till exempel författare, förfallodatum, DRM-information (Digital Rights Management) och så vidare. Metadata är under åtkomstkontroll. AEM Resurser har stöd för följande vanliga metadatascheman:

   * Dublin Core: inklusive författare, beskrivning, datum, ämne och så vidare.
   * IPTC: inklusive händelse, modell, plats och så vidare.
   * WCM: inklusive sidegenskaper, [!UICONTROL On Time] och [!UICONTROL Off Time]osv.

* **Du kan tagga** resurser med taggar och klassificera dem. Se Använda taggar och Administrera taggar.

* **Återgivningar** En återgivning är den binära återgivningen av en resurs. Resurser har alltid en primär representation - den som tillhör den överförda filen. De kan ha valfritt antal ytterligare representationer som skapas, till exempel genom anpassade arbetsflödessteg eller när en resurs överförs. Återgivningar kan ha en annan storlek, med en annan upplösning, med en vattenstämpel eller någon annan förändrad egenskap.

* **Versionshantering** skapar en ögonblicksbild av digitala resurser vid en viss tidpunkt. Du kan återställa resurser till tidigare versioner. Se Versionshantering i AEM Resurser.

* **Delresurser** är resurser som utgör en resurs, till exempel lager i en Adobe Photoshop-fil eller sidor i en PDF-fil. I AEM Resurser kan du hantera underresurser på samma sätt som du hanterar resurser.

### Så här arbetar du med resurser {#how-to-work-with-assets}

Du utför en åtgärd på en resurs eller samling. Funktionsmakron kan skapa och ändra resurser, samlingar och återgivningar. Många av de grundläggande åtgärder du utför på resurser - överföra, ta bort, uppdatera, spara underresurser - utlöser förkonfigurerade arbetsflöden. Dessa aktiveras automatiskt i AEM Resurser och beskrivs i detalj i mediehanterare för AEM Resurser.

De uppgifter du kan utföra med dessa förkonfigurerade arbetsflöden:

* spara resursen i eller ta bort resursen från databasen.
* extrahera och spara metadata för resursen, de enskilda metadataobjekten sparas som XMP.
* generera återgivningar och miniatyrbilder för resursen, inklusive automatisk storleksändring och beskärning vid behov.
* vid behov omkoda tillgången. Video för mobil- och webbanvändning omkodas till exempel med 24 bildrutor per sekund, och video hämtas med 30 bildrutor per sekund. Ljud för mobil- och webbanvändning omkodas med 128 kbit/s, ljud för nedladdning med 192 kbit/s.

Du kan förstås även använda arbetsflöden manuellt. En lista med standardarbetsflöden finns i [AEM Assets Media](/help/assets/media-handlers.md)Handler.

## AEM Assets och AEM MediaLibrary {#cq-dam-vs-cq-medialibrary}

Mer information om skillnaderna finns i [AEM Assets och AEM MediaLibrary](/help/assets/medialibrary.md) .
