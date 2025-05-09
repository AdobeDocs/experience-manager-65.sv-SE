---
title: Vägen till din första upplevelse med AEM utan headless
description: I den här delen av den AEM Headless Developer Journey kommer du att förstå hur du implementerar din första headless-upplevelse i AEM, inklusive planeringsöverväganden, och också lära dig bästa praxis för att göra din väg så smidig som möjligt.
exl-id: 64a87b6b-67ff-4d88-9dfb-c3e5de65bbe6
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 0%

---

# Vägen till din första upplevelse med AEM utan headless {#path-to-first-experience}

I den här delen av [AEM Headless Developer Journey](overview.md) får du en förståelse för hur du implementerar din första headless-upplevelse när det gäller AEM, inklusive planeringsöverväganden, och du får även lära dig bästa praxis för att göra din väg så smidig som möjligt.

## Story hittills {#story-so-far}

I det föregående dokumentet om den AEM resan utan headless lärde du dig [Komma igång med AEM Headless](getting-started.md) grundläggande teori om vad ett headless CMS är och du bör nu:

* Förstå grunderna i AEM headless-funktioner.
* Lär dig grunderna för AEM headless-funktioner.
* Var uppmärksam på AEM integrationsnivåer utan motstycke.
* Du kan definiera projektet utifrån dess omfång.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du förbereder ett eget AEM headless-projekt.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå de steg som krävs för att implementera ditt första projekt. Efter att ha läst den bör du:

* Förstå viktiga planeringsöverväganden när du utformar ditt innehåll.
* Förstå stegen för att implementera headless i AEM.
* Ha koll på vilka verktyg och AEM som krävs.
* Lär dig de bästa sätten att göra den enkla resan smidig, hålla innehållsgenereringen effektiv och se till att innehållet levereras snabbt.

## Krav {#requirements}

Innan du fortsätter med det här dokumentet måste du kontrollera att du har granskat det tidigare dokumentet i den AEM Headless Developer Journey, [Getting Started with AEM Headless](getting-started.md) och se till att du:

* Uppfyll de angivna kraven.
* Har tänkt på din egen projektdefinition, inklusive omfång, roller och prestanda.

## Planering för lyckat resultat {#planning-for-success}

För att starta ditt första AEM headless-projekt måste ni se till att ni har en innehållsmodell som stöder den personalisering och de uppdateringar ni vill göra i alla era kanaler.

Om du skapar ett klientprogram måste du också se till att du har en korrekt utvecklingsmiljö, separat från AEM, så att du kan testa klienten mot API-anrop till AEM.

### Definiera innehållsmodeller och API:er {#defining-models}

Ni vill skapa en enhetlig upplevelse och hantera personaliserade kampanjer i alla kanaler, så att ni kan se varje enskild kanal och yta som sin egen innehållsstruktur att leverera till. Det är dock en utmaning att behålla varje kanal med en egen innehållsmodell.

Istället bör ni överväga hur innehåll på olika ytor är relaterat till en organiseringsprincip som varumärken och produkthierarkier, kategorier av varor eller ytor, eller steg i kundresan. Om du t.ex. har en uppsättning ytor som stöder ett visst varumärke med bilar som du tillverkar, kanske du vill börja med en innehållsmodell för allmän information som är sann för hela bilen och sedan har mer - specifika element som innehåll som behövs när bilen startar vid serviceproblem. En sådan modell kommer att genomdriva arv av allmänt varumärkesinnehåll samtidigt som den möjliggör förändringar baserat på det specifika sammanhang som behövs. Det hjälper även till med framtida hantering av uppdateringar av det här innehållet eftersom ni kan tillämpa kontroll baserat på roller som den övergripande marknadsföraren eller produktchefen för hela varumärket jämfört med en författare som ansvarar för upplevelsen av att starta bilen.

När du har innehållsmodellen och en tydlig vy över de olika klienter som innehållet ska visas för, måste du se till att de GraphQL/API:er som är kopplade till åtkomsten till olika innehållsmodeller publiceras till alla klienter som behöver det här innehållet. Det finns olika sätt att komma åt visst innehåll. Du kan begära ett visst statiskt innehåll som möjliggör cachelagring av innehållet och högre prestanda. Du kan också begära dynamiskt genererat innehåll som kräver mer bearbetning. Se till att kunderna använder de API:er som är mest effektiva för deras affärsbehov.

## Förstå era miljöer {#understanding-environments}

Inom AEM finns det tre typer av miljöer: utveckling, staging och produktion.

Utvecklingsmiljöerna (du kan ha flera) är en säker plats att experimentera med och testa idéer på. Under projektets inledande fas rekommenderar Adobe att utvecklingsmiljöerna används för att testa olika varianter av innehållsmodellerna och för att se vilka som ger de avsedda resultaten för ytorna.

Mellanlagringsmiljön för headless-projekt används för att validera nya AEM produktreleaser innan de börjar producera. Håll en uppdaterad lista över produktionsinnehållsmodellerna där och en delmängd av innehållet, så att du kan få JSON-filer renderade för att jämföra dem som fortfarande ger samma utdata, när du gör ändringar eller AEM gör ändringar

Det är i produktionen som innehållsförfattare skapar och hanterar sitt faktiska innehåll. Modellförändringar i produktionen måste genomföras med försiktighet och bakåtkompatibilitet i åtanke.

Under utvecklingsfasen rekommenderar vi att du arbetar med en utvecklings- och staging-miljö. När du går över till prestandatestning vill du gå över till produktionsmiljön.

### Samarbete mellan utvecklare och innehållsförfattare {#cooperation}

Utvecklarna behöver en AEM utvecklingsmiljö som är anpassad efter de populära innehållsmodellerna. Utvecklaren utvecklar klienten som konsumerar innehåll från AEM headless eftersom innehållsförfattarna fortfarande skapar innehållet. Därför är API-definitionerna mycket viktiga. Genom att använda AEM SDK kan utvecklaren skapa en testkrok så att klient- och enhetstester kan skapas för att säkerställa att klienten kan återge innehållet på rätt sätt.

Innehållsförfattare skapar innehåll baserat på de innehållsmodeller som har definierats i mellanlagringsmiljön. Med hjälp av utvecklingsverktyget för innehållsfragment kan författaren skapa ett innehållsfragment eller redigera ett befintligt innehållsfragment. Innan den publiceras kan författaren förhandsgranska hur den kommer att se ut i klienten genom att arbeta med utvecklaren för att överföra innehållsmodellen till utveckling eller konfigurera en utvecklingsmiljö enbart för att författarna ska kunna se hur den skulle se ut i klienten.

## Inställningar {#setup}

Innan du börjar använda headless i AEM måste du se till att alla nödvändiga funktioner är aktiverade. I det här avsnittet beskrivs vad som krävs. De faktiska stegen för att utföra dessa steg beskrivs senare i [AEM Headless Developer Journey.](#overview.md)

Du kan även se de [ytterligare resurserna](#additional-resources) om du vill ha mer information om de enskilda ämnena.

### Konfiguration {#configuration}

1. Aktivera innehållsfragment
1. Aktivera GraphQL
1. Konfigurera Headless SDK

## Implementera din första AEM Headless-app

Detta är en översikt över vad som behövs för att implementera din första headless-app med AEM för att leverera ditt innehåll. Hur du utför dessa steg beskrivs i detalj i senare delar av den Headless Developer Journey.

1. Skapa modeller för innehållsfragment
1. Skapa innehållsfragment
1. Fråga innehåll med GraphQL

## Bästa praxis {#best-practices}

Ett headless-projekt är inte bara framgångsrikt på grund av den teknik som används, utan också på grund av god planering och projektledning. Här följer några tips som både författare och utvecklare kan använda när du planerar ditt projekt.

### Ordna ditt innehåll {#organizing-content}

* Gör strukturen så komplex som behövs, men gör den så enkel som möjligt. Enklare innehållsstrukturer effektiviserar innehållsstyrningen och förbättrar systemets prestanda.
* Prioritera återanvändning av innehåll i er strategi. Skapa undermodeller och innehållsreferenser som kan återanvändas i flera modeller och kanaler på högre nivå.
* Gör innehållsstrukturerna så självförklarande som möjligt så att skribenterna snabbt kan lära sig och anpassa sig till arbetsmomenten.
* Om du har åtkomstbegränsningar kan du försöka anpassa innehållsmodellen efter åtkomstkraven.
* När ni har åtkomstkrav bör de styra er innehållshierarki. Gruppera innehåll som redigeras av samma grupp av personer.
* Gruppera liknande innehåll i en mapp.
   * Det är troligare att en innehållsförfattare kopierar och klistrar in befintligt innehåll för att skapa nytt innehåll. Om du gör detta i samma mapp blir det därför effektivare.
   * AEM tillåter att tillåtna modeller anges per mapp, så knappen **Skapa ny** visar bara de modeller som stöds på den platsen.
* Det går att förenkla skapandet av nya innehållsfragment i den infogade redigeraren för innehållsfragment om rotmappen är angiven i modellen. Sedan behöver inte behandlaren välja en plats, utan bara ange ett namn och kan börja redigera den nya referensen.

### Skapa innehåll {#authoring}

* För kanalspecifika versioner av ditt innehåll bör du överväga att använda variationer för innehållsfragment. Variationer synkroniseras mot innehållshanteraren för att effektivisera hanteringen av innehållsändringar.
* Bjud in andra innehållsproducenter att granska materialet och ge feedback med kommentarer och kommentarer som är tillgängliga i innehållsfragmentredigeraren och globalt över fragment i innehållsfragment Admin Console.
* Håll saker i rörelse med så få obligatoriska element som möjligt. Obligatoriska element kan blockera arbetsflödet.

### Skapa globalt innehåll {#localization}

* Upprätta regler och styrning för översättning av innehåll. Om du vill minska systembelastningen upprättar du en översättning som en asynkron process som kan köras i längre intervall. Ge tid åt kvalitetskontroll och felkorrigering av lokalisering.
* Utnyttja alla funktioner i översättningstekniksystemet som ni kan integrera med AEM som översättningsminnen.
* Förstå om multimediematerial, som bilder och videor, behöver lokaliseras.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey ska du:

* Förstå viktiga planeringsöverväganden när du utformar ditt innehåll.
* Förstå stegen för att implementera headless i AEM.
* Ha koll på vilka verktyg och AEM som krävs.
* Lär dig de bästa sätten att göra den enkla resan smidig, hålla innehållsgenereringen effektiv och se till att innehållet levereras snabbt.

Vi vill att du bygger vidare på denna grundläggande kunskap för att till fullo förstå styrkan och flexibiliteten hos AEM Headless så att du kan utnyttja den för dina egna projekt. För att göra detta har du alternativ.

### Välj din egen Adventure {#choose-your-path}

Oavsett vilken inlärningsstil du har vill Adobe att du ska lyckas när du börjar med AEM Headless-projekt.

* Om du föredrar att **lära dig mer om headless-koncept och AEM headless-tekniker** bör du fortsätta din AEM resa genom att nästa gång du granskar dokumentet [Så här modellerar du ditt innehåll som AEM innehållsmodeller](model-your-content.md) där du får lära dig hur du modellerar innehållsstrukturen i AEM.
* Om du föredrar att **lära dig genom att göra** kan du hoppa till självstudiekursen [Komma igång med AEM Headless ](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=sv-SE) där du kommer att gå direkt till AEM Headless-utveckling genom att implementera ett enkelt projekt för att visa AEM headless-innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-utvecklingsresan genom att granska dokumentet [Så här modellerar du ditt innehåll som AEM innehållsmodeller](model-your-content.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på den headless-resan.

* [AEM Headless Translation Journey](/help/journey-headless/translation/overview.md) - Den här dokumentationsresan ger dig en bred förståelse för headless-teknik, hur AEM hanterar headless-innehåll och hur du kan översätta det.
* [Headless Development for AEM Sites](/help/sites-developing/headless/introduction.md) - En snabb introduktion som ger den AEM Headless-utvecklaren de nödvändiga funktionerna
* [AEM Headless Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=sv-SE) - Använd de här praktiska självstudiekurserna för att utforska hur du kan använda de olika alternativen för att leverera innehåll till headless-slutpunkter med AEM och välja vad som är rätt för dig.
* [Headless Content Management Using GraphQL APIs](https://experienceleague.adobe.com/sv?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Följ den här kursen för en översikt över det GraphQL API som implementerats i AEM. Autentisering via AdobeID krävs.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Det här GitHub-projektet innehåller exempelprogram som AEM GraphQL API:er.
* [Headless Getting Started Guide](/help/sites-developing/headless/introduction.md#getting-started) - En snabb introduktion till AEM headless-funktioner för användare som redan är AEM.
* [Skapa modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) - teknisk dokumentation om modeller för innehållsfragment
* [Skapa innehållsfragment](/help/assets/content-fragments/content-fragments.md) - teknisk dokumentation om innehållsfragment
* [Fråga innehåll med GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) - Teknisk dokumentation om GraphQL API
* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=sv-SE)
