---
title: Prestandaoptimering
seo-title: Prestandaoptimering
description: Lär dig hur du konfigurerar vissa aspekter av AEM för att optimera prestanda.
seo-description: Lär dig hur du konfigurerar vissa aspekter av AEM för att optimera prestanda.
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Prestandaoptimering{#performance-optimization}

>[!NOTE]
>
>Allmänna riktlinjer för prestanda finns på sidan [Prestandainstruktioner](/help/sites-deploying/performance-guidelines.md) .
>
>Mer information om felsökning och korrigering av prestandaproblem finns också i [Prestandaträdet](/help/sites-deploying/performance-tree.md).
>
>Dessutom kan du läsa en kunskapsbasartikel om tips för [prestandajustering.](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

Ett viktigt problem är den tid det tar för er webbplats att svara på besökarnas förfrågningar. Även om det här värdet varierar för varje begäran kan ett genomsnittligt målvärde definieras. När det här värdet har visat sig vara både genomförbart och underhållbart kan det användas för att övervaka webbplatsens prestanda och indikera utvecklingen av potentiella problem.

De svarstider du vill använda skiljer sig åt mellan skribent- och publiceringsmiljöerna, vilket återspeglar målgruppens olika egenskaper:

## Författarmiljö {#author-environment}

Den här miljön används av författare som anger och uppdaterar innehåll. Det måste ta hänsyn till ett litet antal användare som var och en skapar ett stort antal prestandaintensiva begäranden när innehållssidor uppdateras och de enskilda elementen på dessa sidor.

## Publiceringsmiljö {#publish-environment}

Den här miljön innehåller innehåll som du gör tillgängligt för användarna. Här är antalet förfrågningar ännu större och hastigheten är lika viktig, men eftersom förfrågningarnas karaktär är mindre dynamisk kan ytterligare mekanismer för prestandaförbättring tillämpas. till exempel cachelagra innehållet eller belastningsutjämning.

>[!NOTE]
>
>* När du har konfigurerat för prestandaoptimering följer du procedurerna i [Tough Day](/help/sites-developing/tough-day.md) för att testa miljön under tung belastning.
>* Se även [Prestandajusteringstips](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>



## Prestandaoptimeringsmetod {#performance-optimization-methodology}

En resultatoptimeringsmetod för CQ-projekt kan sammanfattas i fem mycket enkla regler som kan följas för att undvika prestandaproblem redan från början:

1. [Planering för optimering](#planning-for-optimization)
1. [Simulera verklighet](#simulate-reality)
1. [Fastställ solida mål](#establish-solid-goals)
1. [Var relevant](#stay-relevant)
1. [Flexibla itereringscykler](#agile-iteration-cycles)

Dessa regler gäller i stor utsträckning för webbprojekt i allmänhet och är relevanta för projektledare och systemadministratörer för att säkerställa att deras projekt inte ställs inför prestandamässiga utmaningar när de lanseras.

### Planering för optimering {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

Cirka 10 % av projektinsatsen ska planeras för prestandaoptimeringsfasen. De faktiska prestandaoptimeringskraven beror förstås på ett projekts komplexitet och utvecklingsteamets erfarenheter. Även om ditt projekt (i slutänden) inte kräver all tilldelad tid är det bra rutin att alltid planera för prestandaoptimering i den föreslagna regionen.

När så är möjligt bör ett projekt först lanseras på ett mjukt sätt till en begränsad publik för att samla in verkliga erfarenheter och genomföra ytterligare optimeringar, utan det extra tryck som följer efter ett fullständigt meddelande.

När du väl är&quot;live&quot; är prestandaoptimeringen inte över. Detta är tidpunkten då du upplever den&quot;verkliga&quot; belastningen på ditt system. Det är viktigt att planera för ytterligare justeringar efter lanseringen.

Eftersom inläsningen av systemet ändras och prestandaprofilerna för systemet förändras över tid, bör en&quot;trimning&quot; eller&quot;hälsokontroll&quot; för prestandan schemaläggas med 6-12 månaders intervall.

### Simulera verklighet {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

Om du publicerar en webbplats och efter lanseringen får reda på att du stöter på prestandaproblem finns det bara en anledning till detta: Dina belastnings- och prestandatester simulerade inte verkligheten tillräckligt bra.

Det är svårt att simulera verkligheten och hur mycket arbete du rimligen kommer att vilja göra för att bli&quot;verklig&quot; beror på projektets karaktär. &quot;Real&quot; betyder inte bara&quot;riktig kod&quot; och&quot;verklig trafik&quot;, utan även&quot;verkligt innehåll&quot;, särskilt när det gäller innehållets storlek och struktur. Tänk på att mallarna kan uppträda helt olika beroende på databasens storlek och struktur.

### Fastställ solida mål {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

Det är inte underskattat hur viktigt det är att uppnå prestationsmålen på rätt sätt. När man väl har fokuserat på specifika prestationsmål är det ofta mycket svårt att ändra dessa mål efteråt, även om de bygger på vilda antaganden.

Att uppnå goda, gedigna prestationsmål är verkligen ett av de svåraste områdena. Det är oftast bäst att samla in riktiga livsloggar och referensvärden från en jämförbar webbplats (till exempel den nya webbplatsens föregångare).

### Var relevant {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

Det är viktigt att optimera en flaskhals i taget. Om du försöker göra saker parallellt utan att validera effekten av den optimerade optimeringen, kommer du att förlora räkningen på vilken optimeringsåtgärd som faktiskt hjälpte.

### Flexibla itereringscykler {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

Prestandajustering är en iterativ process som innefattar mätning, analys, optimering och validering tills målet nås. För att ta hänsyn till denna aspekt på ett korrekt sätt bör du implementera en flexibel valideringsprocess i optimeringsfasen i stället för en mer tung testprocess efter varje upprepning.

Detta innebär till stor del att utvecklaren som implementerar optimeringen snabbt bör kunna se om optimeringen redan har nått målet. Detta är värdefull information eftersom optimeringen är över när målet har uppnåtts.

## Riktlinjer för grundläggande prestanda {#basic-performance-guidelines}

Generellt sett bör du behålla dina ocachelagrade HTML-begäranden på mindre än 100 ms. Mer specifikt kan följande fungera som riktlinjer:

* 70 % av förfrågningarna om sidor ska besvaras på mindre än 100 ms.
* 25 % av förfrågningarna om sidor bör få ett svar inom 100-300 ms.
* 4 % av förfrågningarna om sidor bör få ett svar inom 300 ms-500 ms.
* 1 % av förfrågningarna om sidor bör få ett svar inom 500 ms-1 000 ms.
* Inga sidor ska svara långsammare än 1 sekund.

Siffrorna ovan förutsätter följande villkor:

* uppmätt vid publicering (inga omkostnader relaterat till en redigeringsmiljö)
* mätt på servern (ingen nätverksbelastning)
* inte cachelagrad (ingen CQ-utdatacache, ingen Dispatcher-cache)
* endast för komplexa objekt med många beroenden (HTML, JS, PDF, ...)
* ingen annan belastning på systemet

Det finns ett antal problem som ofta bidrar till prestandaproblem. Dessa kretsar främst kring:

* ineffektivitet i dispatchercachelagring
* användning av frågor i vanliga visningsmallar.

JVM- och OS-nivåjustering leder vanligtvis inte till stora prestandaförbättringar och bör därför utföras i slutet av optimeringscykeln.

Det sätt på vilket en innehållsdatabas är strukturerad kan även påverka prestanda. För bästa prestanda bör antalet underordnade noder som är kopplade till enskilda noder i en innehållsdatabas inte överstiga 1 000 (som en allmän regel).

Dina bästa vänner under en vanlig prestandaoptimeringsövning är:

* the `request.log`
* komponentbaserad timing
* sist men inte minst en java-profilerare.

### Prestanda vid inläsning och redigering av digitala resurser {#performance-when-loading-and-editing-digital-assets}

På grund av den stora datamängden som används vid inläsning och redigering av digitala resurser kan prestanda bli ett problem.

Två saker påverkar prestandan här:

* CPU - flera kärnor ger jämnare arbete vid omkodning
* Hårddisk - parallella RAID-diskar uppnår samma

Du kan förbättra prestanda genom att tänka på följande:

* Hur många mediefiler överförs per dag? En god uppskattning kan baseras på

![chlimage_1-77](assets/chlimage_1-77.png)

* Tidsram för redigering (vanligtvis arbetsdagens längd, mer för internationella operationer).
* Genomsnittlig storlek på överförda bilder (och storleken på återgivningar som genereras per bild) i MB.
* Bestäm den genomsnittliga datahastigheten:

![chlimage_1-78](assets/chlimage_1-78.png)

* 80 % av alla redigeringar görs på 20 % av tiden, så vid topptid har du 4 gånger den genomsnittliga datahastigheten. Detta är ditt prestationsmål.

## Prestandaövervakning {#performance-monitoring}

Prestanda (eller avsaknaden av) är en av de första saker som användarna märker, så som med andra program med ett användargränssnitt är prestanda av avgörande betydelse. För att optimera prestanda för CQ-installationen måste du övervaka olika attribut för instansen och dess beteende.

Mer information om hur du utför prestandaövervakning finns i [Övervakningsprestanda](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

De problem som orsakar prestandaproblem är ofta svåra att spåra, även när effekterna är enkla att se.

En grundläggande utgångspunkt är goda kunskaper i systemet när det fungerar som vanligt. Om du inte vet hur miljön &quot;ser ut&quot; och &quot;fungerar&quot; när den fungerar som den ska, kan det vara svårt att hitta problemet när prestanda försämras. Det innebär att du bör ägna lite tid åt att undersöka systemet när det körs smidigt och se till att det är en pågående uppgift att samla in prestandainformation. Detta ger dig en grund för jämförelse om prestandan skulle försämras.

I följande diagram visas den väg som en CQ-innehållsbegäran kan ta - och därför antalet olika element som kan påverka prestandan.

![chlimage_1-79](assets/chlimage_1-79.png)

Prestanda är också en balans mellan volym och kapacitet:

**Volym** Den mängd utdata som bearbetas och levereras av systemet.

**Kapacitet** Systemets förmåga att leverera volymen.

Detta kan illustreras på olika platser i hela webbkedjan.

![chlimage_1-80](assets/chlimage_1-80.png)

Det finns flera funktionsområden som ofta är ansvariga för att påverka prestandan:

* Cachelagring
* Programkod (ditt projekt)
* Sökfunktion

### Grundläggande regler för prestanda {#basic-rules-regarding-performance}

Vissa regler bör beaktas vid prestandaoptimering:

* Prestandajustering *måste* ingå i varje projekt.
* Optimera inte tidigt i utvecklingscykeln.
* Prestanda är bara så bra som den svagaste länken.
* Tänk alltid på kapacitet kontra volym.
* Optimera viktiga saker först.
* Optimera aldrig utan *realistiska* mål.

>[!NOTE]
>
>Tänk på att den mekanism du använder för att mäta prestanda ofta kommer att påverka exakt det du försöker mäta. Du bör alltid försöka ta hänsyn till dessa skillnader och eliminera så mycket av deras effekt som möjligt. särskilt bör webbläsarplugin-program avaktiveras när det är möjligt.

## Konfigurera för prestanda {#configuring-for-performance}

Vissa aspekter av CQ (och/eller den underliggande CRX) kan konfigureras för att optimera prestanda. Följande är möjligheter och förslag. Du måste veta om, eller hur, du använder funktionerna i fråga innan du gör några ändringar.

>[!NOTE]
>
>Mer information finns i [KB-artikeln](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

### Sökindexering {#search-indexing}

Från och med AEM 6.0 använder Adobe Experience Manager en Oak-baserad databasarkitektur.

Den uppdaterade indexeringsinformationen finns här:

* [Metodtips för frågor och indexering](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Frågor och indexering](/help/sites-deploying/queries-and-indexing.md)

### Samtidig bearbetning av arbetsflöden {#concurrent-workflow-processing}

Begränsa antalet arbetsflödesprocesser som körs samtidigt för att förbättra prestandan. Som standard bearbetar arbetsflödesmotorn så många arbetsflöden parallellt som det finns processorer tillgängliga för Java VM. När arbetsflödessteg kräver stora mängder bearbetningsresurser (RAM eller CPU) kan flera av dessa arbetsflöden parallellt placera höga krav på tillgängliga serverresurser.

När bilder (eller DAM-resurser i allmänhet) överförs, importeras bilderna automatiskt till DAM i arbetsflöden. Bilderna är ofta högupplösta och kan lätt ta upp hundratals MB av stacken för bearbetning. När du hanterar dessa bilder parallellt placeras en hög belastning på undersystemet för minne och skräpinsamlaren.

Arbetsflödesmotorn använder Apache Sling-jobbköer för hantering och schemaläggning av bearbetning av arbetsobjekt. Följande jobbkötjänster har skapats som standard från tjänsten Apache Sling Job Queue Configuration för bearbetning av arbetsflödesjobb:

* Begränsa arbetsflödeskö: De flesta arbetsflödesstegen, till exempel de som bearbetar DAM-resurser, använder tjänsten Begränsa arbetsflödeskö.
* Begränsa arbetsflöde för extern processjobbkö: Den här tjänsten används för särskilda externa arbetsflödessteg som vanligtvis används för att kontakta ett externt system och avfråga resultat. Exempel: InDesign Media Extraction Process-steget implementeras som en extern process. Arbetsflödesmotorn använder den externa kön för att bearbeta avsökningen. (Se [com.day.cq.workflow.exec.WorkflowExternalProcess](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html).)

Konfigurera de här tjänsterna för att begränsa antalet arbetsflödesprocesser som körs samtidigt.

**** Obs! När du konfigurerar dessa jobbköer påverkas alla arbetsflöden såvida du inte har skapat en jobbkö för en viss arbetsflödesmodell (se [Konfigurera kön för en viss arbetsflödesmodell](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) nedan).

**Konfiguration i databasen**

Om du konfigurerar tjänsterna [med en sling:OsgiConfig-nod](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)måste du hitta PID:t för de befintliga tjänsterna, till exempel: org.apache.sling.event.job.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705. Du kan identifiera ditt PID med webbkonsolen.

Du måste konfigurera egenskapen queue.maxparallel.

**Konfiguration i webbkonsolen**

Om du vill konfigurera de här tjänsterna [med webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)letar du reda på de befintliga konfigurationsobjekten under konfigurationsfabriken för Apache Sling-jobbkön.

Du måste konfigurera egenskapen Maximum Parallel Jobs.

### Konfigurera kön för ett specifikt arbetsflöde {#configure-the-queue-for-a-specific-workflow}

Skapa en jobbkö för en viss arbetsflödesmodell så att du kan konfigurera jobbhantering för den arbetsflödesmodellen. På så sätt påverkar dina konfigurationer bearbetningen för ett visst arbetsflöde, medan konfigurationen av standardarbetsflödeskön för Granite styr bearbetningen av andra arbetsflöden.

När arbetsflödesmodeller körs skapas Sling-jobb för ett specifikt ämne. Som standard matchar ämnet de ämnen som är konfigurerade för den allmänna arbetsflödeskön för Begränsa arbetsflöde eller den externa jobbkön för Begränsa arbetsflöde:

* com/adobe/granite/workflow/job&amp;ast;
* com/adobe/granite/workflow/external/job&amp;ast;

Faktiska jobbämnen som arbetsflödesmodeller genererar innehåller modellspecifikt suffix. Arbetsflödesmodellen DAM Update Asset genererar till exempel jobb med följande ämne:

com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model

Därför kan du skapa en jobbkö för ämnet som matchar jobbavsnitten i arbetsflödesmodellen. När du konfigurerar de prestandarelaterade egenskaperna för kön påverkas endast arbetsflödesmodellen som genererar jobben som matchar köavsnittet.

Följande procedur skapar en jobbkö för ett arbetsflöde med arbetsflödet DAM Update Asset som exempel.

1. Kör arbetsflödesmodellen som du vill skapa jobbkön för så att ämnesstatistik genereras. Lägg till exempel till en bild i Resurser för att köra arbetsflödet DAM Update Asset.
1. Öppna Sling Jobs-konsolen. ([http://localhost:4502/system/console/slingevent](http://localhost:4502/system/console/slingevent))
1. Identifiera arbetsflödesrelaterade ämnen i konsolen. Följande avsnitt finns för DAM Update Asset:

   * com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model
   * com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model
   * com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model

1. Skapa en jobbkö för vart och ett av dessa ämnen. Om du vill skapa en jobbkö skapar du en fabrikskonfiguration för fabrikstjänsten för Apache Sling Job Queue.

   Fabrikskonfigurationerna liknar den Beviljade arbetsflödeskö som beskrivs i [Samtidig arbetsflödesbearbetning](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing), förutom att egenskapen Ämnen matchar ämnet för dina arbetsflödesjobb.

### CQ5 DAM Asset Synchronization Service {#cq-dam-asset-synchronization-service}

Den `AssetSynchronizationService` används för att synkronisera resurser från monterade databaser (inklusive LiveLink, Documentum, bland annat). Som standard utförs en vanlig kontroll var 300:e sekund (5 minuter), så om du inte använder monterade databaser kan du inaktivera den här tjänsten.

Detta görs genom [att konfigurera OSGi-tjänsten](/help/sites-deploying/configuring-osgi.md) **CQ DAM Asset Synchronization Service** för att ange **Synkroniseringsperioden** ( `scheduler.period`) till (minst) 1 år (anges i sekunder).

### Flera DAM-instanser {#multiple-dam-instances}

Distribuering av flera DAM-instanser kan hjälpa prestandan när till exempel:

* du har en hög belastning på grund av regelbunden överföring av ett stort antal resurser för författarmiljön, här kan en separat DAM-instans dedikeras till tjänstförfattaren.
* du har flera team på platser i världen (t.ex. USA, Europa, Asien).

Ytterligare överväganden är:

* separera pågående arbete vid författare från slutlig publicering
* separera interna användare vid författare från externa besökare/användare vid publicering (t.ex. agenter, pressrepresentanter, kunder, studenter).

## Bästa metoder för kvalitetssäkring {#best-practices-for-quality-assurance}

Prestanda är av stor betydelse för er publiceringsmiljö. Därför måste du planera och analysera prestandatesterna noga för publiceringsmiljön när du implementerar projektet.

Detta avsnitt syftar till att ge en standardiserad översikt över problemen med att definiera ett testkoncept specifikt för prestandatester i din *publiceringsmiljö* . Detta är främst av intresse för kvalitetstekniker, projektledare och systemadministratörer.

Nedan beskrivs en standardiserad metod för prestandatester för ett CQ-program i *publiceringsmiljön* . Detta omfattar följande fem faser:

* [Kunskapsverifiering](#verification-of-knowledge)
* [Definition av tillämpningsområde](#scope-definition)
* [Testmetoder](#test-methodologies)
* [Definition av prestandamål](#defining-the-performance-goals)
* [Optimering](#optimization)

Kontrollen är en extra, heltäckande process - nödvändig men inte begränsad till testning.

### Kunskapsverifiering {#verification-of-knowledge}

Ett första steg är att dokumentera den grundläggande information som du behöver känna till innan du kan börja testa:

* arkitekturen i testmiljön
* en programkarta som beskriver de interna element som behöver testas (både separat och i kombination)

#### Testarkitektur {#test-architecture}

Du bör tydligt dokumentera arkitekturen för testmiljön som används för prestandatestningen.

Du behöver en återgivning av den planerade publiceringsmiljön tillsammans med Dispatcher och Load Balancer.

#### Programkarta {#application-map}

Om du vill få en tydlig översikt kan du skapa en karta över hela programmet (du kan mycket väl få den från test i redigeringsmiljön).

En diagramrepresentation av applikationens interna delar kan ge en översikt över testkraven. med färgkodning kan den också fungera som grund för rapporter.

### Omfattningsdefinition {#scope-definition}

Ett program har vanligtvis ett urval av användningsfall. Vissa kommer att vara mycket viktiga, andra mindre viktiga.

Om du vill fokusera omfattningen av prestandatestningen på publicering rekommenderar vi att du definierar:

* de viktigaste användningsområdena
* mest kritiska tekniska användningsfall

Antalet användningsfall är upp till dig, men bör begränsas till ett enkelt hanterbart antal (t.ex. mellan 5 och 10).

När de viktigaste användningsfallen har valts kan nyckelutförandeindikatorerna (KPI) och de verktyg som används för att mäta dem definieras för varje fall. Exempel på vanliga KPI:er är:

* Svarstid från slut till slut
* Svarstid för server
* Svarstid för en enskild komponent
* Svarstid för tjänsterna
* Antal inaktiva trådar i trådpoolen
* Antal kostnadsfria anslutningar
* Systemresurser som processor- och I/O-åtkomst

### Testmetoder {#test-methodologies}

Det här konceptet har fyra scenarier som används för att definiera och testa prestationsmålen:

* Enkomponentstester
* Kombinerade komponenttester
* *Går live* -scenario
* Felscenarier

Baserat på följande principer.

**Komponentbrytpunkter**

* Varje komponent har en specifik brytpunkt när den är relaterad till prestanda. Det innebär att en komponent kan visa bra prestanda tills en viss punkt nås, varefter prestanda snabbt försämras.
* För att få en fullständig översikt över programmet måste du först verifiera dina komponenter för att avgöra när brytpunkten för varje komponent nås.
* För att hitta brytpunkten kan du utföra ett inläsningstest där du under en tidsperiod ökar antalet användare för att skapa en ökad belastning. Genom att övervaka den här inläsningen och komponenternas svar, kommer du att upptäcka specifika prestandabeteenden när komponentens brytpunkt nås. Poängen kan kvalificeras med antalet samtidiga transaktioner per sekund, tillsammans med antalet samtidiga användare (om komponenten är känslig för denna KPI).
* Denna information kan sedan fungera som riktmärke för förbättringar, ange effektiviteten hos de åtgärder som används och hjälpa till att definiera testscenarier.

**Transaktioner**

* Termen transaktion används för att representera begäran om en hel webbsida, inklusive själva sidan och alla efterföljande anrop. dvs. sidförfrågan, eventuella AJAX-anrop, bilder och andra objekt.**Begär detaljgranskning nedåt**
* Om du vill analysera varje begäran fullständigt kan du representera varje element i anropsstacken och sedan summera den genomsnittliga bearbetningstiden för varje.

### Definiera prestandamål {#defining-the-performance-goals}

När omfattningen och relaterade nyckeltal har definierats kan de specifika prestationsmålen ställas in. Det handlar om att utforma testscenarier tillsammans med målvärden.

Du måste testa prestanda både under normala förhållanden och under toppförhållanden. Dessutom måste du göra Going Live-test för att vara säker på att du kan tillgodose det ökade intresset för din webbplats när den blir tillgänglig för första gången.

Alla erfarenheter och all statistik som du har samlat in från en befintlig webbplats kan också vara användbara när du ska fastställa framtida mål. till exempel topptrafik från din webbplats.

#### Enkomponentstester {#single-component-tests}

Viktiga komponenter måste testas - både under medelförhållanden och under högbelastningsförhållanden.

I båda fallen kan du definiera det förväntade antalet transaktioner per sekund när ett fördefinierat antal användare använder systemet.

| Komponent | Testtyp | #Användare | Tx/sek (förväntas) | Tx/sek (testad) | Beskrivning |
|---|---|---|---|---|---|
| Startsida - en användare | Medel | 1 | 1 |  |  |
|  | Toppvärde | 1 | 3 |  |  |
| Startsida 100 användare | Medel | 100 | 3 |  |  |
|  | Toppvärde | 100 | 3 |  |

#### Komponenttester {#combined-component-tests}

Genom att testa komponenterna i kombination får du en närmare bild av hur programmen fungerar. Även här måste man testa genomsnittliga och högsta förhållanden.

| Scenario | Komponent | #Användare | Tx/sek (förväntas) | Tx/sek (testad) | Beskrivning |
|---|---|---|---|---|---|
| Blandat genomsnitt | Hemsida | 10 | 1 |  |  |
|  | Sök | 10 | 1 |  |  |
|  | Nyheter | 10 | 2 |  |  |
|  | Händelser | 10 | 1 |  |  |
|  | Aktiveringar | 10 | 3 |  | Simulering av författarbeteende. |
| Blandad topp | Hemsida | 100 | 5 |  |  |
|  | Sök | 50 | 5 |  |  |
|  | Nyheter | 100 | 10 |  |  |
|  | Händelser | 100 | 10 |  |  |
|  | Aktiveringar | 20 | 20 |  | Simulering av författarbeteende. |

#### Pågående direkttester {#going-live-tests}

Under de första dagarna efter det att webbplatsen har tillgängliggjorts kan du förvänta dig ett ökat intresse. Detta kommer förmodligen att vara ännu större än de toppvärden som du har testat för. Vi rekommenderar att du testar Going Live-scenarier för att se till att systemet klarar detta.

| Scenario | Testtyp | #Användare | Tx/sek (förväntas) | Tx/sek (testad) | Beskrivning |
|---|---|---|---|---|---|
| Live-topp på väg | Hemsida | 200 | 20 |  |  |
|  | Sök | 100 | 10 |  |  |
|  | Nyheter | 200 | 20 |  |  |
|  | Händelser | 200 | 20 |  |  |
|  | Aktiveringar | 20 | 20 |  | Simulering av författarbeteende. |

#### Felscenariotest {#error-scenario-tests}

Felscenarier måste också testas för att säkerställa att systemet reagerar korrekt och korrekt. Inte bara hur själva felet hanteras, utan även hur det kan påverka prestandan. Exempel:

* vad som händer när användaren försöker ange ett ogiltigt sökord i sökrutan
* vad som händer när söktermen är så allmän att den returnerar ett stort antal resultat

När man utformar dessa tester bör man komma ihåg att inte alla scenarier kommer att inträffa regelbundet. Deras inverkan på hela systemet är dock viktig.

| Felscenario | Feltyp | #Användare | Tx/sek (förväntas) | Tx/sek (testad) | Beskrivning |
|---|---|---|---|---|---|
| Överlagring av sökkomponent | Sök på globalt jokertecken (asterisk) | 10 | 1 |  | Endast &amp;stämpel;ast;&amp;ast;&amp;ast; söks igenom. |
|  | Stoppord | 20 | 2 |  | Söker efter ett stoppord. |
|  | Tom sträng | 10 | 1 |  | Söker efter en tom sträng. |
|  | Specialtecken | 10 | 1 |  | Söker efter specialtecken. |

#### Bevarandetester {#endurance-tests}

Vissa problem kommer inte att uppstå förrän systemet har körts under en kontinuerlig period. det är timmar eller till och med dagar. En uthållighetsprovning används för att testa en konstant genomsnittlig belastning under en viss tidsperiod. Alla prestandaförsämringar kan sedan analyseras.

| Scenario | Testtyp | #Användare | Tx/sek (förväntas) | Tx/sek (testad) | Beskrivning |
|---|---|---|---|---|---|
| Varaktighetsprovning (72 timmar) | Hemsida | 10 | 1 |  |  |
|  | Sök | 10 | 1 |  |  |
|  | Nyheter | 20 | 2 |  |  |
|  | Händelser | 10 | 1 |  |  |
|  | Aktiveringar | 1 | 3 |  | Simulering av författarbeteende. |

### Optimering {#optimization}

I de senare faserna av implementeringen måste du optimera programmet för att uppfylla/maximera prestandamålen.

Alla optimeringar som görs måste testas för att säkerställa att de har:

* inte påverkade funktionen
* har kontrollerats med lastprovningarna innan de släpps

Det finns ett urval verktyg som kan hjälpa dig med lastgenerering, prestandaövervakning och/eller resultatanalys:

* [JMeter](https://jakarta.apache.org/jmeter/)
* [Load Runner](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)
* [Determiner](https://www.determyne.com/) InsideApps
* [InfraRED](https://www.infraredsoftware.com/)
* [Java Interactive Profile](https://jiprof.sourceforge.net/)
* många fler...

Efter optimeringen måste du testa igen för att bekräfta påverkan.

### Rapportering {#reporting}

Pågående rapportering kommer att behövas för att hålla alla informerade om statusen. som tidigare nämnts med färgkodning kan arkitekturkartan användas för detta.

När alla tester är klara vill du rapportera om:

* eventuella kritiska fel som påträffats
* icke-kritiska frågor som fortfarande behöver utredas
* eventuella antaganden som gjorts under testningen
* eventuella rekommendationer som följer av testningen

## Optimera prestanda när du använder Dispatcher {#optimizing-performance-when-using-the-dispatcher}

Dispatcher [är](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) Adobes verktyg för cachelagring och/eller belastningsutjämning. När du använder Dispatcher bör du överväga att optimera webbplatsen för cacheprestanda.

>[!NOTE]
>
>Dispatcher-versionerna är oberoende av AEM, men Dispatcher-dokumentationen är inbäddad i AEM-dokumentationen. Använd alltid Dispatcher-dokumentationen som är inbäddad i dokumentationen för den senaste versionen av AEM.
>
>Du kan ha omdirigerats till den här sidan om du har följt en länk till Dispatcher-dokumentationen som är inbäddad i dokumentationen för en tidigare version av AEM.

Dispatcher har ett antal inbyggda funktioner som du kan använda för att optimera prestanda om webbplatsen utnyttjar dem. I det här avsnittet beskrivs hur du utformar din webbplats för att maximera fördelarna med cachning.

>[!NOTE]
>
>Det kan hjälpa dig att komma ihåg att Dispatcher lagrar cachen på en standardwebbserver. Det innebär att du:
>
>* kan cachelagra allt som du kan lagra som en sida och begära med en URL
>* kan inte lagra andra saker, som cookies, sessionsdata och formulärdata.
>
>
I allmänhet handlar många cachelagringsstrategier om att välja bra URL:er och inte förlita sig på dessa ytterligare data.
>
>Med Dispatcher version 4.1.11 kan du även cachelagra svarshuvuden, se [Cachelagra HTTP-svarshuvuden](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache).


### Beräkna Dispatcher-cachens proportioner {#calculating-the-dispatcher-cache-ratio}

Cachekvotsformeln uppskattar procentandelen begäranden som hanteras av cachen av det totala antalet begäranden som kommer in i systemet. För att beräkna cachekvoten behöver du följande:

* Totalt antal begäranden. Den här informationen finns i Apache `access.log`. Mer information finns i den [officiella Apache-dokumentationen](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* Antalet begäranden som den publicerade instansen betjänade. Den här informationen är tillgänglig i `request.log` instansens namn. Mer information finns i [Tolka request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) och [Hitta loggfilerna](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

Formeln för beräkning av cacheförhållandet är:

* (Det totala antalet begäranden **minus** antalet begäranden vid publicering) **delat** med det totala antalet begäranden.

Om det totala antalet begäranden till exempel är 129491 och antalet begäranden som hanteras av Publish-instansen är 58959 är cachekvoten: **(129491 - 58959)/129491= 54,5%**.

Om du inte har en till en utgivare/utgivare måste du lägga ihop förfrågningar från alla utgivare och utgivare för att få en korrekt mätning. Se även [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>För bästa prestanda rekommenderar Adobe en cachekvot på 90 % till 95 %.

#### Använda konsekvent sidkodning {#using-consistent-page-encoding}

Med Dispatcher version 4.1.11 kan du cachelagra svarshuvuden. Om du inte cachelagrar svarshuvuden i Dispatcher kan problem uppstå om du lagrar sidkodningsinformation i sidhuvudet. I det här fallet används webbserverns standardkodning för sidan när Dispatcher visar en sida från cachen. Det finns två sätt att undvika det här problemet:

* Om du bara använder en kodning kontrollerar du att kodningen som används på webbservern är densamma som standardkodningen på AEM-webbplatsen.
* Använd en `<META>` -tagg i HTML- `head` avsnittet för att ställa in kodningen, som i följande exempel:

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### Undvik URL-parametrar {#avoid-url-parameters}

Undvik om möjligt URL-parametrar för sidor som du vill cachelagra. Om du till exempel har ett bildgalleri cachelagras aldrig följande URL (såvida inte Dispatcher har [konfigurerats korrekt](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)):

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

Du kan dock placera de här parametrarna i sidans URL-adress enligt följande:

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>Den här URL:en anropar samma sida och samma mall som gallery.html. I malldefinitionen kan du ange vilket skript som ska återge sidan eller använda samma skript för alla sidor.

#### Anpassa efter URL {#customize-by-url}

Om du tillåter användare att ändra teckensnittsstorleken (eller annan layoutanpassning) kontrollerar du att de olika anpassningarna återspeglas i webbadressen.

Till exempel cachelagras inte cookies, så om du sparar teckensnittsstorleken i en cookie (eller på liknande sätt) bevaras inte teckensnittsstorleken för den cachelagrade sidan. Därför returnerar Dispatcher dokument med valfri teckenstorlek på måfå.

Om du tar med teckensnittsstorleken i URL:en som väljare undviker du det här problemet:

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>I de flesta layoutaspekter går det även att använda formatmallar och/eller skript på klientsidan. Dessa fungerar vanligtvis mycket bra med cachning.
>
>Detta är också användbart för en utskriftsversion där du kan använda en URL-adress som: &quot;
>
>`www.myCompany.com/news/main.print.html`
>
>Med hjälp av skriptordlistan för malldefinitionen kan du ange ett separat skript som återger utskriftssidorna.

#### Invaliderar bildfiler som används som titlar {#invalidating-image-files-used-as-titles}

Om du återger sidrubriker, eller annan text, som bilder bör du lagra filerna så att de tas bort vid en innehållsuppdatering på sidan:

1. Placera bildfilen i samma mapp som sidan.
1. Använd följande namnformat för bildfilen:

   `<page file name>.<image file name>`

Du kan till exempel lagra titeln för sidan myPage.html i filen myPage.title.gif. Den här filen tas automatiskt bort om sidan uppdateras, så alla ändringar av sidans titel återspeglas automatiskt i cachen.

>[!NOTE]
>
>Bildfilen finns inte nödvändigtvis fysiskt på AEM-instansen. Du kan använda ett skript som skapar bildfilen dynamiskt. Dispatcher lagrar sedan filen på webbservern.

#### Ogiltiga bildfiler som används för navigering {#invalidating-image-files-used-for-navigation}

Om du använder bilder för navigeringsposterna är metoden i stort sett densamma som med titlar, något mer komplex. Lagra alla navigeringsbilder med målsidorna. Om du använder två bilder för normal och aktiv användning kan du använda följande skript:

* Ett skript som visar sidan som vanligt.
* Ett skript som bearbetar &quot;.normal&quot;-begäranden och returnerar den normala bilden.
* Ett skript som bearbetar &quot;.active&quot;-begäranden och returnerar den aktiverade bilden.

Det är viktigt att du skapar dessa bilder med samma namngivningshandtag som sidan, så att innehållsuppdateringen tar bort både dessa bilder och sidan.

För sidor som inte ändras finns bilderna kvar i cachen, även om själva sidorna vanligtvis blir automatiskt ogiltiga.

#### Personalisering {#personalization}

Dispatcher kan inte cachelagra anpassade data, så vi rekommenderar att du begränsar personaliseringen till där det är nödvändigt. Så här visar du varför:

* Om du använder en fritt anpassningsbar startsida måste den sidan sammanställas varje gång en användare begär den.
* Om du däremot har 10 olika startsidor kan du cachelagra var och en av dem, vilket förbättrar prestandan.

>[!NOTE]
>
>Om du anpassar varje sida (till exempel genom att placera användarens namn i namnlisten) kan du inte cachelagra den, vilket kan få stor prestandapåverkan.
>
>Om du måste göra det kan du:
>
>* Använd iFrames för att dela upp sidan i en del som är densamma för alla användare och en del som är densamma för alla sidor i användaren. Du kan sedan cachelagra båda dessa delar.
>* använda JavaScript på klientsidan för att visa personlig information. Du måste dock se till att sidan fortfarande visas korrekt om en användare stänger av JavaScript.
>



#### Fästiga anslutningar {#sticky-connections}

[Antikiga anslutningar](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#the-benefits-of-load-balancing) säkerställer att dokumenten för en användare finns på samma server. Om en användare lämnar den här mappen och senare återgår till den, stannar anslutningen fortfarande kvar. Definiera en mapp för alla dokument som kräver klisterlappar för webbplatsen. Försök att inte ha med andra dokument i den. Detta påverkar belastningsutjämningen om du använder personaliserade sidor och sessionsdata.

#### MIME-typer {#mime-types}

Det finns två sätt som en webbläsare kan använda för att avgöra vilken typ av fil det är:

1. Genom filtillägg (t.ex. .html, .gif, .jpg osv.)
1. Med MIME-typen som servern skickar med filen.

För de flesta filer används MIME-typen i filtillägget. dvs.:

1. Genom filtillägg (t.ex. .html, .gif, .jpg osv.)
1. Med MIME-typen som servern skickar med filen.

Om filnamnet inte har något filtillägg visas det som oformaterad text.

Med Dispatcher version 4.1.11 kan du cachelagra svarshuvuden. Om du inte cachelagrar svarshuvuden på Dispatcher bör du vara medveten om att MIME-typen är en del av HTTP-huvudet. Om ditt AEM-program returnerar filer som inte har ett känt filslut, och i stället använder MIME-typen, kan dessa filer visas felaktigt.

Följ dessa riktlinjer för att vara säker på att filerna cachelagras korrekt:

* Kontrollera att filerna alltid har rätt filtillägg.
* Undvik generiska filserverskript med URL-adresser som download.jsp?file=2214. Skriv om skriptet så att URL:er som innehåller filspecifikationen används. i föregående exempel är detta download.2214.pdf.

## Säkerhetskopieringsprestanda {#backup-performance}

I det här avsnittet presenteras en serie prestandatester som används för att utvärdera hur CQ-säkerhetskopieringar fungerar och hur säkerhetskopieringsaktiviteten påverkar programmets prestanda. CQ-säkerhetskopieringen innebär en betydande belastning på systemet medan det körs, och vi mäter detta samt effekterna av inställningarna för fördröjning av säkerhetskopiering som försöker modulera dessa effekter. Målet är att tillhandahålla vissa referensdata om förväntade prestanda för säkerhetskopieringar i realistiska konfigurationer och kvantiteter av produktionsdata, och att ge vägledning om hur man beräknar säkerhetskopieringstider för planerade system.

### Referensmiljö {#reference-environment}

#### Fysiskt system {#physical-system}

De resultat som rapporteras i det här dokumentet har hämtats från referensvärden som körs i en referensmiljö med följande konfiguration. Den här konfigurationen är utformad för att likna en typisk produktionsmiljö i ett datacenter:

* H-P ProLiant DL380 G6, 8 processorer x 2,533 GHz
* Seriellt anslutna SCSI 300 GB 10 000 RPM-enheter
* Maskinvarubaserad RAID-styrenhet; 8 enheter i en RAID 0+5-matris
* VMware image CPU x 2 Intel Xeon E5540 vid 2,53 GHz
* RedHat Linux 2.6.18-194.el5; Java 1.6.0_29
* Single Author-instans som kör CQ 5.5 GM.

Diskundersystemet på den här servern är ganska snabbt och representativt för en RAID-konfiguration med höga prestanda som kan användas i en produktionsserver. Säkerhetskopieringsprestanda kan vara beroende av diskprestanda, och resultatet i den här miljön avspeglar prestanda i en mycket snabb RAID-konfiguration. VMWare-avbildningen är konfigurerad att ha en enda stor diskvolym som fysiskt finns i den lokala disklagringen på RAID-matrisen.

CQ-konfigurationen placerar databasen och datalagret på samma logiska volym, tillsammans med operativsystemet och CQ-programmet. Målkatalogen för säkerhetskopieringar finns också i det här logiska filsystemet.

#### Datavolymer {#data-volumes}

Följande tabell visar storleken på datavolymer som används i prestandatesterna för säkerhetskopiering. Det ursprungliga baslinjeinnehållet installeras först, sedan läggs ytterligare kända datamängder till för att öka storleken på det säkerhetskopierade innehållet. Säkerhetskopior skapas i specifika steg för att representera en stor ökning av innehållet och vad som kan produceras under en dag. Distributionen av innehåll (sidor, bilder, taggar) kommer att vara ungefär baserad på realistisk komposition av produktionsresurser. Sidor, bilder och taggar begränsas till högst 800 underordnade sidor. Varje sida ska innehålla komponenterna title, Flash, text/image, video, bildspel, form, table, cloud och carousel. Bilderna överförs från en pool med 400 unika filer som är mellan 37 kB och 594 kB.

<table>
 <tbody>
  <tr>
   <td><strong>Innehåll</strong></td>
   <td><strong>Noder</strong></td>
   <td><strong>Sidor</strong></td>
   <td><strong>Bilder</strong></td>
   <td><strong>Taggar</strong></td>
  </tr>
  <tr>
   <td>Grundinstallation</td>
   <td>69,610</td>
   <td>562</td>
   <td>256</td>
   <td>237</td>
  </tr>
  <tr>
   <td>Liten information för stegvis säkerhetskopiering</td>
   <td><br type="_moz" /> </td>
   <td>+100</td>
   <td>+2</td>
   <td>+2</td>
  </tr>
  <tr>
   <td>Stort innehåll för fullständig säkerhetskopiering</td>
   <td><br type="_moz" /> </td>
   <td>+10,000</td>
   <td>+100</td>
   <td>+100</td>
  </tr>
 </tbody>
</table>

Prestandatestvärdet för säkerhetskopiering upprepas med ytterligare innehållsuppsättningar som läggs till vid varje upprepning.

#### Benchmark-scenarier {#benchmark-scenarios}

Referensvärdena för säkerhetskopiering omfattar två huvudscenarier: säkerhetskopierar när systemet är under en betydande programbelastning och säkerhetskopierar när systemet är inaktivt. Även om den allmänna rekommendationen är att säkerhetskopieringar ska utföras när CQ-systemet är så inaktivt som möjligt, finns det situationer där det är nödvändigt att säkerhetskopieringen måste köras när systemet är under laddning.

**Säkerhetskopiering av vänteläge** utförs utan någon annan aktivitet på CQ.

**Under Load** Backups utförs medan systemet är under 80 % inläst från onlineprocesser. Fördröjningen för säkerhetskopiering varierade för att se effekten på inläsningen.

Tidpunkter för säkerhetskopiering och storlek för säkerhetskopieringen hämtas från CQ-serverloggarna. Det rekommenderas normalt att säkerhetskopieringar schemaläggs i fel tider när CQ är ledig, till exempel mitt i natten. Detta scenario är representativt för den rekommenderade metoden.

Inläsningen består av sidor som skapar/tar bort, bläddrar och frågor där större delen av inläsningen kommer från sidbläddringar och frågor. Om du lägger till och tar bort för många sidor ökar arbetsytans storlek kontinuerligt och förhindrar att säkerhetskopiorna slutförs. Distributionen av den last som skriptet ska använda är 75 % sidöverföringar, 24 % frågor och 1 % sidskapande (en nivå utan kapslade undersidor). Maximalt medelvärde för transaktioner per sekund i ett system som är inaktivt uppnås med fyra samtidiga trådar, vilket är vad som kommer att användas vid testning av säkerhetskopior under inläsning.

Inläsningens inverkan på säkerhetskopieringsprestanda kan uppskattas av skillnaden mellan prestanda med och utan den här programinläsningen. Effekten av säkerhetskopieringen på programmets dataflöde hittas genom att man jämför scenariogenomströmningen i transaktioner per timme med och utan en pågående säkerhetskopiering, och med säkerhetskopieringar som körs med olika inställningar för fördröjning av säkerhetskopiering.

**Fördröjningsinställning** För flera av scenarierna varierade vi även fördröjningsinställningen för säkerhetskopiering med värden på 10 ms (standard), 1 ms och 0 ms, för att undersöka hur den här inställningen påverkade säkerhetskopieringens prestanda.

**Säkerhetskopieringstyp** Alla säkerhetskopior var externa säkerhetskopior av databasen som gjorts till en säkerhetskopieringskatalog utan att skapa en zip, förutom i ett fall där tjärkommandot användes direkt. Eftersom det inte går att skapa stegvisa säkerhetskopieringar till en zip-fil, eller när den tidigare fullständiga säkerhetskopieringen är en zip-fil, är säkerhetskopieringskatalogmetoden den metod som oftast används i produktionssituationer.

### Sammanfattning av resultat {#summary-of-results}

#### Tid och fel för säkerhetskopiering {#backup-time-and-troughput}

Det främsta resultatet av dessa prestandatester är att visa hur tiden för säkerhetskopiering varierar beroende på säkerhetskopieringstyp och total datamängd. I följande diagram visas säkerhetskopieringstiden som hämtats med standardkonfigurationen för säkerhetskopiering, som en funktion av det totala antalet sidor.

![chlimage_1-81](assets/chlimage_1-81.png)

Säkerhetskopieringstiderna för en inaktiv instans är relativt konsekventa, vilket ger ett genomsnitt på 0,608 MB/s oavsett fullständig eller stegvis säkerhetskopiering (se tabellen nedan). Tidpunkten för säkerhetskopieringen är helt enkelt en funktion av mängden data som säkerhetskopieras. Tiden det tar att slutföra en fullständig säkerhetskopiering ökar tydligt med det totala antalet sidor. Tiden det tar att slutföra en stegvis säkerhetskopiering ökar också med det totala antalet sidor, men med en mycket lägre hastighet. Den tid det tar att slutföra den inkrementella säkerhetskopieringen är mycket kortare på grund av den relativt små mängden data som säkerhetskopieras.

Storleken på säkerhetskopian som skapas är den viktigaste faktorn för den tid det tar att slutföra en säkerhetskopiering. I följande diagram visas hur lång tid det tar som en funktion av den slutliga säkerhetskopieringsstorleken.

![chlimage_1-82](assets/chlimage_1-82.png)

Diagrammet visar att både inkrementella och fullständiga säkerhetskopieringar följer ett enkelt mönster för storlek kontra tid som vi kan mäta som genomströmning. Säkerhetskopieringstiderna för en inaktiv instans är relativt konsekventa, vilket är ett genomsnitt på 0,61 MB/sek oavsett fullständig eller inkrementell säkerhetskopiering i testmiljön.

#### Fördröjning för säkerhetskopiering {#backup-delay}

Parametern för fördröjning av säkerhetskopiering anges för att begränsa i vilken utsträckning säkerhetskopiering kan påverka arbetsbelastningen i produktionen. Parametern anger en väntetid i millisekunder, vilket är inbäddat i säkerhetskopieringen fil för fil. Den övergripande effekten beror delvis på storleken på de filer som påverkas. Genom att mäta säkerhetskopieringsprestanda i MB/sek kan du jämföra fördröjningseffekterna för säkerhetskopieringen på ett rimligt sätt.

* Om du kör en säkerhetskopiering samtidigt med vanlig programinläsning påverkas den reguljära belastningens genomströmning negativt.
* Inverkan kan vara liten - så lite som 5 % - eller mycket signifikant - och orsaka så mycket som 75 % minskning av genomströmningen, och detta beror troligen på applikationen mer än något annat.
* Säkerhetskopiering är inte en stor belastning på processorn och därför påverkas processorintensiva arbetsbelastningar mindre av säkerhetskopieringen än vad I/O-intensiva arbetsbelastningar gör.

![chlimage_1-83](assets/chlimage_1-83.png)

Jämför dataflödet som erhålls med en säkerhetskopia av filsystemet (med hjälp av tar) för att säkerhetskopiera samma databasfiler. Tjärans prestanda är jämförbar, men något högre än säkerhetskopian med fördröjningen inställd på noll. Även om du anger en liten fördröjning minskar säkerhetskopieringens genomströmning avsevärt och standardfördröjningen på 10 ms resulterar det i avsevärt mindre genomströmning. I situationer där säkerhetskopieringar kan schemaläggas när den övergripande programanvändningen är mycket låg eller programmet kan vara helt inaktivt, är det antagligen önskvärt att minska fördröjningen under standardvärdet så att säkerhetskopieringen kan fortsätta snabbare.

Den faktiska effekten av applikationens genomströmning vid en pågående säkerhetskopiering beror på applikations- och infrastrukturinformationen. Fördröjningsvärdet bör väljas genom empirisk analys av programmet, men bör väljas så litet som möjligt så att säkerhetskopieringen kan slutföras så snabbt som möjligt. Eftersom det bara finns en svag korrelation mellan valet av fördröjningsvärde och effekten på applikationens genomströmning, bör valet av fördröjning främja kortare övergripande säkerhetskopieringstider för att minimera den övergripande effekten av säkerhetskopieringar. En säkerhetskopiering som tar 8 timmar att slutföra men påverkar genomströmningen med -20 % har troligen större total effekt än en som tar 2 timmar att slutföra men påverkar genomströmningen med -30 %.

### Referenser {#references}

* [Administrera - Säkerhetskopiera och återställ](/help/sites-administering/backup-and-restore.md)
* [Hantering - kapacitet och volym](/help/managing/best-practices-further-reference.md#capacity-and-volume)

