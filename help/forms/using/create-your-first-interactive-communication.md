---
title: Självstudiekurs - skapa din första interaktiva kommunikation
seo-title: Skapa din första interaktiva kommunikation
description: Lär dig skapa din första interaktiva kommunikation.
seo-description: Lär dig skapa din första interaktiva kommunikation.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Självstudiekurs: Skapa din första interaktiva kommunikation {#tutorial-create-your-first-interactive-communication}

Lär dig skapa din första interaktiva kommunikation.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Interactive Communications centraliserar och hanterar framtagning, sammanställning och leverans av säkra, personaliserade och interaktiva korrespondenser som affärskorrespondens, dokument, kontoutdrag, marknadsföringsmejl, räkningar och välkomstpaket. Interaktiv kommunikation kan levereras via två kanaler: Tryck och webb. Print-kanalen används för att skapa PDF:er och pappersdokument, medan webbkanalen används för att leverera onlineupplevelser.

Den här självstudiekursen är ett komplett ramverk för interaktiv kommunikation. Självstudiekursen är ordnad i ett användningsfall och i flera guider. Varje guide hjälper dig att skapa funktioner som används som byggstenar för att skapa en interaktiv kommunikation.

Följande bild visar de byggstenar som krävs för att skapa ett interaktivt meddelande.

![arbetsflöde](assets/workflow.gif)

I slutet av den här självstudiekursen kan du:

* Skapa byggstenar (formulärdatamodell, dokumentfragment och mallar)
* Skapa en interaktiv kommunikation
* Testa och publicera interaktiv kommunikation

## Använd skiftläge {#use-case}

Resan börjar med att man lär sig hur det fungerar:

En telekomoperatör skickar månadsräkningar till kunderna via e-post. Fakturan är en interaktiv kommunikation. E-postmeddelandet innehåller:

* En lösenordsskyddad PDF-fil som kallas för utskriftskanal i den här självstudiekursen. Det innehåller kundinformation, faktureringsinformation, sammanfattning av avgifter, praktiska sätt att betala räkningen samt användningsinformation.
* En länk till webbversionen av lagförslaget, som kallas webbkanal i den här självstudiekursen. Webbversionen av fakturan innehåller, förutom den information som ingår i PDF-versionen, en grafisk representation av användningsinformation och skräddarsydda erbjudanden baserade på Adobe Target. Webbversionen innehåller även ett onlinebetalningsformulär. Det gör det lättare att göra onlinebetalningar utan att lämna försäkringsbolaget.
* En länk till mervärdesskapande tjänster, som onlinelagring, musikprenumerationer och on-demand-videoprenumerationer.

## Förutsättningar {#prerequisites}

* Konfigurera en AEM-författarinstans.
* Installera [tillägget](/help/forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms på författarinstansen
* Konfigurera MYSQL-databasen
* Hämta JDBC-databasdrivrutin (JAR-fil) från databasprovidern. Exemplen i självstudien är baserade på MySQL-databasen och använder Oracles JDBC-databasdrivrutin [](https://dev.mysql.com/downloads/connector/j/5.1.html)MySQL.

## Steg 1: Planera interaktiv kommunikation {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Det första steget i planeringen av interaktiv kommunikation är att färdigställa innehållet i den interaktiva kommunikationen. När innehållet är klart måste du analysera det för att identifiera de olika resurstyper som krävs för att skapa den interaktiva kommunikationen.

**Mål:**

Så här skapar du en anatomi för den interaktiva kommunikationen med följande datainmatningslägen:

* Statisk text
* Formulärdatamodell
* Agentgränssnitt
* Villkorliga data
* Bilder

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## Steg 2:Skapa formulärdatamodell {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Med en formulärdatamodell kan du koppla en interaktiv kommunikation till olika datakällor. Exempel: AEM-användarprofil, RESTful-webbtjänster, SOAP-baserade webbtjänster, OData-tjänster och relationsdatabaser. En formulärdatamodell är ett enhetligt datarepresentationsschema för affärsenheter och tjänster som är tillgängliga i anslutna datakällor. Du kan använda formulärdatamodellen med en interaktiv kommunikation för att hämta data från anslutna datakällor. Mer information om formulärdatamodell finns i [AEM Forms-dataintegrering](/help/forms/using/data-integration.md).

**Mål:**

* Konfigurera databasinstans (MySQL-databas) som en datakälla
* Skapa formulärdatamodellen med MySQL-databasen som en datakälla
* Lägga till datamodellobjekt i formulärdatamodellen
* Konfigurera läs- och skrivtjänster för formulärdatamodellen
* Skapa associationer mellan datamodellsobjekt
* Visa automatiskt genererade exempeldata
* Redigera exempeldata
* Testa formulärdatamodell och konfigurerade tjänster med testdata

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## Steg 3: Skapa dokumentfragment {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Dokumentfragment är återanvändbara komponenter i en korrespondens som används för att skapa en interaktiv kommunikation. Dokumentfragmenten är av följande typer: Text, Lista och Villkor.

**Mål:**

* Skapa dokumentfragment
* Skapa variabler
* Skapa och tillämpa regler

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## Steg 4: Skapa mallar {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Om du vill skapa en interaktiv kommunikation måste du ha mallar tillgängliga på AEM-servern för utskrifts- och webbkanaler.

Mallarna för utskriftskanalen skapas i Adobe Forms Designer och överförs till AEM-servern. Mallarna kan sedan användas när du skapar en interaktiv kommunikation.

Mallarna för webbkanalen skapas i AEM. Mallförfattare och administratörer kan skapa, redigera och aktivera webbmallar. När mallarna har skapats och aktiverats kan de användas när du skapar en interaktiv kommunikation.

**Mål:**

* Skapa XDP-mallar för tryckkanaler med Adobe Forms Designer
* Överför XDP-mallarna till AEM Forms Server
* Skapa och aktivera mallar för webbkanalen

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## Steg 5: Skapa en interaktiv kommunikation {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

När du har skapat alla byggstenar, t.ex. formulärdatamodell, dokumentfragment och mallar för webbversionen, kan du börja skapa en interaktiv kommunikation.

Interaktiv kommunikation kan levereras via två kanaler: Tryck och webb. Du kan också skapa en interaktiv kommunikationskanal med utskriftskanalen som master. Skriv ut som huvudalternativ för webbkanal säkerställer att innehållet, arvet och databindningen för webbkanalen hämtas från utskriftskanalen.

**Mål:**

* Skapa interaktiv kommunikation för tryckkanalen
* Skapa interaktiv kommunikation för webbkanalen
* Skapa trycksaker och webbinteraktiv kommunikation med Skriv ut som mall
* Skapa en dynamisk tabell i webbversionen av Interactive Communication
* Skapa ett diagram i webbversionen av Interactive Communication
* Skapa hyperlänkar i webbversionen av interaktiv kommunikation

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## Steg 6: Testa interaktiv kommunikation {#step-test-your-interactive-communication}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

När du har skapat en interaktiv kommunikation är det viktigt att du testar alla ändringar du gör i den. Det är omständligt att testa alla fält i en interaktiv kommunikation. AEM Forms tillhandahåller en SDK (Calvin SDK) för att automatisera testning av interaktiv kommunikation i webbläsare.

**Mål:**

* Skapa testsvit
* Skapa testfall
* Kör testfall

## Steg 7: Publicera interaktiv kommunikation {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

När du har skapat och testat interaktiv kommunikation med hjälp av utskrifts- och webbkanaler kan du publicera dessa resurser. Det användningsexempel som beskrivs i den här självstudiekursen fokuserar på att integrera dessa resurser med en e-postklient. E-postklienten fungerar som en brygga för att skicka interaktiv kommunikation till flera e-postadresser.

**Mål:**

* Integrera interaktiv kommunikation med en e-postklient för att kunna skicka ett meddelande till kunderna
* Inkludera ett PDF-dokument som en bifogad fil (interaktiv kommunikation skapad i tryckkanalen)
* Lägg in en länk till webbversionen av Interactive Communication

