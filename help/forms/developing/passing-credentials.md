---
title: Skicka inloggningsuppgifter med WS-security headers
description: Lär dig hur du skickar inloggningsuppgifter med WS-security headers
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Skicka inloggningsuppgifter med WS-Security-huvuden {#using-execute-script-service-aem-forms-jee-workbench}

När du anropar en AEM Forms på JEE-tjänst med hjälp av webbtjänster kan du använda WS-Security-huvuden för att skicka klientautentiseringsinformation som AEM Forms kräver på JEE. WS-Security definierar SOAP tillägg som implementerar klientautentisering, meddelandesekretess och meddelandeintegritet. Det innebär att du kan anropa AEM Forms på JEE-tjänster när AEM Forms på JEE distribueras som en fristående server eller i en klustrad miljö.

Hur du skickar WS-Security-huvuden till AEM Forms på JEE beror på om du använder axelgenererade Java-klasser eller en .NET-klientsammansättning som använder en SOAP.

>[!NOTE]
>
>Som ett exempel på hur en tjänst anropas med WS-Security headers krypterar det här avsnittet ett PDF-dokument med ett lösenord genom att anropa krypteringstjänsten.

Det här dokumentet innehåller följande ämnen:

* Skicka klientautentisering med axelgenererade Java-klasser

* Genererar axelbiblioteksfiler som krävs för att anropa krypteringstjänsten

* Anropa krypteringstjänsten med ett WS-Security-huvud

* Klientautentisering skickas med en .NET-klientsammansättning

* Anropa krypteringstjänsten med ett WS-Security-huvud


## Krav {#requirements}

För att få ut det mesta av det här dokumentet måste du ha en god förståelse för AEM Forms om JEE.

>[!MORELIKETHIS]
>
>* [Skicka autentiseringsuppgifter med WS-Security-huvuden](assets/passing-credentials-using-ws-security-headers.pdf)
