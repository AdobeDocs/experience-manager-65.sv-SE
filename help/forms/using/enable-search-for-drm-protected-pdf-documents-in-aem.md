---
title: Aktivera AEM för att söka efter dokumentskyddade PDF-dokument
seo-title: Enable AEM to search document security protected PDF documents
description: Lär dig hur du aktiverar AEM för fulltextsökning i DRM-skyddade PDF-dokument.
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Aktivera AEM för att söka efter dokumentskyddade PDF-dokument{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM kan söka efter och hitta AEM resurser och utföra textsökning i olika vanliga dokumentformat, t.ex. oformaterade textfiler, Microsoft Office-dokument och PDF. Du kan även utöka den inbyggda sökningen för att utföra fulltextsökning på [PDF-dokument som skyddas med AEM dokumentsäkerhet](../../forms/using/admin-help/document-security.md). Så här aktiverar du AEM att utföra fulltextsökning i sådana dokument:

1. Upprätta en säker anslutning
1. Indexera ett exempelprincipskyddat PDF-dokument

## Förutsättningar {#prerequisites}

* Om du använder AEM Forms på OSGi:

   * Installera [AEM Forms Document Security Indexer](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) på AEM Forms-servern.

   * Kontrollera att en AEM Forms på JEE-server är igång och att dokumentsäkerheten är installerad på motsvarande AEM Forms på JEE-server. Det AEM formuläret på JEE-servern krävs för att indexera det skyddade dokumentet.

* Om du bara använder AEM Forms på JEE-servern är indexeringspaketet redan installerat.
* Se till att alla paket är igång. Om alla paket inte är aktiva väntar du tills alla paket är igång.

   * För AEM Forms on OSGi listas paketen på https://&#39;[server]:[port]&#39;/system/console/bundles.
   * För AEM Forms on JEE listas paketeringen på https://&#39;[server]:[port]&#39;/[kontextsökväg]/system/console/bundles. Exempel: https://localhost:8080/lc/system/console/bundles.

* Lägg till *sun.util.calendar* till tillåtelselista. Så här lägger du till paketet i tillåtelselista:

   1. Öppna AEM webbkonsol. URL:en är https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Hitta och öppna **Konfiguration av brandvägg för deserialisering**.

   1. Lägg till paketet sun.util.calendar i fältet för Tillåtslista klasser eller paketprefix och klicka på **Spara**.

### Skapa en säker anslutning mellan AEM Forms JEE- och OSGi-stackar {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Du kan använda någon av följande metoder för att upprätta en säker anslutning:

* Konfigurera SDK-paketet för LiveCyclet Adobe med autentiseringsuppgifter för AEM Forms på JEE-administratören
* Konfigurera Adobe LiveCycle Client SDK Bundle med hjälp av ömsesidig autentisering

#### Konfigurera SDK-paketet för LiveCyclet Adobe med autentiseringsuppgifter för AEM Forms på JEE-administratören {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Öppna AEM webbkonsol. URL:en är https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Leta reda på och öppna **Adobe LiveCycle Client SDK Bundle**. Ange värde för följande fält:

   * **Server-URL:** Ange HTTPS-URL för AEM Forms på JEE-server. Om du vill aktivera kommunikation via https startar du om servern med -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parameter.
   * **Tjänstnamn**: Lägg till RightsManagementService i listan över angivna tjänster.
   * **Användarnamn:** Ange användarnamnet för det AEM Forms på JEE-konto som ska användas för att initiera anrop från AEM server. Det angivna kontot måste ha behörighet att starta dokumenttjänster på AEM Forms på JEE-servern.
   * **Lösenord**: Ange lösenord för det AEM Forms på JEE-konto som anges i fältet Användarnamn.

   Klicka **Spara**. AEM är aktiverat för att söka efter dokumentsäkerhetsskyddade PDF-dokument.

#### Konfigurera Adobe LiveCycle Client SDK Bundle med hjälp av ömsesidig autentisering {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Aktivera ömsesidig autentisering för AEM Forms på JEE. Mer information finns i [CAC och ömsesidig autentisering](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Öppna AEM webbkonsol. URL:en är https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Leta reda på och öppna **Adobe LiveCycle Client SDK** Paket. Ange värde för följande egenskaper:

   * **Server-URL**: Ange HTTPS-URL för AEM Forms på JEE-server. Om du vill aktivera kommunikation via https startar du om AEM med -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parameter.
   * **Aktivera tvåvägs SSL**: Aktivera alternativet Aktivera tvåvägs SSL.
   * **KeyStore-fil-URL**: Ange URL-adressen till nyckelfilen.
   * **TrustStore-fil-URL**: Ange URL-adressen för förvaltarfilen.
   * **KeyStore-lösenord**: Ange lösenordet för nyckelfilen.
   * **TrustStorePassword**: Ange lösenordet för förvaltarfilen.
   * **Tjänstnamn**: Lägg till RightsManagementService i listan över angivna tjänster.

   Klicka **Spara**. AEM är aktiverat för att söka efter dokumentsäkerhetsskyddade PDF-dokument

### Indexera ett exempelprincipskyddat PDF-dokument {#index-a-sample-policy-protected-pdf-document}

1. Logga in på AEM Assets som administratör.
1. Skapa en mapp i AEM Digital Asset Manager och överför profilskyddade PDF-dokument till den nya mappen.

   Nu kan du söka i principskyddade dokument med hjälp av AEM sökning.
