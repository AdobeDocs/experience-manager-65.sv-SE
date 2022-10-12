---
title: Dokumentskydd
seo-title: Security
description: Programsäkerhet startar under utvecklingsfasen
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Dokumentskydd{#security}

Programsäkerhet startar under utvecklingsfasen. Adobe rekommenderar att du tillämpar följande bästa säkerhetspraxis.

## Använd begärandesession {#use-request-session}

I enlighet med principen om lägsta behörighet rekommenderar Adobe att all databasåtkomst görs genom att använda den session som är bunden till användarens begäran och rätt åtkomstkontroll.

## Protect mot XSS (Cross-Site Scripting) {#protect-against-cross-site-scripting-xss}

Med XSS (Cross-site scripting) kan angripare lägga in kod på webbsidor som visas av andra användare. Säkerhetsluckan kan utnyttjas av skadliga webbanvändare för att kringgå åtkomstkontroller.

AEM tillämpar principen om att filtrera allt innehåll som användaren tillhandahåller vid utskrift. Förhindrande av XSS har högsta prioritet under både utveckling och testning.

Den XSS-skyddsmekanism som tillhandahålls av AEM bygger på [AntiSamy Java Library](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) tillhandahålls av [OWASP (Open Web Application Security Project)](https://www.owasp.org/). Standardkonfigurationen för AntiSamy finns på

`/libs/cq/xssprotection/config.xml`

Det är viktigt att du anpassar den här konfigurationen efter dina egna säkerhetsbehov genom att täcka över konfigurationsfilen. Tjänstemannen [AntiSamy-dokumentation](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ger dig all information du behöver för att kunna uppfylla säkerhetskraven.

>[!NOTE]
>
>Vi rekommenderar att du alltid har tillgång till XSS-skydds-API:t med [XSSAPI tillhandahålls av AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Dessutom en brandvägg för webbprogram, som [mod_security för Apache](https://www.modsecurity.org), kan ge tillförlitlig, central kontroll över distributionsmiljöns säkerhet och skydda mot tidigare oidentifierade serveröverskridande skriptattacker (cross-site scripting).

## Tillgång till Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Åtkomstkontrollistorna för Cloud Service Information och de OSGi-inställningar som krävs för att skydda instansen automatiseras som en del av [Produktionsklar läge](/help/sites-administering/production-ready.md). Detta innebär att du inte behöver göra konfigurationsändringarna manuellt, men vi rekommenderar ändå att du granskar dem innan du publicerar distributionen.

När du [integrera AEM med Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) du använder [Konfigurationer av Cloud Service](/help/sites-developing/extending-cloud-config.md). Information om dessa konfigurationer, tillsammans med all statistik som samlas in, lagras i databasen. Vi rekommenderar att du, om du använder den här funktionen, granskar om standardsäkerheten för den här informationen matchar dina krav.

Webbtjänsternas supportmodul skriver statistik och konfigurationsinformation under:

`/etc/cloudservices`

Med standardbehörigheter:

* Författarmiljö: `read` for `contributors`

* Publiceringsmiljö: `read` for `everyone`

## Protect mot attacker från smidda förfrågningar på olika webbplatser {#protect-against-cross-site-request-forgery-attacks}

Mer information om AEM säkerhetsmekanismer som används för att mildra CSRF-attacker finns i [Sling-referensfilter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) i checklistan och [Dokumentation för CSRF Protection Framework](/help/sites-developing/csrf-protection.md).
