---
title: Jämför Adobe Experience Manager Assets och Media Library.
description: Jämför Experience Manager Assets och Media Library och se skillnaderna.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 1%

---


# Experience Manager Assets jämfört med Experience Manager Media Library {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager Assets är en viktig del av Experience Manager-plattformen. Denna smidiga integrering ses som en stor fördel med Experience Manager och säkerställer enhetlighet i innehållshanteringen och hög produktivitet för innehållsförfattare.

## Vanliga frågor {#frequently-asked-questions}

### Vad är Assets? {#what-is-aem-assets}

Assets är en funktion i Experience Manager som gör att användare kan hantera sina digitala resurser (bilder, videor, dokument och ljudklipp) i en webbaserad databas. Materialet innehåller metadata-support, renderingar, sökaren och administrationsgränssnittet.

### Vad är Experience Manager Media Library? {#what-is-the-aem-media-library}

Experience Manager Media Library är en utsedd del av Experience Manager WCM-innehållslagringsplatsen där bilder och andra delade resurser lagras. Mediebiblioteket innehåller grundläggande funktioner för hantering av digitala resurser för WCM.

### Vad får jag från Assets som inte ingår i WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Unika funktioner som bara är tillgängliga för kunder av Assets är:

* möjlighet att extrahera och redigera andra metadata än titel, taggar och beskrivning.
* Resursadministratören som är tillgänglig från välkomstskärmen.
* alla arbetsflödessteg som rör hantering av digitala resurser, t.ex. hämtning, borttagning av resurser, hantering av underresurser, extrahering av metadata.
* bibliotek inklusive `dam` i paketutrymmet.

Dessa funktioner kräver en giltig licens för Assets.

### Är resurser tillgängliga som ett separat paket? {#is-aem-assets-available-as-a-separate-package}

Nej. För att underlätta installation och driftsättning levereras alla Experience Manager-program och tillägg i ett enda paket med alla funktioner inkluderade. Detta innebär inte att du har behörighet att använda alla funktioner i paketet.

### Jag vill redigera metadata för digitala resurser. Behöver jag Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Om du planerar att redigera andra metadata än titel, beskrivning och taggar måste du licensiera Assets.

### Jag vill använda kategoripredikatet på min webbplats. Behöver jag Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Ja, kategoripredikatet är en del av Assets och kräver en Assets-licens.

### Jag vill automatiskt ändra storlek på bilder vid import. Behöver jag Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Nej. Storleksändring och automatisk arbetsflödesdriven omvandling av statiska bilder samt möjligheten att hantera återgivningar ingår i Experience Manager Media Library. Dessa funktioner kräver ingen Assets-licens.

### Jag vill ändra storlek på bilder med en anpassad bildkomponent. Behöver jag Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Bildkomponenten är en del av WCM. Det grafikbibliotek som används av bildkomponenten (men även av Assets) är en del av Experience Manager-plattformen och kräver ingen Assets-licens.

### Hur kan jag hindra mina användare från att använda Assets om jag inte har licensierat Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Du kan ta bort alla resursspecifika arbetsflöden, komponenter, taxonomier, alternativ och Assets-administratören från Experience Manager. På så sätt förhindras användarna från att oavsiktligt använda Assets-funktioner som du inte har licensierat.

### Jag vill lägga till bilder på en sida och vill beskära och ändra storlek på dessa bilder. Behöver jag Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

I det här fallet behöver du inte köpa Assets, inte ens mediebiblioteket behöver använda bilder på en webbplats eftersom den smarta bildkomponenten tillåter att bilder överförs direkt till sidan.

### En detaljerad lista över funktioner som är tillgängliga i Assets vs Media Library {#listoffeatures}

**Experience Manager Assets**

* Samlingar och ljusbord
* Avancerade metadataegenskaper och hantering
* Adobe Asset Link (anslut till Creative Cloud for enterprise)
* Experience Manager-datorprogram
* Bearbeta profiler
* [!DNL Adobe InDesign Server] integration
* Resursmallar och katalogproduktionsramverk
* [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]och [!DNL Adobe InDesign] integrering
* Hantering av flerspråkiga resurser
* PIM-integrering
* Rättighetshantering
* Stöd för Camera RAW
* Hantering och konfiguration av sökansikten
* Färdiga DAM-arbetsflöden (till exempel fotografering)
* Resursrapportering och -analys som kallas insikter
* 3D-resurshantering
* Anslutna resurser
* Varumärkesportal
* Självbetjäningsåtkomst
* Sök, sök och ladda ned
* Samlingar och mappdelning
* Administratörsverktyg och gränssnitt
* Smart taggning
* Visuell sökning

**Mediebibliotek**

* Grundläggande metadataegenskaper
* Tagghantering
* Versionskontroll
* Statiska återgivningar
* Projekt, uppgifter, arbetsflödesutveckling
* Aktivitetsström (tidslinje)
* Query Builder (API)
* Integrering med Marketing Cloud
* Anpassning och tillägg av användargränssnitt
* Kommentarer och kommentarer
