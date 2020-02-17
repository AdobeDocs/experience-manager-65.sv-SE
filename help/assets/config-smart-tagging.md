---
title: Konfigurera resurstaggning med hjälp av Smart Content Service
description: Lär dig hur du konfigurerar smart taggning och förbättrad smart taggning i AEM med hjälp av Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Konfigurera resurstaggning med Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

Du kan integrera Adobe Experience Manager (AEM) med Smart Content Service med hjälp av Adobe I/O. Använd den här konfigurationen för att komma åt tjänsten Smart Content från AEM.

Artikeln innehåller information om följande viktiga uppgifter som krävs för att konfigurera tjänsten Smart Content. I bakänden autentiserar AEM-servern dina inloggningsuppgifter med Adobe IO-gatewayen innan din begäran vidarebefordras till Smart Content Service.

* Skapa en konfiguration för Smart Content Service i AEM för att generera en offentlig nyckel. Hämta ett offentligt certifikat för OAuth-integrering.
* Skapa en integrering i Adobe I/O och överför den genererade publika nyckeln.
* Konfigurera din AEM-instans med API-nyckeln och andra autentiseringsuppgifter från Adobe I/O.
* Du kan även aktivera automatisk taggning vid överföring av resurser.

## Förutsättningar {#prerequisites}

Innan du kan använda tjänsten Smart Content måste du se till att följande är integrerat med Adobe I/O:

* Ett Adobe ID-konto som har administratörsbehörighet för organisationen.
* Tjänsten Smart Content Service är aktiverad för din organisation.

## Hämta offentligt certifikat {#obtain-public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe I/O.

1. I AEM-användargränssnittet: tryck på AEM-logotypen och gå till **[!UICONTROL Verktyg > Molntjänster]**> **[!UICONTROL Äldre molntjänster]**.

1. Tryck/klicka på **[!UICONTROL Konfigurera nu]** under Smarta taggar för **[!UICONTROL resurser på sidan för molntjänster]**.
1. I dialogrutan **[!UICONTROL Skapa konfiguration]** anger du en rubrik och ett namn för konfigurationen av smarta taggar. Tryck/klicka på **[!UICONTROL Skapa]**.
1. Använd följande värden i dialogrutan **[!UICONTROL AEM Smart Content Service]** :

   **[!UICONTROL Tjänst-URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Auktoriseringsserver]**: `https://ims-na1.adobelogin.com`

   Lämna de andra fälten tomma (kommer senare). Tryck/klicka på **[!UICONTROL OK]**.

   ![Dialogrutan AEM Smart Content Service för att ange innehållstjänstens URL](assets/aem_scs.png)

1. Tryck/klicka på **[!UICONTROL Hämta offentligt certifikat för OAuth-integrering]** och hämta den offentliga certifikatfilen `AEM-SmartTags.crt`.

   ![En representation av de inställningar som har skapats för den smarta taggningstjänsten](assets/download_link.png)

### Konfigurera om när ett certifikat upphör att gälla {#certrenew}

När certifikatet upphör att gälla är det inte längre tillförlitligt. Följ de här stegen för att lägga till ett nytt certifikat. Du kan inte förnya ett certifikat som har upphört att gälla.

1. Logga in din AEM-distribution som administratör. Klicka på **[!UICONTROL Verktyg]** > **[!UICONTROL Dokumentskydd]** > **[!UICONTROL Användare]**.

1. Leta upp och klicka på **[!UICONTROL dam-update-service]** user. Klicka på fliken **[!UICONTROL Nyckelbehållare]** .
1. Ta bort den befintliga **[!UICONTROL nyckelbehållaren för]** likhetssökning med det certifikat som upphört att gälla. Klicka på **[!UICONTROL Spara och stäng]**.

   ![Ta bort befintlig likhetssökningspost i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat](assets/smarttags_delete_similaritysearch_keystore.png)

   Ta bort befintlig likhetssökningspost i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat

1. Navigera till **[!UICONTROL Verktyg]** > **[!UICONTROL Molntjänster]** > **[!UICONTROL Äldre molntjänster]**. Klicka på **[!UICONTROL Resursens smarta taggar]** > **[!UICONTROL Visa konfiguration]** > **[!UICONTROL Tillgängliga konfigurationer]**. Klicka på önskad konfiguration.

1. Om du vill hämta ett offentligt certifikat klickar du på **[!UICONTROL Hämta offentligt certifikat för OAuth-integrering]**.
1. Gå till [https://console.adobe.io](https://console.adobe.io) och navigera till de befintliga tjänsterna för smart innehåll på **[!UICONTROL integreringssidan]** . Överför det nya certifikatet. Mer information finns i anvisningarna i [Skapa Adobe I/O-integrering](#create-adobe-i-o-integration).

## Skapa Adobe I/O-integration {#create-adobe-i-o-integration}

Om du vill använda API:er för tjänsten Smart Content Service skapar du en integrering i Adobe I/O för att generera API-nyckel, ID för tekniskt konto, organisations-ID och klienthemlighet.

1. Gå till [https://console.adobe.io](https://console.adobe.io/).
1. På sidan **[!UICONTROL Integrationer]** väljer du lämpligt konto och kontrollerar att den associerade organisationsrollen är systemadministratör.
1. Tryck på **[!UICONTROL Ny integrering]**.
1. På sidan **[!UICONTROL Skapa en ny integrering]** väljer du **[!UICONTROL Åtkomst till ett API]**. Tryck på **[!UICONTROL Fortsätt]**.
1. Under **[!UICONTROL Experience Cloud]** väljer du **[!UICONTROL Smart innehåll]**. Tryck på **[!UICONTROL Fortsätt]**.

   ![När du skapar en ny integrering väljer du Smart innehåll under Experience Cloud bland de tillgängliga alternativen](assets/smart_content.png)

1. På nästa sida väljer du **[!UICONTROL Ny integrering]**. Tryck/klicka på **[!UICONTROL Fortsätt]**.
1. Ange ett namn för integreringsgatewayen på sidan **[!UICONTROL Integreringsinformation]** och lägg till en beskrivning.
1. Överför **[!UICONTROL filen som du hämtade ovan i certifikaten]** för `AEM-SmartTags.crt` offentliga nycklar.
1. Tryck/klicka på **[!UICONTROL Skapa integrering]**.
1. Om du vill visa integreringsinformationen trycker/klickar du på **[!UICONTROL Fortsätt för att visa integreringsinformationen]**.

   ![På fliken Översikt kan du granska den information som finns för integrering.](assets/integration_details.png)

## Konfigurera Smart Content Service {#configure-smart-content-service}

Om du vill konfigurera integreringen använder du nyckelfälten Teknisk konto-ID, Organisations-ID, Klienthemlighet, Auktoriseringsserver och API från Adobe I/O-integreringen. Om du skapar en molnkonfiguration för smarta taggar kan du autentisera API-begäranden från AEM-instansen.

1. I AEM-användargränssnittet: tryck/klicka på AEM-logotypen. Gå till **[!UICONTROL Verktyg > Molntjänst > Äldre molntjänster]** för att öppna molntjänstkonsolen.
1. Öppna konfigurationen som skapats ovan under Smarta taggar för **[!UICONTROL resurser]**. Klicka på **[!UICONTROL Redigera]** på tjänstinställningssidan.
1. I dialogrutan **[!UICONTROL AEM Smart Content Service]** använder du de förifyllda värdena för fälten **[!UICONTROL Service URL]** och **[!UICONTROL Authorization Server]** .
1. Använd de värden som genereras ovan för fälten **[!UICONTROL API-nyckel]**, ID för **[!UICONTROL tekniskt konto]**, **[!UICONTROL organisations-ID]** och **[!UICONTROL Klienthemlighet]**.

## Validera konfigurationen {#validate-the-configuration}

När du är klar med konfigurationen kan du använda en JMX MBean för att validera konfigurationen. Följ de här stegen för att validera.

1. Gå till din AEM-server på `https://[server]:[port]`.

1. Gå till **[!UICONTROL Verktyg > Åtgärder > Webbkonsol]** för att öppna OSGi-konsolen. Klicka på **[!UICONTROL Meny > JMX]**.
1. Klicka på **[!UICONTROL com.day.cq.dam.similarAritysearch.internal.impl]**. Den öppnar **[!UICONTROL LikhetSök efter andra uppgifter.]**
1. Klicka på **[!UICONTROL validateConfigs()]**. I dialogrutan **[!UICONTROL Validera konfigurationer]** klickar du på **[!UICONTROL Anropa]**.

   Valideringsresultatet visas i samma dialogruta.

## Aktivera smart taggning i arbetsflödet Uppdatera resurs (valfritt) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. I AEM-användargränssnittet: tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg > Arbetsflöde > Modeller]**.
1. På sidan **[!UICONTROL Arbetsflödesmodeller]** väljer du arbetsflödesmodellen **[!UICONTROL DAM-uppdatering]** .
1. Tryck/klicka på **[!UICONTROL Redigera]** i verktygsfältet.
1. Expandera sidopanelen för att visa stegen. Dra steget **[!UICONTROL Smart Tag Asset]** som finns i arbetsflödesavsnittet för DAM och placera det efter steget **[!UICONTROL Bearbeta miniatyrer]** .

   ![Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i arbetsflödet för DAM-uppdatering av resurs](assets/chlimage_1-105.png)

1. Öppna steget i redigeringsläge. Under **[!UICONTROL Avancerade inställningar]** kontrollerar du att alternativet **[!UICONTROL Avancerat]** för hanterare är markerat.

   ![chlimage_1-3](assets/chlimage_1-106.png)

1. På fliken **[!UICONTROL Argument]** väljer du **[!UICONTROL Ignorera fel]** om du vill att arbetsflödet ska slutföras även om det automatiska taggningssteget misslyckas.

   ![chlimage_1-4](assets/chlimage_1-107.png)

   Om du vill tagga resurser när de överförs, oavsett om smart taggning är aktiverat för mappar, väljer du **[!UICONTROL Ignorera smart taggflagga]**.

   ![chlimage_1-5](assets/chlimage_1-108.png)

1. Tryck på **[!UICONTROL OK]** för att stänga processsteget och spara sedan arbetsflödet.

>[!MORELIKETHIS]
>
>* [Hantera smarta taggar](managing-smart-tags.md)
>* [Översikt och utbildning av smarta taggar](enhanced-smart-tags.md)
>* [Riktlinjer och regler för utbildning av Smart Content Service](smart-tags-training-guidelines.md)
>* [Videosjälvstudiekurs om hur du konfigurerar smarta taggar](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

