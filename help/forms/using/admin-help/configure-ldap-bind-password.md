---
title: Konfigurera LDAP-lösenordet för bindning
seo-title: Configure the LDAP bind password
description: Lär dig hur du konfigurerar fältet för bind-lösenord innan du importerar konfigurationsfilen till ett annat system.
seo-description: Learn how to configure the bind password field before you import the configuration file into another system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Konfigurera LDAP-lösenordet för bindning{#configure-the-ldap-bind-password}

För att undvika säkerhetsrisker har fältet för bind-lösenord i den exporterade konfigurationsfilen (config.xml) inte konfigurerats. Innan du importerar konfigurationsfilen till ett annat system måste du konfigurera lösenordet. Det här lösenordet åsidosätter ett befintligt lösenord som lagras i databasen. Ett null-lösenord åsidosätter inte ett befintligt lösenord som inte är null.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler.
1. Om du vill exportera den aktuella konfigurationsinställningen till en fil klickar du på Exportera och sparar konfigurationsfilen på en annan plats.
1. Leta reda på `Domains` > *[Ditt domännamn]* > `DirectoryConfigs` > `LDAPGroupConfig` nod. Här är ett exempel:

   ```xml
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

1. Leta reda på `Domains` > *[Ditt domännamn]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` nod. Här är ett exempel:

   ```xml
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
