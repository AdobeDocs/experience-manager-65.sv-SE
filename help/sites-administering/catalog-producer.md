---
title: Katalogproducent
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Katalogproducent
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Katalogproducent{#catalog-producer}

Lär dig hur du använder Catalog Producer i AEM Assets för att generera produktkataloger med dina digitala resurser.

Med Adobe Experience Manager (AEM) Assets Catalog Producer kan du skapa kataloger för dina varumärkesprodukter med hjälp av InDesign-mallar som importeras från ett InDesign-program. Om du vill importera InDesign-mallar måste du först integrera AEM Assets med en InDesign-server.

## Integrering med InDesign-server {#integrating-with-indesign-server}

Som en del av integrationsprocessen konfigurerar du **DAM-uppdateringsresurs** arbetsflöde som är lämpligt för integrering med InDesign. Konfigurera dessutom en proxyarbetare för InDesign-servern. Mer information finns i [Integrera AEM Assets med InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Du kan generera mallar för InDesign från InDesign-filer innan du importerar dem till AEM Assets. Mer information finns i [Arbeta med filer och mallar](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Du kan mappa elementen i dina InDesign-mallar till XML-märkord. De mappade taggarna visas som egenskaper när du mappar produktegenskaper med mallegenskaper i Catalog Producer. Mer information om XML-märkord i InDesign-filer finns i [Tagga innehåll för XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Endast InDesign-filer (.indd) används som mallar. Filer med filnamnstillägget .indt stöds inte.

## Skapa en katalog {#creating-a-catalog}

I Catalog Producer används PIM-data (Product Information Management) för att mappa produktegenskaper med de XML-egenskaper som visas i mallen. Så här skapar du en katalog:

1. Tryck/klicka på knappen **AEM logotyp** och går till **Resurser > Kataloger**.
1. I **Kataloger** sida, tryck/klicka **Skapa** i verktygsfältet och välj **Katalog** från listan.
1. I **Skapa katalog** anger du ett namn och en beskrivning (valfritt) för katalogen och anger eventuella taggar. Du kan också lägga till en miniatyrbild för katalogen.

   ![create_catalog](assets/create_catalog.png)

1. Tryck/klicka **Spara**. En bekräftelsedialogruta meddelar att katalogen har skapats. Tryck/klicka **Klar** för att stänga dialogrutan.
1. Om du vill öppna den katalog du skapade trycker du på/klickar på den i dialogrutan **Kataloger** sida.

   >[!NOTE]
   >
   >Om du vill öppna katalogen kan du även trycka/klicka **Öppna** i bekräftelsedialogrutan som nämns i föregående steg.

1. Tryck/klicka för att lägga till sidor i katalogen **Skapa** i verktygsfältet och välj sedan **Ny sida** alternativ.
1. I guiden väljer du en InDesign-mall för sidan. Tryck/klicka sedan **Nästa**.
1. Ange ett namn för sidan och en valfri beskrivning. Ange eventuella taggar.
1. Tryck/klicka på **Skapa** i verktygsfältet. Tryck/klicka sedan **Öppna** i dialogrutan. Egenskaperna för produkten visas i den vänstra rutan. De fördefinierade egenskaperna för mallen InDesign visas i den högra rutan.
1. Dra produktegenskaperna från den vänstra rutan till mallegenskaperna för InDesign och skapa en mappning mellan dem.

   Om du vill visa hur sidan ser ut i realtid trycker du/klickar på knappen **Förhandsgranska** till höger.

1. Om du vill skapa fler sidor upprepar du steg 6-9. Om du vill skapa liknande sidor för andra produkter markerar du sidan och trycker/klickar på **Skapa liknande sidor** -ikonen i verktygsfältet.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Du kan bara skapa liknande sidor för produkter med liknande struktur.

   Tryck/klicka på ikonen Lägg till, välj produkter i produktväljaren och tryck/klicka sedan på **Välj** i verktygsfältet.

   ![select_product](assets/select_product.png)

1. Klicka/tryck på verktygsfältet **Skapa**. Tryck/klicka **Klar** för att stänga dialogrutan. Liknande sidor tas med i katalogen.
1. Om du vill lägga till en befintlig InDesign-fil i katalogen trycker du/klickar **Skapa** i verktygsfältet och väljer **Lägg till på befintlig sida** alternativ.
1. Markera filen InDesign och tryck/klicka **Lägg till** i verktygsfältet. Tryck/klicka sedan **OK** för att stänga dialogrutan.

   Om metadata för produkterna som du refererar till på katalogsidorna ändras, återspeglas inte ändringarna automatiskt på katalogsidorna. En banderoll med etiketten **Inaktuell** visas på produktbilderna på de refererande katalogsidorna, vilket anger att metadata för de refererade produkterna inte är aktuella.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   För att produktbilderna ska återspegla de senaste metadataändringarna väljer du sidan i katalogkonsolen och klickar/trycker på **Uppdatera sida** -ikonen i verktygsfältet.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Om du vill ändra metadata för en refererad produkt går du till produktkonsolen (**AEM** > **Handel** > **Produkter**) och välj produkt. Klicka/tryck sedan på **Visa egenskaper** -ikonen i verktygsfältet och redigera metadata på egenskapssidan för resursen.

1. Om du vill ordna om sidorna i katalogen trycker/klickar du på **Skapa** ikonen i verktygsfältet och välj **Sammanfoga** på menyn. I guiden kan du med Carousel överst ändra ordning på sidorna genom att dra dem. Du kan också ta bort sidor.

1. Tryck/klicka **Nästa**. Om du vill lägga till en befintlig InDesign-fil som en försättsblad trycker/klickar du **Bläddra** bredvid **Välj försättsblad** och ange sökvägen för försättsbladet.
1. Tryck/klicka **Spara** och sedan trycka/klicka **Klar** för att stänga bekräftelsedialogrutan.
Vid val av **Klar** öppnas en dialogruta där du kan välja om du vill ha en PDF-rendering.
   ![exportera till pdf](assets/CatalogPDF.png)
Om alternativet Acrobat(PDF) är markerat skapas en PDF-återgivning i  **/jcr:content/renditions** förutom indesign-rendering. Du kan hämta alla återgivningar genom att markera kryssrutan Återgivningar i hämtningsdialogrutan.

1. Om du vill generera en förhandsvisning för den katalog du skapade markerar du den i dialogrutan **Kataloger** konsolen och klicka sedan på **Förhandsgranska** -ikonen i verktygsfältet.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Granska sidorna i katalogen i förhandsgranskningen. Tryck/klicka **Stäng** för att stänga förhandsgranskningen.
