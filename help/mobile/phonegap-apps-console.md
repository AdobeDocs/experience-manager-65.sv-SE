---
title: Skapa och redigera appar med Apps-konsolen
description: Följ den här sidan om du vill veta mer om hur du skapar och redigerar program med hjälp av appkonsolen.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2654'
ht-degree: 0%

---

# Skapa och redigera appar med Apps-konsolen{#creating-and-editing-apps-using-the-apps-console}

{{ue-over-mobile}}

I utvecklingsprocessen för AEM mobilapplikationer erkänns att användare med olika sakkunskap bidrar till utvecklingen av mobilapplikationer. Följande processkarta visar den allmänna ordningen i vilken innehållsförfattare och programutvecklare utför uppgifter.

![chlimage_1-10](assets/chlimage_1-10.gif)

Information om hur du utför marknadsföringsåtgärder visas på den här sidan. Mer information om utvecklaråtgärder finns i Skapa PhoneGap-program.

## Strukturen för mobilprogram {#the-structure-of-mobile-applications}

AEM Mobile tillhandahåller en plan för PhoneGap-appen för att skapa mobilappar. Planen definierar strukturen för de program du skapar. Ansökningarna består av följande:

* Rotsidan.
* Programmets språkvarianter.
* Hemsidan för språkvarianten.

### Roten för en PhoneGap-app {#the-root-of-a-phonegap-app}

Rotsidan för de mobilprogram du skapar i AEM visas i Apps-konsolen.

Rotsidan lagras under egenskapen Målsökväg i programmet som angavs när programmet skapades (standardsökvägen är /content/phonegap/apps). Sidnamnet är egenskapen Name för programmet. Standardwebbadressen för rotsidan på webbplatsen `myphonegapapp` är till exempel `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### Språkvariationen för en PhoneGap-app {#the-language-variation-of-a-phonegap-app}

De första underordnade sidorna på rotsidan är språkvariationerna för programmet. Namnet på varje sida är det språk som programmet skapas för. Engelska är till exempel namnet på den engelska varianten av programmet.

**Obs!** Standardversionen av PhoneGap skapar bara ett engelskt program. Utvecklaren kan ändra planen så att den kan skapa fler språkvarianter.

![chlimage_1-147](assets/chlimage_1-147.png)

Språksidan har två syften:

* Sidinnehållet är den utfällbara sidan för språkvarianten i programmet.
* Sidegenskaperna styr flera designaspekter av programmet, t.ex. den URL som ska användas för att begära innehållsuppdateringar och information om hur du ansluter till molnbygget och Adobe Analytics Services-integrering.

![chlimage_1-148](assets/chlimage_1-148.png)

### Hemsidan {#the-home-page}

Startsidan eller index.html-sidan för en språkvariant av ett program visas när programmet öppnas. På hemsidan finns en meny med länkar till olika sidor i programmet. Med styckesystemet kan du lägga till komponenter på sidan för att skapa innehåll.

## Skapa ett mobilprogram {#creating-a-mobile-application}

Mobilprogram bygger på en plan som definierar en sidstruktur och egenskaper. Du kan konfigurera följande programegenskaper:

* **Titel:** Programnamnet.
* **Målsökväg:** Platsen i databasen där programmet lagras. Låt standardinställningen vara om du vill skapa en sökväg baserat på programnamnet.

* **Namn:** Standardvärdet är värdet på egenskapen Title där blankstegstecken tas bort. Namnet används i CQ för att referera till programmet, till exempel för databasnoden som representerar programmet.
* **Beskrivning:** En beskrivning av programmet.
* **Server-URL:** Den URL som tillhandahåller OTA-innehåll (Over-the-Air) uppdateras i programmet. Standardvärdet är publiceringsserverns URL-adress för instansen som används för att skapa ett program (hämtas från externaliseringstjänsten). Observera att detta måste vara en publiceringsserverinstans i stället för en författare, vilket kräver autentisering.

Du kan också tillhandahålla en bildfil som du kan använda som programminiatyrbild, välja vilken PhoneGap Build-konfiguration som ska användas och välja vilken mobilappsanalyskonfiguration som ska användas. Den här bilden används bara som miniatyrbild för att representera ditt mobilprogram i mobilappskonsolen i Experience Manager.

Det finns ytterligare flikar (och valfria) för att bygga molntjänster och integrera SDK-pluginmodulen för Adobe Mobile Services i appen.

* Bygg: Klicka på Hantera konfigurationer och konfigurera build.phonegap.com här. I listrutan kan du sedan välja den nya molntjänsten PhoneGap build.
* Analys: Klicka på Hantera konfigurationer och konfigurera molntjänsten [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=sv-SE). I listrutan kan du sedan välja den nya mobiltjänsten som ska integreras i din mobilapp.

>[!NOTE]
>
>Utvecklare kan använda AEM PhoneGap Starter Kit för att skapa appar och lägga till dem i konsolen.

I följande procedur används Touch-gränssnittet för att skapa ett mobilprogram.

1. Klicka på Appar på listen.
1. Klicka på ikonen Skapa.

   ![Ikonen Skapa indikeras av ett plustecken inuti en kvadrat.](do-not-localize/chlimage_1-7.png)

1. (Valfritt) Ange en beskrivning för programmet på fliken Avancerat och ändra serverns URL om det behövs.
1. (Valfritt) Om du använder PhoneGap Build för att kompilera programmet väljer du den konfiguration som ska användas på fliken Skapa.

   Om du vill skapa en konfiguration för PhoneGap-bygget klickar du på Hantera konfigurationer.

1. (Valfritt) Om du använder SiteCatalyst för att spåra programaktivitet väljer du den konfiguration som ska användas på fliken Analytics.

   Om du vill skapa en konfiguration för mobilappar klickar du på Hantera konfigurationer.

1. (Valfritt) Om du vill ange en programikon klickar du på knappen Bläddra, markerar bildfilen i filsystemet och klickar på Öppna.
1. Klicka på Skapa.

### Ändra egenskaperna för ett mobilprogram {#changing-the-properties-of-a-mobile-application}

När du har skapat ett mobilprogram kan du ändra egenskaperna.

#### Ändra titel, beskrivning och ikon {#change-the-title-description-and-icon}

1. Klicka på Appar på listen.
1. Välj det program som ska konfigureras och klicka på ikonen Visa sidegenskaper.

   ![Ikonen Visa sidegenskaper, som indikeras av bokstaven I inuti en cirkel.](do-not-localize/chlimage_1-8.png)

1. Om du vill ändra egenskapsvärden klickar du på ikonen Redigera.

   ![Ikonen Redigera indikeras av en penna.](do-not-localize/chlimage_1-9.png)

1. Konfigurera de grundläggande och avancerade egenskaperna och klicka sedan på ikonen Klar.

   ![Klar-ikonen indikeras av en bockmarkeringssymbol.](do-not-localize/chlimage_1-10.png)

#### Konfigurera en språkvariant för programmet {#configure-a-language-variation-of-the-application}

1. Klicka på Appar på listen.
1. Klicka för att gå in i det mobilprogram du vill redigera i apparna Admin Console. Välj den språkversion av programmet som ska konfigureras och klicka på ikonen Visa programegenskaper.

   ![Ikonen Visa programegenskaper som indikeras av bokstaven I i en cirkel.](do-not-localize/chlimage_1-11.png)

1. Om du vill ändra egenskapsvärden klickar du på ikonen Redigera.

   ![Ikonen Redigera indikeras av en penna.](do-not-localize/chlimage_1-12.png)

1. Konfigurera egenskaperna på flikarna Grundläggande, Avancerat, Version och Analytics och klicka sedan på ikonen Done (Klar).

   ![Klar-ikonen indikeras av en bockmarkeringssymbol.](do-not-localize/chlimage_1-13.png)

### Skapa innehåll för ett mobilprogram {#authoring-the-content-of-a-mobile-application}

När du har skapat mobilprogrammet lägger du till innehåll som används som programgränssnitt.

1. Klicka på Appar på listen.
1. Klicka på programmet och sedan på engelska.
1. Redigera hemsidan eller lägg till underordnade sidor efter behov.

### Flytta innehåll till mobilprogram {#moving-content-to-mobile-applications}

Cacheminnet för innehållssynkronisering på den AEM publiceringsinstansen används som en databas för innehåll för mobilprogram:

* Innehåll i cachen för innehållssynkronisering inkluderas i programmet när utvecklare kompilerar programmet.
* Innehåll i cachen är tillgängligt för installerade mobilprogram för uppdatering av programinnehållet.

Mobilprogram innehåller ett uppdateringskommando som hämtar och installerar uppdaterat programinnehåll. När en programinstans skickar en uppdateringsbegäran avgör Innehållssynkronisering vilket innehåll som har ändrats sedan programmet senast uppdaterades eller installerades och tillhandahåller det nya innehållet.

![chlimage_1-149](assets/chlimage_1-149.png)

Om du vill göra uppdaterat innehåll tillgängligt för program uppdaterar du cachen för innehållssynkronisering. Första gången du uppdaterar cachen läggs allt publicerat innehåll till. Efterföljande uppdateringar lägger bara till det publicerade innehåll som har ändrats sedan den föregående uppdateringen.

Innehållssynkronisering spårar även när uppdateringarna utförs. Med den här informationen kan Innehållssynkronisering avgöra vilken cacheuppdatering som ska skickas till ett mobilprogram.

Utför följande procedur på instansen där du vill uppdatera cachen. Om ditt program till exempel begär uppdateringar från publiceringsinstansen utför du proceduren på publiceringsinstansen.

1. Klicka på Appar på listen och klicka sedan på programmet.
1. Markera välkomstsidan och klicka sedan på ikonen Uppdatera cache.

   ![Ikonen Uppdatera cache indikeras av en randig rad med en återvinningssymbol över den.](do-not-localize/chlimage_1-14.png)

### Använda appmallar {#using-app-templates}

Det här är en funktion som är tillgänglig med Apps 6.1 Feature Pack 2 och som gör det enkelt att använda befintliga appmallar för att skapa nya appar i AEM.

Vad är en appmall? Se det som en samling sidmallar och komponenter som utgör en grund eller grund för ett program.
När du skapar ett program baserat på en mall för ett annat program får du ett program som har en startpunkt som representerar det program som det skapades från.

Du måste ha en befintlig mobilappsmall (eller en app som har en appmall) för att kunna använda den här funktionen.

Det senaste exempelpaketet AEM Apps 6.1 innehåller en uppdaterad version av Geometrixx-appen med en appmall. Du kan också installera StarterKit, som även innehåller en mall.

Steg för att skapa ett program baserat på en appmall:

1. Se till att du har det senaste AEM Apps 6.1-funktionspaketet och referensexempelpaketen installerade
1. Klicka på Appar från den vänstra listen.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Klicka på knappen + Skapa överst och välj Skapa app.
1. När du har fått listan över appmallar väljer du en:

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Klicka på Nästa.
1. Ange ett program-ID och en titel, men du kan också inkludera ett namn och en beskrivning.

   1. Du kan också ange en PNG-fil (PhoneGap-ikonformat som stöds) som en ikon genom att bläddra bland AEM resurser.
   1. Kom ihåg att du kan redigera alla dessa fält efter att appen har skapats i panelen Hantera app. Med undantag för app-ID:t kan du inte ändra det när program-ID:t har angetts.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Klicka på knappen Skapa så visas 2 alternativ, antingen Klart (gå tillbaka till katalogvyn Appar) eller Hantera program (öppnar appkontrollpanelen).
1. När du har skapat programmet bör du se den nya appen i katalogen App:

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Klicka på appen för att öppna den. Du har skapat en ny app som är baserad på mallen för ett befintligt program.

>[!NOTE]
>
>Om du avinstallerar referenspaketet för Geometrixx Outdoors från AEM och har ett program som skapats baserat på dess mall kommer det programmet inte längre att fungera. Appen Geometrixx Outdoors kan tas bort, men appmallen måste finnas kvar om den används av andra mobilprogram.

## Utforska exempelappen Geometrixx Outdoors {#exploring-the-sample-geometrixx-outdoors-app}

Geometrixx Outdoors App är ett exempel på PhoneGap-program som demonstrerar funktionerna i standardprogrammet för PhoneGap och de mobila komponenterna i exemplet.

Om du vill öppna programmet går du till fliken Mobilprogram och väljer sedan Geometrixx Outdoors App.

### Funktioner för vanliga sidor - Geometrixx Mobile App {#common-page-features-geometrixx-mobile-app}

Varje sida i mobilappen innehåller följande funktioner:

* En bakåtknapp för att gå tillbaka till den överordnade sidan. Bakåtknappen visas inte på hemsidan.
* En stödlinje som innehåller en meny med kommandon och länkar:

   * Öppna sidan Platser.
   * Öppna kundvagnen.
   * Logga in.
   * Uppdatera programmet.

* Styckesystemet för att lägga till komponenter och skapa innehåll.

### Hemsidan - Geometrixx Mobile App {#the-home-page-geometrixx-mobile-app}

Innehållet på hemsidan består av följande navigeringsverktyg:

* En menylistekomponent som innehåller länkar till de underordnade sidorna Kugghjulet, Recensioner, Nyheter och Om oss.
* En Swipe Carousel-komponent som visar de underordnade sidorna.

### The Gear Page - Geometrixx Mobile App {#the-gear-page-geometrixx-mobile-app}

På sidan Kugghjulet får användarna tillgång till produktsidor. En menylistekomponent ger åtkomst till de underordnade sidorna på sidan Kugghjul. De underordnade sidorna är produktkategorier som webbplatsen har.

* Säsong
* Kläder
* Kön
* Aktivitet

Varje kategorisida har samma innehållsstruktur som sidan Kugghjul. Carousel ger åtkomst till underordnade sidor som är underkategorier av produkter. Underkategorisidorna innehåller produktlistor med länkar till produktsidor.

### The Products page - Geometrixx Mobile App {#the-products-page-geometrixx-mobile-app}

Sidan Produkter och hierarkin med underordnade sidor implementerar ett klassificeringssystem för produktsidor. De lägsta sidorna i varje gren av hierarkin är en produktsida som innehåller en ng-produktkomponent.

Sidan Produkter är inte tillgänglig för programanvändare. På sidan Kugghjul finns alla produktsidor.

### Sidan Recensioner - Geometrixx Mobile App {#the-reviews-page-geometrixx-mobile-app}

Innehåller en bakåtknapp. Med styckesystemet kan du lägga till komponenter.

När du använder programmet är sidan Recensioner tillgänglig från karusellen på den engelska sidan.

### News Page - Geometrixx Mobile App {#the-news-page-geometrixx-mobile-app}

Innehåller en bakåtknapp. Med styckesystemet kan du lägga till komponenter.

När du använder programmet är News page tillgängligt från karusellen på den engelska sidan.

### Sidan Om oss - mobilappen Geometrixx {#the-about-us-page-geometrixx-mobile-app}

Sidan Om oss innehåller flera komponenter med två kolumnrader. Varje kolumn innehåller en bild- eller textkomponent. Komponenterna kan redigeras och med styckesystemet kan du lägga till komponenter.

När du använder programmet är sidan Om oss tillgänglig från karusellen på den engelska sidan.

### Platssidan - Geometrixx Mobile App {#the-locations-page-geometrixx-mobile-app}

Sidan Platser innehåller en Locations-komponent.

När du använder programmet är sidan Platser tillgänglig från menylistan på den engelska sidan.

## Exempel på mobila komponenter {#sample-mobile-components}

Flera komponenter är omedelbart tillgängliga i Sidekick när du redigerar sidor i ett mobilprogram. Komponenterna tillhör PhoneGap-komponentgruppen.

### Svep Carousel {#swipe-carousel}

Komponenten Swipe Carousel är ett verktyg för att visa och navigera på webbplatssidor. Komponenten innehåller en karusell som bläddrar igenom bilder för sidorna ovanför en lista med sidlänkar. Redigera komponenten för att ange vilka sidor som ska visas och hur karusellen fungerar.

Observera att bilder visas i karusellen för sidor som är kopplade till en bild på ett visst sätt. När sidor inte är kopplade till bilder visas bara länklistan.

![chlimage_1-151](assets/chlimage_1-151.png)

**Egenskapsfliken Carousel**

Konfigurera karusellens beteende:

* Uppspelningshastighet: Tiden i millisekunder som varje bild visas innan nästa bild visas.
* Övergångstid: Animeringens varaktighet i millisekunder för bildövergångar.
* Kontrollformat: Den typ av kontroller som finns för att flytta mellan bilder.

**Fliken Listegenskaper**

Ange hur sidlistan ska genereras:

* Skapa lista med: Den metod som ska användas för att ange vilka sidor som ska inkluderas i karusellen. Se Skapa sidlistan.
* Ordna efter: Välj en sidegenskap som ska användas för att sortera sidlistan. Välj t.ex. jcr:title om du vill sortera sidor i bokstavsordning efter rubrik.
* Gräns: Maximalt antal sidor som ska inkluderas. Den här egenskapen är lämplig för sökbaserade metoder för att skapa sidlistan.

#### Bygga sidlistan {#building-the-page-list}

Komponenten Swipe Carousel innehåller följande värden för egenskapen Build List Using. Redigeringsdialogrutan ändras beroende på vilket värde du väljer:

**Underordnade sidor**

Komponenten visar alla underordnade sidor för en viss sida. När du har valt det här värdet markerar du sidan på fliken Underordnade sidor, eller anger inget värde för att visa den aktuella sidans underordnade sidor.

**Fast lista**

Ange en lista med sidor som ska inkluderas. När du har valt det här värdet konfigurerar du listan på fliken Fast lista som visas när du väljer Fast lista:

* Om du vill lägga till en sida klickar du på Lägg till objekt och bläddrar sedan till sidan.
* Använd upp- och nedpilarna för att flytta sidan i listan.
* Klicka på knappen Ta bort för att ta bort en sida från listan.

Egenskapen Ordna efter påverkar inte ordningen för fasta listor.

**Sökning**

Fyll i listan med resultatet av en nyckelordssökning. Sökningen utförs på de underordnade sidorna för en sida som du anger:

1. Om du vill ange sökningens rotsida använder du egenskapen Starta i för att välja sidsökvägen. Ange ingen sökväg att söka efter under den aktuella sidan.
1. Ange söknyckelorden i egenskapen Sökfråga.

**Avancerad sökning**

Fyll i listan med en [Querybuilder](/help/sites-developing/querybuilder-api.md)-fråga.

### Bild {#image}

Lägg till en bild i programinnehållet.

### Text {#text}

Lägg till formaterad text i programinnehållet.

### Lagringsplatser {#store-locations}

Komponenten Store Locations ger användarna verktyg för att hitta affärskommunikation:

* Sök
* Listor över platser som ligger nära eller långt från enhetens GPS-koordinater.

Komponenten kräver att databasen innehåller platsinformation för varje butik. Exempelplatser installeras på noden /etc/commerce/locations/adobe. ![chlimage_1-152](assets/chlimage_1-152.png)

### Två kolumner, rad {#two-column-row}

Gör att du kan lägga till komponenter sida vid sida på en sida.

![chlimage_1-153](assets/chlimage_1-153.png)
