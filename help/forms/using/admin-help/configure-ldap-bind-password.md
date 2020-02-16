---
title: Konfigurera LDAP-lösenordet för bindning
seo-title: Konfigurera LDAP-lösenordet för bindning
description: Lär dig hur du konfigurerar fältet för bind-lösenord innan du importerar konfigurationsfilen till ett annat system.
seo-description: Lär dig hur du konfigurerar fältet för bind-lösenord innan du importerar konfigurationsfilen till ett annat system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera LDAP-lösenordet för bindning{#configure-the-ldap-bind-password}

För att undvika säkerhetsrisker har fältet för bind-lösenord i den exporterade konfigurationsfilen (config.xml) inte konfigurerats. Innan du importerar konfigurationsfilen till ett annat system måste du konfigurera lösenordet. Det här lösenordet åsidosätter ett befintligt lösenord som lagras i databasen. Ett null-lösenord åsidosätter inte ett befintligt lösenord som inte är null.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler.
1. Om du vill exportera den aktuella konfigurationsinställningen till en fil klickar du på Exportera och sparar konfigurationsfilen på en annan plats.
1. Leta upp `Domains` > *[Domännamn]* > `DirectoryConfigs` > `LDAPGroupConfig` i filen. Här är ett exempel:

   ```as3
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Ange ett värde för `bindpassword` och spara ändringarna.

1. I filen letar du upp `Domains` > *[Ditt domännamn]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` -noden. Här är ett exempel:

   ```as3
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Ange ett värde för `bindpassword` och spara ändringarna.

1. Om du vill importera den uppdaterade filen klickar du i Användarhantering på Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Bläddra för att hitta filen, klicka på Importera och sedan på OK.

