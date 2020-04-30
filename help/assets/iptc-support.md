---
title: Arbeta med IPTC-metadata i [!DNL Adobe Experience Manager Assets].
description: Läs om hur [!DNL Adobe Experience Manager Assets] stöder IPTC-metadata, Creative-klassificeringar och nyckelord som lagts till i resurser via Adobe Bridge och andra Creative-program.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Arbeta med IPTC-metadata {#support-for-iptc-metadata}

Lär dig hur [!DNL Adobe Experience Manager Assets] stöder IPTC-metadata, kreativa klassificeringar och nyckelord som läggs till i resurser via [!DNL Adobe Bridge] och andra [!DNL Adobe Creative Cloud] program.

[!DNL Adobe Experience Manager Assets] har stöd för IPTC-metadatastandarden som används ofta för att beskriva resurser. På så sätt blir det enklare att [!DNL Assets] acceptera bilderna från olika håll, t.ex. fotografer, byråer, bibliotek, museer osv.

Standardschemat för metadata för mediefiler innehåller nu metadatamatchningar för IPTC Core och IPTC Extension för att definiera omfattande metadataegenskaper som gör att användare kan lägga till exakta och tillförlitliga data om personer, platser och produkter som visas i en bild. Det har även stöd för datum, namn och identifierare för att skapa bilden samt ett flexibelt sätt att uttrycka rättighetsinformation.

Egenskapssidan för resurser innehåller nu separata flikar för att visa IPTC-kärnan och IPTC-tilläggsmetadata i redigerbara fält.

1. Välj en bild i [!DNL Assets] användargränssnittet.
1. Klicka på **[!UICONTROL Egenskaper]** i verktygsfältet.
1. Klicka på fliken **[!UICONTROL IPTC]** för att visa IPTC-metadata för resursen.
1. Redigera IPTC-metadataegenskaperna efter behov.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. Redigera metadataegenskaperna för IPTC-tillägget efter behov.
1. Klicka på **[!UICONTROL Spara och stäng]** för att spara ändringarna.

## Stöd för kreativa betyg {#creative-rating-support}

Förutom att visa enskilda användarklassificeringar och aggregerade klassificeringar visas nu klassificeringarna som tilldelats resurser via Adobe Bridge och andra Creative-program på sidan Egenskaper

Dessa omdömen finns under **[!UICONTROL Creative Rating]** under fliken **[!UICONTROL Advanced]** .

Den här klassificeringen är en skrivskyddad egenskap och varierar mellan 1 och 5. Du kan söka efter resurser baserat på deras Creative Rating från sökpanelen.

Den här egenskapen är dock för närvarande inte indexerad för att undvika konflikter med anpassade ändringar som görs av användare.

## Stöd för nyckelord {#keyword-support}

På fliken **[!UICONTROL IPTC]** på sidan [!UICONTROL Egenskaper] visas även nyckelord som lagts till i resurser via Adobe Bridge och andra Adobe Creative Cloud-program. Du kan också redigera dessa nyckelord och lägga till fler nyckelord på fliken **[!UICONTROL IPTC]** .

![keywords](assets/keywords-in-iptc-tab.png)
