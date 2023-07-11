---
title: OWASP Top 10
description: Läs om hur AEM hanterar de tio viktigaste säkerhetsriskerna i OWASP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# OWASP Top 10{#owasp-top}

The [Öppna säkerhetsprojekt för webbprogram](https://owasp.org/) (OWASP) har en lista över vad de anser vara [De 10 viktigaste säkerhetsriskerna för webbapplikationer](https://owasp.org/www-project-top-ten/).

Dessa är listade nedan tillsammans med en förklaring av hur CRX hanterar dem.

## 1. Injektion {#injection}

* SQL - Förebyggs av design: Standarddatabaskonfigurationen innehåller ingen eller kräver en traditionell databas. Alla data lagras i innehållsdatabasen. All åtkomst är begränsad till autentiserade användare och kan endast utföras via JCR API. SQL stöds endast för sökfrågor (SELECT). Dessutom har SQL stöd för värdebindning.
* LDAP - LDAP-injektion är inte möjlig eftersom autentiseringsmodulen filtrerar indata och utför användarimporten med bind-metoden.
* OS - Ingen skalkörning utförs inifrån programmet.

## 2. XSS (Cross-Site Scripting) {#cross-site-scripting-xss}

Den allmänna begränsningsmetoden är att koda alla utdata av användargenererat innehåll med hjälp av ett XSS-skyddsbibliotek på serversidan baserat på [OWASP Encoder](https://owasp.org/www-project-java-encoder/) och [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS är en topprioritering både under testning och utveckling, och eventuella problem som hittas löses (normalt) omedelbart.

## 3. Bruten autentisering och sessionshantering {#broken-authentication-and-session-management}

AEM använder ljud och beprövad verifieringsteknik, beroende på [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) och [Apache Sling](https://sling.apache.org/). Webbläsar-/HTTP-sessioner används inte i AEM.

## 4. Osäkra direkta objektreferenser {#insecure-direct-object-references}

All åtkomst till dataobjekt förmedlas av databasen och begränsas därför av rollbaserad åtkomstkontroll.

## 5. CSRF (Cross-Site Request Forgery) {#cross-site-request-forgery-csrf}

CSRF (Cross-Site Request Forgery) reduceras genom att en kryptografisk token automatiskt matas in i alla formulär och AJAX och denna token verifieras på servern för varje POST.

Dessutom levereras AEM med ett hänvisningsfiltret, som kan konfigureras till *endast* tillåt POST från specifika värdar (definieras i en lista).

## 6. Felkonfiguration av säkerhet {#security-misconfiguration}

Det är omöjligt att garantera att all programvara alltid är korrekt konfigurerad. Adobe strävar dock efter att tillhandahålla så mycket vägledning som möjligt och göra konfigurationen så enkel som möjligt. Dessutom AEM fartyg med [integrerade säkerhetshälsokontroller](/help/sites-administering/operations-dashboard.md) som hjälper dig att snabbt övervaka säkerhetskonfigurationen.

Granska [Säkerhetschecklista](/help/sites-administering/security-checklist.md) om du vill ha mer information med stegvisa anvisningar om hur du härdar.

## 7. Osäker kryptografisk lagring {#insecure-cryptographic-storage}

Lösenord lagras som kryptografiska hash-värden i användarnoden. Som standard kan sådana noder bara läsas av administratören och användaren själv.

Känsliga data, som autentiseringsuppgifter från tredje part, lagras i krypterad form med ett FIPS 140-2-certifierat kryptografiskt bibliotek.

## 8. Det gick inte att begränsa URL-åtkomst {#failure-to-restrict-url-access}

I databasen kan du ange [finstilt korniga privilegier (enligt JCR)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) för en viss användare eller grupp på en viss sökväg, via åtkomstkontrollposter. Åtkomstbegränsningar används av databasen.

## 9. Otillräckligt skydd av transportlager {#insufficient-transport-layer-protection}

Hanteras av serverkonfigurationen (använd till exempel bara HTTPS).

## 10. Ovaliderade omdirigeringar och vidarebefordringar {#unvalidated-redirects-and-forwards}

Begränsad genom att alla omdirigeringar till destinationer som användaren anger begränsas till interna platser.
