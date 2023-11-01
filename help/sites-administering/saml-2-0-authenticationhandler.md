---
title: SAML 2.0-autentiseringshanterare
seo-title: SAML 2.0 Authentication Handler
description: Läs mer om autentiseringshanteraren för SAML 2.0 i AEM.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# SAML 2.0-autentiseringshanterare{#saml-authentication-handler}

AEM levererar en [SAML](https://saml.xml.org/saml-specifications) autentiseringshanterare. Hanteraren har stöd för [SAML](https://saml.xml.org/saml-specifications) 2.0 Authentication Request Protocol (Web-SSO-profil) med `HTTP POST` bindning.

Den stöder:

* signering och kryptering av meddelanden
* automatiskt skapa användare
* synkronisera grupper med befintliga grupper i AEM
* Tjänsteleverantören och identitetsleverantören initierade autentisering

Den här hanteraren lagrar det krypterade SAML-svarsmeddelandet i användarnoden ( `usernode/samlResponse`) för att underlätta kommunikationen med en tredjeparts tjänsteleverantör.

>[!NOTE]
>
>Se [en demonstration av AEM och SAML-integrering](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html).

## Konfigurera autentiseringshanteraren för SAML 2.0 {#configuring-the-saml-authentication-handler}

The [Webbkonsol](/help/sites-deploying/configuring-osgi.md) ger åtkomst till [SAML](https://saml.xml.org/saml-specifications) 2.0-konfiguration för autentiseringshanterare har anropats **Autentiseringshanterare för Adobe Granite SAML 2.0**. Följande egenskaper kan anges.

>[!NOTE]
>
>Autentiseringshanteraren för SAML 2.0 är inaktiverad som standard. Du måste ange minst en av följande egenskaper för att aktivera hanteraren:
>
>* Identity Provider POST URL eller IDP URL.
>* Tjänstleverantörens enhets-ID.
>

>[!NOTE]
>
>SAML-försäkringar är signerade och kan eventuellt krypteras. För att detta ska fungera måste du tillhandahålla minst det offentliga certifikatet för identitetsleverantören i TrustStore. Se [Lägger till IdP-certifikatet till TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) för mer information.

**Bana** Databassökväg som den här autentiseringshanteraren ska användas för av Sling. Om detta är tomt inaktiveras autentiseringshanteraren.

**Servicerangordning** OSGi Framework Service Ranking-värde för att ange i vilken ordning tjänsten ska anropas. Detta är ett heltalsvärde där högre värden anger högre prioritet.

**IDP-certifikatalias** Aliaset för IdP:s certifikat i det globala förtroendearkivet. Om den här egenskapen är tom inaktiveras autentiseringshanteraren. Se kapitlet&quot;Add the IdP Certificate to the AEM TrustStore&quot; nedan om hur du konfigurerar det.

**IDP-URL** URL för den IDP dit SAML-autentiseringsbegäran ska skickas. Om den här egenskapen är tom inaktiveras autentiseringshanteraren.

>[!CAUTION]
>
>Identitetsleverantörens värdnamn måste läggas till i **Apache Sling Referer-filter** OSGi-konfiguration. Se [Webbkonsol](/help/sites-deploying/configuring-osgi.md) för mer information.

**Tjänstleverantörens enhets-ID** ID som unikt identifierar den här tjänstleverantören med identitetsleverantören. Om den här egenskapen är tom inaktiveras autentiseringshanteraren.

**Standardomdirigering** Standardplatsen att omdirigera till efter lyckad autentisering.

>[!NOTE]
>
>Den här platsen används bara om `request-path` cookie har inte angetts. Om du begär en sida under den konfigurerade sökvägen utan en giltig inloggningstoken, lagras den begärda sökvägen i en cookie
>och webbläsaren kommer att omdirigeras till den här platsen igen när autentiseringen är klar.

**Användar-ID-attribut** Namnet på attributet som innehåller det användar-ID som används för att autentisera och skapa användaren i CRX-databasen.

>[!NOTE]
>
>Användar-ID hämtas inte från `saml:Subject` noden i SAML-försäkran men från den `saml:Attribute`.

**Använd kryptering** Om den här autentiseringshanteraren förväntar sig krypterade SAML-försäkringar eller inte.

**Skapa CRX-användare automatiskt** Om icke-befintliga användare ska skapas automatiskt i databasen efter att autentiseringen lyckades eller inte.

>[!CAUTION]
>
>Om det automatiska skapandet av CRX-användare är inaktiverat måste användarna skapas manuellt.

**Lägg till i grupper** Anger om en användare automatiskt ska läggas till i CRX-grupper efter lyckad autentisering.

**Gruppmedlemskap** Namnet på saml:Attribute som innehåller en lista med CRX-grupper som den här användaren ska läggas till i.

## Lägg till IdP-certifikatet i AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML-försäkringar är signerade och kan eventuellt krypteras. För att detta ska fungera måste du ange minst det offentliga certifikatet för IdP i databasen. För att göra detta måste du:

1. Gå till *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Tryck på **[!UICONTROL Create TrustStore link]**
1. Ange lösenordet för TrustStore och tryck på **[!UICONTROL Save]**.
1. Klicka på **[!UICONTROL Manage TrustStore]**.
1. Överför IdP-certifikatet.
1. Notera certifikatet Alias. Aliaset är **[!UICONTROL admin#1436172864930]** i exemplet nedan.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Lägg till tjänstleverantörens nyckel och certifikatkedja i AEM nyckelbehållare {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Stegen nedan är obligatoriska, annars kommer följande undantag att inträffa: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Gå till: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Redigera `authentication-service` användare.
1. Skapa en KeyStore genom att klicka på **Skapa KeyStore** under **Kontoinställningar**.

>[!NOTE]
>
>Stegen nedan är bara obligatoriska om hanteraren ska kunna signera eller dekryptera meddelanden.

1. Skapa certifikat/nyckelpar för AEM. Kommandot för att generera det via openssl bör likna exemplet nedan:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Konvertera nyckeln till PKCS#8-format med DER-kodning. Detta är det format som krävs för AEM nyckelbehållare.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Överför filen med den privata nyckeln genom att klicka på **Välj privat nyckelfil**.
1. Överför certifikatfilen genom att klicka på **Välj filer för certifikatkedja**.
1. Tilldela ett alias enligt nedan:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Konfigurera en loggare för SAML {#configure-a-logger-for-saml}

Du kan konfigurera en loggare för att felsöka problem som kan uppstå när SAML felkonfigureras. Du kan göra detta genom att:

1. Gå till webbkonsolen på *http://localhost:4502/system/console/configMgr*
1. Sök efter och klicka på den anropade posten **Konfiguration av loggningsloggare för Apache Sling**
1. Skapa en loggare med följande konfiguration:

   * **Loggnivå:** Felsök
   * **Loggfil:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
