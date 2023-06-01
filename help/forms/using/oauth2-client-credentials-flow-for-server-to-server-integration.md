---
title: Salesforce-integrering med AEM Forms med OAuth 2.0-klientautentiseringsflöde
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: Steg för att integrera Salesforce-integrering med AEM Forms med OAuth 2.0-klientens autentiseringsflöde
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
source-git-commit: f03513c98455e00beef37819a5a47ba56dfa5028
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Integrering av Salesforce med OAuth 2.0-klientautentiseringsflöde  {#configure-salesforce-with-ouath-2.0-client-credential}

För att integrera AEM Forms med Salesforce-programmet används OAuth 2.0-klientens autentiseringsflöde. Det är en standardiserad och säker metod för direkt kommunikation utan att användaren behöver göra något. I det här flödet utbyter klientprogrammet (AEM formulär) klientautentiseringsuppgifterna, som definieras i det Salesforce-anslutna programmet, för att erhålla en åtkomsttoken. De nödvändiga klientautentiseringsuppgifterna innehåller konsumentnyckeln och konsumenthemligheten.

## Fördelar med att integrera Salesforce med AEM Forms med OAuth 2.0-klientens autentiseringsflöde {#advantages-of-integrating-saleforce-aemforms}

AEM Forms stöder integreringen av Salesforce med Authorization Code Flow, utöver inloggningsflödet för OAuth 2.0-klienter. I OAuth 2.0 Authorization Code-flödet får klientprogrammet (AEM Forms) resursåtkomst för en Salesforce-användare, vilket har vissa begränsningar:

* Max fem anslutningar per användare tillåts. Ytterligare anslutningar återkallar automatiskt äldre anslutningar.
* Om en användare är inaktiverad, förlorar åtkomst eller uppdaterar ett lösenord slutar AEM att fungera.

## Förutsättningar {#prerequisites}

För att hämta och hämta data mellan Salesforce- och AEM-miljöer krävs vissa förutsättningar innan du fortsätter:

+++ **Konfigurera ett Saleforce-anslutet program med klientautentiseringsflöde och en API-användare**

Det är obligatoriskt att skapa en Salesforce-ansluten app med klientautentiseringsflödet OAuth 2.0 och en API-användare för din organisation. Detaljerade anvisningar finns i artikeln [OAuth 2.0 Client Credentials Flow for Server-to-Server Integration](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). De här stegen hjälper dig att få fram konsumentnyckeln och konsumenthemligheten.

>[!NOTE]
>
> Tänk på att konsumentnyckeln och konsumenthemligheten måste anges när du skapar en AEM datakällkonfiguration.

+++

+++ **Skapa en Swagger-fil**

Swagger är en öppen källkodsuppsättning regler, specifikationer och verktyg för att utveckla och beskriva RESTful API:er. [Skapa en swagger-fil](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) innan du integrerar Salesforce med AEM Forms.

    >[!OBS!]
    >
    > AEM 6.5 stöder endast filspecifikationer i Swagger 2.0.

+++

## Steg för att konfigurera Salesforce med flöde för klientautentiseringsuppgifter {#steps-to-create-aem-datasource-configuration}

1. Logga in på din Author-instans.
1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**.
1. Välj konfigurationsmappen.
1. Klicka **[!UICONTROL Create]** och **[!UICONTROL Create Data Source Configuration]** visas.
1. Ange **[!UICONTROL Title]** och väljer **[!UICONTROL Service Type]** as **[!UICONTROL RESTful Service]**.
1. Klicka på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Swagger Source]** as **[!UICONTROL File].**
   >[!NOTE]
   >
   > När swagger-filen har valts fylls schemat, värdnamnet och bassökvägen i automatiskt.

1. Överför den skapade swagger-filen från den lokala datorn genom att klicka på **[!UICONTROL Browse]**.
1. Välj **[!UICONTROL Authentication Type]** as **[!UICONTROL OAuth 2.0]** och **[!UICONTROL Authentication Settings]** visas.
1. Välj **[!UICONTROL Grant Type]** as **[!UICONTROL Client Credentials]**.
1. Ange **[!UICONTROL Client Id]** och **[!UICONTROL Client Secret]** som hämtats från Salesforce-appen som är ansluten.
1. Ange **[!UICONTROL Access Token URL]** i format
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Varje organisation har ett eget specifikt domännamn.

1. Klicka på **[!UICONTROL Test Connection]**.
1. Om anslutningen lyckas klickar du på **[!UICONTROL Create]** -knappen.

Nu kan du [skapa formulärdatamodellen](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) för att integrera den konfigurerade datakällan med ditt adaptiva formulär.


