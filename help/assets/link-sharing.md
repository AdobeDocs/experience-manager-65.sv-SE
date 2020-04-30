---
title: Generera en URL till delade resurser
description: I den här artikeln beskrivs hur du delar resurser, mappar och samlingar i AEM Resurser som en URL till externa parter.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Dela resurs via en länk {#asset-link-sharing}

Med Adobe Experience Manager Assets (AEM) kan ni dela resurser, mappar och samlingar som en webbadress med medlemmar i organisationen och externa enheter, inklusive partners och leverantörer. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på AEM Assets.

>[!NOTE]
>
>Du måste ha behörigheten Redigera åtkomstkontrollista för mappen eller resursen som du vill dela som en länk.

## Dela resurser {#sharelink}

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem.

>[!NOTE]
>
>Innan du delar en länk med användarna måste du kontrollera att Dag CQ Mail Service har konfigurerats. Ett fel uppstår om du försöker dela en länk utan att först [konfigurera Day CQ Mail Service](/help/assets/link-sharing.md#configmailservice).

1. I Assets-användargränssnittet väljer du den resurs som ska delas som en länk.
1. Klicka på/tryck på **[!UICONTROL Share Link]** ![assets_share](assets/assets_share.png)i verktygsfältet.

   En resurslänk skapas automatiskt i fältet **[!UICONTROL Dela länk]** . Kopiera den här länken och dela den med användarna. Länkens standardförfallotid är en dag.

   ![Dialogruta med länkresurs](assets/Link-sharing-dialog-box.png)

   *Bild: Dialogrutan där du kan dela resurser som en länk.*

   Du kan också fortsätta med steg 3-7 i den här proceduren för att lägga till e-postmottagare, konfigurera förfallotiden för länken och skicka den från dialogrutan.

   >[!NOTE]
   >
   >Om du vill dela länkar från din AEM Author-instans till externa entiteter, ska du se till att du bara visar följande URL:er (som används för länkdelning) för `GET` begäranden. Blockera andra URL:er för att säkerställa säkerheten för AEM Author.
   >
   >* http://&lt;aem_server>:&lt;port>/linkshare.html
   * http://&lt;aem_server>:&lt;port>/linksharepreview.html
   * http://&lt;aem_server>:&lt;port>/linkexpired.html


   >[!NOTE]
   Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.

1. I AEM-gränssnittet går du till **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.

1. Öppna **[!UICONTROL Dag CQ Link Externalizer]** -konfigurationen och ändra följande egenskaper i fältet **[!UICONTROL Domäner]** med de värden som anges mot `local`, `author`och `publish`. För egenskaperna `local` och `author` anger du URL:en för den lokala instansen respektive författarinstansen. Både `local` och `author` egenskaper har samma värde om du kör en enda Experience Manager Author-instans. Ange t. `publish`ex. URL:en för Experience Manager-publiceringsinstansen.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. Du kan också dela länken med flera användare.

   Om användaren är medlem i din organisation väljer du användarens e-post-ID bland de föreslagna e-post-ID:n som visas i listan under skrivområdet. För en extern användare anger du det fullständiga e-post-ID:t och väljer det sedan i listan.

   Konfigurera SMTP-serverinformationen i [Day CQ Mail Service](#configmailservice)om du vill att e-postmeddelanden ska kunna skickas till användare.

   ![Dela länkar till resurser direkt från dialogrutan Länkdelning](assets/Asset-Sharing-LinkShareDialog.png)

   *Bild: Dela länkar till resurser direkt från dialogrutan[!UICONTROL Länkdelning].*

   >[!NOTE]
   Om du anger ett e-post-ID för en användare som inte är medlem i din organisation anges ordet [!UICONTROL Extern användare] som användarens e-post-ID.

1. I fältet **[!UICONTROL Ämne]** anger du ett ämne för resursen som du vill dela.

1. Ange ett valfritt meddelande i fältet **[!UICONTROL Meddelande]** .

1. I fältet **[!UICONTROL Förfallodatum]** anger du ett förfallodatum och en förfallotid för länken med datumväljaren. Som standard är förfallodatumet inställt för en vecka från det datum du delar länken.

   ![Ange förfallodatum för delad länk](assets/Set-shared-link-expiration.png)

1. Om du vill att användarna ska kunna hämta originalbilden tillsammans med återgivningarna väljer du **[!UICONTROL Tillåt hämtning av originalfilen]**.

   >[!NOTE]
   Som standard kan användare bara hämta återgivningar av resursen som du delar som en länk.

1. Klicka på **[!UICONTROL Dela]**. Ett meddelande bekräftar att länken delas med användarna via ett e-postmeddelande.
1. Om du vill visa den delade resursen klickar/trycker du på länken i det e-postmeddelande som skickas till användaren. Den delade resursen visas på sidan **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

   Om du vill växla till listvyn klickar/trycker du på layoutalternativet i verktygsfältet.

1. Om du vill generera en förhandsgranskning av resursen klickar/trycker du på den delade resursen. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   AEM stöder generering av förhandsgranskning av resurser av dessa MIME-typer: JPG, PNG, GIF, BMP, INDD, PDF och PPT. Du kan bara hämta resurser från andra MIME-typer.

1. Om du vill hämta den delade resursen trycker du på **[!UICONTROL Välj]** i verktygsfältet, klickar/trycker på resursen och sedan på **[!UICONTROL Hämta]** i verktygsfältet.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Om du vill visa de resurser du har delat som länkar går du till resursgränssnittet och trycker på Experience Manager-logotypen. Visa navigeringsrutan genom att välja **[!UICONTROL Navigering]** i listan.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. Om du vill ta bort delningen av en resurs markerar du den och trycker/klickar på **[!UICONTROL Ta bort delning]** i verktygsfältet. Ett bekräftelsemeddelande följer. Posten för resursen tas bort från listan.

## Konfigurera daglig CQ Mail-tjänst {#configmailservice}

1. På Experience Managers hemsida går du till **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.
1. Leta upp **[!UICONTROL Dag CQ Mail Service]** i listan över tjänster.
1. Tap **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Värdnamn för SMTP-server: värdnamn för e-postserver
   * SMTP-serverport: e-postserverport
   * SMTP-användare: e-postserverns användarnamn
   * SMTP-lösenord: e-postserverlösenord
   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Klicka/tryck på **[!UICONTROL Spara]**.

## Konfigurera maximal datastorlek {#maxdatasize}

När du hämtar resurser från den länk som delas med funktionen Länkdelning komprimerar AEM resurshierarkin från databasen och returnerar sedan resursen i en ZIP-fil. I avsaknad av begränsningar för den mängd data som kan komprimeras i en ZIP-fil utsätts stora mängder data för komprimering, vilket leder till minnesfel i JVM. För att skydda systemet från en potentiell denial of service-attack på grund av den här situationen konfigurerar du maxstorleken med parametern **[!UICONTROL Max Content Size (okomprimerad)]** för [!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet] i Configuration Manager. Om resursens okomprimerade storlek överskrider det konfigurerade värdet, avvisas begäranden om hämtning av resurser. Standardvärdet är 100 MB.

1. Klicka/tryck på AEM-logotypen och gå sedan till **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.
1. På webbkonsolen går du till **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Server]** .
1. Öppna konfigurationen för **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Server]** i redigeringsläge och ändra värdet för parametern **[!UICONTROL Maximal innehållsstorlek (okomprimerat)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Spara ändringarna.

## Bästa praxis och felsökning {#bestpractices}

* Resursmappar eller samlingar som innehåller ett tomt utrymme i namnet kanske inte delas.
* Om användarna inte kan hämta de delade resurserna bör du fråga AEM-administratören om vilka [hämtningsgränser](#maxdatasize) som finns.
* Om du inte kan skicka e-post med länkar till delade resurser eller om de andra användarna inte kan ta emot din e-post, bör du kontakta AEM-administratören om [e-posttjänsten](#configmailservice) är konfigurerad eller inte.
* Om du inte kan dela resurser med hjälp av länkdelningsfunktionen måste du se till att du har rätt behörighet. Se [Dela resurser](#sharelink).
