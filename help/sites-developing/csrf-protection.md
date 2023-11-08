---
title: CSRF Protection Framework
description: Ramverket använder tokens för att garantera att kundens begäran är berättigad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# CSRF Protection Framework{#the-csrf-protection-framework}

Förutom referensfiltret för Apache Sling tillhandahåller Adobe även ett nytt CSRF-skyddsramverk som skyddar mot den här typen av attacker.

Ramverket använder tokens för att garantera att kundens begäran är berättigad. Token genereras när formuläret skickas till klienten och valideras när formuläret skickas tillbaka till servern.

>[!NOTE]
>
>Det finns inga token för publiceringsinstanserna för anonyma användare.

## Krav {#requirements}

### Beroenden {#dependencies}

Alla komponenter som är beroende av `granite.jquery` CSRF Protection Framework kommer automatiskt att dra nytta av beroendet. Om detta inte är fallet för någon av dina komponenter måste du deklarera ett beroende för `granite.csrf.standalone` före ramverket.

### Replikerar krypteringsnyckeln {#replicating-crypto-keys}

Om du vill använda token måste du replikera HMAC-binärfilen till alla instanser i distributionen. Se [Replikerar HMAC-nyckeln](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) för mer information.

>[!NOTE]
>
>Se också till att du gör nödvändiga [Konfigurationsändringar för Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) för att använda ramverket för skydd av CSRF.

>[!NOTE]
>
>Om du använder manifest-cachen tillsammans med webbprogrammet måste du lägga till &quot;**&amp;ast;**&quot; till manifestet för att säkerställa att token inte tar genereringsanropet för CSRF-token offline. Mer information finns i [link](https://www.w3.org/TR/offline-webapps/).
>
>Mer information om CSRF-attacker och sätt att mildra dem finns i [OWASP-sida för korsdomänbegäran](https://owasp.org/www-community/attacks/csrf).
