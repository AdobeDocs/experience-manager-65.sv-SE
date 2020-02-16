---
title: Hantera lokala autentiseringsuppgifter
seo-title: Hantera lokala autentiseringsuppgifter
description: Lär dig hur du hanterar lokala autentiseringsuppgifter.
seo-description: Lär dig hur du hanterar lokala autentiseringsuppgifter.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera lokala autentiseringsuppgifter {#managing-local-credentials}

Lokala autentiseringsuppgifter är privata nyckelautentiseringsuppgifter som lagras i Trust Store Management. En *lokal autentiseringsuppgift* identifierar var användarens DES-autentiseringsuppgifter lagras. Med Trust Store Management kan du importera och hantera dina lokala inloggningsuppgifter med exempelvis befintliga PFX-filer så att du kan importera, redigera och ta bort lokala inloggningsuppgifter.

AEM-formulär har stöd för RSA- och DSA-autentiseringsuppgifter på upp till 4 096 bitar i det vanliga PKCS12-formatet (.pfx- och .p12-filer).

Du kan importera och exportera valfritt antal autentiseringsuppgifter. Om du vill ersätta en inloggningsinformation som har gått ut med samma alias tar du bort inloggningsinformationen och importerar sedan den nya inloggningsinformationen med samma alias.

Information och instruktioner om Acrobat Reader DC-tillägg finns i [Konfigurera autentiseringsuppgifter för användning med Acrobat Reader DC-tillägg](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importera en autentiseringsuppgift {#import-a-credential}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på Importera. Välj något av följande alternativ under Pålitlig lagringstyp:

   * **** Autentiseringsuppgifter för dokumentsignering: En autentiseringsuppgift som används för att utfärda en digital signatur i ett dokument.
   * **** Acrobat Reader DC-tillägg Autentiseringsuppgifter: Ett digitalt certifikat som är specifikt för Acrobat Reader DC-tillägg som gör det möjligt att aktivera användningsrättigheter för Adobe Reader i de PDF-dokument som skapas.
   * **** Standard: Anger att det här är standardautentiseringsuppgifter som används med Acrobat Reader DC-tillägg.
   Mer information om hur du hämtar autentiseringsuppgifter finns i [Förbereda för att installera AEM-formulär](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. Ange en identifierare för autentiseringsuppgifterna i rutan Alias. Den här identifieraren används som visningsnamn för inloggningsuppgifterna i Acrobat Reader DC-tillägg och Signature-tjänsten. Det här aliaset används även för att få åtkomst till autentiseringsuppgifter via programmering med AEM-formulärens SDK.

   >[!NOTE]
   >
   >Aliasnamnet konverteras automatiskt till versaler för visning. Aliasnamnet är inte skiftlägeskänsligt när du refererar till det i en process.

1. Klicka på Bläddra för att hitta autentiseringsuppgifterna, skriv lösenordet för autentiseringsuppgifterna och klicka sedan på OK.

   Om felmeddelandet&quot;Det gick inte att importera autentiseringsuppgifter på grund av felaktigt filformat eller felaktigt lösenord&quot; visas kontrollerar du att lösenordet är giltigt.

## Exportera en autentiseringsuppgift {#export-a-credential}

Autentiseringsuppgifterna exporteras som P12-filer i PKCS#12-format.

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på aliasnamnet för de autentiseringsuppgifter som du vill exportera och klicka sedan på Exportera.
1. Skriv lösenordet i rutan Lösenord. Det här lösenordet är nytt och används för att kryptera de exporterade autentiseringsuppgifterna.
1. Klicka på Exportera, följ instruktionerna för att exportera inloggningsuppgifterna och klicka sedan på OK.

## Redigera en autentiseringsuppgiftens alias eller förtroendearkivtyp {#edit-a-credential-s-alias-or-trust-store-type}

När en autentiseringsuppgift har importerats kan du redigera dess aliasnamn och typ av förtroendearkiv.

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på aliasnamnet för de autentiseringsuppgifter som du vill redigera.
1. Klicka på Uppdatera autentiseringsuppgifter.
1. Redigera aliasnamnet och förtroendearkivets typ efter behov och klicka på OK.

## Ta bort en autentiseringsuppgift {#delete-a-credential}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Markera kryssrutorna för de autentiseringsuppgifter som ska tas bort.
1. Klicka på Ta bort och sedan på OK.

