---
title: Hantera certifikat
seo-title: Hantera certifikat
description: Lär dig hur du importerar och exporterar ett certifikat och redigerar dess pålitlighetsinställningar.
seo-description: Lär dig hur du importerar och exporterar ett certifikat och redigerar dess pålitlighetsinställningar.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera certifikat {#managing-certificates}

Med pålitlighetslagerhanteringen kan du importera, redigera och ta bort certifikat som du litar på på servern för validering av digitala signaturer och certifikatautentisering. Du kan importera och exportera valfritt antal certifikat. När ett certifikat har importerats kan du redigera pålitlighetsinställningarna och förtroendearkivets typ. Tänk på följande alternativ när du kombinerar typer av förtroendearkiv:

* **** Förtroende för certifikatautentisering med certifikatutfärdare: För CRL-validering väljer du även Lita på för identitet.
* **** Förtroende för certifikatautentisering med ICA: Välj endast Lita på identitet. En ICA ska inte vara betrodd för certifikatautentisering. Om du litar på ICA för certifikatautentisering blir ICA en certifikatutfärdare för sökvägsuppbyggnad. Om ICA är betrott för både certifikatautentisering och identitet ignoreras certifikatutfärdarens leverantörscertifikat eftersom ICA blir certifikatutfärdare.
* **** Förtroende för OCSP Server med HTTP: Om OSCP-respondentservern finns på en HTTP-plats måste du även välja Lita på SSL-anslutningar. Om OSCP-svaranden kräver CRL-validering måste du även välja Lita på identitet.
* **** Adobe Root: Välj inte SSL-anslutningar eller OCSP Server Trust Store-typer. Adobe Root är inte betrodd för SSL-anslutningar och OCSP Server. Adobe utfärdar inte OCSP- eller SSL-certifikat. Adobe Root är implicit tillförlitligt med alias name=&quot;ADOBEROT&quot;.

Endast X509v3-certifikat stöds. Den här certifikattypen kan anges i en binär DER-kodad fil (.cer-fil) eller en textfil som innehåller en Base64-kodad version av samma DER-kodade certifikat (inklusive X509-certifikat i PEM-format (Privacy Enhanced Mail)).

Certifikat som krävs för att slutföra en signaturverifiering måste finnas i samma arkiv (HSM eller databas).

Du kan också importera och ta bort certifikat med Trust Manager API. Mer information finns i&quot;Importera certifikat med Trust Manager API&quot; och&quot;Ta bort certifikat med Trust Manager API&quot; i [Programmering med AEM-formulär](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importera ett certifikat {#import-a-certificate}

1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Lita på arkivhantering > Certifikat]**.
1. Klicka på Importera och välj något av följande alternativ under Pålitlig lagringstyp:

   * **** Lita på SSL-anslutningar: Anger att AEM-formulär kan använda certifikat för att ansluta till externa system via SSL.
   * **** Lita på att certifiera signatur: Anger att certifikat är pålitliga i dokumentsigneringsåtgärder för certifikatförfattare som har digitala signaturer.
   * **** Lita på signatur: Anger att certifikat är betrodda i dokumentsigneringsåtgärder för digitala signaturer som inte är författare.
   * **** Förtroende för certifikatautentisering: Anger att AEM-formulär använder certifikat för autentisering av användare med certifikat eller smartkortsautentisering.
   * **** Förtroende för OCSP Server: Anger att AEM-formulär kan använda certifikat för att ansluta till externa OCSP-svarare
   * **** Lita på identitet: Anger att certifikat kan användas för att lita på annan information än de som anges ovan.
   >[!NOTE]
   >
   >Förtroendearkivet litar implicit på ett Adobe-rotcertifikat för certifikatautentisering, signatur, certifikatsignatur och identitet.

1. Ange certifikatets identifierare i rutan Alias.
1. Klicka på **[!UICONTROL Bläddra]** för att hitta certifikatet och klicka sedan på **[!UICONTROL OK]**.

## Exportera ett certifikat {#export-a-certificate}

1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Lita på arkivhantering > Certifikat]**.
1. Klicka på aliasnamnet för det certifikat som ska exporteras. Sidan **[!UICONTROL Certifikatinformation]** visas.
1. Klicka på **[!UICONTROL Exportera]**, följ instruktionerna för att exportera certifikatet och klicka sedan på **[!UICONTROL OK]**.

## Redigera pålitlighetsinställningar och förtroendearkivets typ {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Lita på arkivhantering > Certifikat]**.
1. Klicka på aliasnamnet för det certifikat som ska redigeras.
1. Klicka på **[!UICONTROL Uppdatera certifikat]**.
1. Om du vill ändra certifikatets aliasnamn skriver du ett nytt namn i rutan Alias.
1. Välj lämplig typ av förtroendearkiv om du vill uppdatera certifikatets typ av förtroendearkiv.
1. Om du vill uppdatera principbegränsningarna skriver du principinformationen i rutan Certifikatprofiler och klickar sedan på **[!UICONTROL OK]**.

## Ta bort ett certifikat {#delete-a-certificate}

1. I administrationskonsolen klickar du på **[!UICONTROL Inställningar > Lita på arkivhantering > Certifikat]**.
1. Markera kryssrutorna för de certifikat som ska tas bort, klicka på **[!UICONTROL Ta bort]** och sedan på **[!UICONTROL OK]**.

