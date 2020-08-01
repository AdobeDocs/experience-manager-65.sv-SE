---
title: Generera en URL till delade resurser
description: I den här artikeln beskrivs hur du delar resurser, mappar och samlingar [!DNL Experience Manager Assets] i en URL till externa parter.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 4%

---


# Dela resurs via en länk {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] Med kan du dela resurser, mappar och samlingar som en URL-adress med medlemmar i organisationen och externa enheter, inklusive partners och leverantörer. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på [!DNL Assets].

>[!NOTE]
>
>Du måste ha behörigheten Redigera åtkomstkontrollista för mappen eller resursen som du vill dela som en länk.

## Dela resurser {#sharelink}

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem.

>[!NOTE]
>
>Innan du delar en länk med användarna måste du kontrollera att Dag CQ Mail Service har konfigurerats. Ett fel uppstår om du försöker dela en länk utan att först [konfigurera Day CQ Mail Service](/help/assets/link-sharing.md#configmailservice).

1. I [!DNL Assets] användargränssnittet väljer du den resurs som ska delas som en länk.
1. Klicka på ikonen **[!UICONTROL Share Link]** för att ![](assets/do-not-localize/assets_share.png)dela resurser i verktygsfältet.

   En resurslänk skapas automatiskt i **[!UICONTROL Share Link]** fältet. Kopiera den här länken och dela den med användarna. Länkens standardförfallotid är en dag.

   ![Dialogruta med länkresurs](assets/Link-sharing-dialog-box.png)

   *Bild: Dialogrutan där du kan dela resurser som en länk.*

   Du kan också fortsätta med steg 3-7 i den här proceduren för att lägga till e-postmottagare, konfigurera förfallotiden för länken och skicka den från dialogrutan.

   >[!NOTE]
   >
   >Om du vill dela länkar från din [!DNL Experience Manager] författardistribution till externa enheter måste du se till att du bara visar följande URL:er (som används för länkdelning) för `GET` begäranden. Blockera andra URL:er för att säkerställa säkerheten för [!DNL Experience Manager] författaren.
   >
   >* http://[aem_server]:[port]/linkshare.html
   >* http://[aem_server]:[port]/linksharepreview.html
   >* http://[aem_server]:[port]/linkexpired.html


   >[!NOTE]
   >
   >Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.

1. I [!DNL Experience Manager] gränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

1. Öppna **[!UICONTROL Day CQ Link Externalizer]** konfigurationen och ändra följande egenskaper i **[!UICONTROL Domains]** fältet med de värden som anges mot `local`, `author`och `publish`. För egenskaperna `local` och `author` anger du URL:en för den lokala instansen respektive författarinstansen. Både `local` och `author` egenskaper har samma värde om du kör en enda [!DNL Experience Manager] Author-instans. Ange till `publish`exempel URL:en för [!DNL Experience Manager] publiceringsinstansen.

1. Skriv e-post-ID:t för den användare som du vill dela länken med i rutan för e-postadress i dialogrutan **[!UICONTROL Link Sharing]**. Du kan också dela länken med flera användare.

   Om användaren är medlem i din organisation väljer du användarens e-post-ID bland de föreslagna e-post-ID:n som visas i listan under skrivområdet. För en extern användare anger du det fullständiga e-post-ID:t och väljer det sedan i listan.

   Konfigurera SMTP-serverinformationen i [Day CQ Mail Service](#configmailservice)om du vill att e-postmeddelanden ska kunna skickas till användare.

   ![Dela länkar till resurser direkt från dialogrutan Länkdelning](assets/Asset-Sharing-LinkShareDialog.png)

   *Bild: Dela länkar till resurser direkt från[!UICONTROL Link Sharing]dialogrutan.*

   >[!NOTE]
   >
   >Om du anger ett e-post-ID för en användare som inte är medlem i din organisation, [!UICONTROL External User] föregås orden av användarens e-post-ID.

1. I **[!UICONTROL Subject]** fältet anger du ett ämne för resursen som du vill dela.

1. Ange ett valfritt meddelande i **[!UICONTROL Message]** fältet.

1. I **[!UICONTROL Expiration]** fältet anger du ett förfallodatum och en förfallotid för länken med datumväljaren. Som standard är förfallodatumet inställt för en vecka från det datum du delar länken.

   ![Ange förfallodatum för delad länk](assets/Set-shared-link-expiration.png)

1. Om du vill att användarna ska kunna hämta originalbilden tillsammans med återgivningarna väljer du **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >Som standard kan användare bara hämta återgivningar av resursen som du delar som en länk.

1. Klicka på **[!UICONTROL Share]**. Ett meddelande bekräftar att länken delas med användarna via ett e-postmeddelande.
1. Om du vill visa den delade resursen klickar du på länken i e-postmeddelandet som skickas till användaren. Den delade resursen visas på **[!UICONTROL Adobe Marketing Cloud]** sidan.

   ![chlimage_1-260](assets/chlimage_1-545.png)

   Om du vill växla till listvyn klickar du på layoutalternativet i verktygsfältet.

1. Om du vill generera en förhandsgranskning av resursen klickar du på den delade resursen. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] har stöd för att generera en förhandsgranskning av resurser av dessa MIME-typer: JPG, PNG, GIF, BMP, INDD, PDF och PPT. Du kan bara hämta resurser från andra MIME-typer.

1. Om du vill hämta den delade resursen klickar du **[!UICONTROL Select]** i verktygsfältet, på resursen och sedan på **[!UICONTROL Download]** verktygsfältet.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Om du vill visa de resurser du har delat som länkar går du till [!DNL Assets] användargränssnittet och klickar på [!DNL Experience Manager] logotypen. Välj **[!UICONTROL Navigation]** i listan för att visa navigeringsrutan.
1. I navigeringsrutan väljer du **[!UICONTROL Shared Links]** för att visa en lista med delade resurser.
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
