---
title: Driftsättning och underhåll
seo-title: Driftsättning och underhåll
description: Lär dig hur du kommer igång med AEM.
seo-description: Lär dig hur du kommer igång med AEM.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 1%

---

# Distribuera och underhålla{#deploying-and-maintaining}

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
* [Vad är AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Grundläggande begrepp {#basic-concepts}

### Vad är AEM? {#what-is-aem}

Adobe Experience Manager är ett webbaserat klient-serversystem för att bygga, hantera och driftsätta kommersiella webbplatser och tillhörande tjänster. Det kombinerar ett antal funktioner på infrastruktur- och applikationsnivå i ett enda integrerat paket.

På infrastrukturnivå AEM följande:

* **Webbprogramserver**: AEM kan distribueras i fristående läge (det inkluderar en integrerad Jetty-webbserver) eller som ett webbprogram i en tredjepartsprogramserver.
* **Web Application Framework**: AEM innehåller Sling Web Application Framework som förenklar skrivandet av RESTful, innehållsorienterade webbprogram.
* **Innehållsdatabas**: AEM innehåller en Java Content Repository (JCR), en typ av hierarkisk databas som är särskilt utformad för ostrukturerade och halvstrukturerade data. I databasen lagras inte bara användarriktat innehåll utan även all kod, mallar och interna data som används av programmet.

AEM bygger på denna bas och erbjuder även ett antal funktioner på programnivå för att hantera:

* **Webbplatser**
* **Mobila program**
* **Digitala publikationer**
* **Forms**
* **Digital Assets**
* **Communities**
* **Online Commerce**

Slutligen kan kunderna använda dessa infrastruktur- och programnivåbyggstenar för att skapa anpassade lösningar genom att bygga egna applikationer.

Den AEM servern är **Java-baserad** och körs på de flesta operativsystem som stöder den plattformen. All klientinteraktion med AEM görs via en **webbläsare**.

### Vanliga distributionsscenarier {#typical-deployment-scenarios}

I AEM är &quot;instance&quot; en kopia av AEM som körs på en server. AEM omfattar vanligen minst två instanser, vanligtvis på separata maskiner:

* **Författare**: En AEM som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
* **Publicera**: En AEM som skickar det publicerade innehållet till allmänheten.

De här instanserna är identiska vad gäller installerad programvara. De skiljer sig bara åt genom konfiguration. Dessutom använder de flesta installationer en dispatcher:

* **Dispatcher**: En statisk webbserver (Apache httpd, Microsoft IIS osv.) utökad med AEM. Den cachelagrar webbsidor som skapats av publiceringsinstansen för att förbättra prestandan.

Det finns många avancerade alternativ och funktioner för den här konfigurationen, men det grundläggande mönstret för författare, publicering och utskickare är kärnan i de flesta distributioner. Vi börjar med att fokusera på en relativt enkel lösning. Därefter kommer vi att diskutera avancerade alternativ för driftsättning.

I följande avsnitt beskrivs båda scenarierna:

* **Lokalt**: AEM driftsätts och hanteras i er företagsmiljö.

* **Managed Services - Cloud Manager för Adobe Experience Manager**: AEM driftsätts och hanteras av Adobes hanterade tjänster.

### Lokal {#on-premise}

Du kan installera AEM på servrar i din företagsmiljö. Vanliga installationsinstanser: Utvecklings-, testnings- och publiceringsmiljöer. Se avsnittet [Komma igång](/help/sites-deploying/deploy.md#getting%20started) för mer information om hur du får AEM program att installera det lokalt.

Mer information om typiska lokala distributioner finns i [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md).

### Managed Services med Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services är en komplett lösning för hantering av digitala upplevelser. Det ger fördelar med upplevelseleverans i molnet samtidigt som man behåller alla kontroll-, säkerhets- och anpassningsfördelar som en lokal driftsättning ger. AEM Managed Services gör det möjligt för kunderna att lansera snabbare genom att driftsätta i molnet och även genom att lära sig de bästa metoderna och den bästa supporten från Adobe. Organisationer och företagsanvändare kan engagera kunderna på minimal tid, öka marknadsandelen och fokusera på att skapa innovativa marknadsföringskampanjer samtidigt som IT-avdelningen minskar bördan.

Med AEM Managed Services kan man dra nytta av följande fördelar:

**Snabbare time to Market:** Med flexibel molninfrastruktur i Adobe Managed Services kan organisationer snabbt planera, lansera och optimera framgångsrika digitala upplevelser. Adobe hanterar molnarkitekturen utan ytterligare kapital-, maskinvaru- eller programvarubehov och Adobe&#39;s Customer Success Engineers, hjälp med AEM arkitektur, provisionering, anpassning för att ansluta till serverprogram och bästa praxis för att publicera.

**Högre prestanda:** Ger tillförlitliga digitala upplevelser för företaget med fyra alternativ för tillgänglighet: 99,5 %, 99,9 %, 99,95 % och 99,99 %. Dessutom kan man med programmet automatiskt säkerhetskopiera och återställa flera lägen för att säkerställa tillförlitlighet och beredskapshantering.

**Optimerade IT-kostnader:** Proaktiv vägledning och expertis hjälper organisationer att hålla sig uppdaterade med den senaste versionen av AEM. Adobe Platinum Maintenance and Support ingår automatiskt i nya driftsättningar av AMS Enterprise/Basic, med teknisk expertis och driftserfarenhet som hjälper företag att underhålla sina verksamhetskritiska applikationer. Kostnadsfria grundläggande analyser eller Target-funktioner ger ytterligare värde, särskilt för medelstora organisationer med begränsade behov av analys och personalisering.

**Högsta säkerhet:** Säkerställer fysisk säkerhet, nätverks- och datasäkerhet i företagsklass genom att lagra kundapplikationer i en begränsad åtkomstfunktion, bakom brandväggssystem eller i ett virtuellt privat moln. Den innehåller virtuella datorer med en klientorganisation och robust kryptering för datalagring, antivirala program och dataisolering.

**Cloud Manager**: Cloud Manager, som ingår i Adobe Experience Manager Managed Services-erbjudandet, är en självbetjäningsportal som ytterligare gör det möjligt för organisationer att självhantera Adobe Experience Manager i molnet. Den innehåller en modern pipeline för kontinuerlig integrering och kontinuerlig leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet. Cloud Manager är bara tillgängligt för Adobe-kunder med hanterade tjänster.

Mer information om Cloud Manager och dess resurser finns i [**Användarhandbok för Cloud Manager**](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Komma igång {#getting-started}

### Förutsättningar {#prerequisites}

Medan produktionsinstanser vanligtvis körs på dedikerade datorer som kör ett operativsystem som stöds officiellt (se [Tekniska krav](/help/sites-deploying/technical-requirements.md)), kommer Experience Manager-servern att köras på alla system som stöder [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

För att bli bekant och för att kunna utveckla AEM är det mycket vanligt att använda en instans som är installerad på din lokala dator och som kör Apple OS X eller skrivbordsversioner av Microsoft Windows eller Linux.

På klientsidan fungerar AEM med alla moderna webbläsare (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) både på dator och surfplatta. Mer information finns i [Klientplattformar som stöds](/help/sites-deploying/technical-requirements.md#supported-client-platforms).

### Hämta programvaran {#getting-the-software}

Kunder med giltigt underhålls- och supportavtal bör ha fått ett e-postmeddelande med en kod och kunna hämta AEM från [**Adobe licenswebbplats**](https://licensing.adobe.com/). Affärspartners kan begära nedladdningsåtkomst från [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Programpaketet AEM finns i två former:

* **cq-quickstart-6.5.0.jar:** En fristående körbar  ** jarfil som innehåller allt som behövs för att komma igång.

* **cq-quickstart-6.5.0.war:** En  ** warfile för distribution i en tredjepartsprogramserver.

I följande avsnitt beskriver vi den fristående **installationen**. Mer information om hur du installerar AEM på en programserver finns i [Programserverinstallation](/help/sites-deploying/application-server-install.md).

### Lokal standardinstallation {#default-local-install}

1. Skapa en installationskatalog på den lokala datorn. Till exempel:

   Installationsplats för UNIX: **/opt/aem**

   Installationsplats för Windows: **`C:\Program Files\aem`**

   Det är också vanligt att du installerar exempelinstanser i en mapp direkt på skrivbordet. I vilket fall som helst ska vi i allmänhet hänvisa till den här platsen som:

   `<aem-install>`

   *Observera att sökvägen till filkatalogen endast får bestå av ASCII-tecken från USA.*

1. Placera filerna **jar** och **license **i den här katalogen:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Om du inte anger en `license.properties`-fil dirigeras AEM om webbläsaren till en **välkomstskärm när du startar, där du kan ange en licensnyckel.** Du måste begära en giltig licensnyckel från Adobe om du inte redan har en.

1. Om du vill starta instansen i en GUI-miljö dubbelklickar du bara på filen **`cq-quickstart-6.5.0.jar`**.

   Du kan även starta AEM från kommandoraden. För en 32-bitars Java VM anger du följande:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   För en 64-bitars virtuell dator anger du:

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM tar några minuter att packa upp burkfilen, installera och starta. Ovannämnda procedur ger följande resultat:

* en **AEM författare**-instans
* körs på **localhost**
* på port **4502**

Så här kommer du åt instansen genom att peka webbläsaren på:

**`https://localhost:4502`**

Resultatet i författarinstansen konfigureras automatiskt för att ansluta till en **publiceringsinstans** på **`localhost:4503`**.

### Skapa och publicera installationer {#author-and-publish-installs}

Standardinstallationen (en **författare**-instans på **`localhost:4502`**) kan ändras genom att namnet på filen `jar` ändras innan den startas för första gången. Namnmönstret är:

**`cq-<instance-type>-p<port-number>.jar`**

Byt namn på filen till

**`cq-author-p4502.jar`**

om du startar programmet kommer en författarinstans att köras på **`localhost:4502`**.

På samma sätt byter du namn på och startar filen

**`cq-publish-p4503.jar`**

resulterar i att en publiceringsinstans körs på **`localhost:4503`**.

Du installerar de här två instanserna i

`<aem-install>/author`and

**`<aem-install>/publish`**

Mer information om hur du anpassar installationen finns i:

* [Anpassad fristående installation](/help/sites-deploying/custom-standalone-install.md)
* [Körningslägen](/help/sites-deploying/configure-runmodes.md)

### Opackad installationskatalog {#unpacked-install-directory}

När snabbstartburken startas för första gången packas den upp i samma katalog under en ny underkatalog som heter `crx-quickstart`. Resultatet blir följande:

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

Om instansen installerades från användargränssnittet öppnas ett webbläsarfönster automatiskt och ett skrivbordsprogramfönster öppnas med instansens värd och port samt en på/av-knapp:

![startskärmen](assets/screen_shot_.png)

>[!NOTE]
>
>Om du använder symboler bör du ta en titt på [problem med symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Starta och stoppa {#starting-and-stopping}

När AEM har packat upp sig och startat för första gången startar du bara instansen genom att dubbelklicka på burkfilen i installationskatalogen. Den installeras inte igen.

Om du vill stoppa instansen från det grafiska användargränssnittet klickar du på **på/av** i skrivbordsprogramfönstret.

Du kan också stoppa och starta AEM från kommandoraden. Om du redan har installerat instansen för första gången finns kommandoradsskripten **här:**

**`<aem-install>/crx-quickstart/bin/`**

Den här mappen innehåller följande Unix-basskalskript:

* **`start`**: Startar instansen
* `stop`: Stoppar instansen
* **`status`**: Rapporterar status för instansen
* **`quickstart`**: Används för att konfigurera startinformation, om det behövs.

Det finns också motsvarande **`bat`**-filer för Windows. Mer detaljerad information finns i:

* [Kommandoradens start och stopp](/help/sites-deploying/command-line-start-and-stop.md)

AEM startar och dirigerar automatiskt om webbläsaren till rätt sida, vanligtvis inloggningssidan; till exempel:

`https://localhost:4502/`

![inloggningsskärm](assets/screen_shot_2019-04-08at83533am.png)

När du är inloggad har du tillgång till AEM. Mer information, beroende på din roll, finns i:

* [Redigering](/help/sites-authoring/home.md)
* [Administratör](/help/sites-administering/home.md)
* [Utveckling](/help/sites-developing/home.md)
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
* [Vad är AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
