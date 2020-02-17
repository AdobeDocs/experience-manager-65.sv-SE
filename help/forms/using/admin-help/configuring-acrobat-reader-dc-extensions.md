---
title: Konfigurera Acrobat Reader DC-tillägg för datainhämtning
seo-title: Konfigurera Acrobat Reader DC-tillägg för datainhämtning
description: Lär dig hur du konfigurerar Acrobat Reader DC-tillägg för datainhämtning.
seo-description: Lär dig hur du konfigurerar Acrobat Reader DC-tillägg för datainhämtning.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera Acrobat Reader DC-tillägg för datainhämtning {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Om användare av AEM-formulärsinstallationen använder datainhämtningsfunktionen i Content Services (Borttagen) rekommenderar vi att du skapar en roll med skrivskyddad åtkomst för dessa användare.

***Obs **!Adobe® LiveCycle® Content Services ES (utgått) är ett innehållshanteringssystem som installeras med LiveCycle. Det gör det möjligt för användarna att utforma, hantera, övervaka och optimera humancentrerade processer. Supporten för innehållstjänster (borttaget) upphör 2014-12-31. Se[Adobes livscykeldokument](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Mer information om hur du konfigurerar innehållstjänster (borttaget) finns i[Administrera innehållstjänster](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).*

För datainhämtning krävs att du tilldelar en användarroll för att få åtkomst till SampleReaderExtensionsCredential. Du kan tilldela rollen som pålitlig standardadministratör, men tänk på att den här rollen ger allmänna, icke-administrativa användare de administratörsbehörigheter som styr PKI Trust-inställningarna och hanterar PKI-autentiseringsuppgifter, vilket kan äventyra säkerheten i AEM-formulärsinstallationen i en produktionsmiljö. Vi rekommenderar att systemadministratören för AEM-formulär skapar en roll som endast ger skrivskyddad åtkomst till Trust Store och tilldelar den nya rollen till icke-administratörsanvändare som använder datainhämtning.

## Skapa en roll för datainhämtningsanvändare {#create-a-role-for-data-capture-users}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Ny roll.
1. Ange rollnamnet (t.ex. Datainsamlingsanvändare) och beskrivningen i fälten och klicka sedan på Nästa.
1. På skärmen Rollbehörigheter klickar du på Sök behörigheter och väljer sedan Läs autentiseringsuppgifter i listan över tillgängliga behörigheter.
1. Klicka på OK och sedan på Slutför.

## Tilldela datainhämtningsrollen {#assign-the-data-capture-role}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Sök.
1. Klicka på användarrollen för datainhämtning som du skapade.
1. Klicka på Sök efter användare/grupper på fliken Rollanvändare/grupper.
1. På skärmen Sök efter användare och grupper klickar du på Sök, väljer de användare som behöver användarrollen för datainhämtning och klickar sedan på OK.
1. Klicka på Spara på skärmen Redigera roll.

