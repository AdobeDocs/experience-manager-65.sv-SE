---
title: Konfigurera inställningar för SAML-tjänstleverantör
seo-title: Konfigurera inställningar för SAML-tjänstleverantör
description: Du kan konfigurera inställningarna för SAML-tjänsteleverantören så att användarna kan logga in och autentisera till AEM-formulär via en angiven tredjepartsidentitetsleverantör (IDP).
seo-description: Du kan konfigurera inställningarna för SAML-tjänsteleverantören så att användarna kan logga in och autentisera till AEM-formulär via en angiven tredjepartsidentitetsleverantör (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera inställningar för SAML-tjänstleverantör{#configure-saml-service-provider-settings}

SAML (Security Assertion Markup Language) är ett av de alternativ som du kan välja när du konfigurerar auktorisering för en företagsdomän eller hybriddomän. SAML används främst för att stödja enkel inloggning över flera domäner. När SAML är konfigurerat som din autentiseringsleverantör loggar användarna in och autentiserar till AEM-formulär via en angiven tredjeparts identitetsleverantör (IDP).

En förklaring av SAML finns i [Security Assertion Markup Language (SAML) V2.0 Technical Overview](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Inställningar för SAML-tjänstleverantör.
1. Ange ett unikt ID som ska användas som identifierare för implementeringen av AEM-formulärtjänstleverantören i rutan Tjänstleverantörens enhets-ID. Du anger också detta unika ID när du konfigurerar din IDP (till exempel `um.lc.com`.). Du kan också använda den URL som används för att komma åt AEM-formulär (till exempel `https://AEMformsserver`).
1. I rutan Bas-URL för tjänsteleverantör anger du bas-URL:en för formulärservern (till exempel `https://AEMformsserver:8080`).
1. (Valfritt) Gör så här för att aktivera AEM-formulär för att skicka signerade autentiseringsbegäranden till IDP:

   * Använd Pålitlighetshanteraren för att importera en autentiseringsuppgift i PKCS #12-format med Dokumentsigneringsuppgifter som har valts som pålitlighetslagertyp. (Se [Hantera lokala autentiseringsuppgifter](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * I aliaslistan för tjänstleverantörens nyckel för autentiseringsuppgifter markerar du det alias som du tilldelade autentiseringsuppgifterna i Trust Store.
   * Klicka på Exportera om du vill spara URL-innehållet i en fil och sedan importera filen till din IDP.

1. (Valfritt) Välj det namnformat som IDP använder för att identifiera användaren i en SAML-försäkran i listan över namn-ID för tjänsteleverantören. Alternativen är Unspecified, Email och Windows Domain Qualified Name.

   >[!NOTE]
   >
   >Namnformaten är inte skiftlägeskänsliga.

1. (Valfritt) Välj Aktivera autentiseringsfråga för lokala användare. När det här alternativet är markerat visas två länkar:

   * en länk till inloggningssidan för SAML-identitetsleverantören från tredje part, där användare som tillhör en företagsdomän kan autentisera.
   * en länk till inloggningssidan för AEM-formulär, där användare som tillhör en lokal domän kan autentisera.
   När det här alternativet inte är markerat dirigeras användare direkt till inloggningssidan för SAML-identitetsleverantören från tredje part, där användare som tillhör en företagsdomän kan autentisera.

1. (Valfritt) Markera Aktivera artifakt-bindning om du vill aktivera stöd för artefaktbindning. POST-bindning används som standard med SAML. Om du har konfigurerat Artefaktbindning väljer du det här alternativet. När det här alternativet är markerat skickas inte den faktiska användarbekräftelsen via webbläsarbegäran. I stället skickas en pekare till kontrollen och försäkran hämtas med ett serverdelsanrop för webbtjänsten.
1. (Valfritt) Markera Aktivera omdirigeringsbindning om du vill ha stöd för SAML-bindningar som använder omdirigeringar.
1. (Valfritt) Ange ytterligare egenskaper i Anpassade egenskaper. De ytterligare egenskaperna är namn=värde-par avgränsade med nya rader.

   * Du kan konfigurera AEM-formulär så att de utfärdar en SAML-försäkran för en giltighetsperiod som matchar giltighetsperioden för en tredjepartsförsäkran. Lägg till följande rad i Anpassade egenskaper för att efterleva tidsgränsen för SAML-försäkran från tredje part:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Lägg till följande anpassade egenskap för att använda RelayState för att bestämma den URL där användaren ska omdirigeras efter lyckad autentisering.

      `saml.sp.use.relaystate=true`

   * Lägg till följande anpassade egenskap för att konfigurera URL:en för Java Server Pages (JSP), som ska användas för att återge den registrerade listan över identitetsleverantörer. Om du inte har distribuerat något anpassat webbprogram används standardsidan för användarhantering för att återge listan.
   `saml.sp.discovery.url=/custom/custom.jsp`

1. Klicka på Spara.

