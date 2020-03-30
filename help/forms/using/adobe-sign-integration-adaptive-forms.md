---
title: Integrera Adobe Sign med AEM Forms
seo-title: Integrera Adobe Sign med AEM Forms
description: Lär dig hur du konfigurerar Adobe Sign för AEM-formulär
seo-description: Lär dig hur du konfigurerar Adobe Sign för AEM-formulär
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Integrera Adobe Sign med AEM Forms{#integrate-adobe-sign-with-aem-forms}

Adobe Sign möjliggör e-signaturarbetsflöden för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt Adobe Sign och anpassningsbara formulär fyller en användare i ett anpassat formulär som **ansöker om en tjänst**. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder Adobe Sign för att markera programmet som godkänt. Om du vill aktivera liknande arbetsflöden för elektroniska signaturer kan du integrera Adobe Sign med AEM Forms.

Om du vill använda Adobe Sign med AEM Forms konfigurerar du Adobe Sign i AEM Cloud Services:

## Förutsättningar {#prerequisites}

Du behöver följande för att integrera Adobe Sign med AEM Forms:

* Ett aktivt [Adobe Sign-utvecklarkonto.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* En [SSL-aktiverad](/help/sites-administering/ssl-by-default.md) AEM Forms-server.
* Ett [Adobe Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Autentiseringsuppgifter (klient-ID och klienthemlighet) för Adobe Sign API-programmet.

## Konfigurera Adobe Sign med AEM-formulär {#configure-adobe-sign-with-aem-forms}

När förutsättningarna är uppfyllda utför du följande steg för att konfigurera Adobe Sign med AEM Forms på författarinstansen:

1. På AEM Forms-författarinstansen går du till **Verktyg** ![](assets/hammer.png) > **Allmänt** > **Konfigurationsläsaren**.
1. Tryck på **[!UICONTROL Create]** på sidan **[!UICONTROL Configuration Browser]**.
1. I dialogrutan **[!UICONTROL Skapa konfiguration]** anger du en **[!UICONTROL titel]** för konfigurationen, aktiverar **[!UICONTROL molnkonfigurationer]** och trycker på **[!UICONTROL Skapa]**. Den skapar en konfigurationsbehållare för molntjänster.
1. Navigera till **Verktyg** ![](assets/hammer.png) > **Molntjänster** > **Adobe Sign** och välj den konfigurationsbehållare som du skapade i ovanstående steg.

   >[!NOTE]
   >
   >Kontrollera att URL:en för konfigurationssidan för molntjänster börjar med **HTTPS**. Om inte, [aktivera SSL](/help/sites-administering/ssl-by-default.md) för AEM Forms-servern.

1. På konfigurationssidan trycker du på **[!UICONTROL Skapa]** för att skapa Adobe Sign-konfigurationen i AEM Forms.
1. På fliken **[!UICONTROL Allmänt]** på sidan **[!UICONTROL Skapa Adobe Sign-konfiguration]** anger du ett **namn** för konfigurationen och trycker på **Nästa**. Du kan också ange en titel och bläddra för att välja en miniatyrbild för konfigurationen.

   Kopiera URL-adressen i det aktuella webbläsarfönstret. Du måste konfigurera Adobe Sign-programmet med AEM Forms.

1. Konfigurera OAuth-inställningar för Adobe Sign-programmet:

   1. Öppna ett webbläsarfönster och logga in på utvecklarkontot för Adobe Sign.
   1. Välj det program som konfigurerats för AEM Forms och tryck på Configure OAuth for Application.
   1. I rutan **Omdirigerings-URL** lägger du till HTTPS-URL:en som kopierades i föregående steg och klickar på **Spara**.
   1. Aktivera följande OAuth-inställningar för Adobe Sign-programmet och klicka på **Spara**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read
   Stegvis information om hur du konfigurerar OAuth-inställningar för ett Adobe Sign-program och hämtar nycklarna finns i [Konfigurera autentiseringsinställningar för programutvecklardokumentationen](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobeio/adobeio-documentation/master/sign/gstarted/configure_oauth.md) .

   ![OAuth-konfiguration](assets/oauthconfig_new.png)

1. Gå tillbaka till sidan **Skapa Adobe Sign-konfiguration** . På fliken **[!UICONTROL Inställningar]** anger fältet **[!UICONTROL OAuth URL]** följande standard-URL:

   https://secure.na1.echosign.com/public/oauth

   där:

   **na1** refererar till standarddatabasdelningen.

   Du kan ändra värdet för databasdelningen. Starta om servern för att kunna använda det nya värdet för databasdelningen.

1. Ange **klient-ID** (kallas även program-ID) och **klienthemlighet**. Markera alternativet **Aktivera Adobe Sign för bifogade filer även** för att bifoga filer som är kopplade till ett anpassat formulär till motsvarande Adobe Sign-dokument som skickats för signering.

   Tryck på **[!UICONTROL Anslut till Adobe Sign]**. När du uppmanas att ange inloggningsuppgifter anger du användarnamn och lösenord för kontot som används när Adobe Sign-programmet skapas.

   Tryck på **[!UICONTROL Skapa]** för att skapa Adobe Sign-konfigurationen.

1. Öppna AEM Web Console. URL:en är `https://'[server]:[port]'/system/console/configMgr`
1. Öppna **Forms Common Configuration Service.**
1. I fältet **Tillåt** **väljer** du Alla användare - Alla användare, anonyma eller inloggade, kan förhandsgranska bilagor, verifiera och signera formulär och klicka på **Spara.** Författarinstansen är konfigurerad att använda Adobe Sign.
1. Logga in på [Publish](/help/sites-deploying/deploy.md) -instansen och öppna följande URL:

   `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`

1. Upprepa steg 1 till 12 för att konfigurera Adobe Sign med AEM Forms. Använd samma rubrik för konfigurationen (som anges i steg 3) och samma namn (som anges i steg 6) för att replikera inställningarna som konfigurerats på författarinstansen.

   Nu är Adobe Sign integrerat med AEM Forms och klart att användas i anpassningsbara formulär. Om du vill [använda Adobe Sign-tjänsten i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)anger du den konfigurationsbehållare som skapas ovan i anpassningsbara formuläregenskaper.

## Konfigurera Adobe Sign-schemaläggaren för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Ett anpassat formulär aktiverat för Adobe Sign skickas endast när alla signerare har slutfört signeringsprocessen. Som standard är Adobe Signs schemaläggningstjänster schemalagda att kontrollera (avfråga) signerarens svar efter 24 timmars intervall. Du kan ändra standardintervallet för din miljö. Utför följande steg för att ändra standardintervallet:

1. Logga in på AEM Forms-servern med administratörsuppgifter och gå till **Verktyg** > **Åtgärder** > **Webbkonsol**.

   Du kan även öppna följande URL-adress i ett webbläsarfönster:
   `https://[localhost]:'port'/system/console/configMgr`

1. Leta reda på och öppna **konfigurationstjänsten** för Adobe Sign. Ange ett [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) i fältet **Status Update Scheduler Expression** och klicka på **Save**. Om du till exempel vill köra konfigurationstjänsten varje dag klockan 00:00 anger du `0 0 0 1/1 * ? *` i fältet **Status Update Scheduler Expression** .

Standardintervallet för synkroniseringsstatus för Adobe Sign har ändrats.

## Relaterade artiklar {#related-articles}

* [Använda Adobe Sign i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md)
* [Använda Adobe Sign med AEM-formulär (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

