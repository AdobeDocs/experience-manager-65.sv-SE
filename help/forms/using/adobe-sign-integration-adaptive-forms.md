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
source-git-commit: f0038c1f88ea0047cbaae4fe49456a665aa67f10
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---


# Integrera Adobe Sign med AEM Forms{#integrate-adobe-sign-with-aem-forms}

Adobe Sign möjliggör e-signaturarbetsflöden för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt Adobe Sign-scenario och ett scenario med adaptiva formulär fyller en användare i ett adaptivt formulär och **ansöker om en tjänst**. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder Adobe Sign för att markera det som godkänt. För att möjliggöra liknande arbetsflöden för elektroniska signaturer kan du integrera Adobe Sign med AEM Forms.

Konfigurera Adobe Sign i AEM Cloud Services om du vill använda Adobe Sign med AEM Forms:

## Förutsättningar {#prerequisites}

Du behöver följande för att kunna integrera Adobe Sign med AEM Forms:

* Ett aktivt [Adobe Sign-utvecklarkonto.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* En [SSL-aktiverad](/help/sites-administering/ssl-by-default.md) AEM Forms-server.
* Ett [Adobe Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Autentiseringsuppgifter (klient-ID och klienthemlighet) för Adobe Sign API-program.
* När du konfigurerar om tar du bort den befintliga Adobe Sign-konfigurationen från både författare- och publiceringsinstanser.
* Använd [identisk krypteringsnyckel](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) för författare och publiceringsinstanser.

## Konfigurera Adobe Sign med AEM Forms {#configure-adobe-sign-with-aem-forms}

När förutsättningarna är uppfyllda utför du följande steg för att konfigurera Adobe Sign med AEM Forms på Author-instansen:

1. I AEM Forms-författarinstansen går du till **Tools** ![hammer](assets/hammer.png) > **General** > **Configuration Browser**.
1. On the **[!UICONTROL Configuration Browser]** page, tap **[!UICONTROL Create]**.
   * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
1. I **[!UICONTROL Create Configuration]** dialogrutan anger du en **[!UICONTROL Title]** för konfigurationen, aktiverar **[!UICONTROL Cloud Configurations]** och trycker på **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för molntjänster.
1. Navigera till **Verktyg** ![hammare](assets/hammer.png) > **Cloud Services** > **Adobe Sign** och markera den konfigurationsbehållare som du skapade i steget ovan.

   >[!NOTE]
   >
   >Du kan antingen utföra steg 1-4 för att skapa en ny konfigurationsbehållare och skapa en Adobe Sign-konfiguration i behållaren eller använda den befintliga `global` mappen i **Verktyg** ![hammare](assets/hammer.png) > **Cloud Services** > **Adobe Sign**. Om du skapar konfigurationen i den nya konfigurationsbehållaren måste du ange behållarnamnet i **[!UICONTROL Configuration Container]** fältet när du skapar ett anpassat formulär.

   >[!NOTE]
   Kontrollera att URL:en för konfigurationssidan för molntjänster börjar med **HTTPS**. Om inte, [aktivera SSL](/help/sites-administering/ssl-by-default.md) för AEM Forms-servern.

1. På konfigurationssidan trycker du på **[!UICONTROL Create]** för att skapa en Adobe Sign-konfiguration i AEM Forms.
1. Ange ett **[!UICONTROL General]** namn **[!UICONTROL Create Adobe Sign Configuration]** för konfigurationen på **fliken** och tryck sedan på **Nästa**. Du kan också ange en titel och bläddra för att välja en miniatyrbild för konfigurationen.

1. Kopiera URL-adressen i det aktuella webbläsarfönstret till en anteckningsruta. Du måste konfigurera Adobe Sign-programmet med AEM Forms.

1. Konfigurera OAuth-inställningar för Adobe Sign-programmet:

   1. Öppna ett webbläsarfönster och logga in på Adobe Sign utvecklarkonto.
   1. Markera programmet som konfigurerats för AEM Forms och tryck på Konfigurera OAuth för program.
   1. I rutan **Omdirigerings-URL** lägger du till HTTPS-URL:en som kopierades i föregående steg och klickar på **Spara**.
   1. Aktivera följande OAuth-inställningar för Adobe Sign-programmet och klicka på **Spara**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Stegvis information om hur du konfigurerar OAuth-inställningar för ett Adobe Sign-program och hämtar nycklarna finns i [Konfigurera autentiseringsinställningar för programutvecklardokumentationen](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) .

   ![OAuth-konfiguration](assets/oauthconfig_new.png)

1. Gå tillbaka till sidan **Skapa Adobe Sign-konfiguration** . På **[!UICONTROL Settings]** fliken anges följande standard-URL i **[!UICONTROL OAuth URL]** fältet:

   https://secure.na1.echosign.com/public/oauth

   där:

   **na1** refererar till standarddatabasdelningen.

   Du kan ändra värdet för databasdelningen. Starta om servern för att kunna använda det nya värdet för databasdelningen.

1. Ange **klient-ID** (kallas även program-ID) och **klienthemlighet**. Markera alternativet **Aktivera Adobe Sign för bilagor också** om du vill lägga till filer som är kopplade till ett adaptivt formulär i motsvarande Adobe Sign-dokument som skickas för signering.

   Tryck på **[!UICONTROL Connect to Adobe Sign]**. Ange användarnamn och lösenord för kontot som används när Adobe Sign-programmet skapas när du uppmanas att ange inloggningsuppgifter.

   Tryck **[!UICONTROL Create]** för att skapa Adobe Sign-konfigurationen.

1. Öppna AEM webbkonsol. URL:en är `https://'[server]:[port]'/system/console/configMgr`
1. Öppna **Forms Common Configuration Service.**
1. I fältet **Tillåt** **väljer** du Alla användare - Alla användare, anonyma eller inloggade, kan förhandsgranska bilagor, verifiera och signera formulär och klicka på **Spara.** Författarinstansen är konfigurerad att använda Adobe Sign.
1. Publicera konfigurationen.
1. Använd [replikering](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) för att skapa en identisk konfiguration för motsvarande publiceringsinstanser.

Nu är Adobe Sign integrerat med AEM Forms och klart att användas i anpassningsbara formulär. Om du vill [använda Adobe Sign-tjänsten i ett adaptivt formulär](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)anger du den konfigurationsbehållare som skapas ovan i adaptiva formuläregenskaper.



## Konfigurera Adobe Sign-schemaläggaren för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Ett anpassat formulär som har aktiverats av Adobe Sign skickas endast när alla signerare har slutfört signeringsprocessen. Som standard är Adobe Sign Scheduler-tjänster schemalagda att kontrollera (avfråga) signerarens svar efter 24 timmars intervall. Du kan ändra standardintervallet för din miljö. Utför följande steg för att ändra standardintervallet:

1. Logga in på AEM Forms-servern med administratörsuppgifter och gå till **Verktyg** > **Åtgärder** > **Webbkonsol**.

   Du kan även öppna följande URL-adress i ett webbläsarfönster:
   `https://[localhost]:'port'/system/console/configMgr`

1. Leta upp och öppna alternativet **Adobe Sign Configuration Service** . Ange ett [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) i fältet **Status Update Scheduler Expression** och klicka på **Save**. Om du till exempel vill köra konfigurationstjänsten varje dag klockan 00:00 anger du `0 0 0 1/1 * ? *` i fältet **Status Update Scheduler Expression** .

Standardintervallet för synkroniseringsstatus för Adobe Sign har ändrats.

## Relaterade artiklar {#related-articles}

* [Använda Adobe Sign i en adaptiv form](../../forms/using/working-with-adobe-sign.md)
* [Använda Adobe Sign med AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

