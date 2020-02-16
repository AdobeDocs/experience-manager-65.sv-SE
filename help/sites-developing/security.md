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

---


# Dokumentskydd{#security}

Programsäkerhet startar under utvecklingsfasen. Adobe rekommenderar att du tillämpar följande bästa säkerhetspraxis.

## Använd begärandesession {#use-request-session}

Adobe rekommenderar att alla databasbehörigheter görs via den session som är bunden till användarens begäran och korrekt åtkomstkontroll, enligt principen om behörighet.

## Skydda mot XSS (Cross-Site Scripting) {#protect-against-cross-site-scripting-xss}

Med XSS (Cross-site scripting) kan angripare lägga in kod på webbsidor som visas av andra användare. Säkerhetsluckan kan utnyttjas av skadliga webbanvändare för att kringgå åtkomstkontroller.

AEM tillämpar principen att filtrera allt innehåll som användaren tillhandahåller vid utskrift. Förhindrande av XSS har högsta prioritet under både utveckling och testning.

Den XSS-skyddsmekanism som tillhandahålls av AEM baseras på [AntiSamy Java Library](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) som tillhandahålls av [OWASP (Open Web Application Security Project)](https://www.owasp.org/). Standardkonfigurationen för AntiSamy finns på

`/libs/cq/xssprotection/config.xml`

Det är viktigt att du anpassar den här konfigurationen efter dina egna säkerhetsbehov genom att täcka över konfigurationsfilen. Den officiella [dokumentationen](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) för AntiSamy ger dig all information du behöver för att kunna uppfylla dina säkerhetskrav.

>[!NOTE]
>
>Vi rekommenderar att du alltid har tillgång till XSS-skydds-API:t med hjälp av [XSSAPI:n från AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Dessutom kan en brandvägg för ett webbprogram, till exempel [mod_security för Apache](https://www.modsecurity.org), ge tillförlitlig, central kontroll över säkerheten i distributionsmiljön och skydda mot tidigare oidentifierade serveröverskridande skriptattacker (cross-site scripting).

## Åtkomst till information om molntjänster {#access-to-cloud-service-information}

>[!NOTE]
>
>Åtkomstkontrollistorna för molntjänstinformationen och de OSGi-inställningar som krävs för att skydda instansen automatiseras som en del av [produktionsklart läge](/help/sites-administering/production-ready.md). Detta innebär att du inte behöver göra konfigurationsändringarna manuellt, men vi rekommenderar ändå att du granskar dem innan du publicerar distributionen.

När du [integrerar din AEM-instans med Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) använder du konfigurationer [av](/help/sites-developing/extending-cloud-config.md)molntjänster. Information om dessa konfigurationer, tillsammans med all statistik som samlas in, lagras i databasen. Vi rekommenderar att du, om du använder den här funktionen, granskar om standardsäkerheten för den här informationen matchar dina krav.

Webbtjänsternas supportmodul skriver statistik och konfigurationsinformation under:

`/etc/cloudservices`

Med standardbehörigheter:

* Författarmiljö: `read` för `contributors`

* Publiceringsmiljö: `read` för `everyone`

## Skydda dig mot attacker med förfalskade webbplatser {#protect-against-cross-site-request-forgery-attacks}

Mer information om säkerhetsmekanismerna som AEM använder för att mildra CSRF-attacker finns i avsnittet [Sling Referrer-filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) i säkerhetschecklistan och i dokumentationen [för](/help/sites-developing/csrf-protection.md)CSRF-skyddsramverk.