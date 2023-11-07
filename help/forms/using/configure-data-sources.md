---
title: Konfigurera datakällor
description: Lär dig hur du konfigurerar olika typer av datakällor så att du kan skapa formulärdatamodeller.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 0%

---

# Konfigurera datakällor{#configure-data-sources}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html) |
| AEM 6.5 | Den här artikeln |


![Dataintegrering](do-not-localize/data-integeration.png)

Med AEM Forms dataintegrering kan du konfigurera och ansluta till olika datakällor. Följande typer stöds inte. Men med liten anpassning kan ni också integrera andra datakällor.

* Relationsdatabaser - MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS och Sybase
* AEM användarprofil
* RESTful web services
* SOAP-baserade webbtjänster
* OData-tjänster

Dataintegrering stöder OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), grundläggande autentisering och API-nyckelautentiseringstyper är körklara och tillåter implementering av anpassad autentisering för åtkomst till webbtjänster. Medan RESTful-, SOAP-baserade och OData-tjänster konfigureras i AEM Cloud Service, konfigureras JDBC för relationsdatabaser och koppling för AEM användarprofil i AEM webbkonsol.

## Konfigurera relationsdatabas {#configure-relational-database}

Du kan konfigurera relationsdatabaser med hjälp AEM Konfiguration av webbkonsol. Gör följande:

1. Gå till AEM webbkonsol på `https://server:host/system/console/configMgr`.
1. Leta efter **[!UICONTROL Apache Sling Connection Pooled DataSource]** konfiguration. Tryck för att öppna konfigurationen i redigeringsläge.
1. I konfigurationsdialogrutan anger du information för den databas som du vill konfigurera, till exempel:

   * Datakällans namn
   * Egenskapen för datakälltjänst som lagrar datakällans namn
   * Java-klassnamn för JDBC-drivrutinen
   * URI för JDBC-anslutning
   * Användarnamn och lösenord för anslutning till JDBC-drivrutinen

   >[!NOTE]
   >
   >Kontrollera att du krypterar känslig information, t.ex. lösenord, innan du konfigurerar datakällan. Kryptera:
   >
   > 1. Gå till https://&#39;[server]:[port]/system/console/crypto.
   > 1. I **[!UICONTROL Plain Text]** anger du lösenordet eller en sträng som ska krypteras och trycker på **[!UICONTROL Protect]**.
   >
   >Den krypterade texten visas i fältet Skyddad text som du kan ange i konfigurationen.

1. Aktivera **[!UICONTROL Test on Borrow]** eller **[!UICONTROL Test on Return]** för att ange att objekten valideras innan de lånas eller returneras från respektive till poolen.
1. Ange en SQL SELECT-fråga i **[!UICONTROL Validation Query]** fält för att validera anslutningar från poolen. Frågan måste returnera minst en rad. Baserat på din databas anger du något av följande:

   * SELECT 1 (MySQL och MS SQL)
   * VÄLJ 1 från dubbla (Oracle)

1. Tryck **[!UICONTROL Save]** för att spara konfigurationen.

   >[!NOTE]
   >
   > Om din Forms datamodell innehåller ett objekt som är ett reserverat nyckelord för relationsdatabasen kan det leda till problem med tillägg, uppdatering eller hämtning av data. Undvik därför att använda sådana objekt i formulärdatamodellen.

## Konfigurera AEM användarprofil {#configure-aem-user-profile}

Du kan konfigurera AEM användarprofil med hjälp av konfigurationen för anslutning av användarprofil i AEM webbkonsol. Gör följande:

1. Gå till AEM webbkonsol på https://&#39;[server]:[port]system/console/configMgr.
1. Leta efter **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** och tryck för att öppna konfigurationen i redigeringsläge.
1. I dialogrutan Konfiguration av anslutning till användarprofil kan du lägga till, ta bort eller uppdatera egenskaper för användarprofiler. De angivna egenskaperna är tillgängliga för användning i formulärdatamodellen. Använd följande format för att ange egenskaper för användarprofiler:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exempel:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** i ovanstående exempel betecknar alla noder under `profile/empLocation/` i AEM användarprofil i CRXDE-struktur. Det innebär att formulärdatamodellen har åtkomst till `city` type-egenskap `string` finns i en nod under `profile/empLocation/` nod. Noderna som innehåller den angivna egenskapen måste dock följa en konsekvent struktur.

1. Tryck **[!UICONTROL Save]** för att spara konfigurationen.

## Konfigurera mapp för molntjänstkonfigurationer {#cloud-folder}

>[!NOTE]
>
>Konfiguration för molntjänstmappen krävs för konfigurering av molntjänster för RESTful-, SOAP- och OData-tjänster.

Alla konfigurationer av molntjänster i AEM konsolideras i `/conf` AEM i databasen. Som standard är `conf` mappen innehåller `global` mapp där du kan skapa molntjänstkonfigurationer. Du måste dock manuellt aktivera den för molnkonfigurationer. Du kan även skapa ytterligare mappar i `conf` för att skapa och organisera molntjänstkonfigurationer.

Så här konfigurerar du mappen för molntjänstkonfigurationer:

1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   * Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.
1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

   1. I **[!UICONTROL Configuration Browser]** väljer du `global` mapp och tryck **[!UICONTROL Properties]**.

   1. I **[!UICONTROL Configuration Properties]** dialogruta, aktivera **[!UICONTROL Cloud Configurations]**.

   1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

1. I **[!UICONTROL Configuration Browser]**, trycka **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Configuration]** dialogruta, ange en rubrik för mappen och aktivera **[!UICONTROL Cloud Configurations]**.
1. Tryck **[!UICONTROL Create]** för att skapa en mapp som är aktiverad för molntjänstkonfigurationer.

## Konfigurera RESTful-webbtjänster {#configure-restful-web-services}

RESTful-webbtjänsten kan beskrivas med [Swagger-specifikationer](https://swagger.io/specification/) i JSON- eller YAML-format i en Swagger-definitionsfil. Om du vill konfigurera RESTful-webbtjänsten i AEM molntjänster måste du se till att du antingen har Swagger-filen i filsystemet eller URL:en där filen finns.

Gör följande för att konfigurera RESTful-tjänster:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](../../forms/using/configure-data-sources.md#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj URL eller Fil i listrutan Växlingskälla och ange därför SWAGGER-URL:en till Swagger-definitionsfilen eller överför Swagger-filen från det lokala filsystemet.
   * Baserat på indata från Swagger Source fylls följande fält i med värden:

      * Schema: De överföringsprotokoll som används av REST API. Antalet schematyper som visas i listrutan beror på scheman som definieras i Swagger-källan.
      * Värd: Domännamnet eller IP-adressen för värden som använder REST API. Det är ett obligatoriskt fält.
      * Bassökväg: URL-prefixet för alla API-sökvägar. Det är ett valfritt fält.\
        Om det behövs kan du redigera de förifyllda värdena för dessa fält.

   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, API Key, Custom Authentication eller Mutual Authentication - för att få åtkomst till RESTful-tjänsten och ange därmed information för autentisering.

   Om du väljer **[!UICONTROL API Key]** Ange värdet för API-nyckeln som autentiseringstyp. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj ett av dessa alternativ på menyn **[!UICONTROL Location]** nedrullningsbar lista och ange namnet på huvudet eller frågeparametern i **[!UICONTROL Parameter Name]** efter behov.

   Om du väljer **[!UICONTROL Mutual Authentication]** som autentiseringstyp, se [Certifikatbaserad ömsesidig autentisering för RESTful- och SOAP-webbtjänster](#mutual-authentication).

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för RESTful-tjänsten.

### HTTP-klientkonfiguration för formulärdatamodell för optimering av prestanda {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] formulärdatamodell vid integrering med RESTful-webbtjänster som datakälla inkluderar HTTP-klientkonfigurationer för prestandaoptimering.
Utför följande steg för att konfigurera HTTP-klientmodellen för formulärdata:

1. Logga in på [!DNL Experience Manager Forms] Skapa instans som administratör och gå till [!DNL Experience Manager] webbkonsolpaket. Standardwebbadressen är [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Tryck på **[!UICONTROL Form Data Model Http Client Configuration for REST data source]**.

1. I [!UICONTROL Form Data Model Http Client Configuration for REST data source] dialog:

   * Ange maximalt antal tillåtna anslutningar mellan formulärdatamodellen och RESTful-webbtjänster i dialogrutan **[!UICONTROL Connection limit in total]** fält. Standardvärdet är 20 anslutningar.

   * Ange maximalt antal tillåtna anslutningar för varje flöde i dialogrutan **[!UICONTROL Connection limit on per route basis]** fält. Standardvärdet är 2 anslutningar.

   * Ange hur länge en beständig HTTP-anslutning ska vara aktiv i **[!UICONTROL Keep alive]** fält. Standardvärdet är 15 sekunder.

   * Ange varaktigheten som [!DNL Experience Manager Forms] servern väntar på att en anslutning ska upprättas i **[!UICONTROL Connection timeout]** fält. Standardvärdet är 10 sekunder.

   * Ange den maximala tidsperioden för inaktivitet mellan två datapaket i **[!UICONTROL Socket timeout]** fält. Standardvärdet är 30 sekunder.

## Konfigurera SOAP-webbtjänster {#configure-soap-web-services}

SOAP-baserade webbtjänster beskrivs med [WSDL-specifikationer (Web Services Description Language)](https://www.w3.org/TR/wsdl). Om du vill konfigurera en SOAP-baserad webbtjänst i AEM molntjänster kontrollerar du att du har WSDL-webbadressen för webbtjänsten och gör följande:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](../../forms/using/configure-data-sources.md#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL SOAP Web Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande för SOAP-webbtjänsten:

   * WSDL-URL för webbtjänsten.
   * Tjänstslutpunkt. Ange ett värde i det här fältet om du vill åsidosätta tjänstslutpunkten som anges i WSDL.
   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, Custom Authentication, X509 Token eller Mutual Authentication - för att få åtkomst till SOAP-tjänsten och ange därefter information för autentisering.

     Om du väljer **[!UICONTROL X509 Token]** som autentiseringstyp, konfigurera X509-certifikatet. Mer information finns i [Konfigurera certifikat](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Ange KeyStore-alias för X509-certifikatet i **[!UICONTROL Key Alias]** fält. Ange tiden i sekunder tills autentiseringsbegäran är giltig i **[!UICONTROL Time To Live]** fält. Du kan också välja att signera meddelandetexten eller tidsstämpelhuvudet eller båda.

     Om du väljer **[!UICONTROL Mutual Authentication]** som autentiseringstyp, se [Certifikatbaserad ömsesidig autentisering för RESTful- och SOAP-webbtjänster](#mutual-authentication).

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för SOAP-webbtjänsten.

## Konfigurera OData-tjänster {#config-odata}

En OData-tjänst identifieras av tjänstens rot-URL. Om du vill konfigurera en OData-tjänst i AEM molntjänster kontrollerar du att du har tjänstens rot-URL och gör följande:

>[!NOTE]
>
>Formulärdatamodellen stöder [OData version 4](https://www.odata.org/documentation/).
>Stegvisa anvisningar om hur du konfigurerar Microsoft Dynamics 365, online eller lokalt, finns i [Konfiguration av Microsoft Dynamics OData](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](../../forms/using/configure-data-sources.md#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för OData-tjänsten:

   * Tjänstens rot-URL för OData-tjänsten som ska konfigureras.
   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication eller Custom Authentication - för att få åtkomst till OData-tjänsten, och därmed ange autentiseringsinformationen.

   >[!NOTE]
   >
   >Du måste välja autentiseringstypen OAuth 2.0 om du vill ansluta till Microsoft Dynamics-tjänster med OData-slutpunkten som tjänstrot.

1. Tryck **Skapa** för att skapa molnkonfigurationen för OData-tjänsten.

## Certifikatbaserad ömsesidig autentisering för RESTful- och SOAP-webbtjänster {#mutual-authentication}

När du aktiverar ömsesidig autentisering för formulärdatamodell autentiserar både datakällan och AEM Server som kör formulärdatamodellen varandras identitet innan data delas. Du kan använda ömsesidig autentisering för REST- och SOAP-baserade anslutningar (datakällor). Så här konfigurerar du ömsesidig autentisering för en formulärdatamodell i din AEM Forms-miljö:

1. Överför den privata nyckeln (certifikatet) till [!DNL AEM Forms] server. Så här överför du den privata nyckeln:
   1. Logga in på [!DNL AEM Forms] server som administratör.
   1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Välj `fd-cloudservice` användare och knacka **[!UICONTROL Properties]**.
   1. Öppna **[!UICONTROL Keystore]** -fliken, expandera **[!UICONTROL Add Private Key from KeyStore file]** , ladda upp KeyStore-filen, ange alias, lösenord och tryck **[!UICONTROL Submit]**. Certifikatet överförs.  Aliaset för den privata nyckeln anges i certifikatet och anges när certifikatet skapas.
1. Överför förtroendecertifikat till Global Trust Store. Så här överför du certifikatet:
   1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expandera **[!UICONTROL Add Certificate from CER file]** alternativ, tryck **[!UICONTROL Select Certificate File]**, ladda upp certifikatet och tryck på **[!UICONTROL Submit]**.
1. Konfigurera [SOAP](#configure-soap-web-services) eller [RESTful](#configure-restful-web-services) webbtjänster som datakälla och välj **[!UICONTROL Mutual authentication]** som autentiseringstyp. Om du konfigurerar flera självsignerade certifikat för `fd-cloudservice` anger du namnet på certifikatets nyckelalias.

## Nästa steg {#next-steps}

Du har konfigurerat datakällorna. Därefter kan du skapa en formulärdatamodell eller, om du redan har skapat en formulärdatamodell utan en datakälla, associera den med de datakällor du konfigurerade. Se [Skapa formulärdatamodell](/help/forms/using/create-form-data-models.md) för mer information.
