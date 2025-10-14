---
title: ASRP - Adobe lagringsresursleverantör
description: Konfigurera AEM Communities för att använda en relationsdatabas som gemensam lagringsplats
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# ASRP - Adobe lagringsresursleverantör {#asrp-adobe-storage-resource-provider}

## Om ASRP {#about-asrp}

När AEM Communities har konfigurerats att använda ASRP som gemensam lagringsplats är användargenererat innehåll (UGC) tillgängligt från alla författare- och publiceringsinstanser utan behov av synkronisering eller replikering.

Se även [Egenskaper för SRP-alternativ](/help/communities/working-with-srp.md#characteristics-of-srp-options) och [Rekommenderade topologier](/help/communities/topologies.md).

## Krav {#requirements}

Ytterligare en licens krävs för ASRP.

Kontakta din kontorepresentant för att konfigurera din AEM Communities-webbplats så att den använder ASRP för UGC:

* URL till datacenter (adress till ASRP-slutpunkten)
* Konsumentnyckel
* Hemlig nyckel
* Rapportsvitens ID:n

Konsumentnycklarna och de hemliga nycklarna delas över alla rapporteringsprogram för ett företag. Det finns en rapportsvit per innehavare.

## Konfiguration {#configuration}

### Välj ASRP {#select-asrp}

Konsolen [Lagringskonfiguration](/help/communities/srp-config.md) tillåter val av standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

**AEM författarinstans:**

* Navigera från global navigering till **[!UICONTROL Tools > Communities > Storage Configuration]** och välj **[!UICONTROL Adobe Storage Resource Provider (ASRP)]**.

![asrp-default](assets/asrp-default.png)

Följande information kommer från provisioneringsprocessen:

* **URL för datacenter**: Dra ned för att välja det produktionsdatacenter som din kontorepresentant har identifierat.
* **Standard Report Suite**: Ange namnet på standardrapportsviten.
* **Konsumentnyckel**: Ange konsumentnyckeln.
* **Hemlighet**: Ange hemligheten.
* Välj **Skicka**.

Förbered publiceringsinstanserna:

* [Replikera krypteringsnyckeln](#replicate-the-crypto-key)
* [Replikera konfigurationen](#publishing-the-configuration)

Testa anslutningen när konfigurationen har skickats:

* Välj **Testa konfiguration**.

  Testa anslutningen till datacentret från konsolen Lagringskonfiguration för varje författare och publiceringsinstans.

* Se till att URL:er för webbplatsen för profildata kan routas från datacentret genom att [externalisera länkar](#externalize-links).

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Konsumentnyckeln och hemlig nyckel är krypterade. För att nycklarna ska kunna krypteras eller dekrypteras på rätt sätt måste den primära krypteringsnyckeln för Granite vara vara densamma för alla AEM.

Följ instruktionerna på [Replikera krypteringsnyckeln](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Gör länkar externt {#externalize-links}

Korrigera profil- och profilbildslänkar genom att [konfigurera länkfunktionen](/help/sites-developing/externalizer.md).

Var noga med att ange att domänerna ska vara URL:er som är routningsbara från URL:en för datacenter (ASRP-slutpunkt).

### Tidssynkronisering {#time-synchronization}

För att autentiseringen med ASRP-slutpunkten ska lyckas måste datorerna som kör ditt värdbaserade AEM Communities vara tidssynkroniserade, till exempel med [NTP (Network Time Protocol)](https://www.ntp.org/).

### Publicera konfigurationen {#publishing-the-configuration}

ASRP måste identifieras som det gemensamma arkivet för alla författar- och publiceringsinstanser.

Så här gör du den identiska konfigurationen tillgänglig i publiceringsmiljön:

AEM författarinstans:

* Navigera från huvudmenyn till **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
* Välj **Aktivera träd**
* **Startsökväg**: gå till `/conf/global/settings/communities/srpc/`
* Avmarkera **Endast ändrad**
* Välj **Aktivera**

## Uppgradera från AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Om du aktiverar ASRP på en publicerad communitywebbplats visas inte längre någon UGC som redan lagrats i [JCR](/help/communities/jsrp.md) eftersom det inte finns någon synkronisering av data mellan lokal lagring och molnlagring.

**`AEM Communities Extension`** introducerades tidigare i AEM 6.0 sociala communities som en molntjänst. Från och med AEM 6.1 Communities behövs ingen molnkonfiguration. Välj bara ASRP från [lagringskonfigurationskonsolen](/help/communities/srp-config.md).

På grund av den nya lagringsstrukturen är det nödvändigt att följa instruktionerna för [uppgradering](/help/communities/upgrade.md#adobe-cloud-storage) när du uppgraderar från sociala communityn till Communities.

## Hantera användardata {#managing-user-data}

Mer information om *användare*, *användarprofiler* och *användargrupper* som ofta anges i publiceringsmiljön finns på

* [Användarsynkronisering](/help/communities/sync.md)
* [Hantera användare och användargrupper](/help/communities/users.md)

## Felsökning {#troubleshooting}

### UGC försvinner efter uppgradering {#ugc-disappears-after-upgrade}

Om du uppgraderar från en befintlig AEM 6.0-social communitywebbplats måste du följa [uppgraderingsinstruktionerna](/help/communities/upgrade.md#adobe-cloud-storage), annars verkar UGC gå förlorat.

### Autentiseringsfel {#authentication-errors}

Om du får autentiseringsfel mot datacenter-URL:en, och AEM error.log innehåller meddelanden om inaktuella tidsstämplar, kontrollerar du att tidssynkronisering pågår.

Använd ett verktyg som [NTP &#x200B;](https://www.ntp.org/) (Network Time Protocol) för att synkronisera alla AEM författare- och publiceringsservrar.

### Nytt innehåll visas inte i sökningar {#new-content-does-not-appear-in-searches}

Lagringsinfrastrukturen i Adobe använder *slutlig konsekvens* för att uppnå sina mål för skalning och prestanda. Därför är nytt innehåll inte tillgängligt direkt och det tar flera sekunder innan det visas i sökresultaten.

Medan intervallet som påverkar den slutliga konsekvensen övervakas, ska du kontakta din kontorepresentant om det tar längre tid än några sekunder innan nytt innehåll visas i sökningar.

### UGC är inte synlig i ASRP {#ugc-not-visible-in-asrp}

Kontrollera att ASRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP, inte ASRP.

Gå till konsolen Lagringskonfiguration på alla författare och publicera AEM eller kontrollera AEM.

I JCR, om [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Innehåller ingen [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp)-nod, vilket betyder att lagringsprovidern är JSRP.
* Om srpc-noden finns och innehåller [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration)-noden definierar standardkonfigurationens egenskaper att ASRP är standardprovider.
