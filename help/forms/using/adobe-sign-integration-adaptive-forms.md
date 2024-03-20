---
title: Integrera Adobe Sign med AEM Forms
description: Lär dig konfigurera Adobe Sign för din AEM Adaptiva Forms. Adobe Sign förbättrar arbetsflödet och bearbetar dokumenten inom juridik, försäljning, löneadministration, personaladministration och många andra områden.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Integrera [!DNL Adobe Sign] med AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Den här artikeln |

[!DNL Adobe Sign] möjliggör arbetsflöden för e-signaturer för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I en typisk [!DNL Adobe Acrobat Sign] och Adaptiv Forms fyller en användare i ett adaptivt formulär som kan användas för en tjänst. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder [!DNL Adobe Acrobat Sign] för att markera ansökan som godkänd. AEM Forms stöder både Adobe Acrobat Sign och Adobe Acrobat Sign Solutions for Government. Beroende på licens och krav kan du integrera eller ansluta AEM Forms med någon av lösningarna:

* [Anslut AEM Forms till Adobe Acrobat Sign](#adobe-sign)
* [Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter](#adobe-acrobat-sign-for-government)

## Anslut AEM Forms till Adobe Acrobat Sign {#adobe-sign}

Ansluta **[!DNL AEM Forms]** med **[!DNL Adobe Acrobat Sign]**, konfigurera de program och konton som anges i avsnittet Krav och koppla Adobe Sign till alla AEM Forms Author och Publish:

## Förutsättningar {#prerequisites}

Du behöver följande för att kunna integrera [!DNL Adobe Sign] med AEM [!DNL Forms]:

* En aktiv [Adobe Sign utvecklarkonto.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* An [SSL är aktiverat](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] server.
* An [Adobe Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Autentiseringsuppgifter (klient-ID och klienthemlighet) för [!DNL Adobe Sign] API-program.
* Ta bort befintliga [!DNL Adobe Sign] konfiguration från både författare och publiceringsinstanser.
* Använd [identisk krypteringsnyckel](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) för att skapa och publicera instanser.

## Konfigurera [!DNL Adobe Sign] med AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Utför följande steg för att konfigurera [!DNL Adobe Sign] med AEM [!DNL Forms] på Author-instansen:

1. På AEM [!DNL Forms] författarinstans, navigera till **verktyg** ![hammare](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. På **[!UICONTROL Configuration Browser]** sida, markera **[!UICONTROL Create]**.
   * Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.
1. I **[!UICONTROL Create Configuration]** dialogruta, ange **[!UICONTROL Title]** för konfigurationen, aktivera **[!UICONTROL Cloud Configurations]** och markera **[!UICONTROL Create]**. En konfigurationsbehållare skapas.
1. Navigera till **verktyg** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** och välj den konfigurationsbehållare som du skapade i steget ovan.

   >[!NOTE]
   >
   >Du kan antingen köra steg 1-4 för att skapa en konfigurationsbehållare och skapa en [!DNL Adobe Sign] i behållaren eller använd den befintliga `global` mapp i **verktyg** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Om du skapar konfigurationen i den nya konfigurationsbehållaren måste du ange behållarnamnet i dialogrutan **[!UICONTROL Configuration Container]** när du skapar ett adaptivt formulär.

   >[!NOTE]
   >
   Kontrollera att URL:en för konfigurationssidan för Cloud Service börjar med **HTTPS**. Om inte, [aktivera SSL](/help/sites-administering/ssl-by-default.md) för AEM [!DNL Forms] server.


1. Tryck på på konfigurationssidan **[!UICONTROL Create]** att skapa [!DNL Adobe Sign] AEM [!DNL Forms].
1. I **[!UICONTROL General]** -fliken i **[!UICONTROL Create Adobe Sign Configuration]** sida, ange en **[!UICONTROL Name]** för konfigurationen och tryck **[!UICONTROL Next]**. Du kan också ange en titel och bläddra för att välja en miniatyrbild för konfigurationen.
1. Nu kan du **[!UICONTROL Select solution]** för att markera [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. Kopiera URL:en i det aktuella webbläsarfönstret till en anteckningsruta och ta bort delen /`ui#/aem` från webbadressen. Den ändrade URL:en måste sedan konfigureras [!DNL Adobe Acrobat Sign] program med [!DNL AEM Forms], i ett senare steg. Tryck [!UICONTROL Next].

1. I **[!UICONTROL Settings]** tab,
   * den **[!UICONTROL OAuth URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/public/oauth/v2`

     Till exempel:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * den **[!UICONTROL Access token URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/oauth/v2/token`

     Till exempel:
     `https://api.na1.echosign.com/oauth/v2/token`

   där:

   **na1** refererar till standarddatabasfragmentet. Du kan ändra värdet för databasdelningen. Se till att [!DNL  Adobe Acrobat Sign] Molnkonfigurationer pekar mot [korrigera Shard](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   * Behåll **Skapa Adobe Acrobat Sign-konfiguration** sidan öppnas. Stäng den inte. Du kan hämta **Klient-ID** och **Klienthemlighet** efter konfigurering av OAuth-inställningar för [!DNL Adobe Acrobat Sign] som beskrivs i kommande steg.
   * När du har loggat in på ditt Adobe Sign-konto går du till **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API Information]** > **[!UICONTROL REST API Methods Documentation]** > **[!UICONTROL OAuth Access Token]** för att få tillgång till information om Adobe Sign OAuth URL och Access Token URL.

1. Konfigurera OAuth-inställningar för [!DNL Adobe Sign] program:

   1. Öppna ett webbläsarfönster och logga in på [!DNL Adobe Sign] utvecklarkonto.
   1. Välj det program som konfigurerats för AEM [!DNL Forms]och markera **[!UICONTROL Configure OAuth for Application]**.
   1. Kopiera **[!UICONTROL Client ID]** och **[!UICONTROL Client Secret]** till en anteckningsruta.
   1. I **[!UICONTROL Redirect URL]** lägger du till HTTPS-URL:en som kopierades i föregående steg.
   1. Aktivera följande OAuth-inställningar för [!DNL Adobe Sign] program och klickar på **[!UICONTROL Save]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   Om du vill ha stegvis information om hur du konfigurerar OAuth-inställningar för en [!DNL Adobe Sign] program och hämta nycklarna, se [Konfigurera autentiseringsinställningar för programmet](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) dokumentation för utvecklare.

   ![OAuth-konfiguration](assets/oauthconfig_new.png)

<!--
1. Go back to the **[!UICONTROL Create Adobe Sign Configuration]** page. In the **[!UICONTROL Settings]** tab, the **[!UICONTROL OAuth URL]** field mentions the  default URL. The format of the URL is:

   `https://<shard>/public/oAuth/v2`

   For example: 
   `https://secure.na1.echosign.com/public/oauth/v2`

   where:

   **na1** refers to the default database shard.

   You can modify the value for the database shard. Restart the server to be able to use the new value for the database shard.

   >[!NOTE]
   >
   >Ensure that your author and publish instance configurations point to the same shard. If you create multiple Adobe Sign configurations for an organization, ensure all the configurations utilize the same shard. -->

1. Gå tillbaka till **[!UICONTROL Create Adobe Sign Configuration]** sida. I **[!UICONTROL Settings]** -flik, ange **Klient-ID** (kallas även program-ID) och **Klienthemlighet**. Använd [Klient-ID och klienthemlighet för Adobe Sign-program](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) som skapats för AEM Forms.

1. Välj **[!UICONTROL Enable Adobe Sign for attachments also]** möjlighet att lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Sign] dokumentet har skickats för signering.

1. Välj **[!UICONTROL Connect to Adobe Sign]**. Ange användarnamn och lösenord för kontot som används när du skapar inloggningsuppgifter [!DNL Adobe Sign] program.

   ![Konfigurationen av Adobe Acrobat Sign Cloud lyckades](assets/adobe-sign-cloud-configuration-success.png)

1. Tryck **[!UICONTROL Create]** för att skapa [!DNL Adobe Sign] konfiguration.
1. Öppna AEM webbkonsol. URL:en är `https://'[server]:[port]'/system/console/configMgr`
1. Öppna **[!UICONTROL Forms Common Configuration Service].**
1. I **[!UICONTROL Allow]** fält, **välj** Alla användare - Alla användare, anonyma eller inloggade, kan förhandsgranska bilagor, verifiera och signera formulär och klicka på **[!UICONTROL Save].** Författarinstansen är konfigurerad att använda [!DNL Adobe Sign].
1. Publicera konfigurationen.
1. Använd [replikering](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) om du vill skapa en identisk konfiguration för motsvarande publiceringsinstanser.

Nu [!DNL Adobe Sign] är integrerat med AEM [!DNL Forms] och klart för användning i anpassningsbara formulär. Till [använda Adobe Sign-tjänsten i ett adaptivt formulär](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)anger du den konfigurationsbehållare som skapas ovan i anpassningsbara formuläregenskaper.

>[!NOTE]
>
Om du vill konfigurera Adobe Sign-sandlådan kan du följa samma konfigurationssteg som beskrivs i [Adobe Sign](#adobe-sign).

## Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter {#adobe-acrobat-sign-for-government}

Att knyta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter är en flerstegsprocess. Den innehåller följande uppgifter:

* Skapar omdirigerings-URL för dina AEM
* Dela omdirigerings-URL:er och omfattningar med Adobe Sign Solutions for Government-teamet
* Få inloggningsuppgifter från Adobe Sign team
* Använda inloggningsuppgifterna för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Innan du börjar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Innan du börjar ansluta AEM Forms med Adobe Acrobat Sign Solution,

* Se till att [Adobe Acrobat Sign Solutions för myndigheter](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) kontot har etablerats.
* Din AEM [!DNL Forms] servrar är [SSL är aktiverat](/help/sites-administering/ssl-by-default.md) .
* Din AEM [!DNL Forms] servrar använder [identisk krypteringsnyckel](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) för att skapa och publicera instanser.

### Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter {#connect-adobe-acrobat-sign-for-government}

#### Skapa en omdirigerings-URL för AEM

1. I AEM Forms går du till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. På **[!UICONTROL Configuration Browser]** sida, markera **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Configuration]** dialogruta, ange **[!UICONTROL Title]** för konfigurationen, aktivera **[!UICONTROL Cloud Configurations]** och markera **[!UICONTROL Create]**. En konfigurationsbehållare skapas. Kontrollera att behållar-/mappnamnet inte innehåller något utrymme.

1. Navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** och öppna konfigurationsbehållaren som du skapade i föregående steg. När du skapar ett adaptivt formulär anger du behållarnamnet i dialogrutan **[!UICONTROL Configuration Container]** fält.
1. Välj på konfigurationssidan **[!UICONTROL Create]** att skapa [!DNL Adobe Acrobat Sign] i AEM Forms.
1. Kopiera URL-adressen för det aktuella webbläsarfönstret till en anteckningsruta från URL-adressen. Denna URL kallas `re-direct URL`. I nästa avsnitt delar du `re-direct URL` och `Scopes` med Adobe Sign team och begära inloggningsuppgifter (klient-ID och klienthemlighet).

>[!NOTE]
>
>
* A `re-direct URL` måste innehålla [Översta nivån](https://en.wikipedia.org/wiki/Top-level_domain) domän. Exempel: `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* Använd inte en lokal URL som `re-direct URL`. Till exempel: `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.


#### Dela omdirigerings-URL:en och omfattningarna med Adobe Sign team och få inloggningsuppgifter

Adobe Acrobat Sign for Government Solutions-teamet kräver `re-direct URL` och vilka scope som ska aktiveras för ditt Adobe Acrobat Sign-program (se nedan) för att generera autentiseringsuppgifter (klient-ID och klienthemlighet) som gör att du kan ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter.

Dela `scopes` (visas nedan) och `re-direct URL` skapat och noterat i det sista steget i föregående avsnitt med en representant för Adobe Acrobat Sign for Government Solution [Adobe Professional Services teammedlem](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_Omfång_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

Representanten genererar och delar uppgifter med dig. I nästa avsnitt använder du inloggningsuppgifterna (Klient-ID och Klienthemlighet) för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter.

#### Använd de inloggningsuppgifter som tas emot för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för offentlig sektor

1. Öppna `re-direct URL` i webbläsaren. Du skapade och antecknade i `re-direct URL` i det sista steget i [skapa en omdirigerings-URL för din AEM](#create-redirect-url) -avsnitt.

1. I **[!UICONTROL General]** -fliken i **[!UICONTROL Create Adobe Sign Configuration]** sida, ange en **[!UICONTROL Name]** för konfigurationen och välj **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]** och bläddra för att välja **[!UICONTROL Thumbnail]** för konfigurationen. Klicka på **[!UICONTROL Next]**.

1. I **[!UICONTROL Settings]** -fliken i **[!UICONTROL Create Adobe Sign Configuration]** sida, för **[!UICONTROL Select solution]** alternativ, markera [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions för myndigheter](/help/forms/using/assets/adobe-sign-for-govt.png)

1. I **[!UICONTROL Email]** anger du den e-postadress som är kopplad till ditt Adobe Acrobat Sign Solutions for Government-konto.

1. I **[!UICONTROL Settings]** tab,
   * den **[!UICONTROL OAuth URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Till exempel:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * den **[!UICONTROL Access token URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Till exempel:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   där:

   **na1** refererar till standarddatabasfragmentet. Du kan ändra värdet för databasdelningen. Se till att [!DNL  Adobe Acrobat Sign] Molnkonfigurationer pekar mot [korrigera Shard](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   * När du har loggat in på ditt Adobe Sign-konto går du till **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API Information]** > **[!UICONTROL REST API Methods Documentation]** > **[!UICONTROL OAuth Access Token]** för att få tillgång till information om Adobe Sign Autentiserings-URL och Access Token-URL.

1. Använd autentiseringsuppgifterna som delas av Adobe Acrobat Sign för handläggare ([Adobe Professional Services teammedlem]) i föregående avsnitt som [**[!UICONTROL Client ID]** och **[!UICONTROL Client Secret]**].

1. Välj **[!UICONTROL Enable Adobe Acrobat Sign for attachments]** möjlighet att lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Acrobat Sign] dokumentet har skickats för signering.

1. Välj **[!UICONTROL Connect to Adobe Sign]**. Ange användarnamn och lösenord för kontot som används när du skapar inloggningsuppgifter [!DNL Adobe Acrobat Sign] program. När du ombeds att bekräfta åtkomsten för `Adobe Acrobat Sign for Government Solutions` och klickar **[!UICONTROL Allow Access]**. Om autentiseringsuppgifterna är korrekta och du tillåter [!DNL AEM Forms] för att få tillgång till [!DNL Adobe Acrobat Sign] utvecklarkontot visas ett meddelande om att åtgärden lyckades.

   ![Konfigurationen av Adobe Acrobat Sign Cloud lyckades](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Ange användarnamn och lösenord för kontot som används när du skapar inloggningsuppgifter [!DNL Adobe Acrobat Sign] program. När du ombeds att bekräfta åtkomsten för `your account`och klicka **[!UICONTROL Allow Access]**.

1. Välj **[!UICONTROL Create]** för att skapa konfigurationen.
1. Öppna AEM webbkonsol. URL:en är `https://'[server]:[port]'/system/console/configMgr`
1. Öppna **[!UICONTROL Forms Common Configuration Service].**
1. I **[!UICONTROL Allow]** fält, **välj** Alla användare - Alla användare, anonyma eller inloggade, kan förhandsgranska bilagor, verifiera och signera formulär och klicka på **[!UICONTROL Save].** Författarinstansen är konfigurerad att använda [!DNL Adobe Sign].

1. Publicera konfigurationen.
1. Använd [replikering](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) om du vill skapa en identisk konfiguration för motsvarande publiceringsinstanser.

Nu kan du [använda lägg till Adobe Acrobat Sign-fält i ett adaptivt formulär](working-with-adobe-sign.md) eller [AEM](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Se till att du lägger till konfigurationsbehållaren som används för konfigurationen av Cloud Servicen i alla adaptiva Forms som aktiveras för [!DNL Adobe Acrobat Sign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.


## Konfigurera [!DNL Adobe Sign] schemaläggaren för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

An [!DNL Adobe Sign] anpassat formulär skickas endast när alla signerare har slutfört signeringsprocessen. Som standard är [!DNL Adobe Sign] Schemaläggartjänster schemaläggs att kontrollera (avfråga) signerarens svar efter 24 timmars intervall. Du kan ändra standardintervallet för din miljö. Utför följande steg för att ändra standardintervallet:

1. Logga in på AEM [!DNL Forms] server med administratörsuppgifter och navigera till **verktyg** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   Du kan även öppna följande URL-adress i ett webbläsarfönster:
   `https://[localhost]:'port'/system/console/configMgr`

1. Leta reda på och öppna **[!UICONTROL Adobe Sign Configuration Service]** alternativ. Ange en [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) i **[!UICONTROL Status Update Scheduler Expression]** fält och klicka **[!UICONTROL Save]**. Om du till exempel vill köra konfigurationstjänsten varje dag klockan 00:00 anger du `0 0 0 1/1 * ? *` i **[!UICONTROL Status Update Scheduler Expression]** fält.

Standardintervall för synkroniseringsstatus för [!DNL Adobe Sign] har ändrats.

## Relaterade artiklar {#related-articles}

* [Använda Adobe Sign i en adaptiv form](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign med blankettbaserade arbetsflöden](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [Använda Adobe Sign med AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
