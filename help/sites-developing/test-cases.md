---
title: Definiera testfall
seo-title: Definiera testfall
description: Dina testfall ska baseras på användningsfall och detaljerade kravspecifikationer
seo-description: Dina testfall ska baseras på användningsfall och detaljerade kravspecifikationer
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
translation-type: tm+mt
source-git-commit: da08613be784f43ad3e3c3652b7e015640a48a9d

---


# Definiera testfall{#defining-your-test-cases}

Dina testfall ska baseras på följande:

**Användningsexempel**

* Dessa definierar den funktionalitet som krävs för interaktionen mellan Actors (roller som initierar vissa åtgärder) och systemet.
* Användningsärenden ska definieras av kunden.

**Detaljerad kravspecifikation**

* Alla funktions- och prestandakrav bör testas.

Provningarna bör tydligt definiera

* Förutsättningar. dessa kan omfatta specifika system, konfigurationer eller provningsupplevelser.
* Steg som skall följas. på en lämplig detaljnivå.
* Förväntade resultat.
* Tydliga kriterier för godkännande eller fel.

Möjligheten att automatisera testfall är uppenbart attraktiv eftersom den kan eliminera repetitiva uppgifter.

## Manuella eller automatiserade tester {#manual-versus-automated-tests}

Automatisering av testfall är dock en betydande investering, så vissa aspekter bör beaktas:

* Kräv tid, arbete och erfarenhet för att konfigurera och konfigurera.
* Om webbläsarbaserade uppdateringar är installerade finns det en ökad risk för problem. behöver ytterligare tid för att korrigera.
* Det är bara praktiskt för stora projekt.
* Bra när flera releaser genereras antingen för testning eller i den långsiktiga releaseplanen.

## Testa specifika aspekter {#testing-specific-aspects}

Vid testning av AEM är några specifika detaljer av särskilt intresse:

**Skapa och publicera miljöer**

Även om det ingår i [miljöer](/help/sites-developing/the-basics.md#environments) är det värt att betona en avgörande faktor för AEM när det gäller testning.

Du måste tänka på AEM som två program:

* i *redigeringsmiljönDen här instansen* tillåter författare att ange och publicera innehåll.
Detta har en liten(er), förutsägbar uppsättning användare, för vilka specifika funktioner och prestanda är avgörande.

* i *publiceringsmiljön* Den här instansen presenterar webbplatsen i dess publicerade form så att besökarna kan komma åt den.
Detta har vanligtvis en större uppsättning användare, där trafikvolymen inte alltid är helt förutsägbar. Prestanda är fortfarande avgörande - vid svar på förfrågningar. Cachelagring och lastbalansering måste också beaktas.

Även om de är samma programvara:

* har olika syften
* har olika krav på funktionalitet och prestanda
* har konfigurerats på ett annat sätt
* justeras separat
* ska var och en ha sin egen uppsättning godkännandetester

Med andra ord måste de testas separat och med olika testfall.

**Personalisering**

Vid testning av personalisering ska varje enskilt användningsfall upprepas med flera användarkonton för att bevisa beteendet.

Cachelagring måste också kontrolleras för korrekt beteende.

**Dispatcher**

I de flesta projekt installeras Dispatcher för cachelagring och belastningsutjämning.

Testningen är svår (cachelagring sker på olika nivåer och på olika platser) och måste göras i svarta lådor. Viktiga aspekter att testa för är:

* **Noggrannheten** säkerställer att webbplatsens besökare kan se innehållsuppdateringarna.

* **Kontinuitet** säkerställer att webbplatsen fortfarande är tillgänglig när en server stängs av.

* **Klusterkluster** används för att tillhandahålla:

   * **Redundans** Om en server misslyckas tar andra servrar i klustret över bearbetningen.

   * **Prestandabelastningsbalansering med fullständig failover ökar prestanda för ett kluster.**
När det används för ett kundprojekt måste klustret testas för att bekräfta att konfigurationen fungerar korrekt.

## Testar program från tredje part {#testing-third-party-software}

Alla tredjepartsprogram som interagerar med AEM beskrivs i Detaljerade kravspecifikationer.

Alla provningar som krävs (beroende på det definierade omfånget) ska analyseras och rena provningar utföras.
