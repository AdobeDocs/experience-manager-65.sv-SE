---
title: Konfigurera resurstaggning med Smart Content Service.
description: Lär dig hur du konfigurerar smart taggning och förbättrad smart taggning [!DNL Adobe Experience Manager]med hjälp av Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 506b965e4f1c18230357f25532d3fdd10f526ef0
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 45%

---


# Konfigurera resurstaggning med Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

Du kan integrera [!DNL Adobe Experience Manager] med Smart Content Service via Adobe Developer Console. Använd den här konfigurationen för att komma åt Smart Content Service inifrån [!DNL Experience Manager].

Artikeln innehåller information om följande viktiga uppgifter som krävs för att konfigurera Smart Content Service. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. [](#obtain-public-certificate)Skapa en konfiguration för Smart Content Service i [!DNL Experience Manager] för att generera en offentlig nyckel. [Hämta ett offentligt certifikat](#obtain-public-certificate) för OAuth-integrering.

1. [Skapa en integrering i Adobe Developer Console](#create-adobe-i-o-integration) och överför den genererade offentliga nyckeln.

1. [Konfigurera distributionen](#configure-smart-content-service) med API-nyckeln och andra autentiseringsuppgifter från Adobe Developer Console.

1. [Testa konfigurationen](#validate-the-configuration).

1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## Förutsättningar {#prerequisites}

Innan du använder tjänsten Smart Content måste du göra följande för att skapa en integrering på Adobe Developer Console:

* Ett Adobe ID-konto som har administratörsbehörighet för organisationen.

* Att Smart Content är aktiverad för din organisation.

<!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
-->

Om du vill aktivera förbättrade smarta taggar installerar du förutom ovanstående även det senaste [Experience Manager-Service Pack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).

## Skapa konfiguration för Smart Content Service för att få {#obtain-public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe Developer Console.

1. I användargränssnittet för [!DNL Experience Manager] går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. I dialogrutan **[!UICONTROL Create Configuration]** anger du en rubrik och ett namn för konfigurationen av smarta taggar. Klicka på **[!UICONTROL Create]**.

1. Använd följande värden i dialogrutan **[!UICONTROL AEM Smart Content Service]**:

   **[!UICONTROL Service URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Authorization Server]**: `https://ims-na1.adobelogin.com`

   Lämna de andra fälten tomma (kommer senare). Klicka på **[!UICONTROL OK]**.

   ![Dialogrutan Experience Manager Smart Content Service för att tillhandahålla innehållstjänstens URL](assets/aem_scs.png)


   *Bild: Dialogrutan Smart Content Service för att ange innehållstjänstens URL*

   >[!NOTE]
   >
   >URL:en som anges som [!UICONTROL Service URL] är inte tillgänglig via webbläsaren och genererar ett 404-fel. Konfigurationen fungerar bra med samma värde som [!UICONTROL Service URL] parametern. Den övergripande servicestatusen och underhållsschemat finns på [https://status.adobe.com](https://status.adobe.com).

1. Klicka på **[!UICONTROL Download Public Certificate for OAuth Integration]** och hämta den offentliga certifikatfilen `AEM-SmartTags.crt`.

   ![En representation av de inställningar som har skapats för den smarta taggningstjänsten](assets/smart-tags-download-public-cert.png)


   *Bild: Inställningar för tjänsten för smart taggning*

### Reconfigure when a certificate expires {#certrenew}

När ett certifikat har upphört att gälla är det inte längre tillförlitligt. Du kan inte förnya ett certifikat som har upphört att gälla. Följ de här stegen för att lägga till ett nytt certifikat.

1. Logga in på [!DNL Experience Manager]-driftsättningen som administratör. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Leta reda på och klicka på **[!UICONTROL dam-update-service]**-användaren. Klicka på fliken **[!UICONTROL Keystore]**.

1. Ta bort den befintliga **[!UICONTROL similaritysearch]**-nyckelbehållaren med det certifikat som upphört att gälla. Klicka på **[!UICONTROL Save & Close]**.

   ![Ta bort den befintliga posten för likhetssökning i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat](assets/smarttags_delete_similaritysearch_keystore.png)


   *Bild: Ta bort den befintliga`similaritysearch`-posten i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat.*

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Klicka på **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Klicka på önskad konfiguration.

1. Om du vill hämta ett offentligt certifikat klickar du på **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. Gå till [https://console.adobe.io](https://console.adobe.io) och navigera till de befintliga Smart Content Services på sidan **[!UICONTROL Integrations]**. Överför det nya certifikatet. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## Integrering med Adobe Developer Console {#create-adobe-i-o-integration}

Om du vill använda API:er för tjänsten Smart Content Service skapar du en integrering i Adobe Developer Console för att hämta [!UICONTROL API Key] (som genereras i [!UICONTROL CLIENT ID] fältet Adobe Developer Console-integrering), [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID]och [!UICONTROL CLIENT SECRET] för [!UICONTROL Assets Smart Tagging Service Settings] molnkonfiguration i [!DNL Experience Manager].

1. Öppna [https://console.adobe.io](https://console.adobe.io/) i en webbläsare. Välj lämpligt konto och kontrollera att den associerade organisationsrollen är systemadministratör.

1. Skapa ett projekt med valfritt namn. Klicka på **[!UICONTROL Add API]**.

1. På sidan **[!UICONTROL Add an API]** markerar du **[!UICONTROL Experience Cloud]** och väljer **[!UICONTROL Smart Content]**. Klicka på **[!UICONTROL Next]**.

1. Välj **[!UICONTROL Upload your public key]**. Ange certifikatfilen som hämtats från [!DNL Experience Manager]. Ett meddelande [!UICONTROL Public key(s) uploaded successfully] visas. Klicka på **[!UICONTROL Next]**.

   Sidan [!UICONTROL Create a new Service Account (JWT) credential] visar den offentliga nyckeln för det tjänstekonto som just konfigurerats.

1. Klicka på **[!UICONTROL Next]**.

1. På sidan **[!UICONTROL Select product profiles]** markerar du **[!UICONTROL Smart Content Services]**. Klicka på **[!UICONTROL Save configured API]**.

   En sida visar mer information om konfigurationen. Håll den här sidan öppen för att kopiera och lägga till dessa värden i molnkonfigurationen [!UICONTROL Assets Smart Tagging Service Settings] i [!DNL Experience Manager] för att konfigurera smarta taggar.

   ![På fliken Overview kan du granska den information som finns för integrering.](assets/integration_details.png)


   *Bild: Information om integrering i Adobe Developer Console*

## Konfigurera Smart Content Service {#configure-smart-content-service}

To configure the integration, use the values of [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID], [!UICONTROL CLIENT SECRET], and [!UICONTROL CLIENT ID] fields from the Adobe Developer Console integration. Creating a Smart Tags cloud configuration allows authentication of API requests from the [!DNL Experience Manager] deployment.

1. In [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Legacy Cloud Services]** to open the [!UICONTROL Cloud Services] console.

1. Öppna konfigurationen som skapats ovan under **[!UICONTROL Assets Smart Tags]**. Klicka på **[!UICONTROL Edit]** på tjänstinställningssidan.

1. I dialogrutan **[!UICONTROL AEM Smart Content Service]** använder du de förifyllda värdena för fälten **[!UICONTROL Service URL]** och **[!UICONTROL Authorization Server]**.

1. För fälten [!UICONTROL Api Key], [!UICONTROL Technical Account ID], [!UICONTROL Organization ID]och [!UICONTROL Client Secret]kopierar och använder du följande värden som genererats i [Adobe Developer Console-integrering](#create-adobe-i-o-integration).

   | [!UICONTROL Assets Smart Tagging Service Settings] | [!DNL Adobe Developer Console] integreringsfält |
   |--- |--- |
   | [!UICONTROL Api Key] | [!UICONTROL CLIENT ID] |
   | [!UICONTROL Technical Account ID] | [!UICONTROL TECHNICAL ACCOUNT ID] |
   | [!UICONTROL Organization ID] | [!UICONTROL ORGANIZATION ID] |
   | [!UICONTROL Client Secret] | [!UICONTROL CLIENT SECRET] |

## Validera konfigurationen {#validate-the-configuration}

När du har slutfört konfigurationen kan du använda en JMX MBean för att validera konfigurationen. Följ de här stegen för att validera.

1. Gå till din [!DNL Experience Manager]-server på `https://[aem_server]:[port]`.

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** to open the OSGi console. Klicka på **[!UICONTROL Main]>[!UICONTROL JMX]**.

1. Klicka på `com.day.cq.dam.similaritysearch.internal.impl`. Det öppnar **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.

1. Klicka på `validateConfigs()`. I dialogrutan **[!UICONTROL Validate Configurations]** klickar du på **[!UICONTROL Invoke]**.

Valideringsresultaten visas i samma dialogruta.

## Aktivera smart taggning i [!UICONTROL DAM Update Asset] arbetsflödet (valfritt) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. I [!DNL Experience Manager] går du till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Välj arbetsflödesmodellen **[!UICONTROL DAM Update Asset]** på sidan **[!UICONTROL Workflow Models]**.

1. Klicka på **[!UICONTROL Edit]** i verktygsfältet.

1. Expandera sidopanelen för att visa stegen. Dra steget **[!UICONTROL Smart Tag Asset]** som finns i avsnittet med DAM-arbetsflöden och placera det efter steget **[!UICONTROL Process Thumbnails]**.

   ![Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i arbetsflödet för DAM-uppdatering av resurser](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Bild: Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i[!UICONTROL DAM Update Asset]arbetsflödet.*

1. Öppna steget i redigeringsläge. Under **[!UICONTROL Advanced Settings]** kontrollerar du att alternativet **[!UICONTROL Handler Advance]** är markerat.

   ![Konfigurera arbetsflödet för DAM-uppdatering och lägg till steg för smarta taggar](assets/smart-tag-step-properties-workflow1.png)


   *Bild: Konfigurera arbetsflödet för DAM-uppdatering och lägg till steg för smarta taggar*

1. In the **[!UICONTROL Arguments]** tab, select **[!UICONTROL Ignore Errors]** if you want the workflow to complete even if the automatic tagging step fails.

   ![Konfigurera arbetsflödet för DAM-uppdatering av resurser för att lägga till smart tagg och markera hanterarframsteg](assets/smart-tag-step-properties-workflow2.png)


   *Bild: Konfigurera arbetsflödet för DAM-uppdatering av resurser för att lägga till smart tagg och markera hanterarframsteg*

   Om du vill tagga resurser när de överförs, oavsett om smart taggning är aktiverat för mappar eller inte, markerar du **[!UICONTROL Ignore Smart Tag Flag]**.

   ![Konfigurera arbetsflödet för DAM-uppdatering av resurser för att lägga till smart tagg och markera ignorera smart tagg](assets/smart-tag-step-properties-workflow3.png)


   *Bild: Konfigurera arbetsflödet för DAM-uppdatering av resurser för att lägga till smart tagg och markera ignorera smart tagg*

1. Klicka på **[!UICONTROL OK]** för att stänga processsteget och spara sedan arbetsflödet.

>[!MORELIKETHIS]
>
>* [Hantera smarta taggar](managing-smart-tags.md)
>* [Översikt och utbildning av smarta taggar](enhanced-smart-tags.md)
>* [Riktlinjer och regler för utbildning av Smart Content Service](smart-tags-training-guidelines.md)
>* [Videosjälvstudiekurs om hur du konfigurerar smarta taggar](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

