---
title: Konfigurera resurstaggning med Smart Content Service.
description: Lär dig hur du konfigurerar smart taggning och förbättrad smart taggning i Adobe Experience Manager med hjälp av Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f3d699f35c7b1ef832a0857fa2fa41aed1fe5a4e
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 62%

---


# Konfigurera resurstaggning med Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

Du kan integrera [!DNL Adobe Experience Manager] med Smart Content Service via Adobe Developer Console. Använd den här konfigurationen för att komma åt Smart Content Service inifrån [!DNL Experience Manager].

Artikeln innehåller information om följande viktiga uppgifter som krävs för att konfigurera Smart Content Service. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

* Skapa en konfiguration för Smart Content Service i [!DNL Experience Manager] för att generera en offentlig nyckel. Hämta ett offentligt certifikat för OAuth-integrering.
* Skapa en integrering i Adobe Developer Console och överför den genererade offentliga nyckeln.
* Konfigurera din [!DNL Experience Manager]-instans med API-nyckeln och andra autentiseringsuppgifter från Adobe Developer Console.
* Du kan även aktivera automatisk taggning vid överföring av resurser.

## Förutsättningar {#prerequisites}

Innan du kan använda tjänsten Smart Content måste du göra följande för att skapa en integrering på Adobe Developer Console:

* Ett Adobe ID-konto som har administratörsbehörighet för organisationen.
* Att Smart Content Service är aktiverad för din organisation.

## Hämta ett offentligt certifikat {#obtain-public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe Developer Console.

1. I användargränssnittet för [!DNL Experience Manager] går du till **[!UICONTROL Tools > Cloud Services]**> **[!UICONTROL Legacy Cloud Services]**.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. I dialogrutan **[!UICONTROL Create Configuration]** anger du en rubrik och ett namn för konfigurationen av smarta taggar. Klicka på **[!UICONTROL Create]**.
1. Använd följande värden i dialogrutan **[!UICONTROL AEM Smart Content Service]**:

   **[!UICONTROL Service URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Authorization Server]**: `https://ims-na1.adobelogin.com`

   Lämna de andra fälten tomma (kommer senare). Klicka på **[!UICONTROL OK]**.

   ![Dialogrutan Experience Manager Smart Content Service för att tillhandahålla innehållstjänstens URL](assets/aem_scs.png)

1. Klicka på **[!UICONTROL Download Public Certificate for OAuth Integration]** och hämta den offentliga certifikatfilen `AEM-SmartTags.crt`.

   ![En representation av de inställningar som har skapats för den smarta taggningstjänsten](assets/smart-tags-download-public-cert.png)

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

Om du vill använda API:er för smarta innehållstjänster skapar du en integrering i Adobe Developer Console för att generera API-nyckel, ID för tekniskt konto, organisations-ID och klienthemlighet.

1. Öppna [https://console.adobe.io](https://console.adobe.io/) i en webbläsare. Välj lämpligt konto och kontrollera att den associerade organisationsrollen är systemadministratör.
1. Skapa ett projekt med valfritt namn. Klicka på **[!UICONTROL Add API]**.
1. På sidan **[!UICONTROL Add an API]** markerar du **[!UICONTROL Experience Cloud]** och väljer **[!UICONTROL Smart Content]**. Klicka på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Upload your public key]**. Ange certifikatfilen som hämtats från [!DNL Experience Manager]. Ett meddelande [!UICONTROL Public key(s) uploaded successfully] visas. Klicka på **[!UICONTROL Next]**.
1. Sidan [!UICONTROL Create a new Service Account (JWT) credential] visar den offentliga nyckeln för det tjänstekonto som just konfigurerats. Klicka på **[!UICONTROL Next]**.
1. På sidan **[!UICONTROL Select product profiles]** markerar du **[!UICONTROL Smart Content Services]**. Klicka på **[!UICONTROL Save configured API]**. En sida visar mer information om konfigurationen. Håll den sidan öppen för att kopiera och lägga till dessa värden i Experience Manager när du konfigurerar Smart Tags i [!DNL Experience Manager].

   ![På fliken Overview kan du granska den information som finns för integrering.](assets/integration_details.png)

## Konfigurera Smart Content Service {#configure-smart-content-service}

Om du vill konfigurera integreringen använder du nyckelfälten Teknisk konto-ID, Organisations-ID, Klienthemlighet, Auktoriseringsserver och API från Adobe Developer Console-integreringen. Om du skapar en molnkonfiguration för smarta taggar kan du autentisera API-begäranden från [!DNL Experience Manager]-instansen.

1. I [!DNL Experience Manager] navigerar du till **[!UICONTROL Tools > Cloud Service > Legacy Cloud Services]** för att öppna konsolen [!UICONTROL Cloud Services].
1. Öppna konfigurationen som skapats ovan under **[!UICONTROL Assets Smart Tags]**. Klicka på **[!UICONTROL Edit]** på tjänstinställningssidan.
1. I dialogrutan **[!UICONTROL AEM Smart Content Service]** använder du de förifyllda värdena för fälten **[!UICONTROL Service URL]** och **[!UICONTROL Authorization Server]**.
1. För fälten **[!UICONTROL API Key]**, **[!UICONTROL Technical Account Id]**, **[!UICONTROL Organization Id]** och **[!UICONTROL Client Secret]** använder du värdena som genereras ovan.

## Validera konfigurationen {#validate-the-configuration}

När du är klar med konfigurationen kan du använda en JMX MBean för att validera konfigurationen. Följ de här stegen för att validera.

1. Gå till din [!DNL Experience Manager]-server på `https://[aem_server]:[port]`.

1. Gå till **[!UICONTROL Tools > Operations > Web Console]** för att öppna OSGi-konsolen. Klicka på **[!UICONTROL Main > JMX]**.
1. Klicka på **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Det öppnar **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.
1. Klicka på **[!UICONTROL validateConfigs()]**. I dialogrutan **[!UICONTROL Validate Configurations]** klickar du på **[!UICONTROL Invoke]**.

   Valideringsresultatet visas i samma dialogruta.

## Aktivera smart taggning i arbetsflödet DAM-uppdatering (valfritt) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. I [!DNL Experience Manager] går du till **[!UICONTROL Tools > Workflow > Models]**.
1. Välj arbetsflödesmodellen **[!UICONTROL DAM Update Asset]** på sidan **[!UICONTROL Workflow Models]**.
1. Klicka på **[!UICONTROL Edit]** i verktygsfältet.
1. Expandera sidopanelen för att visa stegen. Dra steget **[!UICONTROL Smart Tag Asset]** som finns i avsnittet med DAM-arbetsflöden och placera det efter steget **[!UICONTROL Process Thumbnails]**.

   ![Lägga till resurssteget för smarta taggar efter steget med processminiatyrer i [!UICONTROL DAM Update Asset] arbetsflödet](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Bild: Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i[!UICONTROL DAM Update Asset]arbetsflödet.*

1. Öppna steget i redigeringsläge. Under **[!UICONTROL Advanced Settings]** kontrollerar du att alternativet **[!UICONTROL Handler Advance]** är markerat.

   ![Konfigurera arbetsflödet för DAM-uppdatering och lägg till steg för smarta taggar](assets/smart-tag-step-properties-workflow1.png)

1. In the **[!UICONTROL Arguments]** tab, select **[!UICONTROL Ignore Errors]** if you want the workflow to complete even if the automatic tagging step fails.

   ![Konfigurera arbetsflödet för DAM-uppdatering av resurser för att lägga till smart tagg och markera hanterarframsteg](assets/smart-tag-step-properties-workflow2.png)

   Om du vill tagga resurser när de överförs, oavsett om smart taggning är aktiverat för mappar eller inte, markerar du **[!UICONTROL Ignore Smart Tag Flag]**.

   ![Konfigurera arbetsflödet för DAM-uppdatering av resurser för att lägga till smart tagg och markera ignorera smart tagg](assets/smart-tag-step-properties-workflow3.png)

1. Klicka på **[!UICONTROL OK]** för att stänga processsteget och spara sedan arbetsflödet.

>[!MORELIKETHIS]
>
>* [Hantera smarta taggar](managing-smart-tags.md)
>* [Översikt och utbildning av smarta taggar](enhanced-smart-tags.md)
>* [Riktlinjer och regler för utbildning av Smart Content Service](smart-tags-training-guidelines.md)
>* [Videosjälvstudiekurs om hur du konfigurerar smarta taggar](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

