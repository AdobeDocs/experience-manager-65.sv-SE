---
title: Konfigurera användarhantering för en SSL-aktiverad LDAP-server
seo-title: Konfigurera användarhantering för en SSL-aktiverad LDAP-server
description: Lär dig hur du konfigurerar användarhantering för en SSL-aktiverad LDAP-server så att synkroniseringen kan fungera korrekt i stället för LDAPS.
seo-description: Lär dig hur du konfigurerar användarhantering för en SSL-aktiverad LDAP-server så att synkroniseringen kan fungera korrekt i stället för LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera användarhantering för en SSL-aktiverad LDAP-server {#configure-user-management-for-an-ssl-enabled-ldap-server}

För att synkroniseringen ska fungera korrekt i stället för LDAPS måste LDAP-certifikaten som utfärdades av certifikatutfärdaren finnas i programserverns JRE (Java Runtime Environment). Importera certifikatet till programserverns JRE-cacerts-fil, som vanligtvis finns i katalogen *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Aktivera SSL på katalogservern. Mer information finns i dokumentationen från katalogleverantören.
1. Exportera ett klientcertifikat från katalogservern.
1. Använd nyckelverktygsprogrammet för att importera klientcertifikatfilen till standardcertifikatarkivet för JVM (JVM™) på AEM-formulärprogramservern. Proceduren för den här aktiviteten varierar beroende på dina JVM- och klientinstallationssökvägar. Om du till exempel använder BEA WebLogic Server med JDK 1.5 från en kommandotolk skriver du den här texten:

   `keytool -import -alias`*alias *`-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Skriv lösenordet när du uppmanas till det. (I Java är standardlösenordet `changeit`.) Ett meddelande om att certifikatet har importerats visas.
1. Ange att certifikatet är pålitligt när du uppmanas `Yes` att göra det.
1. Aktivera SSL i Användarhantering och, när du konfigurerar kataloginställningarna, välj Ja för SSL-alternativet och ändra portinställningarna därefter. Standardportnumret är 636.

>[!NOTE]
>
>Om du får problem med SSL kan du använda en LDAP-webbläsare för att kontrollera om den kan komma åt LDAP-systemet när SSL används. Om LDAP-webbläsaren inte kan få åtkomst är certifikatet eller programservern inte korrekt konfigurerad. Om LDAP-webbläsaren fungerar som den ska och du fortfarande har problem, är inte användarhanteringen korrekt konfigurerad.

