---
title: Driftsättning och underhåll
description: Lär dig hur du kommer igång med AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---

# Driftsättning och underhåll{#deploying-and-maintaining}

På den här sidan hittar du:

* [Grundläggande begrepp](#basic-concepts)

   * [Vad är AEM?](#what-is-aem)
   * [Vanliga distributioner](#typical-deployment-scenarios)

      * [Lokalt](#on-premise)
      * [Managed Services med Cloud Manager](#managed-services-using-cloud-manager)

* [Komma igång](#getting-started)

   * [Förutsättningar](#prerequisites)
   * [Hämta programvaran](#getting-the-software)
   * [Lokal standardinstallation](#default-local-install)
   * [Skapa och publicera installationer](#author-and-publish-installs)
   * [Opackad installationskatalog](#unpacked-install-directory)
   * [Starta och stoppa](#starting-and-stopping)

När du har lärt dig grunderna hittar du mer avancerad och detaljerad information på följande undersidor:

* [Tekniska krav](/help/sites-deploying/technical-requirements.md)
* [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md)
* [Anpassad fristående installation](/help/sites-deploying/custom-standalone-install.md)
* [Installation av programserver](/help/sites-deploying/application-server-install.md)
* [Felsökning](/help/sites-deploying/troubleshooting.md)
* [Kommandoradens start och stopp](/help/sites-deploying/command-line-start-and-stop.md)
* [Konfigurerar](/help/sites-deploying/configuring.md)
* [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Instruktionsartiklar för konfiguration](/help/sites-deploying/ht-deploy.md)
* [Webbkonsol](/help/sites-deploying/web-console.md)
* [Felsökning av replikering](/help/sites-deploying/troubleshoot-rep.md)
* [Bästa praxis](/help/sites-deploying/best-practices.md)
* [Distribuera webbgrupper](/help/communities/deploy-communities.md)
* [Introduktion till AEM](/help/sites-deploying/platform.md)
* [Riktlinjer för prestanda](/help/sites-deploying/performance-guidelines.md)
* [Komma igång med AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Vad är AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Grundläggande begrepp {#basic-concepts}

### Vad är AEM? {#what-is-aem}

Adobe Experience Manager är ett webbaserat klient-server-system för att bygga, hantera och driftsätta kommersiella webbplatser och tillhörande tjänster. Den kombinerar flera funktioner på infrastruktur- och applikationsnivå i ett enda integrerat paket.

På infrastrukturnivå AEM följande:

* **Webbprogramserver**: AEM kan distribueras i fristående läge (det inkluderar en integrerad Jetty-webbserver) eller som ett webbprogram i en tredjepartsprogramserver.
* **Web Application Framework**: AEM innehåller Sling Web Application Framework som förenklar skrivandet av RESTful, innehållsorienterade webbprogram.
* **Innehållsdatabas**: AEM innehåller en Java™ Content Repository (JCR), en typ av hierarkisk databas som är särskilt utformad för ostrukturerade och halvstrukturerade data. I databasen lagras inte bara användarriktat innehåll utan även all kod, mallar och interna data som används av programmet.

AEM bygger på denna bas och erbjuder även flera funktioner på programnivå för att hantera:

* **Webbplatser**
* **Mobila program**
* **Digitala publikationer**
* **Forms och dokument**
* **Digital Assets**
* **Communities**
* **Online Commerce**

Slutligen kan kunderna använda dessa byggstenar på infrastruktur- och applikationsnivå för att skapa anpassade lösningar genom att bygga egna applikationer.

AEM server är **Java-baserad** och kan köras på de flesta operativsystem som stöder den plattformen. All kundinteraktion med AEM sker via en **webbläsare**.

>[!NOTE]
>
>Funktionen Adaptive Forms, som finns i AEM 6.5 QuickStart, är avsedd endast för utforsknings- och utvärderingsändamål. För produktion krävs en giltig licens för AEM Forms, eftersom Adaptive Forms-funktionaliteten kräver rätt licensiering.

### Vanliga distributionsscenarier {#typical-deployment-scenarios}

I AEM är &quot;instance&quot; en kopia av AEM som körs på en server. AEM omfattar vanligtvis minst två instanser, som vanligtvis körs på olika datorer:

* **Upphovsman**: En AEM som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
* **Publicera**: En AEM instans som skickar det publicerade innehållet till allmänheten.

De här instanserna är identiska vad gäller installerad programvara. De skiljer sig bara åt genom konfiguration. Dessutom använder de flesta installationer en Dispatcher:

* **Dispatcher**: En statisk webbserver (Apache httpd, Microsoft® IIS o.s.v.) som utökas med AEM Dispatcher-modulen. Den cachelagrar webbsidor som skapats av publiceringsinstansen för att förbättra prestandan.

Det finns många avancerade alternativ och lite mer detaljerade anvisningar för den här konfigurationen, men det grundläggande mönstret för författare, publicering och utskickare är kärnan i de flesta distributioner. Vi börjar med att fokusera på en enkel konfiguration. Här följer diskussioner om avancerade driftsättningsalternativ.

I följande avsnitt beskrivs båda scenarierna:

* **Lokalt**: AEM driftsätts och hanteras i er företagsmiljö.

* **Managed Services - Cloud Manager för Adobe Experience Manager**: AEM driftsätts och hanteras av Adobe Managed Services.

### Lokalt {#on-premise}

Du kan installera AEM på servrar i din företagsmiljö. Typiska installationsinstanser är: Utvecklings-, testnings- och publiceringsmiljöer. Se [Komma igång](/help/sites-deploying/deploy.md#getting%20started) om du vill ha grundläggande information om hur du får AEM program att installera lokalt.

Mer information om de typiska lokala distributionerna finns i [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md).

### Managed Services med Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services är en komplett lösning för Digital Experience Management. Det ger fördelar med upplevelseleverans i molnet samtidigt som man behåller kontrollen, säkerheten och anpassningsfördelarna med en lokal driftsättning. AEM Managed Services gör det möjligt för kunderna att lansera snabbare genom att driftsätta i molnet och även genom att lära sig de bästa metoderna och den bästa supporten från Adobe. Organisationer och företagsanvändare kan engagera kunderna på minimal tid, öka marknadsandelen och fokusera på att skapa innovativa marknadsföringskampanjer samtidigt som IT-avdelningen minskar bördan.

Med AEM Managed Services kan man dra nytta av följande fördelar:

**Snabbare time to market:** Med den flexibla molninfrastrukturen i Adobe Managed Services kan man snabbt planera, lansera och optimera framgångsrika digitala upplevelser. Adobe hanterar molnarkitekturen utan ytterligare kapital-, maskinvaru- eller programvarubehov och Adobe kundlösningstekniker, hjälp med AEM arkitektur, provisionering, anpassning för att ansluta till back-end-appar och praktiska användningsmetoder.

**Högre prestanda:** Ger tillförlitliga digitala upplevelser för företaget med fyra alternativ för tillgänglighet: 99,5 %, 99,9 %, 99,95 % och 99,99 %. Dessutom kan du använda automatiska modeller för säkerhetskopiering och återställning i flera lägen för att säkerställa tillförlitlighet och hantering av oförutsedda händelser.

**Optimerade IT-kostnader:** Proaktiv vägledning och expertis hjälper organisationer att hålla sig uppdaterade med den senaste versionen av AEM. Adobe Platinum Maintenance and Support ingår automatiskt i nya driftsättningar av AMS Enterprise/Basic, med teknisk expertis och driftserfarenhet för att hjälpa företag att underhålla sina verksamhetskritiska applikationer. Kostnadsfria grundläggande analyser eller Target-funktioner ger ytterligare värde, särskilt för medelstora organisationer med begränsade behov av analys och personalisering.

**Högsta säkerhet:** Säkerställer fysisk säkerhet, nätverks- och datasäkerhet i företagsklass genom att lagra kundapplikationer i en begränsad åtkomstfunktion, bakom brandväggssystem eller i ett virtuellt privat moln. Den innehåller virtuella datorer med en klientorganisation och robust kryptering för datalagring, antivirala program och dataisolering.

**Cloud Manager**: Cloud Manager, som ingår i Adobe Experience Manager Managed Services-erbjudandet, är en självbetjäningsportal som ytterligare gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet. Den innehåller en modern pipeline för kontinuerlig integrering och kontinuerlig leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet. Cloud Manager är bara tillgängligt för Adobe-kunder med hanterade tjänster.

Mer information om Cloud Manager och dess resurser finns i [**Användarhandbok för Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html).

## Komma igång {#getting-started}

### Förutsättningar {#prerequisites}

Medan produktionsinstanser körs på dedikerade datorer som kör ett operativsystem som stöds officiellt (se [Tekniska krav](/help/sites-deploying/technical-requirements.md)) kommer Experience Manager-servern att köras på alla system som har stöd för [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8).

För att bli bekant och för att kunna utveckla AEM är det vanligt att använda en instans som är installerad på din dator och som kör Apple OS X eller datorversioner av Microsoft® Windows eller Linux®.

På klientsidan fungerar AEM med alla moderna webbläsare (**Microsoft® Edge**, **Internet Explorer** 11, **Krom **51+** **, **Firefox **47+, **Safari** 8+) på både dator och surfplatta. Se [Klientplattformar som stöds](/help/sites-deploying/technical-requirements.md#supported-client-platforms) för mer information.

### Hämta programvaran {#getting-the-software}

Kunder med giltigt underhålls- och supportavtal ska ha fått ett e-postmeddelande med en kod och kunna hämta AEM från [**Adobe licenswebbplats**](https://licensing.adobe.com/). Affärspartners kan begära nedladdningsåtkomst från [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Det AEM programpaketet finns i två former:

* **cq-quickstart-6.5.0.jar:** En fristående körbar fil *jar* som innehåller allt du behöver för att komma igång.

* **cq-quickstart-6.5.0.war:** A *krig* -fil för distribution till en tredjepartsprogramserver.

I följande avsnitt beskriver vi **fristående installation**. Mer information om hur du installerar AEM på en programserver finns i [Installation av programserver](/help/sites-deploying/application-server-install.md).

### Lokal standardinstallation {#default-local-install}

1. Skapa en installationskatalog på den lokala datorn. Till exempel:

   Installationsplats för UNIX®: **/opt/aem**

   Installationsplats för Windows: **`C:\Program Files\aem`**

   Det är också vanligt att du installerar exempelinstanser i en mapp direkt på skrivbordet. I alla händelser hänvisar Adobe till denna plats i allmänhet som

   `<aem-install>`

   *Sökvägen till filkatalogen får endast bestå av ASCII-tecken från USA.*

1. Placera **jar** och **licens** filer i den här katalogen:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Om du inte anger en `license.properties` AEM dirigerar om webbläsaren till en **Välkommen** när programmet startas, där du kan ange en licensnyckel. Du måste begära en giltig licensnyckel från Adobe om du inte redan har en.

1. Om du vill starta instansen i en GUI-miljö dubbelklickar du på **`cq-quickstart-6.5.0.jar`** -fil.

   Du kan även starta AEM från kommandoraden:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM tar några minuter att packa upp burkfilen, installera sig själv och starta. Ovannämnda procedur ger följande resultat:

* en **AEM** instance
* körs **localhost**
* på port **4502**

Om du vill komma åt instansen pekar du i webbläsaren på:

**`https://localhost:4502`**

Resultatet i författarinstansen konfigureras automatiskt för att ansluta till en **publish instance** på **`localhost:4503`**.

### Skapa och publicera installationer {#author-and-publish-installs}

standardinstallation (en **författare** instans på **`localhost:4502`**) kan ändras genom att du byter namn på `jar` innan du startar programmet för första gången. Namnmönstret är:

**`cq-<instance-type>-p<port-number>.jar`**

Byt namn på filen till

**`cq-author-p4502.jar`**

Och när du startar programmet körs en författarinstans på **`localhost:4502`**.

På samma sätt byter du namn på och startar filen

**`cq-publish-p4503.jar`**

Resultat av en publiceringsinstans som körs på **`localhost:4503`**.

Du installerar de här två instanserna i

`<aem-install>/author`och

**`<aem-install>/publish`**

Mer information om hur du anpassar installationen finns i:

* [Anpassad fristående installation](/help/sites-deploying/custom-standalone-install.md)
* [Körningslägen](/help/sites-deploying/configure-runmodes.md)

### Opackad installationskatalog {#unpacked-install-directory}

När snabbstartsburken startas för första gången packas den upp i samma katalog under en ny underkatalog som kallas `crx-quickstart`. Du bör ha följande:

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

Om instansen installerades från användargränssnittet öppnas ett webbläsarfönster automatiskt och ett skrivbordsprogramfönster öppnas med instansens värd och port och en på/av-knapp:

![startskärmen](assets/screen_shot_.png)

>[!NOTE]
>
>Om du använder symboler kan du titta på [problem med symbollänk](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Starta och stoppa {#starting-and-stopping}

När AEM har packat upp sig själv och startat för första gången startar du instansen genom att dubbelklicka på burkfilen i installationskatalogen, utan att installera om den.

Om du vill stoppa instansen från användargränssnittet klickar du på knappen **på/av** växla till skrivbordsprogramfönstret.

Du kan också stoppa och starta AEM från kommandoraden. Om du redan har installerat instansen för första gången visas **kommandoradsskript** är här:

**`<aem-install>/crx-quickstart/bin/`**

Den här mappen innehåller följande UNIX®-baserade gränssnittsskript:

* **`start`**: Startar instansen
* `stop`: Stoppar instansen
* **`status`**: Rapporterar instansens status
* **`quickstart`**: Används för att konfigurera startinformation, om det behövs.

Det finns också motsvarande **`bat`** filer för Windows. Mer detaljerad information finns i:

* [Kommandoradens start och stopp](/help/sites-deploying/command-line-start-and-stop.md)

AEM startar och dirigerar automatiskt om webbläsaren till rätt sida, vanligtvis inloggningssidan, till exempel:

`https://localhost:4502/`

![inloggningsskärm](assets/screen_shot_2019-04-08at83533am.png)

När du har loggat in har du åtkomst till AEM. Mer information, beroende på din roll, finns i:

* [Redigering](/help/sites-authoring/first-steps.md)
* [Administratör](/help/sites-administering/home.md)
* [Utvecklar](/help/sites-developing/getting-started.md)
* [Hantera](/help/managing/best-practices.md)

## Avancerad distribution {#advanced-deployment}

Ovanstående avsnitt bör ge dig en god förståelse för grunderna i AEM installation. Att installera ett komplett AEM kan dock innebära en betydligt större komplexitet. Mer information om avancerad installation finns i följande undersidor:

* [Tekniska krav](/help/sites-deploying/technical-requirements.md)
* [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md)
* [Anpassad fristående installation](/help/sites-deploying/custom-standalone-install.md)
* [Installation av programserver](/help/sites-deploying/application-server-install.md)
* [Felsökning](/help/sites-deploying/troubleshooting.md)
* [Kommandoradens start och stopp](/help/sites-deploying/command-line-start-and-stop.md)
* [Konfigurerar](/help/sites-deploying/configuring.md)
* [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Instruktionsartiklar för konfiguration](/help/sites-deploying/ht-deploy.md)
* [Webbkonsol](/help/sites-deploying/web-console.md)
* [Felsökning av replikering](/help/sites-deploying/troubleshoot-rep.md)
* [Bästa praxis](/help/sites-deploying/best-practices.md)
* [Distribuera webbgrupper](/help/communities/deploy-communities.md)
* [Introduktion till AEM](/help/sites-deploying/platform.md)
* [Riktlinjer för prestanda](/help/sites-deploying/performance-guidelines.md)
* [Komma igång med AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Vad är AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
