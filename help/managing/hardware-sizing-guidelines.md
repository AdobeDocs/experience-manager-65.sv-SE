---
title: Riktlinjer för maskinvarans storlek
seo-title: Riktlinjer för maskinvarans storlek
description: Dessa riktlinjer för storleksändring ger en uppskattning av de maskinvaruresurser som krävs för att driftsätta ett AEM-projekt.
seo-description: Dessa riktlinjer för storleksändring ger en uppskattning av de maskinvaruresurser som krävs för att driftsätta ett AEM-projekt.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Riktlinjer för maskinvarans storlek{#hardware-sizing-guidelines}

Dessa riktlinjer för storleksändring ger en uppskattning av de maskinvaruresurser som krävs för att driftsätta ett AEM-projekt. Beräkningar av storleken beror på projektets arkitektur, lösningens komplexitet, förväntad trafik och projektkraven. Den här guiden hjälper dig att fastställa maskinvarubehoven för en viss lösning eller att hitta en övre och nedre uppskattning av maskinvarukraven.

Grundläggande faktorer att beakta är (i denna ordning):

* **Nätverkshastighet**

   * Nätverksfördröjning
   * Tillgänglig bandbredd

* **Datorhastighet**

   * Cacheeffektivitet
   * Förväntad trafik
   * Komplexa mallar, applikationer och komponenter
   * Samtidiga författare
   * Redigeringsåtgärdens komplexitet (enkel innehållsredigering, MSM-utrullning osv.)

* **I/O-prestanda**

   * Filens eller databaslagringens prestanda och effektivitet

* **Hårddisk**

   * minst två eller tre gånger större än databasstorleken

* **Minne**

   * Webbplatsens storlek (antal innehållsobjekt, sidor och användare)
   * Antal användare/sessioner som är aktiva samtidigt

## Arkitektur {#architecture}

En vanlig AEM-konfiguration består av en författare och en publiceringsmiljö. De här miljöerna har olika krav på den underliggande maskinvarans storlek och systemkonfiguration. Detaljerade överväganden för båda miljöerna beskrivs i avsnitten om [författarmiljö](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) och [publiceringsmiljö](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) .

I en typisk projektkonfiguration har du flera miljöer där du ska fasa ut projektet:

* **Utvecklingsmiljö** För att utveckla nya funktioner eller göra betydande ändringar. Bästa sättet är att arbeta i en utvecklingsmiljö per utvecklare (vanligen lokala installationer på deras personliga system).

* **Redigeringstestmiljö** Verifiera ändringar. Antalet testmiljöer kan variera beroende på projektkraven (t.ex. separat för kvalitetskontroll, integrationstestning eller testning av användaracceptans).

* **Publicera testmiljö** främst för testning av användningsfall för socialt samarbete och/eller interaktionen mellan författare och flera publiceringsinstanser.

* **Skapa produktionsmiljö** För redigering av innehåll.

* **Publicera produktionsmiljö** för publicerat innehåll.

Dessutom kan miljöerna variera, från ett enserversystem som kör AEM och en programserver till en mycket skalad uppsättning multiserverinstanser med flera processorer. Vi rekommenderar att du använder en separat dator för varje produktionssystem och att du inte kör andra program på dessa datorer.

## Allmän hänsyn till maskinvarustorlek {#generic-hardware-sizing-considerations}

Avsnitten nedan ger vägledning om hur maskinvarukraven ska beräknas, med beaktande av olika överväganden. För stora system föreslår vi att du utför en enkel uppsättning interna prestandatester på en referenskonfiguration.

Prestandaoptimering är en grundläggande uppgift som måste utföras innan det går att utföra riktmärkning för ett visst projekt. Var noga med att följa anvisningarna i dokumentationen [för](/help/sites-deploying/configuring-performance.md) prestandaoptimering innan du utför några prestandatester och använder resultaten för beräkningar av maskinvarustorlekar.

Krav på maskinvarustorlek för fall med avancerad användning måste baseras på en detaljerad prestandautvärdering av projektet. Karakteristika för avancerade användningsområden som kräver exceptionella maskinvaruresurser omfattar följande kombinationer:

* nyttolast/dataflöde för högt innehåll
* omfattande användning av anpassad kod, anpassade arbetsflöden eller programbibliotek från tredje part
* integrering med externa system som inte stöds

### Diskutrymme/hårddisk {#disk-space-hard-drive}

Det diskutrymme som krävs beror till stor del på både volymen och typen av webbprogram. Beräkningarna bör ta hänsyn till följande:

* mängden och storleken på sidor, resurser och andra databaslagrade enheter som arbetsflöden, profiler osv.
* den uppskattade frekvensen av innehållsändringar och därmed skapandet av innehållsversioner
* mängden DAM-resursåtergivningar som ska genereras
* den totala innehållstillväxten över tiden

Diskutrymmet övervakas kontinuerligt under rensning online och offline. Om det tillgängliga diskutrymmet sjunker under ett kritiskt värde avbryts processen. Det kritiska värdet är 25 % av databasens aktuella diskutrymme och kan inte konfigureras. Vi rekommenderar att du ändrar storlek på disken minst två eller tre gånger så stor som databasstorleken, inklusive den beräknade tillväxten.

Överväg att konfigurera redundanta matriser med oberoende diskar (RAID, t.ex. RAID10) för dataredundans.

>[!NOTE]
>
>Den tillfälliga katalogen för en produktionsinstans måste ha minst 6 GB ledigt utrymme.

#### Virtualisering {#virtualization}

AEM fungerar bra i virtualiserade miljöer, men det kan finnas faktorer som CPU eller I/O som inte direkt kan jämföras med fysisk maskinvara. En rekommendation är att välja en högre I/O-hastighet (i allmänhet) eftersom detta är en viktig faktor i de flesta fall. Det är nödvändigt att testa miljön för att få en mer detaljerad förståelse för vilka resurser som kommer att behövas.

#### Parallalisering av AEM-instanser {#parallelization-of-aem-instances}

**Säkert fel**

En felsäker webbplats används i minst två separata system. Om ett system kraschar kan ett annat system ta över och därmed kompensera för systemfelet.

**Skalbarhet för systemresurser**

Alla system körs, men det finns bättre datorprestanda. Den extra prestandan är inte nödvändigtvis linjär med antalet klusternoder eftersom relationen är mycket beroende av den tekniska miljön. Mer information finns i [klusterdokumentationen](/help/sites-deploying/recommended-deploys.md) .

Beräkningen av hur många klusternoder som behövs baseras på de grundläggande kraven och specifika användningsfall för det aktuella webbprojektet:

* När det gäller felsäkerhet är det nödvändigt att för alla miljöer fastställa hur allvarligt felet är och hur lång tid det tar för en klusternod att återställa felet.
* När det gäller skalbarhet är antalet skrivåtgärder i grunden den viktigaste faktorn. Se [Författare arbeta parallellt](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) för författarmiljön och [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) för publiceringsmiljön. Belastningsbalansering kan upprättas för åtgärder som enbart har tillgång till systemet för att behandla läsåtgärder. Mer information finns i [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) .

## Specifika beräkningar för redigeringsmiljön {#author-environment-specific-calculations}

Adobe har utvecklat prestandatester för fristående författarinstanser för testresultat.

* **Benchmark test 1** Beräkna maximal genomströmning för en lastprofil där användarna utför en enkel simulering utöver en basbelastning på 300 befintliga sidor - alla av liknande natur. Stegen var att logga in på webbplatsen, skapa en sida med en SWF och bild/text, lägga till ett taggmoln och sedan aktivera sidan.

   * **Resultat**: Maximalt dataflöde för en enkel sidskapandeövning som ovan (betraktas som en transaktion) befanns vara 1 730 transaktioner/timme.

* **Benchmark test 2** Beräkna maximal genomströmning när inläsningsprofilen har en blandning av nya sidor (10 %), ändringar av en befintlig sida (80 %) och skapande av en ny sida i följd (10 %). Sidornas komplexitet är densamma som i profilen för test 1. Den grundläggande ändringen av sidan görs genom att en bild läggs till och textinnehållet ändras. Återigen utfördes övningen utöver en basbelastning på 300 sidor med samma komplexitet som definieras i test 1 av prestandan.

   * **Resultat**: Maximalt dataflöde för ett sådant blandningsåtgärdsscenario var 3252 transaktioner per timme.

>[!NOTE]
>
>Genomströmningsfrekvensen skiljer inte mellan transaktionstyper i en lastprofil. Den metod som används för att mäta genomströmning säkerställer att en fast andel av varje typ av transaktion inkluderas i arbetsbelastningen.

De två ovanstående testerna visar tydligt att flödet varierar beroende på typ av åtgärd. Använd aktiviteterna i din miljö som grund för att ändra systemstorlek. Du får bättre genomströmning med mindre krävande åtgärder som att ändra (vilket också är vanligare).

### Cachelagring {#caching}

I redigeringsmiljön är cachningseffektiviteten vanligtvis mycket lägre eftersom det är vanligare att ändra webbplatsen och innehållet är mycket interaktivt och personaliserat. Med hjälp av dispatchern kan du cachelagra AEM-bibliotek, JavaScript-skript, CSS-filer och layoutbilder. Detta snabbar upp vissa delar av redigeringsprocessen. Om du konfigurerar webbservern för att ytterligare ange rubriker för webbläsarcachelagring på dessa resurser, kommer antalet HTTP-begäranden att minskas och på så sätt blir systemet mer responsivt som författarna upplever.

### Författare som arbetar parallellt {#authors-working-in-parallel}

I redigeringsmiljön är antalet författare som arbetar parallellt och den belastning som deras interaktioner lägger till i systemet de viktigaste begränsande faktorerna. Därför rekommenderar vi att du skalar ditt system baserat på det delade dataflödet.

För sådana scenarier utförde Adobe prestandatester på ett kluster av författare som inte har några delade noder.

* **Benchmark test 1a** Med ett aktivt-aktivt kluster med delad ingenting med två författarinstanser beräknar du den maximala genomströmningen med en lastprofil där användarna utför en enkel arbetsmoment som bygger på en basbelastning på 300 befintliga sidor, allt av liknande natur.

   * **Resultat**: Maximal genomströmning för en enkel sidskapandeövning, som ovan, (betraktas som en transaktion) är 2016 transaktioner/timme. Detta är en ökning på ungefär 16 % jämfört med en fristående författarinstans för samma test.

* **Benchmark test 2b** Med ett aktivt-aktivt kluster med delad ingenting med två författarinstanser beräknar du den maximala genomströmningen när inläsningsprofilen har en blandning av ny sidgenerering (10 %), ändring av befintliga sidor (80 %) och skapande och ändring av en sida i följd (10 %). Sidans komplexitet är densamma som i profilen för test 1. Den grundläggande ändringen av sidan görs genom att en bild läggs till och textinnehållet ändras. Även här utfördes övningen på en basbelastning på 300 sidor med komplexitet på samma sätt som i prestandatest 1.

   * **Resultat**: Maximalt dataflöde för ett sådant blandat åtgärdsscenario var 6288 transaktioner/timme. Detta är en ökning på ungefär 93 % jämfört med en fristående författarinstans för samma test.

>[!NOTE]
>
>Genomströmningsfrekvensen skiljer inte mellan transaktionstyper i en lastprofil. Den metod som används för att mäta genomströmning säkerställer att en fast andel av varje typ av transaktion inkluderas i arbetsbelastningen.

De två ovanstående testerna visar tydligt att AEM är skalbart väl för författare som utför grundläggande redigeringsåtgärder med AEM. I allmänhet är AEM mest effektivt vid skalning av läsåtgärder.

På en vanlig webbplats sker de flesta redigeringar under projektfasen. När webbplatsen har publicerats har antalet författare som arbetar parallellt vanligtvis sjunkit till ett lägre (driftsläge) genomsnitt.

Du kan beräkna antalet datorer (eller CPU:er) som krävs för författarmiljön enligt följande:

`n = numberOfParallelAuthors / 30`

Den här formeln kan fungera som en allmän riktlinje för skalning av CPU:er när författare utför grundläggande åtgärder med AEM. Det förutsätter att systemet och programmet är optimerade. Formeln kommer dock inte att innehålla true för avancerade funktioner som MSM eller Assets (se avsnitten nedan).

Se även de ytterligare kommentarerna om [parallellisering](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) och [prestandaoptimering](/help/sites-deploying/configuring-performance.md).

### Maskinvarurekommendationer {#hardware-recommendations}

Vanligtvis kan du använda samma maskinvara för din författarmiljö som du rekommenderas för din publiceringsmiljö. Vanligtvis är webbplatstrafiken mycket lägre i redigeringssystemen, men cacheeffektiviteten är också lägre. Den grundläggande faktorn här är dock antalet författare som arbetar parallellt, tillsammans med den typ av åtgärder som görs i systemet. I allmänhet är AEM-klustring (i författarmiljön) mest effektivt vid skalning av läsåtgärder. Med andra ord kan ett AEM-kluster skalas väl tillsammans med författare som utför grundläggande redigeringsåtgärder.

Testerna på Adobe utfördes med operativsystemet RedHat 5.5, som körs på en Hewlett-Packard ProLiant DL380 G5-maskinvaruplattform med följande konfiguration:

* Två Intel Xeon X5450-processorer med fyra kärnor på 3,00 GHz
* 8 GB RAM
* Broadcom NetXtreme II BCM5708 Gigabit Ethernet
* HP Smart Array RAID-styrenhet, 256 MB cache
* Två 146 GB SAS-diskar med 10 000 RPM konfigurerade som en RAID0-stripe-uppsättning
* SPEC CINT2006 Rate-poängen är 110

AEM-instanser kördes med en minsta stackstorlek på 256 MB, en maximal stackstorlek på 1 024 MB.

## Specifika beräkningar för publiceringsmiljön {#publish-environment-specific-calculations}

### Cachelagring av effektivitet och trafik {#caching-efficiency-and-traffic}

Cache-effektiviteten är avgörande för webbplatsens hastighet. I följande tabell visas hur många sidor per sekund ett optimerat AEM-system kan hantera med hjälp av en omvänd proxy, till exempel dispatchern:

| Cachenivåer | Sidor/s (topp) | Miljoner sidor/dag (genomsnitt) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>Ansvarsfriskrivning: Numren baseras på en standardmaskinvarukonfiguration och kan variera beroende på vilken maskinvara som används.

Cachekvoten är den procentandel sidor som dispatchern kan returnera utan att behöva komma åt AEM. 100 % anger att avsändaren besvarar alla förfrågningar, 0 % betyder att AEM beräknar varje sida.

### Komplexa mallar och tillämpningar {#complexity-of-templates-and-applications}

Om du använder komplexa mallar behöver AEM mer tid för att återge en sida. Sidor som tas från cachen påverkas inte av detta, men sidstorleken är fortfarande relevant när den totala svarstiden ska beaktas. Det kan ta tio gånger längre tid att återge en komplex sida än att bara återge en enkel sida.

### Formel {#formula}

Med följande formel kan du beräkna en uppskattning av hur komplex din AEM-lösning är:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

Beroende på komplexiteten kan du bestämma hur många servrar (eller processorkärnor) du behöver för publiceringsmiljön enligt följande:

`n = (traffic * complexity / 1000 ) * activations`

Variablerna i ekvationen är följande:

<table>
 <tbody>
  <tr>
   <td>trafik</td>
   <td>Förväntad topptrafik per sekund. Du kan beräkna detta som antalet sidträffar per dag, delat med 35 000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Använd 1 för ett enkelt program, 2 för ett komplext program eller ett mellanliggande värde:</p>
    <ul>
     <li>1 - en helt anonym, innehållsorienterad webbplats</li>
     <li>1.1 - en helt anonym, innehållsinriktad webbplats med personalisering på klientsidan/målsidan</li>
     <li>1.5 - en innehållsorienterad webbplats med både anonyma och inloggade avsnitt, klientsides-/målpersonalisering</li>
     <li>1.7 - för en innehållsorienterad webbplats med både anonyma och inloggade avsnitt, klientsid-/målpersonalisering och visst användargenererat innehåll</li>
     <li>2 - där hela webbplatsen kräver inloggning, med omfattande användning av användargenererat innehåll och en mängd olika personaliseringstekniker</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>Procentandelen sidor som kommer från dispatchercachen. Använd 1 om alla sidor kommer från cacheminnet, eller 0 om alla sidor beräknas av AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Använd ett värde mellan 1 och 10 för att ange mallarnas komplexitet. Ett högre antal innebär mer komplexa mallar, med värdet 1 för webbplatser med i genomsnitt 10 komponenter per sida, och värdet 5 för en sida är i genomsnitt 40 komponenter och 10 för i genomsnitt över 100 komponenter.</td>
  </tr>
  <tr>
   <td>aktiveringar</td>
   <td>Antal genomsnittliga aktiveringar (replikering av medelstora sidor och resurser från författaren till publiceringsskiktet) per timme dividerat med x, där x är antalet aktiveringar som gjorts i ett system utan prestandaeffekter till andra uppgifter som bearbetats av systemet. Du kan också fördefiniera ett pessimistiskt startvärde som x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Om du har en mer komplex webbplats behöver du också kraftfullare webbservrar så att AEM kan besvara en förfrågan inom en rimlig tid.

* Komplexitet under 4:
・ 1 024 MB JVM RAM* ・ CPU med låg till medelhög prestanda

* Komplexitet mellan 4 och 8:
・ 2 048 MB JVM RAM* ・ MID till högpresterande CPU

* Komplexitet över 8:
・ 4 096 MB JVM RAM* ・ processor med höga eller höga prestanda

>[!NOTE]
>
>* Reservera tillräckligt mycket RAM-minne för ditt operativsystem utöver det minne som krävs för din JVM.

## Ytterligare användningsspecifika beräkningar {#additional-use-case-specific-calculations}

Förutom beräkningen för ett standardwebbprogram kan du behöva ta hänsyn till specifika faktorer för följande användningsområden. De beräknade värdena ska läggas till i standardberäkningen.

### Resursspecifika överväganden {#assets-specific-considerations}

Omfattande bearbetning av digitala resurser kräver optimerade maskinvaruresurser, de viktigaste faktorerna är bildstorlek och högsta genomströmning för bearbetade bilder.

Allokera minst 16 GB stackutrymme och konfigurera arbetsflödet för DAM-uppdatering av resurser så att det använder [Camera Raw-paketet](/help/assets/camera-raw.md) för att lägga in råbilder.

>[!NOTE]
Ett högre bildflöde innebär att datorresurserna måste kunna hålla jämna steg med I/O-system och vice versa. Om arbetsflöden till exempel startas vid import av bilder kan överföringen av många bilder via WebDAV orsaka en eftersläpning i arbetsflödena.
Om du använder separata diskar för tarPM, datalager och sökindex kan det hjälpa till att optimera I/O-beteendet för systemet (det är dock oftast bra att behålla sökindexet lokalt).

>[!NOTE]
Se även [Resursens prestandaguide](/help/sites-deploying/assets-performance-sizing.md).

### Hanterare för flera platser {#multi-site-manager}

Resursanvändningen när AEM MSM används i en redigeringsmiljö beror till stor del på de specifika användningsområdena. De grundläggande faktorerna är:

* Antal live-kopior
* Periodicitet för utrullningar
* Innehållsträdets storlek som ska rullas ut
* Anslutna funktioner för utrullningsåtgärderna

Genom att testa det planerade användningsexemplet med ett representativt utdrag kan du få en bättre förståelse för resursanvändningen. Om du extrapolerar resultaten med den planerade genomströmningen kan du utvärdera de ytterligare resurser som krävs för AEM MSM.

Tänk också på att skribenter som arbetar parallellt kommer att uppleva biverkningar om AEM MSM använder fler resurser än planerat.

### Viktigt om storleksändring av AEM Communities {#aem-communities-sizing-considerations}

AEM-webbplatser som innehåller funktioner för AEM Communities (communitysajter) upplever en hög nivå av interaktion från webbplatsbesökare (medlemmar) i publiceringsmiljön.

Att tänka på vid storleksändring av en community-webbplats beror på den förväntade interaktionen från communitymedlemmar och huruvida optimala prestanda för sidinnehåll är av högre betydelse.

Användargenererat innehåll (UGC) som skickas till medlemmar lagras separat från sidinnehållet. AEM-plattformen använder ett nodarkiv som replikerar webbplatsinnehåll från författaren till publiceringen, men AEM Communities använder en enda gemensam butik för UGC som aldrig replikeras.

För UGC-arkivet är det nödvändigt att välja en lagringsresursleverantör (SRP) som påverkar den valda distributionen.
Se

* [Community-innehåll](/help/communities/working-with-srp.md)
* [Rekommenderade topologier för communities](/help/communities/topologies.md)

