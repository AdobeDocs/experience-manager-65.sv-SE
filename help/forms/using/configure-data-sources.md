---
title: Konfigurera datakällor
seo-title: Konfigurera datakällor
description: Lär dig hur du konfigurerar olika typer av datakällor och använder dem för att skapa formulärdatamodeller.
seo-description: Lär dig hur du konfigurerar olika typer av datakällor och använder dem för att skapa formulärdatamodeller.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---


# Konfigurera datakällor{#configure-data-sources}

![](do-not-localize/data-integeration.png)

Med AEM Forms dataintegrering kan du konfigurera och ansluta till olika datakällor. Följande typer stöds inte. Men med liten anpassning kan ni också integrera andra datakällor.

* Relationsdatabaser - MySQL, Microsoft SQL Server, IBM DB2 och Oracle RDBMS
* AEM användarprofil
* RESTful web services
* SOAP-baserade webbtjänster
* OData-tjänster

Dataintegrering har stöd för autentiseringstyperna OAuth2.0, Grundläggande autentisering och API Key som är färdiga och tillåter implementering av anpassad autentisering för åtkomst till webbtjänster. Medan RESTful-, SOAP-baserade och OData-tjänster är konfigurerade i AEM Cloud Services, konfigureras JDBC för relationsdatabaser och koppling för AEM användarprofil i AEM webbkonsol.

## Konfigurera relationsdatabas {#configure-relational-database}

Du kan konfigurera relationsdatabaser med hjälp AEM Konfiguration av webbkonsol. Gör följande:

1. Gå till AEM webbkonsol på https://server:host/system/console/configMgr.
1. Leta efter **[!UICONTROL Apache Sling Connection Pooled DataSource]**-konfiguration. Tryck för att öppna konfigurationen i redigeringsläge.
1. I konfigurationsdialogrutan anger du information för den databas som du vill konfigurera, till exempel:

   * Datakällans namn
   * Egenskapen för datakälltjänst som lagrar datakällans namn
   * Java-klassnamn för JDBC-drivrutinen
   * URI för JDBC-anslutning
   * Användarnamn och lösenord för anslutning till JDBC-drivrutinen

   >[!NOTE]
   >
   >Kontrollera att du krypterar känslig information, t.ex. lösenord, innan du konfigurerar datakällan. Så här krypterar du:
   >
   >    
   >    
   >    1. Gå till https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. I fältet **[!UICONTROL Plain Text]** anger du lösenordet eller en sträng som ska krypteras och trycker på **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >Den krypterade texten visas i fältet Skyddad text som du kan ange i konfigurationen.

1. Aktivera **[!UICONTROL Test on Borrow]** eller **[!UICONTROL Test on Return]** för att ange att objekten valideras innan de lånas eller returneras från respektive till poolen.
1. Ange en SELECT-fråga (SQL) i fältet **[!UICONTROL Validation Query]** om du vill validera anslutningar från poolen. Frågan måste returnera minst en rad. Baserat på din databas anger du något av följande:

   * SELECT 1 (MySQL och MS SQL)
   * SELECT 1 from dual (Oracle)

1. Tryck på **[!UICONTROL Save]** för att spara konfigurationen.

## Konfigurera AEM användarprofil {#configure-aem-user-profile}

Du kan konfigurera AEM användarprofil med hjälp av konfigurationen för anslutning av användarprofil i AEM webbkonsol. Gör följande:

1. Gå till AEM webbkonsol på https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Leta efter **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** och tryck för att öppna konfigurationen i redigeringsläge.
1. I dialogrutan Konfiguration av anslutning till användarprofil kan du lägga till, ta bort eller uppdatera egenskaper för användarprofiler. De angivna egenskaperna kommer att vara tillgängliga för användning i formulärdatamodellen. Använd följande format för att ange egenskaper för användarprofiler:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exempel:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >***** i ovanstående exempel betecknar alla noder under noden `profile/empLocation/` i AEM användarprofil i CRXDE-strukturen. Det betyder att formulärdatamodellen har åtkomst till egenskapen `city` av typen `string` i alla noder under noden `profile/empLocation/`. Noderna som innehåller den angivna egenskapen måste dock följa en konsekvent struktur.

1. Tryck på **[!UICONTROL Save]** för att spara konfigurationen.

## Konfigurera mapp för molntjänstkonfigurationer {#cloud-folder}

>[!NOTE]
Konfiguration för molntjänstmappen krävs för konfigurering av molntjänster för RESTful-, SOAP- och OData-tjänster.

Alla konfigurationer av molntjänster i AEM konsolideras i mappen `/conf` i AEM. Mappen `conf` innehåller som standard mappen `global` där du kan skapa molntjänstkonfigurationer. Du måste dock manuellt aktivera det för molnkonfigurationer. Du kan också skapa ytterligare mappar i `conf` för att skapa och organisera molntjänstkonfigurationer.

Så här konfigurerar du mappen för molntjänstkonfigurationer:

1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   * Mer information finns i [Configuration Browser](/help/sites-administering/configurations.md)-dokumentationen.
1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

   1. I **[!UICONTROL Configuration Browser]** markerar du mappen `global` och trycker på **[!UICONTROL Properties]**.

   1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan **[!UICONTROL Configuration Properties]**.

   1. Tryck på **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

1. Tryck på **[!UICONTROL Create]** i **[!UICONTROL Configuration Browser]**.
1. I dialogrutan **[!UICONTROL Create Configuration]** anger du en rubrik för mappen och aktiverar **[!UICONTROL Cloud Configurations]**.
1. Tryck på **[!UICONTROL Create]** för att skapa mappen som är aktiverad för molntjänstkonfigurationer.

## Konfigurera RESTful-webbtjänster {#configure-restful-web-services}

RESTful-webbtjänsten kan beskrivas med [Swagger-specifikationer](https://swagger.io/specification/) i JSON- eller YAML-format i en Swagger-definitionsfil. Om du vill konfigurera RESTful-webbtjänsten i AEM-molntjänster måste du ha antingen Swagger-filen i filsystemet eller URL:en där filen finns.

Gör följande för att konfigurera RESTful-tjänster:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](../../forms/using/configure-data-sources.md#cloud-folder).

1. Tryck på **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och tryck på **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj URL eller Fil i listrutan Växlingskälla och ange därför SWAGGER-URL:en till Swagger-definitionsfilen eller överför Swagger-filen från det lokala filsystemet.
   * Baserat på indata från Swagger Source fylls följande fält i med värden:

      * Schema: De överföringsprotokoll som används av REST API. Antalet schematyper som visas i listrutan beror på scheman som definieras i Swagger-källan.
      * Värd: Domännamnet eller IP-adressen för värden som använder REST API. Det är ett obligatoriskt fält.
      * Grundsökväg: URL-prefixet för alla API-sökvägar. Det är ett valfritt fält.\
         Om det behövs kan du redigera de förifyllda värdena för dessa fält.
   * Välj autentiseringstyp - Ingen, OAuth2.0, Grundläggande autentisering, API-nyckel, Anpassad autentisering eller Ömsesidig autentisering - för att få åtkomst till RESTful-tjänsten och ange information för autentisering.

   Om du väljer **[!UICONTROL API Key]** som autentiseringstyp anger du värdet för API-nyckeln. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj något av dessa alternativ i listrutan **[!UICONTROL Location]** och ange namnet på huvudet eller frågeparametern i fältet **[!UICONTROL Parameter Name]**.

   Om du väljer **[!UICONTROL Mutual Authentication]** som autentiseringstyp, se [Certifikatbaserad ömsesidig autentisering för RESTful- och SOAP-webbtjänster](#mutual-authentication).

1. Tryck på **[!UICONTROL Create]** för att skapa molnkonfigurationen för RESTful-tjänsten.

## Konfigurera SOAP-webbtjänster {#configure-soap-web-services}

SOAP-baserade webbtjänster beskrivs med [WSDL-specifikationer](https://www.w3.org/TR/wsdl) (Web Services Description Language). Om du vill konfigurera en SOAP-baserad webbtjänst i AEM-molntjänster kontrollerar du att du har WSDL-webbadressen för webbtjänsten och gör följande:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](../../forms/using/configure-data-sources.md#cloud-folder).

1. Tryck på **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL SOAP Web Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och tryck på **[!UICONTROL Next]**.
1. Ange följande för SOAP-webbtjänsten:

   * WSDL-URL för webbtjänsten.
   * Tjänstslutpunkt. Ange ett värde i det här fältet om du vill åsidosätta tjänstslutpunkten som anges i WSDL.
   * Välj autentiseringstypen - Ingen, OAuth2.0, Grundläggande autentisering, Anpassad autentisering, X509-token eller Ömsesidig autentisering - för att få åtkomst till SOAP-tjänsten och ange därför informationen för autentisering.

      Om du väljer **[!UICONTROL X509 Token]** som autentiseringstyp konfigurerar du X509-certifikatet. Mer information finns i [Konfigurera certifikat](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Ange KeyStore-alias för X509-certifikatet i fältet **[!UICONTROL Key Alias]**. Ange tiden i sekunder tills autentiseringsbegäran är giltig i fältet **[!UICONTROL Time To Live]**. Du kan också välja att signera meddelandetexten eller tidsstämpelhuvudet eller båda.

      Om du väljer **[!UICONTROL Mutual Authentication]** som autentiseringstyp, se [Certifikatbaserad ömsesidig autentisering för RESTful- och SOAP-webbtjänster](#mutual-authentication).

1. Tryck på **[!UICONTROL Create]** för att skapa molnkonfigurationen för SOAP-webbtjänsten.

## Konfigurera OData-tjänster {#config-odata}

En OData-tjänst identifieras av tjänstens rot-URL. Om du vill konfigurera en OData-tjänst i AEM-molntjänster kontrollerar du att du har tjänstens rot-URL och gör följande:

>[!NOTE]
Stegvisa anvisningar om hur du konfigurerar Microsoft Dynamics 365, online eller lokalt, finns i [Microsoft Dynamics OData Configuration](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](../../forms/using/configure-data-sources.md#cloud-folder).

1. Tryck på **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och tryck på **[!UICONTROL Next]**.
1. Ange följande information för OData-tjänsten:

   * Tjänstens rot-URL för OData-tjänsten som ska konfigureras.
   * Välj autentiseringstyp - Ingen, OAuth2.0, Grundläggande autentisering eller Anpassad autentisering - för att få åtkomst till OData-tjänsten och ange därefter information för autentisering.

   >[!NOTE]
   Du måste välja autentiseringstypen OAuth 2.0 om du vill ansluta till Microsoft Dynamics-tjänster med OData-slutpunkten som tjänstrot.

1. Tryck på **Create** för att skapa molnkonfigurationen för OData-tjänsten.

## Certifikatbaserad ömsesidig autentisering för RESTful- och SOAP-webbtjänster {#mutual-authentication}

När du aktiverar ömsesidig autentisering för formulärdatamodell autentiserar både datakällan och AEM Server som kör formulärdatamodellen varandras identitet innan data delas. Du kan använda ömsesidig autentisering för REST- och SOAP-baserade anslutningar (datakällor). Så här konfigurerar du ömsesidig autentisering för en formulärdatamodell i din AEM Forms-miljö:

1. Överför den privata nyckeln (certifikatet) till [!DNL AEM Forms]-servern. Så här överför du den privata nyckeln:
   1. Logga in på din [!DNL AEM Forms]-server som administratör.
   1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Markera `fd-cloudservice`-användaren och tryck på **[!UICONTROL Properties]**.
   1. Öppna fliken **[!UICONTROL Keystore]**, utöka alternativet **[!UICONTROL Add Private Key from KeyStore file]**, ladda upp KeyStore-filen, ange alias, lösenord och tryck på **[!UICONTROL Submit]**. Certifikatet överförs.  Aliaset för den privata nyckeln anges i certifikatet och anges när certifikatet skapas.
1. Överför förtroendecertifikat till Global Trust Store. Så här överför du certifikatet:
   1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expandera alternativet **[!UICONTROL Add Certificate from CER file]**, tryck på **[!UICONTROL Select Certificate File]**, överför certifikatet och tryck på **[!UICONTROL Submit]**.
1. Konfigurera [SOAP](#configure-soap-web-services) eller [RESTful](#configure-restful-web-services)-webbtjänster som datakälla och välj **[!UICONTROL Mutual authentication]** som autentiseringstyp. Om du konfigurerar flera självsignerade certifikat för `fd-cloudservice`-användare anger du namnet på certifikatets nyckelalias.

## Nästa steg {#next-steps}

Du har konfigurerat datakällorna. Därefter kan du skapa en formulärdatamodell eller, om du redan har skapat en formulärdatamodell utan en datakälla, associera den med de datakällor du just konfigurerade. Mer information finns i [Skapa formulärdatamodell](/help/forms/using/create-form-data-models.md).
