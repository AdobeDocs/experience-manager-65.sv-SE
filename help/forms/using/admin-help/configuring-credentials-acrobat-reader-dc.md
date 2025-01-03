---
title: Konfigurera autentiseringsuppgifter för användning med Acrobat Reader DC Extensions
description: Lär dig hur du konfigurerar autentiseringsuppgifter för användning med Acrobat Reader DC Extensions.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Konfigurera autentiseringsuppgifter för användning med Acrobat Reader DC Extensions{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Om du vill lägga in användarrättigheter i PDF-dokument konfigurerar du AEM formulär med en giltig inloggningsinformation för Acrobat Reader DC Extensions. En autentiseringsuppgift kan ha konfigurerats under installationen av AEM formulär. Om du inte konfigurerade dina autentiseringsuppgifter för Acrobat Reader DC Extensions när du kör Configuration Manager eller, om du behöver importera en ny eller ersättande autentiseringsuppgift, kan du göra det med hjälp av hanteringssidorna i Trust Store.

Om du använder en utvärderingsreferens ersätter du den med en produktionsautentiseringsuppgift när du flyttar till produktionsmiljön. Om du vill uppdatera en inloggningsinformation som har gått ut eller utvärdera den tar du först bort den gamla Acrobat Reader DC Extensions-autentiseringen.

Mer information om hur du hämtar autentiseringsuppgifter finns i [Förbereder för att installera AEM formulär (en server)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

Trust Store kan innehålla fler än en Acrobat Reader DC Extensions-autentiseringsuppgift. Ange en av dessa autentiseringsuppgifter som standardautentiseringsuppgifter för Reader Extensions. Standardautentiseringsuppgifterna används när en Workbench-användare inte kan avgöra vilka autentiseringsuppgifter som ska användas när processen skapas. Dessa regler gäller för standardautentiseringsuppgifter:

* Om du importerar en Acrobat Reader DC Extensions-autentiseringsuppgift och Trust Store inte innehåller några andra Acrobat Reader DC Extensions-autentiseringsuppgifter, anges den som standard.
* Om du importerar en autentiseringsuppgift för Acrobat Reader DC Extensions med standardalternativet markerat tas standardtypen bort från en befintlig standardautentiseringsuppgift. De importerade autentiseringsuppgifterna blir standard.
* Du kan inte ta bort en standardautentiseringsuppgift för Acrobat Reader DC Extensions. Om du vill ta bort standardautentiseringsuppgifterna anger du först en annan autentiseringsuppgift som standard. Ett undantag till den här regeln är att om det bara finns en autentiseringsuppgift kan du ta bort den även om den är standard.
* Du kan inte uppdatera Acrobat Reader DC Extensions-standardautentiseringsuppgifter.

>[!NOTE]
>
>Du kan också importera och ta bort autentiseringsuppgifter via programmering. (Se [Programmera med AEM formulär](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html).)

## Importera autentiseringsuppgifter för Acrobat Reader DC Extensions {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på Importera och välj Acrobat Reader DC Extensions Credential under Pålitlig lagringstyp.
1. (Valfritt) Om du vill ange att den här autentiseringsuppgiften är standardautentiseringsuppgiften som används med Acrobat Reader DC Extensions väljer du Standard.
1. Ange en identifierare för autentiseringsuppgifterna i rutan Alias. Den här identifieraren används som visningsnamn för autentiseringsuppgifterna i Acrobat Reader DC Extensions. Det här aliaset används även för att få åtkomst till autentiseringsuppgifterna via programmering med hjälp av de AEM formulären SDK.

   >[!NOTE]
   >
   >Aliasnamnet konverteras automatiskt till versaler för visning. Aliasnamnet är inte skiftlägeskänsligt när du refererar till det i en process.

1. Klicka på Välj fil för att leta upp autentiseringsuppgifterna, skriv lösenordet för autentiseringsuppgifterna och klicka sedan på OK.

   Om felmeddelandet&quot;Det gick inte att importera autentiseringsuppgifter på grund av felaktigt filformat eller felaktigt lösenord&quot; visas kontrollerar du att lösenordet är giltigt.

## Ta bort autentiseringsuppgifter för Acrobat Reader DC Extensions {#remove-a-acrobat-reader-dc-extensions-credential}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Markera autentiseringsuppgifterna och klicka på Ta bort.

## Ersätta autentiseringsuppgifter för Acrobat Reader DC Extensions {#replace-a-acrobat-reader-dc-extensions-credential}

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Observera det befintliga autentiseringsuppgiftens alias, markera det och klicka sedan på Ta bort.
1. Importera de nya autentiseringsuppgifterna med exakt samma aliasnamn.
