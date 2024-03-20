---
title: Konfigurera användarhantering för en SSL-aktiverad LDAP-server
description: Lär dig hur du konfigurerar användarhantering för en SSL-aktiverad LDAP-server så att synkroniseringen kan fungera korrekt i stället för LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Konfigurera användarhantering för en SSL-aktiverad LDAP-server {#configure-user-management-for-an-ssl-enabled-ldap-server}

För att synkroniseringen ska fungera korrekt i stället för LDAPS måste LDAP-certifikaten som utfärdades av certifikatutfärdaren finnas i programserverns JRE (Java Runtime Environment). Importera certifikatet till programserverns JRE-cacerts-fil, som vanligtvis finns i *[JAVA_HOME]*/jre/lib/security/cacerts-katalog.

1. Aktivera SSL på katalogservern. Mer information finns i dokumentationen från katalogleverantören.
1. Exportera ett klientcertifikat från katalogservern.
1. Använd nyckelverktygsprogrammet för att importera klientcertifikatfilen till standardcertifikatarkivet för JVM™ (Java Virtual Machine) i AEM formulärprogramserver. Proceduren för den här aktiviteten varierar beroende på dina JVM- och klientinstallationssökvägar. Om du till exempel använder BEA WebLogic Server med JDK 1.5 från en kommandotolk skriver du den här texten:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Skriv lösenordet när du uppmanas till det. (För Java är standardlösenordet `changeit`.) Ett meddelande om att certifikatet har importerats visas.
1. Skriv när du uppmanas att göra det `Yes` för att lita på certifikatet.
1. Aktivera SSL i Användarhantering och, när du konfigurerar kataloginställningarna, välj Ja för SSL-alternativet och ändra portinställningarna därefter. Standardportnumret är 636.

>[!NOTE]
>
>Om du får problem med SSL kan du använda en LDAP-webbläsare för att kontrollera om den kan komma åt LDAP-systemet när SSL används. Om LDAP-webbläsaren inte kan få åtkomst är certifikatet eller programservern inte korrekt konfigurerad. Om LDAP-webbläsaren fungerar som den ska och du fortfarande har problem, är inte användarhanteringen korrekt konfigurerad.
