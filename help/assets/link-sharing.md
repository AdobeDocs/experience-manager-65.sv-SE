---
title: Dela resurser via en länk
description: Dela resurser, mappar och samlingar som en URL-adress.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f6da1c69ea3b3c3f07e8ac10fd8e1e9c7208158
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 3%

---


# Dela resurs via en länk {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] Med kan du dela resurser, mappar och samlingar som en URL-adress med medlemmar i organisationen och externa enheter, inklusive partners och leverantörer. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på [!DNL Assets].

>[!PREREQUISITES]
>
>* Du måste ha behörigheten Redigera åtkomstkontrollista för mappen eller resursen som du vill dela som en länk.
>* Konfigurera SMTP-serverinformationen i [Day CQ Mail Service](#configmailservice)om du vill skicka e-postmeddelanden till användarna.


## Dela resurser {#sharelink}

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem.

1. I [!DNL Assets] användargränssnittet väljer du den resurs som ska delas som en länk.
1. Klicka på ikonen **[!UICONTROL Share Link]** för att ![](assets/do-not-localize/assets_share.png)dela resurser i verktygsfältet.

   Länken som skapas när du klickar [!UICONTROL Share] visas i förväg i [!UICONTROL Share Link] fältet. Länkens standardförfallotid är en dag.

   ![Dialogruta med länkresurs](assets/Link-sharing-dialog-box.png)

   *Bild: Dialogrutan där du kan dela resurser som en länk.*

   >[!NOTE]
   >
   >Om du vill dela länkar från din [!DNL Experience Manager] författardistribution till externa enheter måste du se till att du bara visar följande URL:er (som används för länkdelning) för `GET` begäranden. Blockera andra URL-adresser av säkerhetsskäl.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. I [!DNL Experience Manager] gränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

1. Öppna **[!UICONTROL Day CQ Link Externalizer]** konfigurationen och ändra följande egenskaper i **[!UICONTROL Domains]** fältet med de värden som anges mot `local`, `author`och `publish`. För egenskaperna `local` och `author` anger du URL:en för den lokala instansen respektive författarinstansen. Både `local` och `author` egenskaper har samma värde om du kör en enda [!DNL Experience Manager] författarinstans. För publiceringsinstanser anger du URL:en för [!DNL Experience Manager] publiceringsinstansen.

1. Skriv e-post-ID:t för den användare som du vill dela länken med i rutan för e-postadress i dialogrutan **[!UICONTROL Link Sharing]**. Du kan lägga till en eller flera användare.

   ![Dela länkar till resurser direkt från dialogrutan Länkdelning](assets/Asset-Sharing-LinkShareDialog.png)

   *Bild: Dela länkar till resurser direkt från [!UICONTROL Link Sharing] dialogrutan.*

   >[!NOTE]
   >
   >Om du anger ett e-post-ID för en användare som inte är medlem i din organisation, [!UICONTROL External User] föregås orden av användarens e-post-ID.

1. Ange en ämnesrad i **[!UICONTROL Subject]** fältet.

1. Ange ett valfritt meddelande i **[!UICONTROL Message]** fältet.

1. Ange ett förfallodatum och en förfallotid i **[!UICONTROL Expiration]** fältet för att länken ska sluta fungera. Som standard är förfallodatumet inställt för en vecka från det datum du delar länken.

   ![Ange förfallodatum för delad länk](assets/Set-shared-link-expiration.png)

1. Om du vill att användarna ska kunna hämta den ursprungliga resursen tillsammans med återgivningarna väljer du **[!UICONTROL Allow download of original file]**. Som standard kan användare bara hämta återgivningar av resursen som du delar som en länk.

1. Klicka på **[!UICONTROL Share]**. Ett meddelande bekräftar att länken delas med användarna via ett e-postmeddelande.

1. Om du vill visa den delade resursen klickar du på länken i e-postmeddelandet som skickas till användaren. Den delade resursen visas på **[!UICONTROL Adobe Marketing Cloud]** sidan.

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. Om du vill generera en förhandsgranskning av resursen klickar du på den delade resursen. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] har stöd för att generera en förhandsgranskning av resurser [för endast de filtyper](/help/assets/assets-formats.md)som stöds. Om andra MIME-typer delas kan du bara hämta resurserna och inte förhandsgranska.

1. Om du vill hämta den delade resursen klickar du **[!UICONTROL Select]** i verktygsfältet, på resursen och sedan på **[!UICONTROL Download]** verktygsfältet.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Om du vill visa resurser som du har delat som länkar går du till [!DNL Assets] användargränssnittet och klickar på [!DNL Experience Manager] logotypen. Choose **[!UICONTROL Navigation]**. In the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.

1. Om du vill ta bort delningen av en resurs markerar du den och klickar på **[!UICONTROL Unshare]** i verktygsfältet. Ett bekräftelsemeddelande följer. Posten för resursen tas bort från listan.

## Konfigurera daglig CQ Mail-tjänst {#configmailservice}

1. Navigera till [!DNL Experience Manager] > **[!UICONTROL Tools]** > **[!UICONTROL Operations]** på startsidan **[!UICONTROL Web Console]**.
1. I listan med tjänster går du till **[!UICONTROL Day CQ Mail Service]**.
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Värdnamn för SMTP-server: värdnamn för e-postserver
   * SMTP-serverport: e-postserverport
   * SMTP-användare: e-postserverns användarnamn
   * SMTP-lösenord: e-postserverlösenord

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Klicka på **[!UICONTROL Save]**.

## Konfigurera maximal datastorlek {#maxdatasize}

När du hämtar resurser från den länk som delas med funktionen Länkdelning komprimerar resurshierarkin från databasen och returnerar sedan resursen i en ZIP-fil. [!DNL Experience Manager] I avsaknad av begränsningar för den mängd data som kan komprimeras i en ZIP-fil utsätts stora mängder data för komprimering, vilket leder till minnesfel i JVM. För att skydda systemet från en potentiell denial of service-attack på grund av den här situationen måste du konfigurera maxstorleken med hjälp av parametern **[!UICONTROL Max Content Size (uncompressed)]** för [!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet] i Configuration Manager. Om resursens okomprimerade storlek överskrider det konfigurerade värdet, avvisas begäranden om hämtning av resurser. Standardvärdet är 100 MB.

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Leta reda på konfigurationen i webbkonsolen **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** .
1. Öppna **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** konfigurationen i redigeringsläge och ändra värdet på **[!UICONTROL Max Content Size (uncompressed)]** parametern.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Spara ändringarna.

## Bästa praxis och felsökning {#bestpractices}

* Resursmappar eller samlingar som innehåller ett tomt utrymme i namnet kanske inte delas.
* Om användarna inte kan hämta de delade resurserna bör du fråga din [!DNL Experience Manager] administratör om vilka [hämtningsgränser](#maxdatasize) som finns.
* Om du inte kan skicka e-post med länkar till delade resurser eller om de andra användarna inte kan ta emot din e-post, bör du kontakta din [!DNL Experience Manager] administratör om [e-posttjänsten](#configmailservice) är konfigurerad eller inte.
* Om du inte kan dela resurser med hjälp av länkdelningsfunktionen måste du se till att du har rätt behörighet. Se [Dela resurser](#sharelink).
* Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.
