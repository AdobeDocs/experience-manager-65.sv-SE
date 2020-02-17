---
title: Stöd för IPTC-metadata
description: Läs om hur Adobe Experience Manager (AEM) Assets stöder IPTC-metadata, kreativa klassificeringar och nyckelord som lagts till i resurser via Adobe Bridge och andra Creative-program.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Stöd för IPTC-metadata {#support-for-iptc-metadata}

Läs om hur Adobe Experience Manager (AEM) Assets stöder IPTC-metadata, kreativa klassificeringar och nyckelord som lagts till i resurser via Adobe Bridge och andra Creative-program.

Adobe Experience Manager Assets (AEM) stöder IPTC-metadatastandarden som används ofta för att beskriva resurser. På så sätt kan AEM Assets förbättra accepterandet av bilder från olika parter, bland annat fotografer, byråer, bibliotek och museer.

Standardschemat för metadata för mediefiler innehåller nu metadatamodeller för IPTC Core och IPTC Extension för att definiera omfattande metadataegenskaper som gör att användare kan lägga till exakta och tillförlitliga data om personer, platser och produkter som visas i en bild. Det har även stöd för datum, namn och identifierare för att skapa bilden samt ett flexibelt sätt att uttrycka rättighetsinformation.

Egenskapssidan för resurser innehåller nu separata flikar för att visa IPTC-kärnan och IPTC-tilläggsmetadata i redigerbara fält.

1. Välj en bild i användargränssnittet Resurser.
1. Tryck på **[!UICONTROL Egenskaper]** i verktygsfältet.
1. Tryck på fliken **[!UICONTROL IPTC]** för att visa IPTC-metadata för resursen.
1. Redigera IPTC-metadataegenskaperna efter behov.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Klicka/tryck på fliken **[!UICONTROL IPTC-tillägg]** för att visa IPTC-tilläggsmetadata för resursen.
1. Redigera metadataegenskaperna för IPTC-tillägget efter behov.
1. Tryck/klicka på **[!UICONTROL Spara och stäng]** för att spara ändringarna.

## Stöd för kreativa betyg {#creative-rating-support}

Förutom att visa enskilda användarklassificeringar och aggregerade klassificeringar visas nu klassificeringarna som tilldelats resurser via Adobe Bridge och andra Creative-program på sidan Egenskaper

Dessa omdömen finns under **[!UICONTROL Creative Rating]** under fliken **[!UICONTROL Advanced]** .

Den här klassificeringen är en skrivskyddad egenskap och varierar mellan 1 och 5. Du kan söka efter resurser baserat på deras Creative Rating från sökpanelen.

Den här egenskapen är dock för närvarande inte indexerad för att undvika konflikter med anpassade ändringar som görs av användare.

## Stöd för nyckelord {#keyword-support}

På fliken **[!UICONTROL IPTC]** på sidan [!UICONTROL Egenskaper] visas även nyckelord som lagts till i resurser via Adobe Bridge och andra Adobe Creative Cloud-program. Du kan också redigera dessa nyckelord och lägga till fler nyckelord på fliken **[!UICONTROL IPTC]** .

![keywords](assets/keywords-in-iptc-tab.png)
