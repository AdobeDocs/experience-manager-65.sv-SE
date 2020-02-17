---
title: Katalogproducent
seo-title: Katalogproducent
seo-description: Lär dig hur du använder Catalog Producer i AEM Assets för att generera produktkataloger med hjälp av dina digitala resurser.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Katalogproducent{#catalog-producer}

Lär dig hur du använder Catalog Producer i AEM Assets för att generera produktkataloger med hjälp av dina digitala resurser.

Med Adobe Experience Manager (AEM) Assets Catalog Producer kan ni skapa kataloger för era varumärkesprodukter med InDesign-mallar som importeras från ett InDesign-program. Om du vill importera InDesign-mallar måste du först integrera AEM-resurser med en InDesign-server.

## Integrera med InDesign-server {#integrating-with-indesign-server}

Som en del av integreringsprocessen konfigurerar du arbetsflödet **DAM Update Asset** , som är lämpligt för integrering med InDesign. Konfigurera dessutom en proxyarbetare för InDesign-servern. Mer information finns i [Integrera AEM-resurser med InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Du kan generera InDesign-mallar från InDesign-filer innan du importerar dem till AEM Resurser. Mer information finns i [Arbeta med filer och mallar](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Du kan mappa elementen i dina InDesign-mallar till XML-märkord. De mappade taggarna visas som egenskaper när du mappar produktegenskaper med mallegenskaper i Catalog Producer. Mer information om XML-taggning i InDesign-filer finns i [Tagga innehåll för XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Endast InDesign-filer (.indd) används som mallar. Filer med filnamnstillägget .indt stöds inte.

## Skapa en katalog {#creating-a-catalog}

I Catalog Producer används PIM-data (Product Information Management) för att mappa produktegenskaper med de XML-egenskaper som visas i mallen. Så här skapar du en katalog:

1. I Assets-användargränssnittet: tryck/klicka på **AEM-logotypen** och gå till **Assets > Catalogs**.
1. På sidan **Kataloger** trycker/klickar du på **Skapa** i verktygsfältet och väljer sedan **Katalog** i listan.
1. Ange ett namn och en beskrivning (valfritt) för katalogen på sidan **Skapa katalog** och ange eventuella taggar. Du kan också lägga till en miniatyrbild för katalogen.

   ![create_catalog](assets/create_catalog.png)

1. Tryck/klicka på **Spara**. En bekräftelsedialogruta meddelar att katalogen har skapats. Tryck/klicka på **Klar** för att stänga dialogrutan.
1. Om du vill öppna den katalog du skapade trycker/klickar du på den på sidan **Kataloger** .

   >[!NOTE]
   >
   >Om du vill öppna katalogen trycker du på/klickar på **Öppna** i bekräftelsedialogrutan som nämns i föregående steg.

1. Om du vill lägga till sidor i katalogen trycker/klickar du på **Skapa** i verktygsfältet och väljer sedan alternativet **Ny sida** .
1. Välj en InDesign-mall för sidan i guiden. Tryck/klicka sedan på **Nästa**.
1. Ange ett namn för sidan och en valfri beskrivning. Ange eventuella taggar.
1. Tryck/klicka på **Skapa** i verktygsfältet. Tryck/klicka sedan på **Öppna** i dialogrutan. Egenskaperna för produkten visas i den vänstra rutan. De fördefinierade egenskaperna för InDesign-mallen visas i den högra rutan.
1. Dra produktegenskaperna från den vänstra rutan till InDesign-mallegenskaperna och skapa en koppling mellan dem.

   Om du vill visa hur sidan visas i realtid trycker/klickar du på fliken **Förhandsgranska** i den högra rutan.

1. Om du vill skapa fler sidor upprepar du steg 6-9. Om du vill skapa liknande sidor för andra produkter markerar du sidan och trycker/klickar på ikonen **Skapa liknande sidor** i verktygsfältet.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Du kan bara skapa liknande sidor för produkter med liknande struktur.

   Tryck/klicka på ikonen Lägg till, välj produkter i produktväljaren och tryck/klicka sedan på **Välj** i verktygsfältet.

   ![select_product](assets/select_product.png)

1. Klicka/tryck på **Skapa** i verktygsfältet. Tryck/klicka på **Klar** för att stänga dialogrutan. Liknande sidor tas med i katalogen.
1. Om du vill lägga till en befintlig InDesign-fil i katalogen trycker/klickar du på **Skapa** i verktygsfältet och väljer alternativet **Lägg till i befintlig sida** .
1. Markera InDesign-filen och tryck/klicka på **Lägg till** i verktygsfältet. Stäng sedan dialogrutan genom att trycka/klicka på **OK** .

   Om metadata för produkterna som du refererar till på katalogsidorna ändras, återspeglas inte ändringarna automatiskt på katalogsidorna. En banderoll med etiketten **Stale** visas på produktbilderna på de refererande katalogsidorna, vilket anger att metadata för de refererade produkterna inte är aktuella.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Om du vill vara säker på att produktbilderna återspeglar de senaste metadataändringarna markerar du sidan i katalogkonsolen och klickar/trycker på ikonen för **uppdateringssidan** i verktygsfältet.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Om du vill ändra metadata för en refererad produkt går du till produktkonsolen (**AEM-logotyp** > **Handel** > **Produkter**) och väljer produkten. Klicka/tryck sedan på ikonen **Visa egenskaper** i verktygsfältet och redigera metadata på egenskapssidan för resursen.

1. Om du vill ordna om sidorna i katalogen trycker/klickar du på ikonen **Skapa** i verktygsfältet och väljer sedan **Sammanfoga** på menyn. I guiden kan du med Carousel överst ändra ordning på sidorna genom att dra dem. Du kan också ta bort sidor.

1. Tryck/klicka på **Nästa**. Om du vill lägga till en befintlig InDesign-fil som försättsblad trycker/klickar du på **Bläddra** bredvid rutan **Välj försättsblad** och anger sökvägen för försättsbladet.
1. Tryck/klicka på **Spara** och sedan på/klicka på **Klar** för att stänga bekräftelsedialogrutan.
När du väljer alternativet **Klar** öppnas en dialogruta där du kan välja om du vill ha en PDF-återgivning.
   ![exportera till pdf](assets/CatalogPDF.png)Om alternativet Acrobat(PDF) är markerat skapas en PDF-återgivning i **/jcr:content/renditions** förutom indesign-återgivning. Du kan hämta alla återgivningar genom att markera kryssrutan Återgivningar i hämtningsdialogrutan.

1. Om du vill generera en förhandsvisning för den katalog du skapade markerar du den i **katalogkonsolen** och klickar sedan på ikonen **Förhandsgranska** i verktygsfältet.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Granska sidorna i katalogen i förhandsgranskningen. Tryck/klicka på **Stäng** för att stänga förhandsgranskningen.

