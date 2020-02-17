---
title: Översikt över konfigurering av SSL
seo-title: Översikt över konfigurering av SSL
description: Lär dig hur du förbättrar kommunikationssäkerheten genom att konfigurera SSL.
seo-description: Lär dig hur du förbättrar kommunikationssäkerheten genom att konfigurera SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Översikt över konfigurering av SSL {#overview-of-configuring-ssl}

Du kan skapa SSL-autentiseringsuppgifter (Secure Sockets Layer) och konfigurera SSL på programservern för att förbättra säkerheten vid kommunikation med programservern.

Som säkerhetsprodukt kräver Rights Management konfigurationen av SSL. När du konfigurerar SSL-certifikat bör du kontrollera att du bara använder RSA-nycklar. SSL-certifikat med DSA-nycklar stöds inte.

Den information som ges gäller körklara, automatiska och manuella installationer. Det innehåller ett exempel på en metod för att konfigurera SSL. Du kan också använda andra metoder som passar ditt nätverk eller din organisation bättre.

>[!NOTE]
>
>Vi rekommenderar att du slutför installation, konfiguration och driftsättning av dina AEM-formulärmoduler och ser till att produkterna körs korrekt innan du konfigurerar SSL på programservern.

>[!NOTE]
>
>När du skapar SSL-säkerhetscertifikat och autentiseringsuppgifter använder du samma användarkontobehörighet som du använde för att köra programservern. Om programservern körs med andra användarbehörigheter kan det hända att formuläret inte återges korrekt för PDFForm-återgivningar när ContentRootURI pekar på https.

Om du har en SSL-aktiverad LDAP-server konfigurerar du användarhantering så att den fungerar med den. (Se [Konfigurera användarhantering för en SSL-aktiverad LDAP-server](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
