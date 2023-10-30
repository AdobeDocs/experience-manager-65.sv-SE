---
title: Konfigurera SSL i Windows Vista
description: Lär dig hur du konfigurerar SSL i Windows Vista. Använd och kör Java Keytool för att generera SSL-certifikatet med RSA-nycklar för autentiseringen.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Konfigurera SSL i Windows Vista {#configuring-ssl-on-windows-vista}

Om du vill konfigurera SSL på Windows Vista™ behöver du ett SSL-certifikat med RSA-nycklar för autentisering. Du kan använda Java-nyckelverktyget för att skapa certifikatet.

>[!NOTE]
>
>Windows Vista fungerar inte med DSA-nycklar.

Du kan köra nyckelverktyget med ett enda kommando som innehåller all information som krävs för att skapa certifikatet och nyckelbehållaren.

**Skapa ett SSL-certifikat**

1. I en kommandotolk går du till *`[JAVA HOME]`*/bin och skriv följande kommando för att skapa certifikatet och nyckelbehållaren:

   `keytool -genkey -keyalg RSA -dname "CN=`*Värdnamn* `, OU=`*Gruppnamn* `, O=`*Företagsnamn* `,L=`*Ortsnamn* `, S=`*Läge* `, C=`*Landskod* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *lösenord* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Ersätt *`[JAVA_HOME]`med den katalog där JDK är installerat och ersätt texten i kursiv stil med värden som motsvarar din miljö.*

1. Typ `changeit` som lösenord. Det här lösenordet är standard för en Java-installation och systemadministratören kan ha ändrat det.
