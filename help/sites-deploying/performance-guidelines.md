---
title: Riktlinjer för prestanda
seo-title: Riktlinjer för prestanda
description: Den här artikeln innehåller allmänna riktlinjer för hur du optimerar prestanda för din AEM-distribution.
seo-description: Den här artikeln innehåller allmänna riktlinjer för hur du optimerar prestanda för din AEM-distribution.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
translation-type: tm+mt
source-git-commit: a678716e2c0520891e4228bc49b075f070ea45b7

---


# Riktlinjer för prestanda{#performance-guidelines}

Den här sidan innehåller allmänna riktlinjer för hur du optimerar prestanda för din AEM-distribution. Om du inte har använt AEM tidigare bör du gå igenom följande sidor innan du börjar läsa riktlinjerna för prestanda:

* [Grundläggande AEM-begrepp](/help/sites-deploying/deploy.md#basic-concepts)
* [Översikt över lagring i AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md)
* [Tekniska krav](/help/sites-deploying/technical-requirements.md)

Illustrator below are the deployment options available for AEM (scroll to view all the options):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Produkt</strong></p> </td>
   <td><p><strong>Topologi</strong></p> </td>
   <td><p><strong>Operativsystem</strong></p> </td>
   <td><p><strong>Programserver</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Dokumentskydd</strong></p> </td>
   <td><p><strong>Micro Kernel</strong></p> </td>
   <td><p><strong>Datastore</strong></p> </td>
   <td><p><strong>Indexering</strong></p> </td>
   <td><p><strong>Webbserver</strong></p> </td>
   <td><p><strong>Webbläsare</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Webbplatser</p> </td>
   <td><p>Ej-HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>tar</p> </td>
   <td><p>Segment</p> </td>
   <td><p>Egenskap</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Mål</p> </td>
  </tr>
  <tr>
   <td><p>Resurser</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>Arkiv</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analyser</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>Red Hat</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Formulär</p> </td>
   <td><p>Författaravlastning</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Krom</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>Mobil</p> </td>
   <td><p>Författarkluster</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>Målgrupp</p> </td>
  </tr>
  <tr>
   <td><p>Flera platser</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Resurser</p> </td>
  </tr>
  <tr>
   <td><p>Handel</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Aktivering</p> </td>
  </tr>
  <tr>
   <td><p>Dynamiska medier</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Mobil</p> </td>
  </tr>
  <tr>
   <td><p>Varumärkesportal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Skärmar</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Dokumentsäkerhet</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Processhantering</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>datorprogram</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Riktlinjerna för prestanda gäller främst AEM Sites.

## När prestandarådarna ska användas {#when-to-use-the-performance-guidelines}

Du bör använda riktlinjerna för prestanda i följande situationer:

* **Första gången du distribuerar**: När du planerar att distribuera AEM-platser eller -resurser för första gången är det viktigt att du förstår vilka alternativ som är tillgängliga när du konfigurerar mikrokärnan, nodarkivet och datalagret (jämfört med standardinställningarna). Om du till exempel ändrar standardinställningarna för datalagret för tarMK till fildatalagret.
* **Uppgradera till en ny version**: När du uppgraderar till en ny version är det viktigt att du förstår prestandaskillnaderna jämfört med körningsmiljön. Du kan till exempel uppgradera från AEM 6.1 till 6.2 eller från AEM 6.0 CRX2 till 6.2 OAK.
* **Svarstiden är långsam**: När den valda Nodestore-arkitekturen inte uppfyller dina krav är det viktigt att förstå prestandaskillnaderna jämfört med andra topologialternativ. Du kan till exempel distribuera tarMK i stället för MongoMK, eller använda ett File Data Store i stället för ett Amazon S3- eller Microsoft Azure-datalager.
* **Lägga till fler författare**: När den rekommenderade TjäraMK-topologin inte uppfyller prestandakraven och om du uppgraderar redigeringsnoden så att den maximala tillgängliga kapaciteten nås, är det viktigt att förstå prestandaskillnaderna jämfört med att använda MongoMK med tre eller fler Author-noder. Du kan till exempel distribuera MongoMK i stället för tarMK.
* **Lägga till mer innehåll**: När den rekommenderade datalagerarkitekturen inte uppfyller dina krav är det viktigt att förstå prestandaskillnaderna jämfört med andra datalageralternativ. Exempel: med Amazon S3 eller Microsoft Azure Data Store i stället för ett File Data Store.

## Introduktion {#introduction}

I det här kapitlet ges en allmän översikt över AEM-arkitekturen och dess viktigaste komponenter. Den innehåller också riktlinjer för utveckling och beskriver de testscenarier som används i prestandatesterna TjärMK och MongoMK.

### AEM Platform {#the-aem-platform}

AEM-plattformen består av följande komponenter:

![chlimage_1](assets/chlimage_1a.png)

Mer information om AEM-plattformen finns i [Vad är AEM](/help/sites-deploying/deploy.md#what-is-aem).

### AEM-arkitekturen {#the-aem-architecture}

Det finns tre viktiga byggstenar för en AEM-driftsättning. Den **författarinstans** som används av innehållsförfattare, redigerare och godkännare för att skapa och granska innehåll. När innehållet godkänns publiceras det till en andra instanstyp som heter **Publish Instance** , som slutanvändarna kommer åt det från. Det tredje byggblocket är **Dispatcher** , som är en modul som hanterar cachelagring och URL-filtrering och som är installerad på webbservern. Mer information om AEM-arkitekturen finns i [Vanliga distributionsscenarier](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro Kernels {#micro-kernels}

Micro Kernels fungerar som persistencehanterare i AEM. Det finns tre typer av Micro Kernels som används med AEM: TARMK, MongoDB och Relational Database (med begränsat stöd). Vilken som passar dina behov beror på syftet med instansen och vilken distributionstyp du överväger. Mer information om Micro Kernels finns på sidan [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md) .

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

I AEM kan binära data lagras oberoende av innehållsnoder. Platsen där binära data lagras kallas för **datalagret**, medan platsen för innehållsnoderna och -egenskaperna kallas **nodarkivet**.

>[!NOTE]
>
>Adobe rekommenderar att TARMK är standardbeständighetstekniken som används av kunder för både AEM Author och Publish.

>[!CAUTION]
>
>Mikrokärnan i relationsdatabasen har begränsat stöd. Kontakta [Adobes kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) innan du använder den här typen av mikrokärna.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Datalager {#data-store}

När du hanterar ett stort antal binära filer bör du använda ett externt datalager i stället för standardnodarkiven för att maximera prestandan. Om ditt projekt till exempel kräver ett stort antal medieresurser kan du lagra dem under Arkiv eller Azure/S3 Data Store så att du kommer åt dem snabbare än att lagra dem direkt i en MongoDB.

Mer information om tillgängliga konfigurationsalternativ finns i [Konfigurera nod- och datalager](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe rekommenderar att du väljer alternativet att distribuera AEM på Azure eller Amazon Web Services (AWS) med Adobes hanterade tjänster, där kunderna drar nytta av ett team som har erfarenhet och kunskaper av att driftsätta och driva AEM i dessa molndatormiljöer. Se vår [ytterligare dokumentation om Adobes hanterade tjänster](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).
>
>För rekommendationer om hur AEM ska distribueras på Azure eller AWS, utanför Adobes hanterade tjänster, rekommenderar vi starkt att du arbetar direkt med molnleverantören eller en av våra partners som stöder distributionen av AEM i den molnmiljö du väljer. Den valda molnleverantören eller partnern ansvarar för storleksspecifikationerna, designen och implementeringen av den arkitektur som de stöder för att uppfylla dina specifika krav på prestanda, belastning, skalbarhet och säkerhet.
>
>Mer information finns även på sidan [Tekniska krav](/help/sites-deploying/technical-requirements.md#supported-platforms) .

### Sök {#search-features}

I det här avsnittet finns de anpassade indexproviders som används med AEM. Mer information om indexering finns i [Fråga och indexering](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>För de flesta installationer rekommenderar Adobe att du använder Lucene-index. Du bör endast använda Solr för skalbarhet vid specialiserad och komplex driftsättning.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Utvecklingsriktlinjer {#development-guidelines}

Du bör utveckla för AEM med sikte på **prestanda och skalbarhet**. Nedan visas ett antal metodtips som du kan följa:

**GÖR**

* Separera presentation, logik och innehåll
* Använd befintliga AEM API:er (t.ex.: Sling) och verktyg (t.ex. replikering)
* Utveckla i rätt sammanhang
* Utveckla för optimal tillgänglighet
* Minimera antalet besparingar (t.ex.: genom att använda tillfälliga arbetsflöden)
* Kontrollera att alla HTTP-slutpunkter är RESTful
* Begränsa omfattningen av JCR-observation
* Var uppmärksam på asynkron tråd

**INTE**

* Använd inte JCR-API:er direkt om du kan
* Ändra inte /libs, utan använd övertäckningar
* Använd inte frågor där det är möjligt
* Använd inte Sling Bindings för att hämta OSGi-tjänster i Java-kod, utan använd istället:

   * @Referens i en DS-komponent
   * @Injicera i en körningsmodell
   * sling.getService() i en lättanvänd klass
   * sling.getService() i en JSP
   * en ServiceTracker
   * direktåtkomst till OSGi-tjänstregistret

Mer information om hur du utvecklar med AEM finns i [Utveckla - Grunderna](/help/sites-developing/the-basics.md). Mer information finns i Bästa metoder för [utveckling](/help/sites-developing/best-practices.md).

### Benchmark-scenarier {#benchmark-scenarios}

>[!NOTE]
>
>Alla test som visas på den här sidan har utförts i laboratoriemiljö.

De testscenarier som beskrivs nedan används för prestandatestavsnitten i kapitlen TjärMK, MongoMk och TjärMK jämfört med MongoMk. Om du vill se vilket scenario som användes för ett visst test av referensvärden läser du avsnittet Scenario i tabellen [Tekniska specifikationer](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) .

**Scenario för en produkt**

AEM Assets:

* Användarinteraktioner: Bläddra bland resurser/Sök resurser/Hämta resurs/Läs resursmetadata/Uppdatera resursmetadata/Överför resurs/Kör arbetsflöde för överföring av resurs
* Körningsläge: samtidiga användare, enstaka interaktion per användare

**Scenario med blandade produkter**

AEM Sites + Assets:

* Webbplatsens användarinteraktioner: Läs artikelsidan / Läs sidan / Skapa stycke / Redigera stycke / Skapa innehållssida / Aktivera innehållssida / Författarsökning
* Resursens användarinteraktioner: Bläddra bland resurser/Sök resurser/Hämta resurs/Läs resursmetadata/Uppdatera resursmetadata/Överför resurs/Kör arbetsflöde för överföring av resurs
* Körningsläge: samtidiga användare, blandade interaktioner per användare

**Vertikalt scenario för användning**

Media:

* Läs artikelsida (27,4 %), Läs sida (10,9 %), Skapa session (2,6 %), Aktivera innehållssida (1,7 %), Skapa innehållssida (0,4 %), Skapa stycke (4,3 %), Redigera stycke (0,9 %), Bildkomponent (0,9 %), Bläddra bland resurser (20 %), Läs resursmetadata (2) 8,5 %), Hämta resurs (4,2 %), Sökresurs (0,2 %), Uppdatera resursmetadata (2,4 %), Överför resurs (1,2 %), Bläddra i projekt (4,9 %), Läs projekt (6,6 %), Lägg till resurs i projekt (1,2 %), Lägg till webbplats i projekt (1,2 %), Skapa projekt (0,1 %), Författare eller Sök (0,4 %)
* Körningsläge: samtidiga användare, blandade interaktioner per användare

## tarMK {#tarmk}

I det här kapitlet finns allmänna riktlinjer för prestanda för TjäraMK som specificerar minimikraven för arkitektur och inställningskonfigurationen. Riktmärkestester tillhandahålls också för ytterligare förtydliganden.

Adobe rekommenderar att TARMK är standardbeständighetstekniken som används av kunder i alla distributionsscenarier, både för AEM Author- och Publish-instanserna.

Mer information om TjäraMK finns i [Distributionsscenarier](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) och [Tjärlagring](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### TaMK - riktlinjer för minimiarkitektur {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>De riktlinjer för minimiarkitektur som presenteras nedan gäller för produktionsmiljöer och stora trafikplatser. Detta är **inte** de [minimispecifikationer](/help/sites-deploying/technical-requirements.md#prerequisites) som krävs för att köra AEM.

För att få goda prestanda när du använder tarMK bör du utgå från följande arkitektur:

* En författarinstans
* Två publiceringsinstanser
* Två utskickare

Nedan visas riktlinjerna för arkitektur för AEM-webbplatser och AEM Assets.

>[!NOTE]
>
>Binärfri replikering ska aktiveras **PÅ** om fildatalagret delas.

**Riktlinjer för TAR-arkitektur för AEM-webbplatser**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Riktlinjer för TAR-arkitektur för AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Riktlinje för inställningar för TARMK {#tarmk-settings-guideline}

För bästa prestanda bör du följa riktlinjerna nedan. Instruktioner om hur du ändrar inställningarna [finns på den här sidan](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Inställning</strong></td>
   <td><strong>Parameter</strong></td>
   <td><strong>Värde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Sling-jobbköer</td>
   <td><code>queue.maxparallel</code></td>
   <td>Ange värdet till hälften av antalet processorkärnor. </td>
   <td>Som standard är antalet samtidiga trådar per jobbkö lika med antalet processorkärnor.</td>
  </tr>
  <tr>
   <td>Bevilja tillfällig arbetsflödeskö</td>
   <td><code>Max Parallel</code></td>
   <td>Ange värdet till hälften av antalet processorkärnor</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM-parametrar</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>Lägg till de här JVM-parametrarna i AEM-startskriptet för att förhindra att omfattande frågor överbelastar systemen.</td>
  </tr>
  <tr>
   <td>Lucene-indexkonfiguration</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Aktiverad</p> <p>Aktiverad</p> <p>Aktiverad</p> </td>
   <td>Mer information om tillgängliga parametrar finns på <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">den här sidan</a>.</td>
  </tr>
  <tr>
   <td>Datalager = S3 Datastore</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) eller mindre</p> <p>2-10 % av maximal stackstorlek</p> </td>
   <td>Se även <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Data Store-konfigurationer</a>.</td>
  </tr>
  <tr>
   <td>Arbetsflöde för DAM-uppdatering</td>
   <td><code>Transient Workflow</code></td>
   <td>checked</td>
   <td>Det här arbetsflödet hanterar uppdateringen av resurser.</td>
  </tr>
  <tr>
   <td>DAM MetaData Writeback</td>
   <td><code>Transient Workflow</code></td>
   <td>checked</td>
   <td>Detta arbetsflöde hanterar XMP-återskrivning till det ursprungliga binärdokumentet och anger det senaste ändringsdatumet i JCR.</td>
  </tr>
 </tbody>
</table>

### Resultatjämförelse för tarMK {#tarmk-performance-benchmark}

#### Tekniska specifikationer {#technical-specifications}

Testerna utfördes på följande specifikationer:

|  | **Författarnod** |
|---|---|
| Server | Maskinvara av oädel metall (HP) |
| Operativsystem | RedHat Linux |
| Processor/kärnor | Processorn Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 kärnor |
| RAM | 32GB |
| Skiva | Magnetiskt |
| Java | Oracle JRE version 8 |
| JVM-heap | 16GB |
| Produkt | AEM 6.2 |
| Nodestore | tarMK |
| Datastore | Fil-DS |
| Scenario | En produkt: Resurser/30 samtidiga trådar |

#### Resultat av prestandatest {#performance-benchmark-results}

>[!NOTE]
>
>Siffrorna nedan har normaliserats till 1 som baslinje och är inte de faktiska flödenumren.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

Den främsta anledningen till att du väljer MongoMK-beständighetsbackend framför tarMK är att skalförändra instanserna vågrätt. Det innebär att två eller flera aktiva författarinstanser alltid körs och att MongoDB används som beständigt lagringssystem. Behovet av att köra mer än en författarinstans beror i allmänhet på att processorn och minneskapaciteten på en enda server, som stöder alla samtidiga redigeringsaktiviteter, inte längre är hållbara.

Mer information om TjäraMK finns i [Distributionsscenarier](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) och [Mongo-lagring](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Riktlinjer för minimiarkitektur i MongoMK {#mongomk-minimum-architecture-guidelines}

För att få bra prestanda när du använder MongoMK bör du utgå från följande arkitektur:

* Tre författarinstanser
* Två publiceringsinstanser
* Tre MongoDB-instanser
* Två utskickare

>[!NOTE]
>
>I produktionsmiljöer kommer MongoDB alltid att användas som en replikuppsättning med en primär och två sekundära. Läsningar och skrivningar går till huvudlistan och läsningar kan gå till de sekundära. Om lagring inte är tillgängligt kan en av de sekundära ersättas med en skiljedomare, men MongoDB-replikuppsättningar måste alltid bestå av ett ojämnt antal instanser.

>[!NOTE]
>
>Binärfri replikering ska aktiveras **PÅ** om fildatalagret delas.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Riktlinjer för MongoMK-inställningar {#mongomk-settings-guidelines}

För bästa prestanda bör du följa riktlinjerna nedan. Instruktioner om hur du ändrar inställningarna [finns på den här sidan](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>Inställning</strong></td>
   <td><strong>Parameter</strong></td>
   <td><strong>Värde (standard)</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Sling-jobbköer</td>
   <td><code>queue.maxparallel</code></td>
   <td>Ange värdet till hälften av antalet processorkärnor. </td>
   <td>Som standard är antalet samtidiga trådar per jobbkö lika med antalet processorkärnor.</td>
  </tr>
  <tr>
   <td>Bevilja tillfällig arbetsflödeskö</td>
   <td><code>Max Parallel</code></td>
   <td>Ange värdet till hälften av antalet processorkärnor.</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM-parametrar</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>Lägg till de här JVM-parametrarna i AEM-startskriptet för att förhindra att omfattande frågor överbelastar systemen.</td>
  </tr>
  <tr>
   <td>Lucene-indexkonfiguration</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Aktiverad</p> <p>Aktiverad</p> <p>Aktiverad</p> </td>
   <td>Mer information om tillgängliga parametrar finns på <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">den här sidan</a>.</td>
  </tr>
  <tr>
   <td>Datalager = S3 Datastore</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) eller mindre</p> <p>2-10 % av maximal stackstorlek</p> </td>
   <td>Se även <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Data Store-konfigurationer</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>Standardstorleken för cacheminnet är 256 MB.</p> <p>Påverkar hur lång tid det tar att göra cachen ogiltig.</p> </td>
  </tr>
  <tr>
   <td>ek-observation</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>min &amp; max = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Prestandatest för MongoMK {#mongomk-performance-benchmark}

### Tekniska specifikationer {#technical-specifications-1}

Testerna utfördes på följande specifikationer:

|  | **Författarnod** | **MongoDB-nod** |
|---|---|---|
| Server | Maskinvara av oädel metall (HP) | Maskinvara av oädel metall (HP) |
| Operativsystem | RedHat Linux | RedHat Linux |
| Processor/kärnor | Processorn Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 kärnor | Processorn Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 kärnor |
| RAM | 32GB | 32GB |
| Skiva | Magnetiskt - >1 k IOPS | Magnetiskt - >1 k IOPS |
| Java | Oracle JRE version 8 | Ej tillämpligt |
| JVM-heap | 16GB | Ej tillämpligt |
| Produkt | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | Ej tillämpligt |
| Datastore | Fil-DS | Ej tillämpligt |
| Scenario | En produkt: Resurser/30 samtidiga trådar | En produkt: Resurser/30 samtidiga trådar |

### Resultat av prestandatest {#performance-benchmark-results-1}

>[!NOTE]
>
>Siffrorna nedan har normaliserats till 1 som baslinje och är inte de faktiska flödenumren.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## tarMK jämfört med MongoMK {#tarmk-vs-mongomk}

Den grundläggande regeln som ska beaktas när du väljer mellan de två är att tarMK är utformat för prestanda, medan MongoMK används för skalbarhet. Adobe rekommenderar att TARMK är standardbeständighetstekniken som används av kunder i alla distributionsscenarier, både för AEM Author- och Publish-instanserna.

Den främsta anledningen till att du väljer MongoMK-beständighetsbackend framför tarMK är att skalförändra instanserna vågrätt. Det innebär att två eller flera aktiva författarinstanser alltid körs och att MongoDB används som beständigt lagringssystem. Behovet av att köra mer än en författarinstans beror i allmänhet på att processorn och minneskapaciteten på en enda server, som stöder alla samtidiga redigeringsaktiviteter, inte längre är hållbara.

Mer information om TjäraMK jämfört med MongoMK finns i [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Riktlinjer för tarMK jämfört med MongoMk {#tarmk-vs-mongomk-guidelines}

**Fördelar med tarMK**

* Ändamålsenlig för content management-program
* Filerna är alltid konsekventa och kan säkerhetskopieras med valfritt filbaserat säkerhetskopieringsverktyg
* Tillhandahåller en failover-mekanism - mer information finns i [Vänteläge](/help/sites-deploying/tarmk-cold-standby.md) för Cold
* Ger höga prestanda och tillförlitlig datalagring med minimal driftkostnad
* Lägre ägandekostnader (total ägandekostnad)

**Kriterier för att välja MongoMK**

* Antal namngivna användare anslutna under en dag: i tusental eller mer
* Antal samtidiga användare: på hundratals eller fler
* Volym för tillgångsinmatningar per dag: på hundratusentals eller fler
* Antal sidredigeringar per dag: på hundratusentals eller fler
* Antal sökningar per dag: tiotusentals eller fler

### Benchmarks för tarMK jämfört med MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>Siffrorna nedan har normaliserats till 1 som baslinje och är inte faktiska flödesnummer.

### Tekniska specifikationer för scenario 1 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Author OAK Node</strong></td>
   <td><strong>MongoDB-nod</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Server</td>
   <td>Maskinvara av oädel metall (HP)</td>
   <td>Maskinvara av oädel metall (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Operativsystem</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>Processor/kärnor</td>
   <td>Processorn Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 kärnor</td>
   <td>Processorn Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 kärnor</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32GB</td>
   <td>32GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skiva</td>
   <td>Magnetiskt - &gt;1 k IOPS</td>
   <td>Magnetiskt - &gt;1 k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE version 8</td>
   <td>Ej tillämpligt</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM Heap16 GB</td>
   <td>16GB</td>
   <td>Ej tillämpligt</td>
   <td> </td>
  </tr>
  <tr>
   <td>Produkt </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>tarMK eller MongoMK</td>
   <td>Ej tillämpligt</td>
   <td> </td>
  </tr>
  <tr>
   <td>Datastore</td>
   <td>Fil-DS </td>
   <td>Ej tillämpligt</td>
   <td> </td>
  </tr>
  <tr>
   <td>Scenario</td>
   <td><p><br /> En produkt: Resurser/30 samtidiga trådar per körning</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Resultat av prestandatest för scenario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Tekniska specifikationer för scenario 2 {#scenario-technical-specifications-1}

>[!NOTE]
>
>Om du vill aktivera samma antal författare med MongoDB som med ett TarmMK-system behöver du ett kluster med två AEM-noder. Ett mongoDB-kluster med fyra noder kan hantera 1,8 gånger så många författare som en tarMK-instans. Ett åtta-nods MongoDB-kluster kan hantera 2,3 gånger så många författare som en tarMK-instans.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Författare tarMK-nod</strong></td>
   <td><strong>Författare MongoMK-nod</strong></td>
   <td><strong>MongoDB-nod</strong></td>
  </tr>
  <tr>
   <td>Server</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>Operativsystem</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
  </tr>
  <tr>
   <td>Processor/kärnor</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60GB</td>
   <td>60GB</td>
   <td>60GB</td>
  </tr>
  <tr>
   <td>Skiva</td>
   <td>SSD - 10 000 IOPS</td>
   <td>SSD - 10 000 IOPS</td>
   <td>SSD - 10 000 IOPS</td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE version 8</td>
   <td><br /> Oracle JRE version 8</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>JVM Heap16 GB</td>
   <td>30GB</td>
   <td>30GB</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Produkt </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>tarMK </td>
   <td>MongoMK</td>
   <td><br /> Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Datastore</td>
   <td>Fil-DS </td>
   <td><br /> Fil-DS</td>
   <td><br /> Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Scenario</td>
   <td><p><br /> <br /> Vertikalt användningsfall: Media/2000 samtidiga trådar</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Resultat av prestandatest för scenario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Riktlinjer för arkitekturskalbarhet för AEM-webbplatser och -resurser {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Sammanfattning av riktlinjer för prestanda {#summary-of-performance-guidelines}

Riktlinjerna på denna sida kan sammanfattas enligt följande:

* **Den rekommenderade arkitekturen för de flesta kunder** är tarMK med File Datastore:

   * Minimitopologi: en Author-instans, två Publish-instanser, två Dispatcher
   * Binärfri replikering aktiveras om fildatalagret delas

* **MongoMK med File DataStore** är den rekommenderade arkitekturen för vågrät skalbarhet i Author-nivån:

   * Minimitopologi: tre Author-instanser, tre MongoDB-instanser, två Publish-instanser, två Dispatcher
   * Binärfri replikering aktiveras om fildatalagret delas

* **Nodestore** ska lagras på den lokala disken, inte på en nätverksansluten lagringsenhet (NAS)
* När du använder **Amazon S3**:

   * Amazon S3-datalagret delas mellan författaren och publiceringsskiktet
   * Binär replikering måste vara aktiverad
   * Datastore-skräpinsamlingen kräver en första körning på alla författar- och publiceringsnoder, och sedan en andra körning på författare

* **Anpassat index bör skapas utöver indexvärdet** för utanför rutan baserat på de vanligaste sökningarna

   * Lucene-index bör användas för anpassade index

* **Om du anpassar arbetsflödet kan du förbättra prestandan** avsevärt, till exempel genom att ta bort videomsteget i arbetsflödet Uppdatera resurs, inaktivera avlyssnare som inte används osv.

Mer information finns även på sidan [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md) .
