---
title: Konfigurera SSL i Windows Vista
description: Lär dig hur du konfigurerar SSL i Windows Vista. Använd och kör Java Keytool för att generera SSL-certifikatet med RSA-nycklar för autentiseringen.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Konfigurera SSL i Windows Vista {#configuring-ssl-on-windows-vista}

Om du vill konfigurera SSL på Windows Vista™ behöver du ett SSL-certifikat med RSA-nycklar för autentisering. Du kan använda Java-nyckelverktyget för att skapa certifikatet.

>[!NOTE]
>
>Windows Vista fungerar inte med DSA-nycklar.

Du kan köra nyckelverktyget med ett enda kommando som innehåller all information som krävs för att skapa certifikatet och nyckelbehållaren.

**Skapa ett SSL-certifikat**

1. I en kommandotolk går du till *`[JAVA HOME]`*/bin och skriver följande kommando för att skapa certifikatet och nyckelbehållaren:

   `keytool -genkey -keyalg RSA -dname "CN=`*Värdnamn* `, OU=`*Gruppnamn* `, O=`*Företagsnamn* `,L=`*Ortnamn* `, S=`*Delstat* `, C=`*Landskod* `" -alias`*&quot;LC-certifikat&quot;* `-keypass` `key`*_* *password* `-keystore`*key. storename* `.keystore`

   >[!NOTE]
   >
   >Ersätt *`[JAVA_HOME]`med katalogen där JDK är installerat och ersätt texten i kursiv stil med värden som motsvarar din miljö.*

1. Skriv `changeit` som lösenord. Det här lösenordet är standard för en Java-installation och systemadministratören kan ha ändrat det.
