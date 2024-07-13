---
title: Testar mobilappar
description: Lär dig hur du automatiserar eller manuellt testar dina mobilappar med olika verktyg.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Testar mobilappar{#testing-mobile-apps}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Med tanke på det stora utbudet av enheter på marknaden och de enheter som släpps har testning av apparna blivit avgörande. Det här är ett område där funktionalitet och användbarhet kan ge låga granskningar i en appbutik, men ett enda fel kan leda till att appen avinstalleras. Var försiktig med testningsplaner och kvalitetssäkring. Följande länk täcker många av de ämnen som måste behandlas i allmänhet, t.ex. att identifiera din miljö, definiera testfall, testtyper, antaganden och kundens medverkan. De verktyg som är till hjälp vid testningen beskrivs också. Interna verktyg, som [Hobbes](/help/sites-developing/hobbes.md), kan vara till hjälp vid webbaserad gränssnittstestning. [Med Dag](/help/sites-developing/tough-day.md) kan du stressa dina instanser med en simulerad belastning. Om din testmiljö redan har erfarenhet av tredjepartsverktyg, som Selenium, kan även dessa användas.

När du utvecklar en mobilapp finns det många nya problem som är specifika för enheter som måste hanteras tillsammans med traditionella testningar.

* Funktionell - Uppfyller appen alla krav?
* Användbarhet - Är appen enkel att använda och förstå för kunden?
* Prestanda - Vad händer under en plötslig användning? Är appelementen, som svepningar och carousel, snabba och minskar inte upplevelsen?
* Fel eller avbrott - Vad händer när ett inkommande samtal eller meddelande visas medan appen körs? Vad händer om ett nätverksfel eller en avstängning inträffar?
* Installation och uppdateringar - Hur fungerar installationen? Hur skickas uppdateringar ut?
* Teknisk - Använder din app för mycket ström från en enhet?
* Lokalisering - Översätts alla delar i din app?
* Certifiering - Har din app certifierats? Kan kunderna lita på att den följer alla lagkrav för datasekretess?

Dessa frågor bör besvaras under din automatiska och manuella testning.

## Automatiserad testning {#automated-testing}

Viss grad av automatiserad testning bör utföras för att täcka olika skärmstorlekar, minnesbegränsningar, inmatningsmetoder och operativsystem. Det täcker inte bara många av testfallen, utan kan också påskynda regressionstestningen när nya funktioner eller enheter införs. Helst bör automatiseringsverktygen minska eller begränsa dubbelarbete. Använd verktyg eller ramverk så att testarbetet kan användas på alla plattformar. I följande diagram visas en förenklad struktur i en testmiljö för både webbaserad UI-testning och testning av mobilappar. På vänster sida av diagrammet visas en serie Selenium-noder med webbläsare. SeleniumGrid kan utföra vanliga, webbaserade gränssnittstester på alla dessa noder. Selenium-hubben kan även ansluta till Appium för apptestning över flera plattformar. Det är bara simulatorer som visas, men du kan inkludera adb för Android™ och Xcode för iOS-enheter. Länkar ges senare i det här dokumentet där du kan hitta specifik information om de verktyg som nämns.

![chlimage_1](assets/chlimage_1.jpeg)

## Manuell provning {#manual-testing}

Utöver automatiserad testning bör din app genomgå en serie manuella tester. Kunder som kör appen på en riktig enhet kan inte dupliceras av ett skript. Här har du också många alternativ. Du kan använda en plattform, till exempel HockeyApp, för att definiera vem som har åtkomst till och samla in feedback. Eller så kan du lägga ut hela processen på en tjänst som UTest, ElusiveStars eller Testin. Om du har en grupp interna testare, men saknar enhetsvarianter, finns det molntjänster där du kan utföra manuell testning på deras enhetspool. En sådan tjänst är SauceLabs. Du kan även fjärrbygga appar till PhoneGap Enterprise och installera dem på lokala enheter som en nivå av accepttestning eller degradering. På PhoneGap-webbplatsen (`https://phonegap.com/`) finns de senaste funktionerna och dokumentationen. Oavsett vilken metod man väljer bör manuell testning göra följande:

* träffade ett stort antal testare,
* testa mot en stor pool av enheter (helst verkliga enheter, men simulatorer/emulatorer om verkliga enheter inte är tillgängliga),
* ge informativ feedback:

   * kraschrapporter,
   * analys/spårning,
   * användbarhet,
   * områden med uppmärksamhet,
   * prestanda,
   * data-/strömförbrukning och så vidare.

## verktyg {#tools}

Det finns ett stort antal verktyg för testning av mobilappar. Valet av alternativ bör baseras på din specifika situation: funktioner, pris, support, täckning och så vidare. Här följer en liten beskrivning av några av de verktyg och tjänster som är tillgängliga.

**Selen**

* Ramverk som innehåller ett API för att testa skript för att mata in WebDriver och styra olika webbläsare.
* Du kan använda det här tillsammans med Appium för att testa på riktiga enheter.
* SeleniumGrid dirigerar tester över noder för parallell testning.
* Selenium IDE hjälper till att minska skrivningen av testfall.

Mer information finns i [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* En molnbaserad testningstjänst med kontinuerliga integreringskopplingar och verklig enhetstestning.
* Det ingår en App Crawler som kontrollerar enhetskompatibilitet, analyserar loggar, går igenom vyer, tar skärmbilder och övervakar prestanda.

Mer information finns i [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium är ett populärt ramverk för flera plattformar för automatisering av mobiltester.
* Dessutom ingår en inspektör med funktioner för att koda testfall.

Mer information finns i [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs erbjuder molnbaserad testning och integreras med kontinuerlig integrering.
* Testerna körs automatiskt i molnmiljön eller så kan du starta en viss enhet eller plattform och utföra manuell testning för att felsöka problem.

Mer information finns i [https://saucelabs.com/](https://saucelabs.com/).

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**HockeyApp**

* HockeyApp genomgår manuell testning där mobilappen skickas ut till en personlig app-butik där testare kan hämta och testa den.

Mer information finns i [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Även om det inte är ett testverktyg är Jenkins ett ramverk för kontinuerlig integrering som utgör ryggraden i automatiska tester. Det finns många plugin-program från tredje part som kan utöka funktionaliteten. Exempelvis innehåller SeleniumGrid-pluginen ett gränssnitt som hjälper dig att hantera Selenium-hubben och -noderna.

Mer information finns i [https://www.jenkins.io/](https://www.jenkins.io/) och [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
