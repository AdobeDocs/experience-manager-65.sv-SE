---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Läs om hur AEM hanterar de 10 viktigaste säkerhetsriskerna i OWASP.
seo-description: Läs om hur AEM hanterar de 10 viktigaste säkerhetsriskerna i OWASP.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: cd7331f5f57ec90ea72d41d467891dc832347a3c
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# OWASP Top 10{#owasp-top}

[Open Web Application Security Project](https://www.owasp.org) (OWASP) innehåller en lista över vad de anser vara de 10 viktigaste säkerhetsriskerna för webbprogram](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).[

Dessa är listade nedan tillsammans med en förklaring av hur CRX hanterar dem.

## 1. Injektion {#injection}

* SQL - Förebyggs av design: Standarddatabaskonfigurationen innehåller ingen eller kräver en traditionell databas. Alla data lagras i innehållsdatabasen. All åtkomst är begränsad till autentiserade användare och kan endast utföras via JCR API. SQL stöds endast för sökfrågor (SELECT). Furthemore SQL har stöd för värdebindning.
* LDAP - LDAP-injektion är inte möjlig eftersom autentiseringsmodulen filtrerar indata och utför användarimporten med bind-metoden.
* OS - Ingen skalkörning utförs inifrån programmet.

## 2. XSS (Cross-Site Scripting) {#cross-site-scripting-xss}

Det allmänna begränsningsarbetet är att koda alla utdata av användargenererat innehåll med hjälp av ett XSS-skyddsbibliotek på serversidan som baseras på [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) och [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS är en topprioritering både under testning och utveckling, och eventuella problem som hittas löses (normalt) omedelbart.

## 3. Bruten autentisering och sessionshantering {#broken-authentication-and-session-management}

AEM använder ljudtekniker och beprövade autentiseringstekniker som är beroende av [Apache Jackrabbit](https://jackrabbit.apache.org/) och [Apache Sling](https://sling.apache.org/). Webbläsar-/HTTP-sessioner används inte i AEM.

## 4. Osäkra direkta objektreferenser {#insecure-direct-object-references}

All åtkomst till dataobjekt förmedlas av databasen och begränsas därför av rollbaserad åtkomstkontroll.

## 5. CSRF (Cross-Site Request Forgery) {#cross-site-request-forgery-csrf}

CSRF (Cross-Site Request Forgery) reduceras genom att en kryptografisk token automatiskt matas in i alla formulär och AJAX och denna token verifieras på servern för varje POST.

Dessutom levereras AEM med ett hänvisningsrubrikbaserat filter, som kan konfigureras till *endast* tillåter förfrågningar från POSTER från specifika värdar (definieras i en lista).

## 6. Felkonfiguration av säkerhet {#security-misconfiguration}

Det är omöjligt att garantera att all programvara alltid är korrekt konfigurerad. Vi strävar dock efter att ge så mycket vägledning som möjligt och göra konfigurationen så enkel som möjligt. Dessutom levereras AEM med [integrerade säkerhetshälsokontroller](/help/sites-administering/operations-dashboard.md) som hjälper dig att övervaka säkerhetskonfigurationen snabbt.

Läs [säkerhetschecklistan](/help/sites-administering/security-checklist.md) om du vill ha mer information som ger dig steg-för-steg-anvisningar om hur du härdar.

## 7. Osäker kryptografisk lagring {#insecure-cryptographic-storage}

Lösenord lagras som kryptografiska hashvärden i användarnoden. Som standard kan sådana noder bara läsas av administratören och användaren själv.

Känsliga data, som autentiseringsuppgifter från tredje part, lagras i krypterad form med ett FIPS 140-2-certifierat kryptografiskt bibliotek.

## 8. Det gick inte att begränsa URL-åtkomst {#failure-to-restrict-url-access}

Databasen tillåter inställning av [finstilt kornig behörighet (enligt JCR)](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) för en given användare eller grupp på en given sökväg, via åtkomstkontrollposter. Åtkomstbegränsningar används av databasen.

## 9. Otillräckligt skydd för transportskikt {#insufficient-transport-layer-protection}

Hanteras av serverkonfigurationen (använd t.ex. endast HTTPS).

## 10. Ovaliderade omdirigeringar och vidarebefordringar {#unvalidated-redirects-and-forwards}

Begränsad genom att alla omdirigeringar till destinationer som användaren anger begränsas till interna platser.

