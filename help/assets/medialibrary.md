---
title: Jämför [!DNL Assets] och Mediebibliotek
description: Jämför [!DNL Experience Manager Assets] och Mediebibliotek och se skillnaderna.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# [!DNL Experience Manager Assets] jämfört med  [!DNL Experience Manager] mediebibliotek  {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] är en viktig del av  [!DNL Experience Manager] plattformen. Denna smidiga integrering ses som en stor fördel med [!DNL Experience Manager] och säkerställer enhetlighet i innehållshanteringen och hög produktivitet för skribenter.

## Vanliga frågor {#frequently-asked-questions}

### Vad är [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] är en funktion i  [!DNL Experience Manager] vilken användare kan hantera sina digitala resurser (bilder, videoklipp, dokument och ljudklipp) i en webbaserad databas. [!DNL Assets] innehåller metadata-support, renderingar, sökaren och administrationsgränssnittet.

### Vad är mediebiblioteket [!DNL Experience Manager]? {#what-is-the-aem-media-library}

Mediebiblioteket [!DNL Experience Manager] är en del av [!DNL Experience Manager] WCM-innehållskatalogen där bilder och andra delade resurser lagras. Mediebiblioteket innehåller grundläggande funktioner för hantering av digitala resurser för WCM.

### Vad får jag från [!DNL Assets] som inte är en del av WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Unika funktioner som bara är tillgängliga för kunder med [!DNL Assets] är:

* möjlighet att extrahera och redigera andra metadata än titel, taggar och beskrivning.
* [!DNL Assets]-administratören som är tillgänglig från välkomstskärmen.
* alla arbetsflödessteg som rör hantering av digitala resurser, t.ex. hämtning, borttagning av resurser, hantering av underresurser, extrahering av metadata.
* bibliotek som innehåller `dam` i paketutrymmet.

För att använda dessa funktioner krävs en giltig licens för [!DNL Assets].

### Är [!DNL Assets] tillgängligt som ett separat paket? {#is-aem-assets-available-as-a-separate-package}

Nej. Alla [!DNL Experience Manager]-program och tillägg levereras i ett och samma paket med alla funktioner inkluderade för att underlätta installation och driftsättning. Det innebär inte att du har behörighet att använda alla funktioner i paketet.

### Jag vill redigera metadata för digitala resurser. Behöver jag [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Om du planerar att redigera andra metadata än titel, beskrivning och taggar måste du licensiera [!DNL Assets].

### Jag vill använda kategoripredikatet på min webbplats. Behöver jag [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Ja, kategoripredikatet är en del av [!DNL Assets] och kräver en [!DNL Assets]-licens.

### Jag vill automatiskt ändra storlek på bilder vid import. Behöver jag [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Nej. Storleksändring och automatisk arbetsflödesdriven omvandling av statiska bilder samt möjligheten att hantera återgivningar ingår i mediebiblioteket [!DNL Experience Manager]. Dessa funktioner kräver ingen [!DNL Assets]-licens.

### Jag vill ändra storlek på bilder med en anpassad bildkomponent. Behöver jag [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Bildkomponenten är en del av WCM. Grafikbiblioteket som används av bildkomponenten (men även av [!DNL Assets]) är en del av [!DNL Experience Manager]-plattformen och kräver ingen [!DNL Assets]-licens.

### Hur förhindrar jag att mina användare använder [!DNL Assets] om jag inte har licens för [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Du kan ta bort alla [!DNL Assets]-specifika arbetsflöden, komponenter, taxonomier, alternativ och administratören för [!DNL Assets] från [!DNL Experience Manager]. På så sätt förhindras användarna från att oavsiktligt använda [!DNL Assets]-funktioner som du inte har licensierat.

### Jag vill lägga till bilder på en sida och vill beskära och ändra storlek på dessa bilder. Behöver jag Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

I det här fallet behöver du inte köpa [!DNL Assets], inte ens mediebiblioteket behöver använda bilder på en webbplats eftersom den smarta bildkomponenten tillåter att bilder överförs direkt till sidan.

### En detaljerad lista över funktioner som är tillgängliga i [!DNL Assets] vs mediebibliotek {#listoffeatures}

**Experience Manager Assets**

* Samlingar och ljusbord
* Avancerade metadataegenskaper och hantering
* Adobe Asset Link (anslut till Creative Cloud for enterprise)
* [!DNL Experience Manager] datorprogram
* Bearbeta profiler
* [!DNL Adobe InDesign Server] integration
* Resursmallar och katalogproduktionsramverk
* [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]och  [!DNL Adobe InDesign] integrering
* Hantering av flerspråkiga resurser
* PIM-integrering
* Rättighetshantering
* Camera Raw stöd
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
