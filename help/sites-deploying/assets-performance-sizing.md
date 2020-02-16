---
title: Prestandahandbok för resurser
seo-title: Prestandahandbok för resurser
description: Lär dig hur du avgör den optimala maskinvarustorleken för en ny konfiguration av Digital Asset Management (DAM) och hur du felsöker prestandaproblem
seo-description: Lär dig hur du avgör den optimala maskinvarustorleken för en ny konfiguration av Digital Asset Management (DAM) och hur du felsöker prestandaproblem
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prestandahandbok för resurser{#assets-performance-guide}

Digital resurshantering används ofta i de fall där prestanda är viktiga. Den vanliga DAM-installationen innehåller dock ett antal maskinvaru- och programvarukomponenter som kan påverka prestandan. Det här dokumentet innehåller följande:

* Information för systemadministratörer om hur man fastställer optimal maskinvarustorlek för en ny installation av Digital Asset Management
* Information för programutvecklare som vill felsöka DAM-instanser med prestandaproblem

## Prestandaproblem {#performance-issues}

Dåliga prestanda inom digital resurshantering kan påverka användarupplevelsen på tre sätt: interaktiva prestanda, bearbetning av resurser och nedladdningshastighet. För att förbättra prestandan är det viktigt att mäta de observerade prestandan korrekt och att fastställa målvärden.

**1. Interaktiv sökning och bläddring** Användare söker efter resurser eller bläddrar i DAM Finder och klagar över långsamma svarstider eller att sökresultaten inte visas omedelbart. Detta är ett interaktivt prestandaproblem.

Interaktiva prestanda mäts i svarstid för sidor. Detta är den tid det tar från att ta emot HTTP-begäran till att stänga HTTP-svaret, som kan avgöras av loggfilerna för begäran. Vanliga målprestanda är en sidsvarstid på mindre än två sekunder.

**2. Resurshantering** Ett problem med resurshanteringen är när användare överför resurser och det tar några minuter tills resurser konverteras och hämtas till AEM DAM.

Prestanda för tillgångsbearbetning mäts i genomsnittlig slutförandetid för arbetsflödet. Det här är den tid det tar från det att arbetsflödet för resursuppdatering anropas till det slutförs, vilket kan avgöras av användargränssnittet för arbetsflödesrapporter. Normala målprestanda beror på storleken och typen av resurser som bearbetas och antalet renderingar. Exempel på målprestanda kan vara följande:

* under tio sekunder för bilder som är mindre än 1 280 x 1 280 pixlar med standardåtergivningar
* under en minut för bilder som är mindre än 100 MB med standardrenderingar
* under fem minuter för HD-videoklipp som är kortare än en minut

**3. Hämtningshastighet** Ett genomströmningsproblem uppstår när hämtningen från AEM DAM tar lång tid och miniatyrerna visas inte direkt när du bläddrar i DAM-administratören eller DAM Finder.

Dataöverföringsprestanda mäts i antal kilobit per sekund. Det vanliga målet för prestanda är 300 kB per sekund för 100 samtidiga hämtningar.

**4. Faktorer som påverkar bearbetningen av tillgångar**

För att kunna uppskatta vilken maskinvara du behöver för att bearbeta resurser måste följande aspekter beaktas:

* Bildernas upplösning i antal pixlar
* Den heap som tilldelats AEM:s process

Mängden pixlar i bilden avgör bearbetningstiden - fler pixlar innebär att bearbetningen tar längre tid.
Bildtyp, komprimeringshastighet eller den relaterade storleken på filen som bilden lagras i påverkar inte den övergripande prestandan nämnvärt.

Heap har identifierats som den viktigaste begränsningsfaktorn. När resursen överskrider det tillgängliga lediga minnet minskar bearbetningsprestandan snabbt.

DAM-processerna är väl lämpade att utföras parallellt för stora mängder. När du överför resurser i en batch och processorer med flera kärnor går det snabbare att överföra den absoluta tiden per resurs.

**5. Uppskattar maskinvarukrav för att utföra tillgångsbearbetning**

Omfattande bearbetning av digitala resurser kräver optimerade maskinvaruresurser, de viktigaste faktorerna är bildstorlek och högsta genomströmning för bearbetade bilder.

Allokera minst 16 GB stackutrymme och konfigurera arbetsflödet för DAM-uppdatering av resurser så att det använder [Camera Raw-paketet](/help/assets/camera-raw.md) för att lägga in råbilder.

## Förstå systemet {#understanding-the-system}

En vanlig DAM-konfiguration består av slutanvändare som använder DAM via en belastningsutjämnare. DAM-instansen kan ingå i en grupperad konfiguration, där varje DAM-instans körs i en Java Virtual Machine-process på en fysisk eller virtuell dator. DAM-lagring tillhandahålls antingen av en RAID-disk vid installation av en enda dator eller av ett hanterat nätverksanslutet lagringsutrymme vid klustrade konfigurationer.

I följande förklaring beskrivs de möjliga prestandafallsområdena med vissa lösningar, beroende på vad som är lämpligt.

**Nätverksanslutning till slutanvändare** En långsam nätverksanslutning kan orsaka dataflödesproblem, i vissa sällsynta fall även latensproblem. Ibland har användaren en långsam anslutning från Internet, särskilt i intranät. Detta är ett tecken på felaktig nätverkstopologi.

**Tillfälligt filsystem** Ett långsamt lokalt filsystem kan orsaka interaktiva prestandaproblem, särskilt när det gäller sökning, eftersom sökindexen lagras på den lokala disken. Det kan dessutom orsaka problem med resursbearbetningen om kommandoradsprocessen används.

**AEM DAM Finder** Interaktiva prestandaproblem som ofta uppstår i sökningar orsakas av hög processoranvändning på grund av många samtidiga användare eller andra CPU-krävande processer i samma instans. Genom att gå från virtuella datorer till dedikerade datorer och se till att inga andra tjänster körs på datorn kan du förbättra prestandan. Om hög processorbelastning orsakas av resursbearbetning och många samtidiga användare rekommenderar dag att du lägger till ytterligare klusternoder.

**AEM DAM-arbetsflöde** Långvariga arbetsflödesprocesser vid tillgångsinmatning orsakar prestandaproblem vid bearbetning av resurser. Beroende på vilken typ av resurser som bearbetas kan detta visa på överanvändning av processorn. Dag rekommenderar att du minskar antalet andra processer som körs i systemet och ökar antalet tillgängliga processorer genom att lägga till klusternoder.

**NAS-anslutning** Dålig nätverksanslutning till NAS orsakar interaktiva prestandaproblem, eftersom åtkomst till nya noder under resurshanteringen blir långsammare på grund av nätverksfördröjning. Dessutom påverkar långsam nätverksgenomströmning negativt genomströmning, men även bearbetningsprestanda, eftersom inläsning och sparande av återgivningar blir långsammare.

Orsaker till dålig fördröjning och genomströmning i en NAS är vanligtvis nätverkstopologi eller överutnyttjande av NAS av andra tjänster.

**Nätverksansluten lagring** Överutnyttjade nätverksanslutna lagringssystem kan orsaka en mängd problem:

* Det har ofta uppstått problem med diskutrymmet som kan förebyggas genom korrekt storleksändring av ett DAM-projekt.
* Hög diskfördröjning kan spridas till långsamma åtkomsttider för CRX och kan leda till interaktiva prestandaproblem.
* Låg diskgenomströmning kan ge sämre prestanda för CQ5 DAM.

## Prestandatestning {#testing-for-performance}

För varje digitalt resurshanteringsprojekt måste du se till att det finns ett system för prestandatestning som snabbt kan identifiera och åtgärda flaskhalsar. Tänk på följande kontrollpunkter:

1. Prestandatester från början till slut med JMeter - Simulera ett exempel på sökning och bläddring för att upptäcka interaktiva prestandaproblem.
1. Genomströmnings- och fördröjningstester med JMeter - Om du kör på en klientdator ser du till att det inte finns några topologirelaterade problem.
1. Standardiserade materialbearbetningstester - Använd ett litet antal exempelresurser och mät tiden. Detta bör omfatta integration med externa arbetsflöden.
1. Övervaka processoranvändning, disk- och minnesanvändning för varje klusternod.
1. Diagnostik för läs-/skrivprestanda för CRX för att identifiera problem som inte är relaterade till bearbetning.
1. Övervaka nätverksfördröjning och -genomströmning från DAM-kluster till din NAS.
1. Testa läs- och skrivprestanda samt diskfördröjning direkt på NAS, om det är möjligt.

## Justera flaskhalsar {#tweaking-bottlenecks}

Följande prestandaförbättringar har hittills använts i projekt:

* Selektiv renderingsgenerering: generera bara de återgivningar du behöver genom att lägga till villkor i arbetsflödet för resursbearbetning, så att mer kostsamma återgivningar bara genereras för vissa resurser.
* Delat datalager bland instanser: när diskutrymmet börjar ta slut kan detta avsevärt minska det diskutrymme som behövs, till priset av högre konfigurationsinsatser och förlorad automatisk rensning av datalagret.

## Ytterligare läsning {#further-reading}

* [Analyserar långsamma och blockerade processer](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

