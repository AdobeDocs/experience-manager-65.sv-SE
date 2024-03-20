---
title: Hantera lokala autentiseringsuppgifter
description: Lär dig hur du hanterar lokala autentiseringsuppgifter med pålitlighetslagerhanteringen. AEM formulär har stöd för RSA- och DSA-referenser i PKCS12-standardformulär.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Hantera lokala autentiseringsuppgifter {#managing-local-credentials}

Lokala autentiseringsuppgifter är privata nyckelautentiseringsuppgifter som lagras i Trust Store Management. A *lokal autentisering* används för att identifiera var användarens DES-autentiseringsuppgifter lagras. Med Trust Store Management kan du importera och hantera dina lokala inloggningsuppgifter med exempelvis befintliga PFX-filer så att du kan importera, redigera och ta bort lokala inloggningsuppgifter.

AEM har stöd för RSA- och DSA-referenser på upp till 4 096 bitar i det vanliga PKCS12-formatet (.pfx- och .p12-filer).

Du kan importera och exportera valfritt antal autentiseringsuppgifter. Om du vill ersätta en inloggningsinformation som har gått ut med samma alias tar du bort inloggningsinformationen och importerar sedan den nya inloggningsinformationen med samma alias.

Mer information och instruktioner om Acrobat Reader DC Extensions finns i [Konfigurera autentiseringsuppgifter för användning med Acrobat Reader DC Extensions](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importera en autentiseringsuppgift {#import-a-credential}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på Importera. Välj något av följande alternativ under Pålitlig lagringstyp:

   * **Dokumentsigneringsbehörighet:** En autentiseringsuppgift som används för att utfärda en digital signatur i ett dokument.
   * **Acrobat Reader DC Extensions Credential:** Ett digitalt certifikat som är specifikt för Acrobat Reader DC Extensions och som gör det möjligt att aktivera Adobe Reader användarrättigheter i de PDF-dokument som skapas.
   * **Standard:** Anger att det här är standardautentiseringsuppgifter som används med Acrobat Reader DC Extensions.

   Mer information om hur du hämtar en inloggningsinformation finns i [Förbereder installation av AEM formulär](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. Ange en identifierare för autentiseringsuppgifterna i rutan Alias. Den här identifieraren används som visningsnamn för autentiseringsuppgifterna i Acrobat Reader DC Extensions och Signature service. Det här aliaset används även för att få åtkomst till autentiseringsuppgifter via programmering med AEM formulär SDK.

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
1. Klicka på Exportera, följ instruktionerna så att du kan exportera inloggningsuppgifterna och klicka sedan på OK.

## Redigera en autentiseringsuppgiftens alias eller förtroendearkivtyp {#edit-a-credential-s-alias-or-trust-store-type}

När en autentiseringsuppgift har importerats kan du redigera dess aliasnamn och typ av förtroendearkiv.

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på aliasnamnet för den inloggningsinformation som du vill redigera.
1. Klicka på Uppdatera autentiseringsuppgifter.
1. Redigera aliasnamnet och förtroendearkivets typ efter behov och klicka på OK.

## Ta bort en autentiseringsuppgift {#delete-a-credential}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Markera kryssrutorna för de autentiseringsuppgifter som ska tas bort.
1. Klicka på Ta bort och sedan på OK.
