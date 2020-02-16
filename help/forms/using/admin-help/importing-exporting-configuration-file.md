---
title: Importera och exportera konfigurationsfilen
seo-title: Importera och exportera konfigurationsfilen
description: Lär dig hur du importerar och exporterar konfigurationsfilen för att redigera serverinställningar eller konfigurera en annan AEM-formulärsproduktinstans.
seo-description: Lär dig hur du importerar och exporterar konfigurationsfilen för att redigera serverinställningar eller konfigurera en annan AEM-formulärsproduktinstans.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importera och exportera konfigurationsfilen {#importing-and-exporting-the-configuration-file}

Använd sidan Manuell konfiguration för att hämta en kopia av konfigurationsinställningarna i XML-format. Inställningarna i den här filen styr alla serverinställningar. Du kan sedan redigera filen och överföra den tillbaka till servern. Du kan också använda filen för att konfigurera en annan instans av AEM-formulärsprodukten.

För att undvika säkerhetsrisker inkluderas inte det binda lösenordsvärdet för katalogservern i en exporterad konfigurationsfil. Uppdatera lösenordet i XML-filen innan du importerar filen till ett nytt system.

>[!NOTE]
>
>Om du importerar konfigurationsfilen konfigureras AEM-formulär om baserat på informationen i filen. Det är bara systemadministratörer eller konsulter som känner till AEM-formulärsprodukten och XML som bör överväga att ändra konfigurationsfilen. De kan behöva redigera konfigurationsfilen, till exempel för att konfigurera om en skadad inställning.

**Exportera konfigurationsinformationen**

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Exportera. Om du använder Microsoft Internet Explorer uppmanas du att ange var filen ska sparas. Om du använder Firefox sparas filen på skrivbordet.

**Importera konfigurationsinformation**

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Bläddra för att hitta konfigurationsfilen, klicka på Importera och sedan på OK.

