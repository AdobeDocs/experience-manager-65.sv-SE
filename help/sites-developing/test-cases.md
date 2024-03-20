---
title: Definiera testfall
description: Dina testfall ska baseras på användningsfall och detaljerade kravspecifikationer
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Definiera testfall{#defining-your-test-cases}

Dina testfall ska baseras på följande:

**Användningsexempel**

* Dessa definierar den funktionalitet som krävs för interaktionen mellan Actors (roller som initierar vissa åtgärder) och systemet.
* Användningsärenden ska definieras av kunden.

**Detaljerad kravspecifikation**

* Alla funktions- och prestandakrav bör testas.

Provningarna bör tydligt definiera

* Förutsättningar; dessa kan omfatta specifika system, konfigurationer eller provningsupplevelser.
* Steg som ska följas, på lämplig detaljnivå.
* Förväntade resultat.
* Tydliga kriterier för godkännande eller fel.

Möjligheten att automatisera testfall är attraktiv eftersom man slipper repetitiva arbetsmoment.

## Manuella eller automatiserade tester {#manual-versus-automated-tests}

Automatisering av testfall är dock en betydande investering, så vissa aspekter bör beaktas:

* Kräv tid, arbete och erfarenhet för att konfigurera och konfigurera.
* Om webbläsarbaserade uppdateringar är installerade finns det en ökad risk för problem, vilket kräver ytterligare tid för att korrigera.
* Endast möjligt för stora projekt.
* Bra när flera releaser genereras antingen för testning eller i den långsiktiga releasen.

## Testa specifika aspekter {#testing-specific-aspects}

När AEM testas är det av särskilt intresse med vissa detaljer:

**Skapa och publicera miljöer**

Även om det ingår i [Miljö](/help/sites-developing/the-basics.md#environments)är det värt att betona en avgörande faktor AEM testning.

AEM som två program:

* den *Upphovsman* miljö Den här instansen tillåter författare att ange och publicera innehåll.
Detta har en liten(er), förutsägbar uppsättning användare, för vilka specifika funktioner och prestanda är avgörande.

* den *Publicera* miljö Den här instansen visar webbplatsen i dess publicerade form så att besökarna kan komma åt den.
Detta har vanligtvis en större uppsättning användare, där trafikvolymen inte alltid är helt förutsägbar. Prestanda är fortfarande avgörande - vid svar på förfrågningar. Överväg även cachning och lastbalansering.

Även om de är samma programvara:

* har olika syften
* har olika krav på funktionalitet och prestanda
* har konfigurerats på ett annat sätt
* justeras separat
* var och en har en egen uppsättning godkännandetester

Med andra ord måste de testas separat och med olika testfall.

**Personalisering**

Vid testning av personalisering ska varje enskilt användningsfall upprepas med hjälp av flera användarkonton för att bevisa beteendet.

Kontrollera även att cachning fungerar korrekt.

**Dispatcher**

I de flesta projekt installeras Dispatcher för cachelagring och belastningsutjämning.

Testningen är svår (cachelagring sker på olika nivåer och på olika platser) och måste göras i svarta lådor. Viktiga aspekter att testa:

* **Noggrannhet**
Ser till att webbplatsbesökaren kan se innehållsuppdateringar.

* **Kontinuitet**
Kontrollera att webbplatsen fortfarande är tillgänglig när en server stängs av.

* **Kluster**
Används för att tillhandahålla följande:

   * **Redundans**
Om en server inte fungerar tar andra servrar i klustret över bearbetningen.

   * **Prestanda**
Belastningsutjämning med fullständig failover ökar prestanda för ett kluster.
När det används för ett kundprojekt måste klustret testas för att bekräfta att konfigurationen fungerar korrekt.

## Testar program från tredje part {#testing-third-party-software}

Alla tredjepartsprogram som AEM interagerar med kommer att anges i Detaljerade kravspecifikationer.

Alla provningar som krävs (beroende på det definierade omfånget) ska analyseras och rena provningar utföras.
