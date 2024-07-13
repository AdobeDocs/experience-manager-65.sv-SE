---
title: Salesforce-integrering med AEM Forms med OAuth 2.0-klientens autentiseringsflöde
description: Steg för att integrera Salesforce-integrering med AEM Forms med OAuth 2.0-klientens autentiseringsflöde
exl-id: 4c356aa6-ebd4-40b9-89e3-bc4519e4a7c5
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 1%

---

# Integrering av Salesforce med OAuth 2.0-klientens autentiseringsflöde {#configure-salesforce-with-ouath-2.0-client-credential}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM 6.5 | Den här artikeln |

Du kan använda klientautentiseringsuppgifter för OAuth 2.0 för att integrera AEM Forms med Salesforce-programmet. OAuth 2.0-klientens autentiseringsuppgifter är en standard och säker metod för direkt kommunikation utan användarinblandning.

![Arbetsflöde vid inställning av kommunikation mellan AEM Forms och Salesforce-program](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms utbyter klientautentiseringsuppgifterna (konsumentnyckel och hemlighet), som definieras i det Salesforce-anslutna programmet, för att få en åtkomsttoken.

Det finns många fördelar med att använda OAuth 2.0-klientautentiseringsuppgifter för autentisering över autentisering av Authorization Code Flow:

* Autentisering med OAuth 2.0-klientautentiseringsuppgifter tillåter mer än fem anslutningar per användare.
* AEM datakällkonfiguration fortsätter att arbeta med inaktivering, åtkomständringar och lösenordsuppdatering för en AEM användare.

## Förutsättningar {#prerequisites}

Innan du ställer in kommunikation mellan ett Salesforce-program och en AEM-miljö:

* Skapa en [Salesforce-ansluten app med OAuth 2.0-klientautentiseringsflöde](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) och en API-användare för din organisation och hämta konsumentnyckeln och konsumenthemligheten för appen.

* Kontrollera att Swagger-filen är rätt konfigurerad för att matcha organisationens API:er. Du kan också välja att [skapa en Swagger-fil](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) från början, som är anpassad för användning i AEM.
>[!NOTE]
>
> AEM 6.5 stöder bara filspecifikationer i Swagger 2.0.

+++

## Steg för att konfigurera Salesforce med flöde för klientautentiseringsuppgifter {#steps-to-create-aem-datasource-configuration}

1. Logga in på din Author-instans.
1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**.
1. Välj konfigurationsmappen.
1. Klicka på **[!UICONTROL Create]** så visas **[!UICONTROL Create Data Source Configuration]**.
1. Ange **[!UICONTROL Title]** och välj **[!UICONTROL Service Type]** som **[!UICONTROL RESTful Service]**.
1. Klicka på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Swagger Source]** som **[!UICONTROL File].**
   >[!NOTE]
   >
   > När swagger-filen har valts fylls schemat, värdnamnet och bassökvägen i automatiskt.

1. Överför den skapade swagger-filen från den lokala datorn genom att klicka på **[!UICONTROL Browse]**.
1. Markera **[!UICONTROL Authentication Type]** som **[!UICONTROL OAuth 2.0]** så visas panelen **[!UICONTROL Authentication Settings]**.
1. Välj **[!UICONTROL Grant Type]** som **[!UICONTROL Client Credentials]**.
1. Ange **[!UICONTROL Client Id]** och **[!UICONTROL Client Secret]** som hämtats från Salesforce-appen som är ansluten.
1. Ange **[!UICONTROL Access Token URL]** i format
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Varje organisation har ett eget specifikt domännamn.

1. Klicka på **[!UICONTROL Test Connection]**.
1. Om anslutningen lyckas klickar du på knappen **[!UICONTROL Create]**.

Nu kan du [skapa formulärdatamodellen](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) för att integrera den konfigurerade datakällan med din adaptiva Forms.
