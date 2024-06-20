---
title: Översikt över konfigurering av SSL
description: Lär dig hur du förbättrar kommunikationssäkerheten genom att konfigurera SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Översikt över konfigurering av SSL {#overview-of-configuring-ssl}

Du kan skapa SSL-autentiseringsuppgifter (Secure Sockets Layer) och konfigurera SSL på programservern för att förbättra säkerheten vid kommunikation med programservern.

Som säkerhetsprodukt kräver Rights Management att SSL är konfigurerat. När du konfigurerar SSL-certifikat bör du kontrollera att du bara använder RSA-nycklar. SSL-certifikat med DSA-nycklar stöds inte.

Den information som ges gäller körklara, automatiska och manuella installationer. Det innehåller ett exempel på en metod för att konfigurera SSL. Du kan också använda andra metoder som passar ditt nätverk eller din organisation bättre.

>[!NOTE]
>
>Vi rekommenderar att du slutför installation, konfiguration och distribution av dina AEM formulärmoduler och ser till att produkterna körs korrekt innan du konfigurerar SSL på programservern.

>[!NOTE]
>
>När du skapar SSL-säkerhetscertifikat och autentiseringsuppgifter använder du samma användarkontobehörighet som du använde för att köra programservern. Om programservern körs med andra användarbehörigheter kan det hända att formuläret inte återges korrekt för PDFForm-återgivningar när ContentRootURI pekar på https.

Om du har en SSL-aktiverad LDAP-server konfigurerar du användarhantering så att den fungerar med den. (Se [Konfigurera användarhantering för en SSL-aktiverad LDAP-server](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
