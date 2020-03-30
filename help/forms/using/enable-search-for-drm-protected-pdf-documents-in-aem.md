---
title: Aktivera AEM för att söka efter dokumentskyddade PDF-dokument
seo-title: Aktivera AEM för att söka efter dokumentskyddade PDF-dokument
description: 'Lär dig hur du aktiverar AEM-sökning för fulltextsökning i DRM-skyddade PDF-dokument.  '
seo-description: 'Lär dig hur du aktiverar AEM-sökning för fulltextsökning i DRM-skyddade PDF-dokument.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Aktivera AEM för att söka efter dokumentskyddade PDF-dokument{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM-sökning kan användas för att söka efter och hitta AEM-resurser och för textsökning i olika vanliga dokumentformat, t.ex. oformaterade textfiler, Microsoft Office-dokument och PDF-dokument. Du kan även utöka den inbyggda sökningen för att utföra fulltextsökning i [PDF-dokument som skyddas med AEM-dokumentsäkerhet](../../forms/using/admin-help/document-security.md). Gör så här för att göra det möjligt för AEM att utföra fulltextsökning i sådana dokument:

1. Upprätta en säker anslutning
1. Indexera ett exempel på ett policyskyddat PDF-dokument

## Förutsättningar {#prerequisites}

* Om du använder AEM Forms på OSGi:

   * Installera [AEM Forms Document Security Indexer-paketet](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) på AEM Forms-servern.

   * Kontrollera att ett AEM Forms på JEE-servern är igång och att dokumentsäkerheten är installerad på motsvarande AEM Forms på JEE-server. AEM-formuläret på JEE-servern krävs för att indexera det skyddade dokumentet.

* Om du bara använder AEM Forms på JEE-servern är indexeringspaketet redan installerat.
* Se till att alla paket är igång. Om alla paket inte är aktiva väntar du tills alla paket är igång.

   * För AEM Forms on OSGi listas paketen på https://&#39;[server]:[port]&#39;/system/console/bundles.
   * För AEM Forms på JEE listas paketen på https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Till exempel https://localhost:8080/lc/system/console/bundles.

* Whitelist the *sun.util.calendar* package. Så här vitlistar du paketet:

   1. Öppna AEM Web Console. URL:en är https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Leta reda på och öppna **Brandväggskonfiguration** för deserialisering.

   1. Lägg till paketet sun.util.calendar i fältet för vitlistade klasser eller paketprefix och klicka på **Spara**.

### Skapa en säker anslutning mellan AEM Forms JEE- och OSGi-stackar {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Du kan använda någon av följande metoder för att upprätta en säker anslutning:

* Konfigurera Adobe LiveCycle Client SDK Bundle med AEM Forms på JEE-administratörsautentiseringsuppgifter
* Konfigurera Adobe LiveCycle Client SDK Bundle med ömsesidig autentisering

#### Konfigurera Adobe LiveCycle Client SDK Bundle med AEM Forms på JEE-administratörsautentiseringsuppgifter {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Öppna AEM Web Console. URL:en är https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Leta upp och öppna **Adobe LiveCycle Client SDK Bundle**. Ange värde för följande fält:

   * **Server-URL:** Ange HTTPS-URL för AEM Forms på JEE-server. Om du vill aktivera kommunikation över https startar du om servern med parametern -Djavax.net.ssl.trustStore=&lt;sökväg till AEM Forms i JEE-nyckelfil>.
   * **Tjänstnamn**: Lägg till RightsManagementService i listan över angivna tjänster.
   * **Användarnamn:** Ange användarnamn för det AEM Forms på JEE-konto som ska användas för att initiera anrop från AEM-servern. Det angivna kontot måste ha behörighet att starta dokumenttjänster på AEM Forms på JEE-servern.
   * **Lösenord**: Ange lösenordet för AEM Forms på JEE-kontot som anges i fältet Användarnamn.
   Click **Save**. AEM är aktiverat för att söka i dokumentskyddade PDF-dokument.

#### Konfigurera Adobe LiveCycle Client SDK Bundle med ömsesidig autentisering {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Aktivera ömsesidig autentisering för AEM Forms på JEE. Mer information finns i [CAC och ömsesidig autentisering](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Öppna AEM Web Console. URL:en är https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Leta upp och öppna **Adobe LiveCycle Client SDK** Bundle. Ange värde för följande egenskaper:

   * **Server-URL**: Ange HTTPS-URL för AEM Forms på JEE-server. Om du vill aktivera kommunikation över https startar du om AEM-servern med parametern -Djavax.net.ssl.trustStore=&lt;sökväg till AEM Forms i JEE-nyckelfil>.
   * **Aktivera tvåvägs SSL**: Aktivera alternativet Aktivera tvåvägs SSL.
   * **KeyStore-fil-URL**: Ange URL:en för nyckelfilen.
   * **TrustStore-fil-URL**: Ange URL-adressen för förvaltarfilen.
   * **KeyStore-lösenord**: Ange lösenordet för nyckelfilen.
   * **TrustStorePassword**: Ange lösenordet för förvaltarfilen.
   * **Tjänstnamn**: Lägg till RightsManagementService i listan över angivna tjänster.
   Click **Save**. AEM är aktiverat för att söka efter dokumentskyddade PDF-dokument

### Indexera ett exempel på ett policyskyddat PDF-dokument {#index-a-sample-policy-protected-pdf-document}

1. Logga in på AEM Assets som administratör.
1. Skapa en mapp i AEM Digital Asset Manager och överför profilskyddade PDF-dokument till den nya mappen.

   Nu kan du söka i principskyddade dokument med hjälp av AEM-sökning.

