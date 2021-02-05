---
title: Integrera Adobe Sign med AEM Forms
seo-title: Integrera Adobe Sign med AEM Forms
description: Lär dig konfigurera Adobe Sign för AEM Forms
seo-description: Lär dig konfigurera Adobe Sign för AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: fd9ee8e4eb35bd5d303d7bbdd9660a94c54925ff
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---


# Integrera [!DNL Adobe Sign] med AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] möjliggör arbetsflöden för e-signaturer för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt [!DNL Adobe Sign]- och adaptivt formulärscenario fyller en användare i ett adaptivt formulär som **söker efter en tjänst**. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder [!DNL Adobe Sign] för att markera programmet som godkänt. Om du vill aktivera liknande arbetsflöden för elektroniska signaturer kan du integrera [!DNL Adobe Sign] med AEM [!DNL Forms].

Om du vill använda [!DNL Adobe Sign] med AEM [!DNL Forms] ska du konfigurera [!DNL Adobe Sign] i AEM Cloud-tjänsterna:

## Förutsättningar {#prerequisites}

Du behöver följande för att integrera [!DNL Adobe Sign] med AEM [!DNL Forms]:

* Ett aktivt [Adobe Sign-utvecklarkonto.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* En [SSL aktiverad](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms]-server.
* Ett [Adobe Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Autentiseringsuppgifter (klient-ID och klienthemlighet) för API-programmet [!DNL Adobe Sign].
* När du konfigurerar om tar du bort den befintliga [!DNL Adobe Sign]-konfigurationen från både författare- och publiceringsinstanser.
* Använd [identisk krypteringsnyckel](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) för författare- och publiceringsinstanser.

## Konfigurera [!DNL Adobe Sign] med AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

När förutsättningarna är uppfyllda utför du följande steg för att konfigurera [!DNL Adobe Sign] med AEM [!DNL Forms] på Author-instansen:

1. På AEM [!DNL Forms] författarinstans går du till **Verktyg** ![hammer](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. Tryck på **[!UICONTROL Create]** på sidan **[!UICONTROL Configuration Browser]**.
   * Mer information finns i [Configuration Browser](/help/sites-administering/configurations.md)-dokumentationen.
1. I dialogrutan **[!UICONTROL Create Configuration]** anger du **[!UICONTROL Title]** för konfigurationen, aktiverar **[!UICONTROL Cloud Configurations]** och trycker på **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för molntjänster.
1. Navigera till **Verktyg** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** och välj den konfigurationsbehållare som du skapade i ovanstående steg.

   >[!NOTE]
   >
   >Du kan antingen köra steg 1-4 för att skapa en ny konfigurationsbehållare och skapa en [!DNL Adobe Sign]-konfiguration i behållaren eller använda den befintliga `global`-mappen i **Verktyg** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Om du skapar konfigurationen i den nya konfigurationsbehållaren måste du ange behållarnamnet i fältet **[!UICONTROL Configuration Container]** när du skapar ett anpassat formulär.

   >[!NOTE]
   Kontrollera att URL:en för konfigurationssidan för molntjänster börjar med **HTTPS**. Om inte, [aktivera SSL](/help/sites-administering/ssl-by-default.md) för AEM [!DNL Forms]-server.

1. Tryck på **[!UICONTROL Create]** på konfigurationssidan för att skapa [!DNL Adobe Sign]-konfigurationen i AEM [!DNL Forms].
1. På fliken **[!UICONTROL General]** på sidan **[!UICONTROL Create Adobe Sign Configuration]** anger du **[!UICONTROL Name]** för konfigurationen och trycker på **[!UICONTROL Next]**. Du kan också ange en titel och bläddra för att välja en miniatyrbild för konfigurationen.

1. Kopiera URL-adressen i det aktuella webbläsarfönstret till en anteckningsruta. Du måste konfigurera [!DNL Adobe Sign]-programmet med AEM[!DNL Forms].

1. Konfigurera OAuth-inställningar för [!DNL Adobe Sign]-programmet:

   1. Öppna ett webbläsarfönster och logga in på [!DNL Adobe Sign]-utvecklarkontot.
   1. Markera programmet som är konfigurerat för AEM [!DNL Forms] och tryck på **[!UICONTROL Configure OAuth for Application]**.
   1. Kopiera **[!UICONTROL Client ID]** och **[!UICONTROL Client Secret]** till ett anteckningsblock.
   1. Lägg till HTTPS-URL:en som kopierades i föregående steg i rutan **[!UICONTROL Redirect URL]**.
   1. Aktivera följande OAuth-inställningar för [!DNL Adobe Sign]-programmet och klicka på **[!UICONTROL Save]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Stegvis information om hur du konfigurerar OAuth-inställningar för ett [!DNL Adobe Sign]-program och hämtar nycklarna finns i [Konfigurera autentiseringsinställningar för programmets](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) utvecklardokumentation.

   ![OAuth-konfiguration](assets/oauthconfig_new.png)

1. Gå tillbaka till sidan **[!UICONTROL Create Adobe Sign Configuration]**. På fliken **[!UICONTROL Settings]** anger fältet **[!UICONTROL OAuth URL]** följande standard-URL:

   https://secure.na1.echosign.com/public/oauth

   där:

   **na1** refererar till standarddatabasdelningen.

   Du kan ändra värdet för databasdelningen. Starta om servern för att kunna använda det nya värdet för databasdelningen.

   >[!NOTE]
   Se till att författaren och publicera instanskonfigurationer pekar på samma nivå. Om du skapar flera Adobe Sign-konfigurationer för en organisation måste du se till att alla konfigurationer använder samma fragment.

1. Ange **klient-ID** (kallas även program-ID) och **klienthemlighet** som kopieras i steg 8. Välj alternativet **[!UICONTROL Enable Adobe Sign for attachments also]** om du vill lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Sign]-dokument som skickats för signering.

   Tryck på **[!UICONTROL Connect to Adobe Sign]**. När du uppmanas att ange autentiseringsuppgifter anger du användarnamn och lösenord för kontot som används när [!DNL Adobe Sign]-programmet skapas.

   Tryck på **[!UICONTROL Create]** för att skapa [!DNL Adobe Sign]-konfigurationen.

1. Öppna AEM webbkonsol. URL:en är `https://'[server]:[port]'/system/console/configMgr`
1. Öppna **[!UICONTROL Forms Common Configuration Service].**
1. I fältet **[!UICONTROL Allow]** **väljer du** Alla användare - Alla användare, anonyma eller inloggade, kan förhandsgranska bilagor, verifiera och signera formulär och klicka på **[!UICONTROL Save].** Författarinstansen är konfigurerad att använda  [!DNL Adobe Sign].
1. Publicera konfigurationen.
1. Använd [replikering](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) för att skapa en identisk konfiguration för motsvarande publiceringsinstanser.

Nu är [!DNL Adobe Sign] integrerat med AEM [!DNL Forms] och klart att användas i anpassningsbara formulär. Om du vill [använda Adobe Sign-tjänsten i en adaptiv form](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form) anger du den konfigurationsbehållare som skapas ovan i adaptiva formuläregenskaper.



## Konfigurera schemaläggaren för [!DNL Adobe Sign] för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Ett anpassningsbart formulär som är aktiverat för [!DNL Adobe Sign] skickas endast när alla signerare har slutfört signeringsprocessen. Som standard är schemalagda för att kontrollera (avfråga) signerarens svar efter 24 timmars intervall. [!DNL Adobe Sign] Du kan ändra standardintervallet för din miljö. Utför följande steg för att ändra standardintervallet:

1. Logga in på AEM [!DNL Forms]-server med administratörsuppgifter och navigera till **Verktyg** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   Du kan även öppna följande URL-adress i ett webbläsarfönster:
   `https://[localhost]:'port'/system/console/configMgr`

1. Leta reda på och öppna alternativet **[!UICONTROL Adobe Sign Configuration Service]**. Ange ett [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) i fältet **[!UICONTROL Status Update Scheduler Expression]** och klicka på **[!UICONTROL Save]**. Om du till exempel vill köra konfigurationstjänsten varje dag kl. 00:00 anger du `0 0 0 1/1 * ? *` i fältet **[!UICONTROL Status Update Scheduler Expression]**.

Standardintervallet för synkroniseringsstatusen [!DNL Adobe Sign] har ändrats.

## Relaterade artiklar {#related-articles}

* [Använda Adobe Sign i en adaptiv form](../../forms/using/working-with-adobe-sign.md)
* [Använda Adobe Sign med AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)


