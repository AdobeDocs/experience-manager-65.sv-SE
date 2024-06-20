---
title: Konfigurera LDAP-lösenordet för bindning
description: Lär dig hur du konfigurerar fältet för bind-lösenord innan du importerar konfigurationsfilen till ett annat system.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
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

1. Om du vill importera den uppdaterade filen går du till Användarhantering och klickar på Konfiguration > Importera och exportera konfigurationsfiler.
1. Klicka på Bläddra för att hitta filen, klicka på Importera och sedan på OK.
