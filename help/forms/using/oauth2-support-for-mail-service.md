---
title: Konfigurera OAuth2-baserad autentisering för e-postserverprotokoll i Microsoft® Office 365
description: Konfigurera OAuth2-baserad autentisering för e-postserverprotokoll i Microsoft® Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Integrera med e-postserverprotokoll för Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

AEM Forms erbjuder OAuth 2.0-stöd för integrering med Microsoft® Office 365-protokoll för e-postservrar, så att organisationer kan uppfylla kraven för e-post. Du kan använda Azure Active Directory (Azure AD) OAuth 2.0-autentiseringstjänsten för att ansluta till olika protokoll som IMAP, POP eller SMTP och komma åt e-postdata för Office 365-användare. Nedan finns stegvisa instruktioner för hur du konfigurerar e-postserverprotokoll för Microsoft® Office 365 för autentisering via OAuth 2.0-tjänsten:

1. Inloggning [https://portal.azure.com/](https://portal.azure.com/) och söka efter **Azure Active Directory** i sökfältet och klicka på resultatet.
Du kan även bläddra direkt till [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Klicka **Lägg till** > **Appregistrering** > **Ny registrering**

   ![Appregistrering](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Fyll i informationen enligt dina krav och klicka sedan **Registrera**.
   ![Konto som stöds](/help/forms/using/assets/azure_suuportedaccountype.png)
I ovanstående fall 
**Konton i alla organisationskataloger (alla Azure AD-kataloger - Multitenant) och personliga Microsoft®-konton (till exempel Skype, Xbox)** är markerat.

   >[!NOTE]
   >
   > * För **Konton i alla organisationskataloger (alla Azure AD-kataloger - Multitenant)** rekommenderar vi att du använder ett arbetskonto i stället för ett personligt e-postkonto.
   > * **Endast personliga Microsoft®-konton** programmet stöds inte.
   > * Det rekommenderas att använda **Multi-tenant och personligt Microsoft®-konto** program.


1. Nästa, gå till **Certifikat och hemligheter**, klicka **Ny klienthemlighet** och följ stegen på skärmen för att skapa en hemlighet. Observera detta hemliga värde för senare bruk.

   ![Hemlig nyckel](/help/forms/using/assets/azure_secretkey.png)

1. Om du vill lägga till behörigheter går du till det nya programmet och väljer **API-behörigheter** > **Lägg till en behörighet** > **Microsoft® Graph** > **Delegerade behörigheter**
1. Markera kryssrutorna för behörigheterna nedan för appen och klicka på **Lägg till behörighet**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API-behörighet](/help/forms/using/assets/azure_apipermission.png)

1. Välj **Autentisering** > **Lägg till en plattform** > **Webb** och i **Omdirigerings-URL** lägger du till någon av URI:erna nedan (Universal Resource Identifier) som:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   I detta fall `https://login.microsoftonline.com/common/oauth2/nativeclient` används som omdirigerings-URI.

1. Klicka **Konfigurera** efter att du lagt till varje URL-adress och konfigurerat inställningarna enligt dina önskemål.
   ![Omdirigerings-URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > Det är obligatoriskt att välja **Åtkomsttoken** och **ID-token** kryssrutor.

1. Klicka **Översikt** i den vänstra rutan och kopiera värdena för **Program-ID (klient)**, **Katalog-ID (klientorganisation)** och **Klienthemlighet** för senare bruk.

   ![Översikt](/help/forms/using/assets/azure_overview.png)

## Generera auktoriseringskoden {#generating-the-authorization-code}

Därefter måste du generera auktoriseringskoden, vilket förklaras i följande steg:

1. Öppna följande URL i webbläsaren när du har ersatt den `clientID` med `<client_id>` och `redirect_uri` med programmets omdirigerings-URI:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > Om det gäller single tenant-programmet ska `common` med `[tenantid]` i följande URL för generering av auktoriseringskod: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. När du skriver ovanstående URL omdirigeras du till inloggningsskärmen:
   ![Inloggningsskärm](/help/forms/using/assets/azure_loginscreen.png)

1. Ange e-postadressen och klicka på **Nästa** och fönstret App permission visas:

   ![Tillåt behörighet](/help/forms/using/assets/azure_permission.png)

1. När du tillåter det omdirigeras du till en ny URL som: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Kopiera värdet för `<code>` från ovanstående URL `0.ASY...` till `&session_state` i ovanstående URL.

## Genererar uppdateringstoken {#generating-the-refresh-token}

Därefter måste du generera en uppdateringstoken, som beskrivs i följande steg:

1. Öppna kommandotolken och använd följande cURL-kommando för att hämta refreshToken.

1. Ersätt `clientID`, `client_secret` och `redirect_uri` med värdena för programmet tillsammans med värdet för `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > I ett single tenant-program använder du följande cURL-kommando och ersätt för att generera en uppdateringstoken `common` med `[tenantid]` in:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Notera uppdateringstoken.

## Konfigurera e-posttjänst med stöd för OAuth 2.0 {#configureemailservice}

Nu måste du konfigurera e-posttjänsten på den senaste JEE-servern genom att logga in i administratörsgränssnittet:

1. Gå till **Startsida** > **Tjänst** > **Program och tjänster** > **Tjänsthantering** > **E-posttjänst**, **E-posttjänst för konfiguration** visas, konfigurerad för grundläggande autentisering.

   >[!NOTE]
   >
   > Om du vill aktivera Autentiseringstjänsten Auto 2.0 måste du välja **Om SMTP-servern kräver autentisering (SMTP-autentisering)** kryssrutan.

1. Ange **Autentiseringsinställningar för Auto 2.0** as `True`.
1. Kopiera värdena för **Klient-ID** och **Klienthemlighet** från Azure Portal.
1. Kopiera värdet för genererad **Uppdatera token**.
1. Logga in på **Workbench** och söka **E-post 1.0** från **Aktivitetsväljaren**.
1. Tre alternativ är tillgängliga under E-post 1.0 som:
   * **Skicka med dokument**: Skickar e-post med enstaka bilagor.
   * **Skicka med karta över bilagor**: Skickar e-post med flera bilagor.
   * **Ta emot**: Tar emot ett e-postmeddelande från IMAP.

   >[!NOTE]
   >
   >* Transportsäkerhetsprotokollet har giltiga värden som: &#39;blank&#39;, &#39;SSL&#39; eller &#39;TLS&#39;. Du måste ange värden för **SMTP-transportsäkerhet** och **Ta emot transportsäkerhet** till **TLS** för att aktivera autentiseringstjänsten för autentisering.
   >* **POP3-protokoll** stöds inte för OAuth när e-postslutpunkter används.


   ![Anslutningsinställningar](/help/forms/using/assets/oauth_connectionsettings.png)

1. Testa programmet genom att välja **Skicka med dokument**.
1. Ange **TILL** och **Från** adresser.
1. Anropa programmet och e-postmeddelandet skickas med autentiseringen 0Auth 2.0.

   >[!NOTE]
   >
   >Om du vill ändra autentiseringsinställningen Auth 2.0 till grundläggande autentisering för en viss process i en workbench kan du ange **OAuth 2.0-autentisering** värdet som &#39;False&#39; under **Använd globala inställningar** i **Anslutningsinställningar** -fliken.

## Så här aktiverar du autenticeringsmeddelanden {#enable_oauth_task}

1. Gå till **Startsida** > **Tjänster** > **Formulärarbetsflöde** > **Serverinställningar** > **E-postinställningar**
1. Om du vill aktivera autenticeringsmeddelanden väljer du **Aktivera autentisering** kryssrutan.
1. Kopiera värdena för **Klient-ID** och **Klienthemlighet** från Azure Portal.
1. Kopiera värdet för genererad **Uppdatera token**.
1. Klicka **Spara** för att spara informationen.

   ![Aktivitetsmeddelande](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Om du vill veta mer om aktivitetsmeddelanden [klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Konfigurera e-postslutpunkt {#configure_email_endpoint}

1. Gå till **Startsida** > **Tjänster** > **Program och tjänster** > **Hantering av slutpunkter**
1. Konfigurera e-postslutpunkt genom att ange **Autentiseringsinställningar för Auto 2.0** as `True`.
1. Kopiera värdena för **Klient-ID** och **Klienthemlighet** från Azure Portal.
1. Kopiera värdet för genererad **Uppdatera token**.
1. Klicka **Spara** för att spara informationen.

   ![Anslutningsinställningar](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Om du vill ha mer information om hur du konfigurerar e-postslutpunkter klickar du på [Konfigurera en e-postslutpunkt](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Felsökning {#troubleshooting}

* Om e-posttjänsten inte fungerar som den ska. Försök att återskapa `Refresh Token` enligt ovan. Det tar några minuter innan det nya värdet distribueras.

* Ett fel uppstod när e-postserverinformation konfigurerades i e-postslutpunkten med Workbench.Försök att konfigurera slutpunkten via administratörsgränssnittet i stället för Workbench.
