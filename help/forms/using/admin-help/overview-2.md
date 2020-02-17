---
title: Grunderna för hantering av certifikat och autentiseringsuppgifter
seo-title: Grunderna för hantering av certifikat och autentiseringsuppgifter
description: Lär dig mer om grunderna för hantering av certifikat och autentiseringsuppgifter.
seo-description: Lär dig mer om grunderna för hantering av certifikat och autentiseringsuppgifter.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Grunderna för hantering av certifikat och autentiseringsuppgifter {#basics-of-managing-certificates-and-credentials}

En *autentiseringsuppgift* innehåller den privata nyckelinformation som behövs för att signera eller identifiera dokument. Ett *certifikat* är information om offentlig nyckel som du konfigurerar för förtroende. AEM-formulär använder certifikat och autentiseringsuppgifter för flera syften:

* I Acrobat Reader DC-tillägg används en autentiseringsuppgift för att aktivera användarrättigheter för Adobe Reader i PDF-dokument. (Se [Konfigurera inloggningsuppgifter för användning med Acrobat Reader DC-tillägg](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Du kan konfigurera Rights Management så att autentiseringsuppgifter endast visas för användning i Acrobat från betrodda utfärdare. (Se [Konfigurera visningsinställningar](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)för Rights Management.) Det allmänna namnet (CN) måste finnas i certifikatet.
* Signaturtjänsten får åtkomst till certifikat och autentiseringsuppgifter. Mer information om signaturtjänsten finns i [Tjänstreferens](https://www.adobe.com/go/learn_aemforms_services_63).

**Skapa en parnyckel**

AEM-formulär använder sin Trust Store för att lagra och hantera certifikat, autentiseringsuppgifter och listor över återkallade certifikat. Dessutom kan du använda en oberoende HSM-enhet (Hardware Security Module) för att lagra privata nycklar.

I AEM-formulär finns inget alternativ för att generera nyckelpar. Du kan dock generera det med verktyg som Java-nyckelverktyg och importera det i AEM-formulär Trust Store. Mer information om Java-nyckelverktyget finns i:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

Följande signaturtyper stöds och kan importeras i AEM-formulär:

* XML-signatur
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA-signaturer

**Hantera förlorad eller komprometterad nyckel**

Om du misstänker att nyckeln har gått förlorad eller har komprometterats ska du göra följande:

1. Informera certifikatutfärdaren så att de lägger till den kompromissade nyckeln i listan över återkallade certifikat för att återkalla nyckeln.
1. Hämta en ny nyckel och dess certifikat från den attesterande myndigheten.
1. Signera dokument som signerats med den kompromissade nyckeln igen med den nya nyckeln.

