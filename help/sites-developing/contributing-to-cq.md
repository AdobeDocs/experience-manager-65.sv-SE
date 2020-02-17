---
title: Bidrar till AEM
seo-title: Bidrar till AEM
description: AEM utvecklas enligt beprövade metoder som ofta används i stora öppen källkodsprojekt
seo-description: AEM utvecklas enligt beprövade metoder som ofta används i stora öppen källkodsprojekt
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Bidrar till AEM{#contributing-to-aem}

## Utvecklingsmetod {#development-methodology}

AEM utvecklas enligt beprövade metoder som ofta används i stora öppen källkodsprojekt. Många kärnelement i AEM:s teknologi bibehålls i själva verket som aktiva öppen källkodsprojekt, som Sling och Jackrabbit, som har bidragit till Apache Software Foundation. En viktig aspekt av denna anda som finns i AEM är att du uppmuntras att använda de tillgängliga e-postlistorna och onlineforumen för direktinteraktion med utvecklingsteamet.

Om du bidrar till komponenter i AEM bör du bekanta dig med AEM på samma sätt som när du bidrar till ett öppen källkodsprojekt och kommunicera med det befintliga kärnteamet på samma sätt som när du skulle ha tänkt bidra till ett sådant projekt.

## Nödvändig upplevelse {#required-experience}

HTTP-protokollet (HyperText Transfer Protocol) är centralt för allt vi gör. Innan du bidrar till AEM bör du därför ha en djupgående förståelse för HTTP, helst i den utsträckning som du skulle kunna skriva en egen Java-implementering av en flertrådig HTTP-server med trådpooling. Du bör också ha en förståelse för HTTP/1.1 keep-alive-beteendet, och du bör ha en djupgående kunskap om interaktioner på server-/klientsidan med JavaScript, särskilt den asynkrona typ av interaktion som representeras av AJAX.

Eftersom siddynamik och interaktivt innehåll är avgörande för WM-upplevelsen är det viktigt att du har en tämligen djup förståelse för Document Object Model och dess potential för programmatisk manipulering som svar på händelser. Du bör känna till exempelvis DOM-manipulering i realtid och dra-och-släpp-beteenden över flera webbläsardokument (t.ex. användning av iframes).

På den högsta nivån bör du alltså ha en god förståelse för:

* protokollet [HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (helst [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Cascading Style Sheets
* XML (Extensible Markup Language)
* Asynkrona designmönster för JavaScript och XML (AJAX)
* JavaScript-objektnotation (JSON)
* Document Object Model
* Tillståndskänslig eller tillståndslös interaktion
* [Identifierare för enhetliga resurser](https://www.ietf.org/rfc/rfc2396.txt)
* Webbläsarcookies
* och andra moderna webbutvecklingskoncept

Adobe Experience Managers teknikstack bygger på [Apache Felix](https://felix.apache.org/) OSGI-behållaren med [Apache Sling](https://sling.apache.org/site/index.html) -webbramverket och bäddar in en Java Content Repository ([JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)) baserad på [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Du bör bekanta dig med dessa enskilda projekt, liksom med andra komponenter med öppen källkod (t.ex. Apache Lucene) som används i området där du tänker bidra.

## Tribal Knowledge {#tribal-knowledge}

Vissa koncept och vägledande principer är djupt inrotade i den tidigare dagskulturen. I det här avsnittet beskrivs några av de&quot;djupt DNA-inbäddade&quot; problemen som du bör känna till.

### Allt är innehåll {#everything-is-content}

Innehållet innehåller inte bara alla data som finns kvar i webbprogrammet. Programkoden, biblioteken, skripten, mallarna, HTML, CSS, bilder och artefakter av alla de slag, allt och allt finns kvar i Content Repository och importeras/exporteras i form av paket via Package Manager och Package Share.

### David&#39;s Model {#david-s-model}

Det sätt på vilket innehåll ska modelleras i en Java Content Repository kräver ett helt annat sätt att tänka än vad som är vanligt inom programvarubranschen för datamodellering i relationsvärlden. Grundläggande läsning för alla nykomlingar i content management är [Davids modell JCR-vägen: En guide för innehållsmodellering](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

REST-strategin är djupt inrotad i det vi gör. Detta innebär bland annat att man undviker tillståndskänsliga interaktioner och att man måste tänka på att URI:er är definitiva adresser för innehåll och tjänster.

REST (REpresentational State Transfer) avser den programarkitekturstil som World Wide Web bygger på. Den beskriver de viktigaste elementen som får webben att fungera och innehåller därför en uppsättning principer för hur webbaserade program ska utformas. När du utformar ett API som ska användas via webben är det därför klokt att följa dessa&quot;bästa praxis&quot;.

Eftersom REST ger en vägledande filosofi bakom så mycket av det vi gör, bör ni se det som viktigt att bli väl insatt i de stora delarna av RESTful-design. Ett bra ställe att börja på är med [Roy Fielings avhandling](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Sling Request Resolution {#sling-request-resolution}

En viktig aspekt när det gäller AEM är hur inkommande begäranden relaterar till innehåll och programbeteende, hur innehåll struktureras i innehållsdatabasen och var AEM letar efter programlogiken som hanterar begäran. Läs om Apache [Sling-URL:ens sönderdelning](https://sling.apache.org/site/url-decomposition.html) och hur den används för REST:s arkitekturstil och dess tillståndslösa, cacheable- och lageruppbyggda systembegränsningar.

Viktiga aspekter att förstå om Apache Sling:s begäranupplösning är hur begäranden primärt mappas till en viss resurs i innehållsdatabasen, hur ytterligare egenskaper i begäran tillsammans med egenskaper för dessa innehållsobjekt avgör vilken programkod som ska anropas för att återge innehållet och hur kod i /apps åsidosätter kod i /libs.

### Quickstart {#quickstart}

Inget steg tre: Om du vill installera och köra programmet hämtar och dubbelklickar du på JAR-filen Quickstart. Det finns inget steg tre. Ytterligare valfria funktioner behöver bara installera rätt paket från paketresursen.

Liten snabbstartsstorlek: Behåll storleken på JAR-filen för QuickStart med ett minimum. Använd bibliotek på ett smart och optimerat sätt och flytta tillvalsfunktioner till paketdelning.

Snabbare starttid: När du gör en ändring som kan påverka starttiden måste du se till att den blir kortare, inte längre.

### Medel {#lean-and-mean}

Vi föredrar kod och projekt som är lätta, små, snabba och eleganta. &quot;Bra nog&quot; är inte tillräckligt bra.

Återanvändning av kod: Vår OSGi-baserade produktarkitektur och&quot;allt är innehåll&quot;-filosofi innebär att vi har ovanligt goda möjligheter att återanvända kod och artefakter. Vi försöker dra nytta av detta när det är möjligt för att behålla funktioner som är både smala och tydliga.

Lös koppling: Vi föredrar löst kopplade interaktioner framför nära beroenden och&quot;oönskad intimitet&quot;. Förlorad koppling möjliggör också mer återanvändning av kod.

### Bryt inte demon {#don-t-break-the-demo}

Bekanta dig med demoskript och produktfunktioner som oftast visas i demos. Förstå att i alla fall inget du gör någonsin bör bryta mot en&quot;demomanusfunktion&quot;. Kärnprodukten bör alltid vara redo för demo, även under utvecklingen.

### Design för tillförlitlighet {#design-for-reliability}

Vi strävar efter att designa och koda funktioner på ett icke-mjukt sätt så att (till exempel) ett problem med ett enskilt DOM-element inte gör att en hel sida inte återges. Med andra ord: Gör saker som borde vara dödliga. Gör allt annat överblivet. Gör produkten &quot;förlåt&quot;.

### Onormal är New Normal {#abnormal-is-the-new-normal}

Förlita dig inte på att du stänger av kopplingar. Se till att du rensar vid start. Onormal avslutning är normal avslutning.

`shutdown == kill -9 == power outage`

### Var redo för elastisk klustring {#be-ready-for-elastic-clustering}

Var alltid redo för elastisk klustring, anta alltid att det finns klustring. I allmänhet innebär en lösning med stöd för klustring att du följer allt som finns i innehållsdatabasen.

### Design för bakåtkompatibilitet {#design-for-backward-compatibility}

Ingenting ni gör ska bryta mot en kunds gamla kod. Överväg bara `/libs` att innehålla produktkod som kan uppdateras under en uppgradering. Avsnittet `/apps` i databasen är projektkod och avsnittet innehåller anpassade konfigurationer som måste bevaras `/etc` . I allmänhet ska du inte skriva över något i `/apps`, `/content` och `/home`. Efter en uppgradering bör den gamla projektkoden, konfigurationerna och innehållet fortsätta att fungera som tidigare.

Att skapa bakåtkompatibelt material säkerställer också att uppgraderingsupplevelsen matchar enkelheten i den första installationen. Det räcker att bara stoppa AEM, ersätta JAR-filen från Quickstart och starta AEMagain. Med en snabbt växande installationsbas blir uppgraderingseffektiviteten en allt större fördel.

Befintliga API:er kan och bör markeras som inaktuella när de är nyare, men bättre funktioner ersätter dem, men alla API:er som publicerades i en tidigare version av 5.x måste fortsätta att fungera eftersom de kan användas i anpassad programkod. Inga sådana API:er ska tas bort.

Bakåtkompatibiliteten bör också beaktas när det gäller den allmänna konsekvensen i innehållsstrukturen och användarupplevelsen.

## Kärnbegrepp {#core-concepts}

**Designinstans** - Av säkerhetsskäl, av styrningsskäl och av andra skäl delas instanser av AEM in i Author- och Publish-instanser på en produktionsplats. Mer information om distributionsarkitektur (inklusive författare/publiceringsinstanser) finns i dokumentationen om AEM-instanser.

**Cachelagring, kopiering och bakning** - Traditionellt sett är koncepten bakning kontra kopiering en viktig skillnad mellan olika Web Content Management-system. I CMS-jargon avser&quot;baking&quot; begreppet implementering av data i statiska filer vid publicering, medan&quot;frying&quot; avser begreppet att bearbeta data för slutlig presentation vid begäran (dvs. precis i tid).

**Klustring och lastbalansering** - För att öka tillgängligheten och förbättra prestandan i en produktionsmiljö är det vanligt att kombinera flera författare- och/eller publiceringsinstanser (i kluster), antingen genom att göra dem tillgängliga för olika användargrupper eller genom lastbalansering bakom en Dispatcher-konfiguration.

Det går också att kombinera flera instanser av innehållsdatabasen för att skapa en JCR-lösning med *hög tillgänglighet* , som sedan kan integreras med din AEM-lösning för att maximera skyddet mot maskinvaru- och programvarufel. Mer information finns i [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) .

**Komponent** - I AEM är en komponent en objekttyp, som i allmänhet kan skapas genom att du drar och släpper dem från t.ex. Sidsparken. De färdiga komponenterna som levereras med AEM är till exempel komponenterna Text, Title, Tag Cloud, Carousel, Image och List, som alla finns tillgängliga från Sidekick vid körning.

**Innehållssökning** - I redigeringsläget är panelen Innehållssökning en särskild panel (bildruta) till vänster på sidan som, beroende på vilken flik du väljer längst upp, visar listor med bilder, dokument, Flash-resurser, sidor, stycken eller databasresurser som du kan dra och släppa från Innehållssökning till den sida du arbetar med (till höger).

**Digitala resurser** - I AEM är digitala resurser (vanligtvis) bilder och multimediefiler. Mer information finns i Arbeta med digitala resurser i DAM.

**Dispatcher** - Dispatcher är både ett cachnings- och belastningsutjämningsverktyg och tillhandahåller vissa säkerhetsfunktioner.

**ExtJS-widgetar** - De flesta användargränssnittselement i AEM använder ExtJS, som är ett tredjepartswidgetbibliotek som är skrivet i JavaScript. ExtJS har anpassningsbara gränssnittswidgetar med höga prestanda och en väldesignad och utbyggbar komponentmodell.

**JCR, Java Content Repository** - Java Content Repository-specifikationen (JSR-283) tillhandahåller både en abstrakt datamodell och ett Application Programming-gränssnitt för att skapa ett enormt skalbart NoSQL-datalager som kombinerar funktioner i ett filsystem och en objektdatabas. Du behöver inte förstå JSR-283 i detalj, men du bör ägna lite tid åt att bekanta dig med de grundläggande funktionerna i JCR och den underliggande datamodellen, eftersom JCR är det som gör det möjligt att&quot;allt är innehåll&quot;-filosofin i AEM.

JCR är alltså ett system med noder och egenskaper, där noder kan ärva från andra noder och allt innehåll lagras som *egenskapsvärden*. Observera, att JCR, förutom vanliga arv, även innehåller konceptet&quot;mixin&quot;-noder, som möjliggör modellering av flera arv.

JCR har ett antal fördefinierade nodtyper och egenskapstyper, men i allmänhet är typningssystemet relativt flexibelt och (faktiskt) en av styrkorna hos JCR är att det gör det möjligt att lagra och hantera både strukturerat och ostrukturerat innehåll lika enkelt. JCR kan alltså rymma mycket strukturerade data, men kan även rymma godtyckliga dynamiska datastrukturer utan schemabegränsningar.

JavaDoc för JCR:s Java API är [här](http://jackrabbit.apache.org/jcr/jcr-api.html).

Innan du försöker läsa JavaDoc eller JCR-specifikationen själv kanske du vill titta på [den här förklaringen](/help/sites-developing/the-basics.md#java-content-repository) av JCR på hög nivå som implementerats av Adobe Experience Services.

**Multi-Site Manager (MSM)** - MSM-funktionen i AEM hjälper kunderna att hantera flerspråkigt och internationellt innehåll, vilket gör det möjligt för dem att balansera centraliserad branding med lokaliserat innehåll.

**OSGi** - OSGi är den tjänstebaserade runtime-tekniken som utgör grunden för modulär Java-utveckling i AEM. Det är ett ramverk som inte bara erbjuder en mycket dynamisk (och säker) miljö för klassinläsning och körning av kodresurser (så kallade paket), utan också fullständig kontroll över synligheten och livscykeln för de olika tjänster som paketeras med. Ett tjänsteregister tillhandahåller en samarbetsmodell för paket som tar hänsyn till livscykeldynamik (och versionskrav). OSGi löser många av de problem som programservrar var tänkta att lösa, men gör det på ett lätt och mycket dynamiskt sätt, vilket till exempel gör det möjligt att använda tjänster under drift (så att den nya koden blir omedelbart tillgänglig utan att servern startas om).

**Parsys, Paragraph System** - Styckesystemet (parsys) är en sammansatt komponent som gör att författare kan lägga till komponenter av olika typer på en sida och som innehåller andra styckekomponenter. Varje stycketyp representeras som en komponent. Styckesystemet är också en komponent som innehåller de andra styckekomponenterna.

**Microkernel** - Alla arbetsytor i databasen kan konfigureras separat för att lagra data via en viss mikrokernel (en klass som hanterar läsning och skrivning av data). På samma sätt kan databasens hela versionsarkiv även konfigureras separat så att en viss mikrokärna används. Det finns ett antal olika mikrokärnor som kan lagra data i en mängd olika filformat eller relationsdatabaser. (Det finns till exempel beständiga hanterare för MongoDB, DB2 eller Oracle) Standardmikrokärnan för AEM är tarMK (se vidare nedan).

**Publiceringsinstans** - Av säkerhetsskäl, av styrningsskäl och av andra skäl delas instanser av AEM vanligtvis upp i Author- och Publish-instanser på en produktionsplats. Mer information om distributionsarkitektur (inklusive författare/publiceringsinstanser) finns i dokumentationen om AEM-instanser.

**QuickStart** - Till skillnad från många andra program installerar du AEM med hjälp av en och samma självextraherande JAR-fil. När du dubbelklickar på JAR-filen för första gången installeras allt du behöver automatiskt. Snabbstart-JAR innehåller alla filer som behövs för CRX-databasen (inklusive administrativa funktioner), virtuella databastjänster, index- och söktjänster, arbetsflödestjänster, säkerhet och en webbserver, plus CQ Servlet Engine (CQSE) och alla AEM-tjänster. Det finns inga andra filer att installera: QuickStart är självständigt.

Första gången du startar Quickstart skapas en hel JCR-kompatibel databas i bakgrunden, vilket kan ta flera minuter. Efter den här initiala starten går det mycket snabbare att starta eftersom databasinfrastrukturen redan har fastställts.

Många startalternativ (t.ex. det aktiva portnumret och om AEM-instansen i fråga ska vara en Publish-instans eller en Author-instans). och mycket mer) kan du styra genom att byta namn på QuickStart-filen. Om du vill se en lista med alternativ i det här avseendet kör du JAR med &quot;-help&quot; på kommandoraden:

```shell
java -jar <quickstartfilename>.jar -help
```

**Replikeringsagenter** - Replikeringsagenter är centrala för AEM eftersom den mekanism som används för att publicera (aktivera) innehåll från en författare till en publiceringsmiljö. tömma innehåll från Dispatcher-cachen, returnerar användargenererat innehåll (till exempel formulärindata) från publiceringsmiljön till författarmiljön.

**Ställning** - Med hjälp av ställningar kan du skapa ett formulär (en struktur) med fält som återspeglar den struktur du vill ha för sidorna och sedan använda det här formuläret för att enkelt skapa sidor som baseras på den strukturen.

**Segmentering** - Besökare har olika intressen och mål när de besöker en webbplats. Att förstå besökarnas mål och uppfylla deras förväntningar är en viktig förutsättning för onlinemarknadsföring. Segmentering hjälper till att uppnå detta genom att analysera och karakterisera en besökares detaljer.

**Sidespark** - Sidsparken är ett palettliknande flytande fönster som visas på den redigerbara sidan, där nya komponenter kan dras och åtgärder som gäller för sidan kan utföras.

**Site Catalyst** - SiteCatalyst ger marknadsförarna ett ställe där de kan mäta, analysera och optimera integrerade data från alla onlineinitiativ i flera olika marknadsföringskanaler. Du kan använda Adobe SiteCatalyst för att analysera data från AEM-webbplatser.

**Tjärlagring (tarMK)** - tarMK är standardbeständighetssystemet i AEM. Även om AEM kan konfigureras att använda ett annat beständigt system (till exempel MongoDB), har tarMK vissa fördelar eftersom det är prestandaoptimerat för vanliga JCR-fall (vilket är mycket snabbt), använder ett standarddataformat och kan snabbt och enkelt säkerhetskopieras.

**Mall** - I AEM anger en mall en viss typ av sida. Den definierar strukturen för en sida (och anger vanligtvis en miniatyrbild och olika egenskaper). Du kan till exempel ha separata mallar för produktsidor, platskartor och kontaktinformation.

**Arbetsflöde** - Med AEM Workflow System kan man skapa automatiserade processer som innefattar sidor eller resurser.
