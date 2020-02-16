---
title: ASRP - Adobe Storage Resource Provider
seo-title: ASRP - Adobe Storage Resource Provider
description: Konfigurera AEM Communities så att en relationsdatabas används som gemensam butik
seo-description: Konfigurera AEM Communities så att en relationsdatabas används som gemensam butik
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# ASRP - Adobe Storage Resource Provider{#asrp-adobe-storage-resource-provider}

## Om ASRP {#about-asrp}

När AEM Communities har konfigurerats att använda ASRP som gemensam lagringsplats är användargenererat innehåll (UGC) tillgängligt från alla författare och publiceringsinstanser utan behov av synkronisering eller replikering.

Se även [egenskaper för SRP-alternativ](/help/communities/working-with-srp.md#characteristics-of-srp-options) och [rekommenderade topologier](/help/communities/topologies.md).

## Krav {#requirements}

Ytterligare en licens krävs för ASRP.

Om du vill konfigurera din AEM Communities-webbplats så att den använder ASRP för UGC kontaktar du din kontorepresentant för:

* URL till datacenter (adress till ASRP-slutpunkten)
* Konsumentnyckel
* Hemlig nyckel
* Rapportsvitens ID:n

Konsumentnycklarna och de hemliga nycklarna delas över alla rapporteringsprogram för ett företag. Det finns en rapportsvit per innehavare.

## Konfiguration {#configuration}

### Välj ASRP {#select-asrp}

Med konsolen [för](/help/communities/srp-config.md) lagringskonfiguration kan du välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

**I AEM Author-instans:**

* Från global navigering (Verktyg, Communities, Storage Configuration) väljer du** Adobe Storage Resource Provider (ASRP).**

![chlimage_1-30](assets/chlimage_1-30.png)

Följande information kommer från provisioneringsprocessen:

* **URL för datacenter. **Nedrullningsbar meny för att välja det produktionsdatacenter som din kontorepresentant har identifierat.
* **Standard Report Suite. **Ange namnet på standardrapportsviten.
* **Konsumentnyckel**. Ange konsumentnyckeln.
* **Hemlighet. **Ange hemligheten.
* Välj **Skicka.**

Förbered publiceringsinstanserna:

* [replikera krypteringsnyckeln](#replicate-the-crypto-key)
* [replikera konfigurationen](#publishing-the-configuration)

Testa anslutningen när konfigurationen har skickats:

* Välj **Testa konfiguration**. Testa anslutningen till datacentret från lagringskonsolen för varje författare och publiceringsinstans.

* Se till att URL:er för webbplatsen för profildata kan dirigeras från datacentret genom att [externalisera länkar](#externalize-links).

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Konsumentnyckeln och hemlig nyckel är krypterade. För att nycklarna ska kunna krypteras eller dekrypteras på rätt sätt måste huvudkrypteringsnyckeln för Granite vara vara densamma för alla AEM-instanser.

Följ instruktionerna på [Replikera krypteringsnyckeln](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Gör länkar externt {#externalize-links}

Korrigera länkarna för profil- och profilbilder genom att [konfigurera länkfunktionen](/help/sites-developing/externalizer.md).

Var noga med att ange att domänerna ska vara URL:er som är routningsbara från URL:en för datacenter (ASRP-slutpunkt).

### Tidssynkronisering {#time-synchronization}

För att autentiseringen med ASRP-slutpunkten ska lyckas måste datorerna som kör din värdbaserade AEM Communities vara tidssynkroniserade, till exempel med [NTP (Network Time Protocol)](https://www.ntp.org/).

### Publicera konfigurationen {#publishing-the-configuration}

ASRP måste identifieras som det gemensamma arkivet för alla författar- och publiceringsinstanser.

Så här gör du den identiska konfigurationen tillgänglig i publiceringsmiljön:

I AEM Author-instans:

* Navigera från huvudmenyn till `Tools > Operations > Replication.`
* Välj **Aktivera träd.**
* **Startsökväg:
**gå till /etc/socialconfig/srpc/
* Avmarkera **Endast ändrad.**
* Välj **Aktivera.**

## Uppgradera från AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Om du aktiverar ASRP på en publicerad communitywebbplats visas inte längre UGC som redan lagrats i [](/help/communities/jsrp.md)JCR, eftersom det inte finns någon synkronisering av data mellan lokal lagring och molnlagring.

**`AEM Communities Extension`**introducerades tidigare i AEM 6.0-communityn för sociala nätverk som en molntjänst. Från och med AEM 6.1 Communities behövs ingen molnkonfiguration. Välj bara ASRP från [lagringskonfigurationskonsolen](/help/communities/srp-config.md).

På grund av den nya lagringsstrukturen är det nödvändigt att följa [uppgraderingsinstruktionerna](/help/communities/upgrade.md#adobe-cloud-storage) när du uppgraderar från sociala communityn till Communities.

## Hantera användardata {#managing-user-data}

Information om *användare*, *användarprofiler* och *användargrupper* som ofta används i publiceringsmiljön finns på

* [Användarsynkronisering](/help/communities/sync.md)
* [Hantera användare och användargrupper](/help/communities/users.md)

## Felsökning {#troubleshooting}

### UGC försvinner efter uppgradering {#ugc-disappears-after-upgrade}

Om du uppgraderar från en befintlig AEM 6.0-webbplats för sociala nätverk måste du följa [uppgraderingsinstruktionerna](/help/communities/upgrade.md#adobe-cloud-storage), annars försvinner användargenererat innehåll.

### Autentiseringsfel {#authentication-errors}

Om du får autentiseringsfel mot datacenter-URL:en, och AEM error.log innehåller meddelanden om inaktuella tidsstämplar, kontrollerar du att tidssynkronisering pågår.

Använd ett verktyg som NTP ( [Network Time Protocol)](https://www.ntp.org/) för att synkronisera alla AEM-författare och publiceringsservrar.

### Nytt innehåll visas inte i sökningar {#new-content-does-not-appear-in-searches}

Adobes infrastruktur för molnlagring använder *en konsekvent* lösning för att uppnå sina mål för skalning och prestanda. Därför är nytt innehåll inte tillgängligt direkt och det tar flera sekunder innan det visas i sökresultaten.

Medan intervallet som påverkar den slutliga konsekvensen övervakas, ska du kontakta din kontorepresentant om det tar längre tid än några sekunder innan nytt innehåll visas i sökningar.

### UGC är inte synlig i ASRP {#ugc-not-visible-in-asrp}

Kontrollera att ASRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP, inte ASRP.

Gå till konsolen Lagringskonfiguration eller kontrollera AEM-databasen på alla författare och publicera AEM-instanser.

I JCR, if [/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* innehåller ingen [srpc](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) -nod, vilket betyder att lagringsprovidern är JSRP.
* Om srpc-noden finns och innehåller [standardkonfiguration](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)för noden definierar standardkonfigurationens egenskaper att ASRP är standardprovider.

