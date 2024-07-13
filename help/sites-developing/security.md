---
title: Dokumentskydd
description: Programsäkerhet startar under utvecklingsfasen
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Dokumentskydd{#security}

Programsäkerhet startar under utvecklingsfasen. Adobe rekommenderar att du tillämpar följande bästa säkerhetspraxis.

## Använd begärandesession {#use-request-session}

I enlighet med principen om lägsta behörighet rekommenderar Adobe att all databasåtkomst görs genom att använda den session som är bunden till användarens begäran och rätt åtkomstkontroll.

## Protect mot XSS (Cross-Site Scripting) {#protect-against-cross-site-scripting-xss}

Med XSS (Cross-site scripting) kan angripare lägga in kod på webbsidor som visas av andra användare. Säkerhetsluckan kan utnyttjas av skadliga webbanvändare för att kringgå åtkomstkontroller.

AEM tillämpar principen om att filtrera allt innehåll som användaren tillhandahåller vid utskrift. Förhindrande av XSS har högsta prioritet under både utveckling och testning.

XSS-skyddsmekanismen som tillhandahålls av AEM baseras på [AntiSamy Java™ Library](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) som tillhandahålls av [OWASP (Open Web Application Security Project)](https://owasp.org/). Standardkonfigurationen för AntiSamy finns på

`/libs/cq/xssprotection/config.xml`

Det är viktigt att du anpassar den här konfigurationen efter dina egna säkerhetsbehov genom att täcka över konfigurationsfilen. Den officiella [dokumentationen för AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ger dig all information du behöver för att implementera säkerhetskraven.

>[!NOTE]
>
>Adobe rekommenderar att du alltid får tillgång till XSS-skydds-API:t med hjälp av [XSSAPI:n som tillhandahålls av AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

En brandvägg för ett webbprogram, till exempel [mod_security för Apache](https://www.modsecurity.org), kan dessutom ge tillförlitlig, central kontroll över distributionsmiljöns säkerhet och skydda mot tidigare oidentifierade serveröverskridande skriptattacker (cross-site scripting).

## Tillgång till information om Cloud Servicen {#access-to-cloud-service-information}

>[!NOTE]
>
>Åtkomstkontrollistorna för den Cloud Service-information och de OSGi-inställningar som krävs för att skydda din instans automatiseras som en del av [Produktionsklart läge](/help/sites-administering/production-ready.md). Detta innebär att du inte behöver ändra konfigurationen manuellt, men vi rekommenderar ändå att du granskar dem innan du publicerar distributionen.

När du [integrerar AEM med Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md) använder du [Cloud Service-konfigurationer](/help/sites-developing/extending-cloud-config.md). Information om dessa konfigurationer, tillsammans med all statistik som samlas in, lagras i databasen. Adobe rekommenderar att du, om du använder den här funktionen, granskar om standardsäkerheten för den här informationen matchar dina krav.

Webbtjänsternas supportmodul skriver statistik och konfigurationsinformation under:

`/etc/cloudservices`

Med standardbehörigheter:

* Författarmiljö: `read` för `contributors`

* Publish-miljö: `read` för `everyone`

## Protect mot attacker från smidda förfrågningar på olika webbplatser {#protect-against-cross-site-request-forgery-attacks}

Mer information om vilka säkerhetsmekanismer AEM använder för att mildra CSRF-attacker finns i avsnittet [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) i säkerhetschecklistan och i dokumentationen för [CSRF Protection Framework](/help/sites-developing/csrf-protection.md).
