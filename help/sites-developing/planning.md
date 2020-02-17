---
title: Planering
seo-title: Planering
description: Vad du behöver veta för att planera ditt test
seo-description: Vad du behöver veta för att planera ditt test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Planering{#planning}

Det här dokumentet beskriver vad du behöver veta för att kunna planera ditt test. Dessutom bör du svara på följande frågor innan du genomför testerna:

* [Vilka testmiljöer behövs?](/help/sites-developing/test-environments.md)
* [Definiera testfall](/help/sites-developing/test-cases.md)
* [Testning - när och med vem?](/help/sites-developing/when-who.md)

## Before You Start {#before-you-start}

Innan du börjar med den faktiska analysen och definitionen av tester ska du granska följande information:

**AEM-arkitektur** - Se Grundläggande koncept för att presentera dig för arkitekturen och grundprinciperna i AEM.

**Dokumentation** - Mer information finns i avsnitten om dokumentation och Använda artiklar.

**Grundprinciper för testning** - Du bör vara medveten om de grundläggande principerna för testning av programvara och kvalitetssäkring. Du bör helst ha erfarenhet av att testa projekt.

Det finns många webbplatser, böcker och kurser som behandlar sådana principer och de kommer därför inte att behandlas i detalj i detta dokument.

**Förutsättningar att undvika** - Det största antagandet (görs regelbundet) är att din webbplats behöver betjäna miljontals förfrågningar varje dag. Under vissa omständigheter kan detta vara sant, men det kan inte antas.

Även om framtida siffror inte kan förutsägas med 100 % noggrannhet, kan du få en bra indikation genom att observera din befintliga webbplats och den trafik som används. Du kan sedan göra uppskattningar beroende på vilken faktor du förväntar dig/hoppas att trafiken kommer att öka.

**Engagemang för kvalitet** - Det är oerhört viktigt att alla som testar förblir neutrala och bara rapporterar resultaten av utförda tester.

Det är projektledarens ansvar att besluta om och initiera åtgärder beroende på resultaten.

**Bli involverad** - Även om det är projektledarens ansvar att se till att alla parter är fullt engagerade vid alla möten (status, workshops osv.) bör du också försöka att bli involverade så tidigt som möjligt i projektcykeln, inklusive informationsinsamling och kravanalysprocesser.

**Involvera kunden** - På ett liknande tema kan du försöka engagera kunden (där det är möjligt) när du definierar testfall och plan.

## Provningstyper {#types-of-tests}

Det finns olika standardklassificeringar av tester som är lämpliga att använda vid testning av ett AEM-projekt. Du bör känna till dessa för att avgöra vilken du ska använda:

>[!NOTE]
>
>De listas i sin kronologiska ordning.

**Testenheter** - tester (vanligtvis) som gjorts av utvecklingsgruppen för att säkerställa att de enskilda elementen beter sig korrekt, om än separat.

**Integrationstester** - Testar moduler när de kombineras. Dessa tester utförs efter enhetstestning, men före systemtestning.

**Röktest** - Detta är snabba och smutsiga tester som används för att bevisa att programmet körs och att det finns högnivåfunktioner. Detaljerna har inte testats.

**Funktionstester** - De används för att testa programmets funktion. En serie tester kommer att utformas för att omfatta alla funktionella detaljer, med både förväntad och oväntad och/eller felaktig inmatning.

Black-box-tester är funktionstester av en komplett enhet/komponent/modul som utförs utan kunskap om elementets interna funktion.

**Systemtester** - Dessa testar hela systemet när det har integrerats fullständigt och installerats på en lämplig plattform.

De testar funktionen i svart kartong.

**Prestandatester** - Prestandatester är avgörande vid testning av AEM.

De används för att illustrera prestanda under olika förhållanden:

* Normal

   Villkor som webbplatsen kommer att uppleva för till exempel 90 % av tiden. Om till exempel bara en del av författarna använder systemet.

* Toppvärde

   Villkor som på grund av särskilda omständigheter kommer att upplevas under en proportionellt kort tid. till exempel när alla författare använder systemet samtidigt eller när nytt innehåll publiceras och ett ökat antal besökare visar din webbplats.

* Extreme

   Kan användas för att emulera resultatprognosen när nytt, extremt intressant innehåll publiceras på din webbplats. Sedan kan en extrem topp ses, men det är inte alltid helt förutsägbart.

   Dessa omständigheter kan ibland uppstå när biljetter för särskilda evenemang görs tillgängliga eller när en eftersökt webbplats publiceras för första gången.

Resultatet används sedan för att justera programmet.

**Stresstester** - Stresstester görs för att bekräfta hur en komponent eller ett program beter sig under extrema förhållanden. Dessa tester används särskilt för att visa hur beteendet försämras, när elementet kommer att misslyckas - och hur.

**Regressionstester** - Regressionstester används för att bekräfta att funktioner som redan har befunnits i en tidigare version av programmet fortfarande fungerar korrekt.

Regressionstester är bra för automatisering (om möjligt) för att säkerställa att de kan upprepas snabbt och konsekvent.

**Godkännandetester** - Acceptanstester är en särskild kategori eftersom de används för att ange att kunden godkänner projektet.

Listan över godkännandetester kan innehålla en kombination av tester från de olika kategorierna ovan, och väljs för att kontrollera att projektet uppfyller kundens krav

Mer information finns i [Godkännande och Avregistrering](/help/sites-developing/acceptance-signoff.md) .

## Komma igång {#getting-started}

Innan du börjar med dina detaljerade testfall och testplaner kan du:

**Definiera målen** - Definiera era högnivåmål som fungerar som en startpunkt för finjustering när testningen pågår. Du vill:

* Testa funktionaliteten enligt den detaljerade kravspecifikationen.
* Testa prestanda enligt [målmått](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

bland annat.

**Samla in trafikstatistik från den befintliga webbplatsen** - Den här informationen kan extraheras från loggfilerna - mer information finns i Prestandaövervakning.

Dessa siffror ger en indikation på den aktuella trafiken (volym och spridning) på den befintliga webbplatsen och kan användas som utgångspunkt för den nya webbplatsen.

**Samla in trafikstatistik från externa webbplatser** - Om det är möjligt kan du försöka samla in trafikstatistik från andra webbplatser för jämförelse, men dessa siffror publiceras inte alltid.

**Bekräfta målmått** - Mätvärden används för att definiera kvantitativa mått för kvaliteten på webbplatsen, eftersom de representerar de prestationsmål som ska uppnås.

De bör definieras i början av projektet, tillsammans med kunden. Mer information finns i [Måttvärden](/help/sites-developing/planning.md) .
