---
title: Aktivera AEM för att söka efter dokumentsäkerhetsskyddade PDF- och Microsoft Office-dokument
description: Lär dig hur du aktiverar AEM för fulltextsökning i DRM-skyddade PDF-dokument.
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# Aktivera AEM för att söka efter dokumentsäkerhetsskyddade PDF- och Microsoft Office-dokument{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager har ett användargränssnitt för att söka efter och hitta olika resurser som lagras i AEM. Den inbyggda sökningen kan användas för att söka efter och hitta AEM resurser och för textsökning i olika vanliga dokumentformat, t.ex. oformaterade textfiler, Microsoft Office-dokument och PDF. Du kan också utöka och aktivera den inbyggda sökningen för att utföra fulltextsökning på DRM-skyddade PDF- och Microsoft Office-dokument.

Följ de här stegen för att aktivera AEM att söka efter dokumentsäkerhetsskyddade PDF- och Microsoft Office-dokument:

## Innan du börjar {#before-you-start}

* Installera och konfigurera AEM Forms dokumentsäkerhet.
* Lägg till paketet sun.util.calendar till tillåtelselista i **Konfiguration av brandvägg för deserialisering.** Konfigurationen visas på `https://'[server]:[port]'/system/console/configMgr`.
* Kontrollera att alla AEM är igång. Paketen listas på `https://'[server]:[port]'/system/console/bundles`. Om alla paket inte är aktiva väntar du och kontrollerar paketens status efter några minuter.

## Skapa en säker anslutning i AEM Forms arbetsflöde (AEM Forms på JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

En säker anslutning möjliggör ett smidigt informationsflöde mellan AEM Forms på JEE och OSGi-tjänsterna som körs på samma server. Använd någon av följande metoder för att upprätta en säker anslutning:

* Konfigurera AEM Forms Client SDK Bundle med AEM Forms på JEE-administratörsbehörighet
* Konfigurera AEM Forms Client SDK Bundle med hjälp av ömsesidig autentisering

### Konfigurera AEM Forms Client SDK Bundle med AEM Forms på JEE-administratörsbehörighet {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Öppna AEM konfigurationshanteraren och logga in som administratör. Standardwebbadressen är https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Sök efter och öppna AEM Forms Client SDK Bundle. Ange värde för följande egenskaper:

   * **Server-URL:** Ange HTTP-URL för AEM Forms på JEE-server. Om du vill aktivera kommunikation via https startar du om AEM Forms på JEE-servern med -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parameter.
   * **Tjänstnamn**: Lägg till RightsManagementService i listan över angivna tjänster.
   * **Användarnamn:** Ange användarnamn för det AEM Forms på JEE-konto som ska användas för att initiera anrop från AEM Forms på JEE-servern. Det angivna kontot måste ha behörighet att anropa Document Services på AEM Forms på JEE-servern.
   * **Lösenord**: Ange lösenord för det AEM Forms på JEE-konto som anges i fältet Användarnamn.

   Klicka **Spara**. AEM är aktiverat för att söka efter dokumentsäkerhetsskyddade PDF- och Microsoft Office-dokument.

### Konfigurera AEM Forms Client SDK Bundle med hjälp av ömsesidig autentisering {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Aktivera ömsesidig autentisering för AEM Forms på JEE. Mer information finns i [CAC och ömsesidig autentisering](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Öppna AEM konfigurationshanteraren och logga in som administratör. Standardwebbadressen är https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Sök efter och öppna AEM Forms Client SDK Bundle. Ange värde för följande egenskaper:

   * **Server-URL:** Ange HTTPS-URL för AEM Forms på JEE-server. Om du vill aktivera kommunikation via https startar du om AEM Forms på JEE-servern med -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parameter.
   * **Aktivera tvåvägs SSL**: Aktivera alternativet Aktivera tvåvägs SSL.
   * **KeyStore-fil-URL**: Ange URL-adressen till nyckelfilen.
   * **TrustStore-fil-URL**: Ange URL-adressen för förvaltarfilen.
   * **KeyStore-lösenord**: Ange lösenordet för nyckelfilen.
   * **TrustStorePassword**: Ange lösenordet för förvaltarfilen.
   * **Tjänstnamn**: Lägg till RightsManagementService i listan över angivna tjänster.

   Klicka **Spara**. AEM är aktiverat för att söka efter dokumentsäkerhetsskyddade PDF- och Microsoft Office-dokument

   >[!NOTE]
   >
   > Du bör använda kommandot Ctrl + C för att starta om SDK:n. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java-processer, kan det leda till inkonsekvenser i den AEM utvecklingsmiljön.

## Indexera ett exempel på ett policyskyddat PDF- eller Microsoft Office-dokument {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Logga in på AEM Assets som administratör.
1. Skapa en mapp i AEM Digital Asset Manager och överför ett policyskyddat PDF- eller Microsoft Office-dokument till den nya mappen. Nu kan du söka efter innehållet i de profilskyddade dokumenten med hjälp av AEM sökning. Det måste returnera dokumentet som innehåller den sökta texten.
