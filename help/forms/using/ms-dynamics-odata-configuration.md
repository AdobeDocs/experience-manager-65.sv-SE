---
title: Microsoft Dynamics OData-konfiguration
description: Lär dig hur du använder, integrerar och arbetar med online- och lokala Microsoft Dynamics-tjänster via formulärdatamodell.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Microsoft Dynamics OData-konfiguration{#microsoft-dynamics-odata-configuration}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html) |
| AEM 6.5 | Den här artikeln |

![dataintegrering](assets/data-integeration.png)

Microsoft Dynamics är en CRM- och ERP-programvara (Enterprise Resource Planning) som innehåller företagslösningar för att skapa och hantera kundkonton, kontakter, leads, möjligheter och ärenden. [AEM Forms dataintegrering](../../forms/using/data-integration.md) tillhandahåller en OData-molntjänstkonfiguration som integrerar Forms med både online- och lokal Microsoft Dynamics-server. Det gör att du kan skapa en formulärdatamodell som baseras på de enheter, attribut och tjänster som definieras i Microsoft Dynamics-tjänsten. Formulärdatamodellen kan användas för att skapa anpassade formulär som interagerar med Microsoft Dynamics-servern för att möjliggöra affärsarbetsflöden. Till exempel:

* Fråga Microsoft Dynamics-servern efter data och förifylla adaptiva formulär
* Skriv data i Microsoft Dynamics när formulär skickas med adaptiv form
* Skriv data i Microsoft Dynamics via anpassade entiteter som definierats i formulärdatamodellen och omvänt

AEM Forms tilläggspaket innehåller även OData-konfiguration för referens som du kan använda för att snabbt integrera Microsoft Dynamics med AEM Forms.

När paketet är installerat är följande enheter och tjänster tillgängliga på din AEM Forms-instans:

* MS Dynamics OData-Cloud Service (OData-tjänst)
* Formulärdatamodell med förkonfigurerade Microsoft Dynamics-enheter och -tjänster.

Förkonfigurerade Microsoft Dynamics-enheter och -tjänster i en formulärdatamodell är bara tillgängliga på din AEM Forms-instans om körningsläget för den AEM instansen har angetts som `samplecontent` (standard). MS Dynamics OData-Cloud Servicen (OData Service) är även tillgänglig med andra körningslägen. Mer information om hur du konfigurerar körningslägen för en AEM instans finns i [Körningslägen](/help/sites-deploying/configure-runmodes.md).

## Förutsättningar {#prerequisites}

Innan du börjar konfigurera och konfigurera Microsoft Dynamics måste du se till att du har:

* Installerade [AEM Forms tilläggspaket](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Konfigurerade Microsoft Dynamics 365 online eller installerade en instans av någon av följande Microsoft Dynamics-versioner:

   * Lokal Microsoft Dynamics 365
   * Lokal Microsoft Dynamics 2016

* [Registrerade programmet för onlinetjänsten Microsoft Dynamics med Microsoft Azure Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Notera värdena för klient-ID (kallas även program-ID) och klienthemlighet för den registrerade tjänsten. Dessa värden används medan [konfigurerar molntjänsten för din Microsoft Dynamics-tjänst](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Ange svars-URL för registrerat Microsoft Dynamics-program {#set-reply-url-for-registered-microsoft-dynamics-application}

Gör följande för att ange svars-URL för det registrerade Microsoft Dynamics-programmet:

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar AEM Forms med Microsoft Dynamics onlineserver.

1. Gå till Microsoft Azure Active Directory-kontot och lägg till följande URL för molntjänstkonfiguration i **Svar-URL:er** inställningar för ditt registrerade program:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure-katalogen](assets/azure_directory_new.png)

1. Spara konfigurationen.

## Konfigurera Microsoft Dynamics för IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics använder anspråksbaserad autentisering för att ge åtkomst till data på Microsoft Dynamics CRM-servern till externa användare. Gör så här för att konfigurera Microsoft Dynamics för Internet-baserad distribution (IFD) och konfigurera anspråksinställningar om du vill aktivera detta.

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar AEM Forms med en lokal Microsoft Dynamics-server.

1. Konfigurera den lokala instansen av Microsoft Dynamics för IFD enligt beskrivningen i [Konfigurera IFD för Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Kör följande kommandon med Windows PowerShell för att konfigurera anspråksinställningar för IFD-aktiverade Microsoft Dynamics:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Se [Appregistrering för CRM lokalt (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) för mer information.

## Konfigurera OAuth-klient på AD FS-dator {#configure-oauth-client-on-ad-fs-machine}

Gör följande för att registrera en OAuth-klient på AD FS-datorn (Active Directory Federation Services) och bevilja åtkomst på AD FS-datorn:

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar AEM Forms med en lokal Microsoft Dynamics-server.

1. Kör följande kommando:

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Var:

   * `Client-ID` är ett klient-ID som du kan generera med valfri GUID-generator.
   * `redirect-uri` är URL:en till molntjänsten Microsoft Dynamics OData på AEM Forms. Standardmolntjänsten som installeras med AEM Forms-paketet distribueras på följande URL:
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Kör följande kommando för att bevilja åtkomst på AD FS-datorn:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   Var:

   * `resource` är Microsoft Dynamics organisations-URL.

1. Microsoft Dynamics använder HTTPS-protokoll. Om du vill anropa AD FS-slutpunkter från Forms-servern installerar du platscertifikatet för Microsoft Dynamics i Java-certifikatarkivet med hjälp av `keytool` på den dator där AEM Forms körs.

## Konfigurera molntjänsten för din Microsoft Dynamics-tjänst {#configure-cloud-service-for-your-microsoft-dynamics-service}

The **MS Dynamics OData-Cloud Service (OData-tjänst)** konfigurationen levereras med OData-standardkonfiguration. Så här konfigurerar du den för att ansluta till din Microsoft Dynamics-tjänst.

1. Navigera till **[!UICONTROL Tools > Cloud Services > Data Sources]** och väljer `global` konfigurationsmapp.
1. Välj **MS Dynamics OData-Cloud Service (OData-tjänst)** konfigurera och välja **[!UICONTROL Properties]**. Dialogrutan för konfigurationsegenskapen för molntjänster öppnas.

   I **Autentiseringsinställningar** tab:

   1. Ange värdet för **Tjänstrot** fält. Gå till Dynamics-instansen och navigera till **Resurser för utvecklare** om du vill visa värdet för fältet Tjänstrot. Till exempel https://&lt;tenant-name>/api/data/v9.1/

   1. Ersätt standardvärdena i dialogrutan **Klient-ID**(kallas även **Program-ID**), **Klienthemlighet**, **OAuth-URL**, **Uppdatera token-URL**, **Åtkomsttoken-URL** och **Resurs** fält med värden från din Microsoft Dynamics-tjänstkonfiguration. Det är obligatoriskt att ange dynamicinstansens URL i **Resurs** för att konfigurera Microsoft Dynamics med en formulärdatamodell. Använd tjänstens rot-URL för att härleda den dynamiska instansens URL. Till exempel: [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Ange **open** i **Auktoriseringsomfång** fält för auktoriseringsprocess i Microsoft Dynamics.

   ![Autentiseringsinställningar](assets/dynamics_authentication_settings_new.png)

1. Klicka på **[!UICONTROL Connect to OAuth]**. Du omdirigeras till inloggningssidan för Microsoft Dynamics.
1. Logga in med dina Microsoft Dynamics-autentiseringsuppgifter och godkänn för att tillåta molntjänstkonfigurationen att ansluta till Microsoft Dynamics-tjänsten. Det är en engångsuppgift att upprätta en anslutning mellan molntjänsten och tjänsten.

   Du omdirigeras sedan till konfigurationssidan för molntjänsten, som visar ett meddelande om att OData-konfigurationen har sparats.

Molntjänsten MS Dynamics OData Cloud Service (OData Service) är konfigurerad och ansluten till Dynamics-tjänsten.

## Skapa formulärdatamodell {#create-form-data-model}

När du installerar AEM Forms-paketet skapas en formulärdatamodell,**Microsoft Dynamics FDM**, distribueras på din AEM. Som standard använder formulärdatamodellen Microsoft Dynamics-tjänsten som konfigurerats i MS Dynamics OData-Cloud Servicen (OData-tjänsten) som datakälla.

När formulärdatamodellen öppnas för första gången ansluter den till den konfigurerade Microsoft Dynamics-tjänsten och hämtar enheter från din Microsoft Dynamics-instans. Enheterna &quot;contact&quot; och &quot;lead&quot; från Microsoft Dynamics har redan lagts till i formulärdatamodellen.

Gå till om du vill granska formulärdatamodellen **[!UICONTROL Forms > Data Integrations]**. Välj **Microsoft Dynamics FDM** och klicka **Redigera** för att öppna formulärdatamodellen i redigeringsläge. Du kan även öppna formulärdatamodellen direkt från följande URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

Därefter kan du skapa ett anpassat formulär baserat på formulärdatamodellen och använda det i olika varianter av formuläranvändningen, till exempel:

* Fyll i anpassat formulär i förväg genom att fråga information från enheter och tjänster i Microsoft Dynamics
* Anropa Microsoft Dynamics-serveråtgärder som definierats i en formulärdatamodell med hjälp av adaptiva formulärregler
* Skriv skickade formulärdata till Microsoft Dynamics-enheter

Vi rekommenderar att du skapar en kopia av den formulärdatamodell som medföljer AEM Forms-paketet och konfigurerar datamodeller och tjänster så att de passar dina behov. Det ser till att eventuella framtida uppdateringar av paketet inte åsidosätter formulärdatamodellen.

Mer information om hur du skapar och använder formulärdatamodell i affärsarbetsflöden finns i [Dataintegrering](../../forms/using/data-integration.md).
