---
title: AEM Sites - beredskap för GDPR
seo-title: AEM Sites - beredskap för GDPR
description: Läs mer om GDPR-beredskap för AEM Sites.
seo-description: Läs mer om GDPR-beredskap för AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Sites - beredskap för GDPR{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR används som exempel i avsnitten nedan, men de ingående detaljerna är tillämpliga på alla dataskydds- och sekretessbestämmelser. såsom GDPR, CCPA osv.

Europeiska unionens allmänna dataskyddsförordning om integritetsskydd får verkan från och med maj 2018.

AEM Sites är redo att hjälpa kunderna med deras GDPR-efterlevnadsskyldigheter. På den här sidan får kunderna hjälp med hur de hanterar GDPR-förfrågningar i AEM Sites. Den beskriver platsen för privata data som lagras och hur du tar bort dem manuellt eller med kod.

Mer information finns på [GDPR-sidan på Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Mer information finns i [AEM GDPR-beredskap](/help/managing/data-protection-and-privacy.md) .

## Författarserver {#author-server}

Användarkonton och UGC-innehåll på författarservern beskrivs i [plattformens GDPR-dokumentation](/help/managing/data-protection-and-privacy.md).

## Publish Server {#publish-server}

Användarkonton som används för att autentisera besökare på webbplatsen och UGC-innehåll på publiceringsservern beskrivs i [plattformens GDPR-dokumentation](/help/managing/data-protection-and-privacy.md).

Som standard lagras inte formulärdata som anges av besökare på publiceringsservern i AEM Sites-komponenter. Vi rekommenderar att du vidarebefordrar data till ett tredjepartssystem eller Adobe Campaign för vidare bearbetning.

## Opt-In/Opt-Out {#opt-in-opt-out}

AEM har en [cookie-avanmälningstjänst](/help/sites-developing/cookie-optout.md) som kan användas för att hantera avanmälan/avanmälan för användare.

## Förbättrade insikter från Analytics {#enhanced-insights-by-analytics}

AEM Sites innehåller en valfri integrering med Enhanced Insights by Analytics som använder funktioner i Adobe Analytics On-Demand Service.

Mer information om hur du hanterar förfrågningar från registrerade GDPR-data relaterade till Adobe Analytics finns i [Adobe Analytics och GDPR](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/).

## Förbättrad personalisering med Target {#enhanced-personalization-by-target}

AEM Sites innehåller en valfri integrering med Förbättrad personalisering via Target som använder funktioner i Adobe Target On-Demand Service.

Mer information om hur man hanterar förfrågningar från registrerade GDPR-data relaterade till Adobe Target finns i [Adobe Target - Privacy and General Data Protection Regulation](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM tillhandahåller ett valfritt datalager med [ContextHub](/help/sites-developing/contexthub.md). På så sätt behålls besökarspecifika data i webbläsaren som ska användas för regelbaserad personalisering.

Dessa besökardata lagras som standard inte i AEM. AEM skickar regler till datalagret för att fatta personaliseringsbeslut i webbläsaren.

>[!NOTE]
>
>Före Adobe CQ 5.6 skickade ClientContext (en tidigare version av ContextHub) data till servern, men lagrade dem inte.
>
>Adobe CQ 5.5 och tidigare är nu EOL och omfattas inte av denna dokumentation.

### Implementera anmälan/avanmälan {#implementing-opt-in-opt-out}

Webbplatsägaren måste implementera en avanmälningskomponent enligt följande riktlinjer.

I dessa riktlinjer används anmälan som standard. Därför måste en besökare på webbplatsen tydligt samtycka till detta innan personuppgifter lagras i webbläsarens (klientsidan) beständighet.

* Avanmälningskomponenten ska inkluderas varje gång ContextHub-komponenten inkluderas.
* De villkor som gäller GDPR för webbplatsen måste visas för webbplatsbesökaren så att de kan

   * acceptera
   * avvisa
   * ändra sitt föregående val

* Om en besökare godkänner villkoren för webbplatsen bör cookien för ContextHub-avanmälan tas bort:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Om en besökare inte accepterar webbplatsens villkor ska cookie för ContextHub-avanmälan anges:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* För att kontrollera om ContextHub körs i avanmälningsläge bör följande anrop göras i webbläsarens konsol:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Förhandsgranska Persistence för ContextHub {#previewing-persistence-of-contexthub}

Om du vill förhandsgranska den beständiga ContextHub som används kan användaren:

* Använda webbläsarens konsol. till exempel:

   * Krom:

      * Öppna Utvecklarverktyg > Program > Lagring:

         * Lokal lagring > (webbplats) > ContextHubPersistence
         * Sessionslagring > (webbplats) > ContextHubPersistence
         * Cookies > (website) > SessionPersistence
   * Firefox:

      * Öppna Utvecklarverktyg > Lagring:

         * Lokal lagring > (webbplats) > ContextHubPersistence
         * Sessionslagring > (webbplats) > ContextHubPersistence
         * Cookies > (website) > SessionPersistence
   * Safari:

      * Öppna Inställningar > Avancerat > Visa menyn Framkalla i menyraden
      * Öppna Utveckla > Visa JavaScript-konsol

         * Konsol > Lagring > Lokal lagring > (webbplats) > ContextHubPersistence
         * Konsol > Lagring > Sessionslagring > (webbplats) > ContextHubPersistence
         * Konsol > Lagring > Cookies > (webbplats) > ContextHubPersistence
   * Internet Explorer:

      * Öppna Utvecklarverktyg > Konsol

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* Använd ContextHub-API:t i webbläsarens konsol:

   * ContextHub tillhandahåller följande beständiga datalager:

      * ContextHub.Utils.Persistence.Modes.LOCAL (standard)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      ContextHub-arkivet definierar vilket beständigt lager som ska användas, och för att visa det aktuella läget för beständigheten bör alla lager kontrolleras.


Så här visar du data som lagras i localStorage:

Om du vill förhandsgranska den beständiga ContextHub som används kan användaren:

* Använd webbläsarens konsol:

   * Chrome - open Developer Tools > Application > Storage:

      * Lokal lagring > (webbplats) > ContextHubPersistence
      * Sessionslagring > (webbplats) > ContextHubPersistence
      * Cookies > (website) > SessionPersistence
   * Firefox - öppna Utvecklarverktyg > Lagring:

      * Lokal lagring > (webbplats) > ContextHubPersistence
      * Sessionslagring > (webbplats) > ContextHubPersistence
      * Cookies > (website) > SessionPersistence


* Använd ContextHub-API:t i webbläsarens konsol:

   * ContextHub tillhandahåller följande beständiga datalager:

      * ContextHub.Utils.Persistence.Modes.LOCAL (standard)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      ContextHub-arkivet definierar vilket beständigt lager som ska användas, och för att visa det aktuella läget för beständigheten bör alla lager kontrolleras.


Så här visar du data som lagras i localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Rensar Persistence för ContextHub {#clearing-persistence-of-contexthub}

Så här rensar du ContextHub-beständighet:

* Så här rensar du beständighet för inlästa arkiv:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* för att rensa ett visst beständigt lager, sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Om du vill ta bort alla ContextHub-beständiga lager måste rätt kod anropas för alla lager:

   * ContextHub.Utils.Persistence.Modes.LOCAL (standard)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

