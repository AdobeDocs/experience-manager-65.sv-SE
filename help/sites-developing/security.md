---
title: Dokumentskydd
seo-title: Dokumentskydd
description: Programsäkerhet startar under utvecklingsfasen
seo-description: Programsäkerhet startar under utvecklingsfasen
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Dokumentskydd{#security}

Programsäkerhet startar under utvecklingsfasen. Adobe rekommenderar att du tillämpar följande bästa säkerhetspraxis.

## Använd begärandesession {#use-request-session}

I enlighet med principen om leas-behörighet rekommenderar Adobe att all databasåtkomst görs genom att använda den session som är bunden till användarens begäran och rätt åtkomstkontroll.

## Protect mot XSS (Cross-Site Scripting) {#protect-against-cross-site-scripting-xss}

Med XSS (Cross-site scripting) kan angripare lägga in kod på webbsidor som visas av andra användare. Säkerhetsluckan kan utnyttjas av skadliga webbanvändare för att kringgå åtkomstkontroller.

AEM tillämpar principen om att filtrera allt innehåll som användaren tillhandahåller vid utskrift. Förhindrande av XSS har högsta prioritet under både utveckling och testning.

XSS-skyddsmekanismen som tillhandahålls av AEM baseras på [AntiSamy Java Library](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) som tillhandahålls av [OWASP (Open Web Application Security Project)](https://www.owasp.org/). Standardkonfigurationen för AntiSamy finns på

`/libs/cq/xssprotection/config.xml`

Det är viktigt att du anpassar den här konfigurationen efter dina egna säkerhetsbehov genom att täcka över konfigurationsfilen. Den officiella [dokumentationen för AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ger dig all information du behöver för att kunna genomföra säkerhetskraven.

>[!NOTE]
>
>Vi rekommenderar att du alltid har tillgång till XSS-skydds-API:t med [XSSAPI som tillhandahålls av AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Dessutom kan en brandvägg för ett webbprogram, till exempel [mod_security för Apache](https://www.modsecurity.org), ge tillförlitlig, central kontroll över distributionsmiljöns säkerhet och skydda mot tidigare oidentifierade serveröverskridande skriptattacker (cross-site scripting).

## Åtkomst till information om Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>ACL:er för Cloud Service Information och de OSGi-inställningar som krävs för att skydda instansen automatiseras som en del av [Production Ready Mode](/help/sites-administering/production-ready.md). Detta innebär att du inte behöver göra konfigurationsändringarna manuellt, men vi rekommenderar ändå att du granskar dem innan du publicerar distributionen.

När du [integrerar din AEM med Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) använder du [Cloud Service configurations](/help/sites-developing/extending-cloud-config.md). Information om dessa konfigurationer, tillsammans med all statistik som samlas in, lagras i databasen. Vi rekommenderar att du, om du använder den här funktionen, granskar om standardsäkerheten för den här informationen matchar dina krav.

Webbtjänsternas supportmodul skriver statistik och konfigurationsinformation under:

`/etc/cloudservices`

Med standardbehörigheter:

* Författarmiljö: `read` för `contributors`

* Publiceringsmiljö: `read` för `everyone`

## Protect mot attacker av typen Cross-Site Request Attacks {#protect-against-cross-site-request-forgery-attacks}

Mer information om vilka säkerhetsmekanismer AEM använder för att mildra CSRF-attacker finns i [filtret Sling Referrer](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) i säkerhetschecklistan och [dokumentationen för CSRF-skyddsramverk](/help/sites-developing/csrf-protection.md).