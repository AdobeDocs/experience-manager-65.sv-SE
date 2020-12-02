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
>* Konfigurera SMTP-serverinformationen i [Day CQ Mail Service](#configmailservice) om du vill skicka e-postmeddelanden till användarna.


## Dela resurser {#sharelink}

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` plats kan visa de länkar som delas med dem.

1. I [!DNL Assets]-användargränssnittet väljer du resursen som ska delas som en länk.
1. Klicka på ikonen **[!UICONTROL Share Link]** ![Dela resurser](assets/do-not-localize/assets_share.png) i verktygsfältet.

   Länken som skapas när du klickar på [!UICONTROL Share] visas i förväg i fältet [!UICONTROL Share Link]. Länkens standardförfallotid är en dag.

   ![Dialogruta med länkresurs](assets/Link-sharing-dialog-box.png)

   *Bild: Dialogrutan där du kan dela resurser som en länk.*

   >[!NOTE]
   >
   >Om du vill dela länkar från din [!DNL Experience Manager] Author-distribution till externa entiteter måste du se till att du bara visar följande URL:er (som används för länkdelning) för `GET`-begäranden. Blockera andra URL-adresser av säkerhetsskäl.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. I [!DNL Experience Manager]-gränssnittet öppnar du **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

1. Öppna konfigurationen **[!UICONTROL Day CQ Link Externalizer]** och ändra följande egenskaper i fältet **[!UICONTROL Domains]** med de värden som anges för `local`, `author` och `publish`. För egenskaperna `local` och `author` anger du URL:en för den lokala instansen respektive författarinstansen. Både `local`- och `author`-egenskaperna har samma värde om du kör en enda [!DNL Experience Manager]-författarinstans. För publiceringsinstanser anger du URL:en för publiceringsinstansen [!DNL Experience Manager].

1. Skriv e-post-ID:t för den användare som du vill dela länken med i rutan för e-postadress i dialogrutan **[!UICONTROL Link Sharing]**. Du kan lägga till en eller flera användare.

   ![Dela länkar till resurser direkt från dialogrutan Länkdelning](assets/Asset-Sharing-LinkShareDialog.png)

   *Bild: Dela länkar till resurser direkt från  [!UICONTROL Link Sharing] dialogrutan.*

   >[!NOTE]
   >
   >Om du anger ett e-post-ID för en användare som inte är medlem i din organisation, kommer ordet [!UICONTROL External User] att föregås av användarens e-post-ID.

1. Ange en ämnesrad i fältet **[!UICONTROL Subject]**.

1. Ange ett valfritt meddelande i fältet **[!UICONTROL Message]**.

1. I fältet **[!UICONTROL Expiration]** anger du ett förfallodatum och en förfallotid för att länken ska sluta fungera. Som standard är förfallodatumet inställt för en vecka från det datum du delar länken.

   ![Ange förfallodatum för delad länk](assets/Set-shared-link-expiration.png)

1. Om du vill att användarna ska kunna hämta den ursprungliga resursen tillsammans med återgivningarna väljer du **[!UICONTROL Allow download of original file]**. Som standard kan användare bara hämta återgivningar av resursen som du delar som en länk.

1. Klicka på **[!UICONTROL Share]**. Ett meddelande bekräftar att länken delas med användarna via ett e-postmeddelande.

1. Om du vill visa den delade resursen klickar du på länken i e-postmeddelandet som skickas till användaren. Den delade resursen visas på sidan **[!UICONTROL Adobe Marketing Cloud]**.

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. Om du vill generera en förhandsgranskning av resursen klickar du på den delade resursen. Om du vill stänga förhandsgranskningen och gå tillbaka till sidan **[!UICONTROL Marketing Cloud]** klickar du på **[!UICONTROL Back]** i verktygsfältet. Om du har delat en mapp klickar du på **[!UICONTROL Parent Folder]** för att återgå till den överordnade mappen.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] har stöd för att generera en förhandsgranskning av resurser  [för endast de filtyper](/help/assets/assets-formats.md) som stöds. Om andra MIME-typer delas kan du bara hämta resurserna och inte förhandsgranska.

1. Om du vill hämta den delade resursen klickar du på **[!UICONTROL Select]** i verktygsfältet, på resursen och sedan på **[!UICONTROL Download]** i verktygsfältet.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Om du vill visa resurser som du har delat som länkar går du till [!DNL Assets]-användargränssnittet och klickar på logotypen [!DNL Experience Manager]. Choose **[!UICONTROL Navigation]**. I navigeringsrutan väljer du **[!UICONTROL Shared Links]** för att visa en lista med delade resurser.

1. Om du vill ta bort delningen av en resurs markerar du den och klickar på **[!UICONTROL Unshare]** i verktygsfältet. Ett bekräftelsemeddelande följer. Posten för resursen tas bort från listan.

## Konfigurera daglig CQ-e-posttjänst {#configmailservice}

1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** på startsidan för [!DNL Experience Manager].
1. Leta reda på **[!UICONTROL Day CQ Mail Service]** i listan över tjänster.
1. Klicka på **[!UICONTROL Edit]** bredvid tjänsten och konfigurera följande parametrar för **[!UICONTROL Day CQ Mail Service]** med informationen som anges mot deras namn:

   * Värdnamn för SMTP-server: värdnamn för e-postserver
   * SMTP-serverport: e-postserverport
   * SMTP-användare: e-postserverns användarnamn
   * SMTP-lösenord: e-postserverlösenord

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Klicka på **[!UICONTROL Save]**.

## Konfigurera maximal datastorlek {#maxdatasize}

När du hämtar resurser från den länk som delas med funktionen Länkdelning komprimerar [!DNL Experience Manager] resurshierarkin från databasen och returnerar sedan resursen i en ZIP-fil. I avsaknad av begränsningar för den mängd data som kan komprimeras i en ZIP-fil utsätts stora mängder data för komprimering, vilket leder till minnesfel i JVM. För att skydda systemet från en potentiell denial of service-attack på grund av den här situationen konfigurerar du den maximala storleken med parametern **[!UICONTROL Max Content Size (uncompressed)]** för [!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet] i Configuration Manager. Om resursens okomprimerade storlek överskrider det konfigurerade värdet, avvisas begäranden om hämtning av resurser. Standardvärdet är 100 MB.

1. Klicka på logotypen [!DNL Experience Manager] och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Leta reda på konfigurationen **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** på webbkonsolen.
1. Öppna konfigurationen **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** i redigeringsläge och ändra värdet för parametern **[!UICONTROL Max Content Size (uncompressed)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Spara ändringarna.

## Bästa tillvägagångssätt och felsökning {#bestpractices}

* Resursmappar eller samlingar som innehåller ett tomt utrymme i namnet kanske inte delas.
* Om användarna inte kan hämta de delade resurserna bör du fråga din [!DNL Experience Manager]-administratör om vilka hämtningsgränser [som finns.](#maxdatasize)
* Om du inte kan skicka e-post med länkar till delade resurser eller om de andra användarna inte kan ta emot din e-post, bör du kontakta [!DNL Experience Manager]-administratören om [e-posttjänsten](#configmailservice) är konfigurerad eller inte.
* Om du inte kan dela resurser med hjälp av länkdelningsfunktionen måste du se till att du har rätt behörighet. Se [dela resurser](#sharelink).
* Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.
