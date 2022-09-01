---
title: OAuth2-stöd för e-posttjänsten
description: 'Oauth2-stöd för e-posttjänsten  '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# OAuth2-stöd för e-posttjänsten {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service erbjuder OAuth2-stöd för sin integrerade e-posttjänst, så att organisationer kan följa e-postkraven.

Du kan konfigurera OAuth för flera e-postleverantörer. Nedan visas steg-för-steg-instruktioner för hur du konfigurerar AEM Mail Service för att autentisera via OAuth2 med Microsoft Office 365 Outlook. Andra leverantörer kan konfigureras på liknande sätt.

## Microsoft Outlook {#microsoft-outlook}

1. Gå till [https://portal.azure.com/](https://portal.azure.com/) och logga in.
1. Sök efter **Azure Active Directory** i sökfältet och klicka på resultatet. Du kan även bläddra direkt till [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Klicka på **Appregistrering** - **Ny registrering**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. Fyll i informationen enligt dina krav och klicka sedan på **Registrera**
1. Gå till den nya appen och välj **API-behörigheter**
1. Gå till **Lägg till behörighet** - **Diagrambehörighet** - **Delegerade behörigheter**
1. Välj behörigheter nedan för din app och klicka sedan på **Lägg till behörighet**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Gå till **Autentisering** - **Lägg till en plattform** - **Webb** och i **Omdirigerings-URL** lägger du till nedanstående URL:er - en med och en utan snedstreck:
   * `http://localhost/`
   * `http://localhost`
1. Tryck **Konfigurera** efter att du lagt till varje URL-adress och konfigurerat inställningarna enligt dina önskemål
1. Nästa, gå till **Certifikat och hemligheter**, klicka på **Ny klienthemlighet** och följ stegen på skärmen för att skapa en hemlighet. Observera denna hemlighet för senare bruk
1. Tryck **Översikt** i den vänstra rutan och kopiera värdena för **Program-ID (klient)** för senare bruk.

För att komma tillbaka behöver du följande information för att konfigurera OAuth2 för e-posttjänsten på AEM sida:

* Autentiserings-URL i formuläret: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* Token-URL i formuläret: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* Uppdatera URL i formuläret: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* Klient-ID
* Klienthemlighet

### Genererar uppdateringstoken {#generating-the-refresh-token}

Därefter måste du generera en uppdateringstoken, vilket visas i ett senare steg.

Så här gör du:

1. Öppna följande URL i webbläsaren när du har ersatt den `clientID` med de värden som är specifika för ditt konto:

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. Tillåt tillstånd där det behövs.
1. URL:en kommer att omdirigeras till en ny plats som har följande format: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Kopiera värdet för `<code>` i exemplet ovan
1. Använd följande cURL-kommando för att hämta refreshToken. Ersätt clientID, clientSecret med värdena för ditt konto och värdet för `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Notera refreshToken och accessToken.

### Validerar token {#validating-the-tokens}

Innan du fortsätter att konfigurera OAuth på AEM-sidan måste du verifiera både accessToken och refreshToken med proceduren nedan:

1. Generera accessToken med hjälp av den refreshToken som skapades i föregående procedur. Du kan uppnå detta med följande kurva och ersätta värdena för `<client_id>`,`<client_secret>` tillsammans med `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Skicka ett e-postmeddelande med accessToken för att se om det fungerar som det ska.

>[!NOTE]
>
> Du kan hämta Postman API-samlingen från [den här platsen](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Konfigurera e-posttjänst med stöd för Auth2.0 {#configureemailservice}

Nu måste du konfigurera e-posttjänsten på den senaste JEE-servern genom att logga in i administratörsgränssnittet:

1. Gå till **Startsida** - **Tjänst** - **Program och tjänster** - **Tjänsthantering** - **E-posttjänst**
1. **E-posttjänst för konfiguration** fönster visas, konfigurera **SMPT** och **IMP** servrar för grundläggande autentisering.
1. Om du vill aktivera tjänsten för e-postautentisering i Outlook väljer du **Autentiseringsinställningar för Auto 2.0** kryssrutan.
1. Kopiera värdena för **Klient-ID** och **Klienthemlighet** från Azure Portal.
1. Kopiera värdet för genererad **Uppdatera token**.
1. Klicka **Spara** för att spara informationen.
1. Logga in på workbench och sök **E-post 1.0** från **Aktivitetsväljaren**.
1. Tre alternativ är tillgängliga under E-post 1.0 som:
   * **Skicka med dokument**: Skickar e-post med enstaka bilagor.
   * **Skicka med karta över bilagor**: Skickar e-post med flera bilagor.
   * **Ta emot**: Tar emot ett e-postmeddelande från POP3 eller IMAP.
1. Testa programmet genom att välja **Skicka med dokument**
1. Ange **TILL** och **Från** adresser.
1. Anropa programmet och e-postmeddelandet skickas med autentisering av oAuth2.0.

>[!NOTE]
>
> Om du vill ändra autentiseringsinställningen Auth 2.0 till grundläggande autentisering för en viss process i en workbench kan du avmarkera **Autentisering med oAuth2.0** kryssruta under **Använd globala inställningar** i **Anslutningsinställningar** -fliken.

### Felsökning {#troubleshooting}

Om e-posttjänsten inte fungerar som den ska genererar du om `refreshToken` enligt ovan. Det tar några minuter innan det nya värdet distribueras.


