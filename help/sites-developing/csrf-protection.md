---
title: CSRF Protection Framework
seo-title: CSRF Protection Framework
description: Ramverket använder tokens för att garantera att kundens begäran är berättigad
seo-description: Ramverket använder tokens för att garantera att kundens begäran är berättigad
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518
workflow-type: tm+mt
source-wordcount: '300'
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

Alla komponenter som är beroende av `granite.jquery`-beroendet drar automatiskt nytta av CSRF Protection Framework. Om detta inte är fallet för någon av dina komponenter måste du deklarera ett beroende till `granite.csrf.standalone` innan du kan använda ramverket.

### Krypteringsnyckeln replikeras {#replicating-crypto-keys}

Om du vill använda token måste du replikera binärfilen `/etc/keys/hmac` till alla instanser i distributionen. Ett praktiskt sätt att kopiera HMAC-nyckeln till alla instanser är att skapa ett paket som innehåller nyckeln och installera den via Package Manager på alla instanser.

>[!NOTE]
>
>Se till att du också gör de [konfigurationsändringar för Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) som krävs för att använda CSRF Protection Framework.

>[!NOTE]
>
>Om du använder manifestcachen med ditt webbprogram måste du lägga till &quot;**&amp;ast;**&quot; i manifestet för att vara säker på att token inte tar genereringsanropet för CSRF-token offline. Mer information finns i den här [länken](https://www.w3.org/TR/offline-webapps/).
>
>Mer information om CSRF-attacker och hur du kan mildra dem finns på [sidan Cross-Site Request Forgery OWASP](https://owasp.org/www-community/attacks/csrf).
