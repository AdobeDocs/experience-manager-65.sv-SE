---
title: Konfigurera resurstaggning med Smart Content Service
description: Lär dig hur du konfigurerar smart taggning och förbättrad smart taggning [!DNL Adobe Experience Manager]med hjälp av Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 29%

---


# Förbered [!DNL Assets] för smart taggning {#configure-asset-tagging-using-the-smart-content-service}

Innan du kan börja tagga dina resurser med smarta innehållstjänster bör du integrera [!DNL Experience ManageR Assets] med Adobe Developer Console för att utnyttja smarta tjänster i [!DNL Adobe Sensei]. När du har konfigurerat tåget med några bilder och en tagg.

Innan du använder tjänsten för smart innehåll bör du kontrollera följande:

* [Integrera med Adobe Developer Console](#integrate-adobe-io).
* [Utbilda Smart Content Service](#training-the-smart-content-service).

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* Installera det senaste [Experience Manager-servicepaketet](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## Integrera med Adobe Developer Console {#integrate-adobe-io}

När du integrerar med Adobe Developer Console autentiserar [!DNL Experience Manager] servern dina inloggningsuppgifter med Adobe Developer Console-gatewayen innan du vidarebefordrar din begäran till Smart Content Service. För att integrera behöver ni ett Adobe ID-konto med administratörsbehörighet för organisationen och en licens för Smart Content Service som köpts och aktiverats för organisationen.

Så här konfigurerar du tjänsten Smart Content:

1. [](#obtain-public-certificate)Skapa en konfiguration för Smart Content Service i [!DNL Experience Manager] för att generera en offentlig nyckel. [Hämta ett offentligt certifikat](#obtain-public-certificate) för OAuth-integrering.

1. [Skapa en integrering i Adobe Developer Console](#create-adobe-i-o-integration) och överför den genererade offentliga nyckeln.

1. [Konfigurera distributionen](#configure-smart-content-service) med API-nyckeln och andra autentiseringsuppgifter från Adobe Developer Console.

1. [Testa konfigurationen](#validate-the-configuration).

1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Skapa konfiguration för tjänsten Smart Content för att hämta offentligt certifikat {#obtain-public-certificate}

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

#### Reconfigure when a certificate expires {#certrenew}

När ett certifikat har upphört att gälla är det inte längre tillförlitligt. Du kan inte förnya ett certifikat som har upphört att gälla. Följ de här stegen för att lägga till ett nytt certifikat.

1. Logga in på [!DNL Experience Manager]-driftsättningen som administratör. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Leta reda på och klicka på **[!UICONTROL dam-update-service]**-användaren. Klicka på fliken **[!UICONTROL Keystore]**.

1. Ta bort den befintliga **[!UICONTROL similaritysearch]**-nyckelbehållaren med det certifikat som upphört att gälla. Klicka på **[!UICONTROL Save & Close]**.

   ![Ta bort den befintliga posten för likhetssökning i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat](assets/smarttags_delete_similaritysearch_keystore.png)


   *Bild: Ta bort den befintliga `similaritysearch`-posten i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat.*

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Klicka på **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Klicka på önskad konfiguration.

1. Om du vill hämta ett offentligt certifikat klickar du på **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. Gå till [https://console.adobe.io](https://console.adobe.io) och navigera till de befintliga Smart Content Services på sidan **[!UICONTROL Integrations]**. Överför det nya certifikatet. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

### Integrering med Adobe Developer Console {#create-adobe-i-o-integration}

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

### Konfigurera Smart Content Service {#configure-smart-content-service}

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

### Validera konfigurationen {#validate-the-configuration}

När du har slutfört konfigurationen kan du använda en JMX MBean för att validera konfigurationen. Följ de här stegen för att validera.

1. Gå till din [!DNL Experience Manager]-server på `https://[aem_server]:[port]`.

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** to open the OSGi console. Klicka på **[!UICONTROL Main]>[!UICONTROL JMX]**.

1. Klicka på `com.day.cq.dam.similaritysearch.internal.impl`. Det öppnar **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.

1. Klicka på `validateConfigs()`. I dialogrutan **[!UICONTROL Validate Configurations]** klickar du på **[!UICONTROL Invoke]**.

Valideringsresultaten visas i samma dialogruta.

### Aktivera smart taggning i [!UICONTROL DAM Update Asset] arbetsflödet (valfritt) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. I [!DNL Experience Manager] går du till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Välj arbetsflödesmodellen **[!UICONTROL DAM Update Asset]** på sidan **[!UICONTROL Workflow Models]**.

1. Klicka på **[!UICONTROL Edit]** i verktygsfältet.

1. Expandera sidopanelen för att visa stegen. Dra steget **[!UICONTROL Smart Tag Asset]** som finns i avsnittet med DAM-arbetsflöden och placera det efter steget **[!UICONTROL Process Thumbnails]**.

   ![Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i arbetsflödet för DAM-uppdatering av resurser](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Bild: Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i [!UICONTROL DAM Update Asset] arbetsflödet.*

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

## Utbilda tjänsten Smart Content {#training-the-smart-content-service}

För att Smart Content Service ska känna igen din företagsklonomi kan du köra den på en uppsättning resurser som redan innehåller taggar som är relevanta för ditt företag. För att effektivt märka upp varumärkesbilderna måste utbildningsbilderna följa vissa riktlinjer. Efter utbildning kan tjänsten tillämpa samma taxonomi på liknande resurser.

Du kan utbilda tjänsten flera gånger för att förbättra dess förmåga att använda relevanta taggar. Efter varje utbildningscykel kör du ett taggningsarbetsflöde och kontrollerar om dina resurser är taggade på rätt sätt.

Du kan utbilda Smart Content Service regelbundet eller efter behov.

>[!NOTE]
>
>Utbildningsarbetsflödet kan endast användas på mappar.

### Riktlinjer för utbildning {#guidelines-for-training}

För bästa resultat bör bilderna i din utbildningsserie följa följande riktlinjer:

**Kvantitet och storlek:** Minst 30 bilder per tagg. Minst 500 pixlar på den längre sidan.

**Samstämmighet**: Bilderna för en tagg bör vara visuellt lika.

Det är till exempel ingen bra idé att tagga alla dessa bilder som `my-party` (för utbildning) eftersom de inte är visuellt lika.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/coherence.png)

**Täckning**: Det ska finnas tillräckligt med variation i bilderna i utbildningen. Tanken är att ge några men relativt olika exempel så att Experience Manager lär sig att fokusera på rätt saker. Om du använder samma tagg på bilder som ser olika ut bör du ta med minst fem exempel av varje typ.

För taggen *model-down* kan du t.ex. inkludera fler utbildningsbilder som liknar den markerade bilden nedan för tjänsten för att identifiera liknande bilder mer exakt under taggningen.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/coverage_1.png)

**Distraktion/obstruktion**: Tjänsten tränar bättre på bilder som inte är så distraherande (framträdande bakgrunder, icke-relaterade komponenter, t.ex. objekt/personer med huvudmotivet).

För taggen *casual-shoe*&#x200B;är den andra bilden till exempel inte en bra träningskandidat.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/distraction.png)

**Fullständighet:** Om en bild kvalificerar sig för mer än en tagg lägger du till alla tillämpliga taggar innan du inkluderar bilden för träning. For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![Illustrativa bilder som exempel på riktlinjer för utbildning](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>Möjligheten för Smart Content Service att lära sig taggar och använda dem på andra bilder beror på kvaliteten på de bilder du använder i utbildningen. För bästa resultat rekommenderar Adobe att du använder visuellt liknande bilder för att utbilda tjänsten för varje tagg.

### Periodisk utbildning {#periodic-training}

Du kan aktivera tjänsten Smart Content Service för att med jämna mellanrum utbilda resurser och tillhörande taggar i en mapp. Öppna [!UICONTROL Properties] sidan i resursmappen, markera **[!UICONTROL Enable Smart Tags]** under **[!UICONTROL Details]** fliken och spara ändringarna.

![enable_smart_tags](assets/enable_smart_tags.png)

När det här alternativet har valts för en mapp [!DNL Experience Manager] körs ett utbildningsarbetsflöde automatiskt för att utbilda Smart Content Service i mappresurserna och deras taggar. Som standard körs utbildningsarbetsflödet varje vecka kl. 12.30 på lördagar.

### On-demand-utbildning {#on-demand-training}

Du kan utbilda tjänsten för smart innehåll när det behövs från arbetsflödeskonsolen.

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. I **[!UICONTROL Run Workflow]** dialogrutan bläddrar du till den nyttolastmapp som innehåller de taggade resurserna för att utbilda tjänsten.
1. Ange en rubrik för arbetsflödet och lägg till en kommentar. Klicka sedan på **[!UICONTROL Run]**. Resurserna och taggarna skickas in för utbildning.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>När materialet i en mapp har behandlats för utbildning behandlas endast de ändrade resurserna i efterföljande utbildningscykler.

### Visa utbildningsrapporter {#viewing-training-reports}

Om du vill kontrollera om Smart Content Service är utbildad i dina taggar i övningsresurserna kan du läsa rapporten om utbildningsarbetsflödet i rapportkonsolen.

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Ange en titel och beskrivning för rapporten. Under **[!UICONTROL Schedule Report]** låter du alternativet **[!UICONTROL Now]** vara markerat. Om du vill schemalägga rapporten till ett senare tillfälle väljer du **[!UICONTROL Later]** och anger ett datum och en tid. Then, click **[!UICONTROL Create]** from the toolbar.
1. På sidan **[!UICONTROL Asset Reports]** markerar du rapporten som du skapat. Om du vill visa rapporten klickar du **[!UICONTROL View]** i verktygsfältet.
1. Granska informationen i rapporten.

   Rapporten visar träningsstatusen för de taggar du har tränat. Den gröna färgen i kolumnen **[!UICONTROL Training Status]** anger att smarta innehållstjänster har tränats för taggen. Gul färg anger att tjänsten inte är helt tränad för en viss tagg. I det här fallet lägger du till fler bilder med just den taggen och kör träningsarbetsflödet för att träna tjänsten helt för taggen.

   Om du inte ser dina taggar i den här rapporten kör du utbildningsarbetsflödet igen för dessa taggar.

1. Om du vill hämta rapporten markerar du den i listan och klickar på **[!UICONTROL Download]** i verktygsfältet. Rapporten hämtas som ett Microsoft Excel-kalkylblad.

## Begränsningar {#limitations}

* Förbättrade smarta taggar bygger på inlärningsmodeller för bilder och taggar. Dessa modeller är inte alltid perfekta när det gäller att identifiera taggar. Den aktuella versionen av Smart Content Service har följande begränsningar:

   * Oförmåga att identifiera små skillnader i bilder. Till exempel tunna eller jämna skjortor.
   * Oförmåga att identifiera taggar baserat på små mönster/delar av en bild. Till exempel logotyper på T-shirts.
   * Taggning stöds i de språkområden som [!DNL Experience Manager] stöds i. En lista med språk finns i Versionsinformation för [Smart Content Services](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html).

* Om du vill söka efter resurser med smarta taggar (vanliga eller förbättrade) använder du [!DNL Assets] Omnissearch (fulltextsökning). Det finns inget separat sökpredikat för smarta taggar.

>[!MORELIKETHIS]
>
>* [Översikt och utbildning av smarta taggar](enhanced-smart-tags.md)
>* [Videosjälvstudiekurs om smarta taggar](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

