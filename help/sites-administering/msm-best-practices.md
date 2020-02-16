---
title: MSM Best Practices
seo-title: MSM Best Practices
description: Här hittar du bästa praxis som sammanställts av Adobes tekniker och konsultteam för att hjälpa till att komma igång med AEM Multi Site Manager.
seo-description: Här hittar du bästa praxis som sammanställts av Adobes tekniker och konsultteam för att hjälpa till att komma igång med AEM Multi Site Manager.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# MSM Best Practices{#msm-best-practices}

## Allmänt {#general}

MSM är ett konfigurerbart ramverk för automatisering av innehållsdistribution. Implementeringar omfattar ofta större delar av en webbplats och omfattar organisationer och geografiska områden. Vi rekommenderar därför att du planerar MSM-implementeringar lika noggrant som du planerar din webbplats:

* Planera noggrant **struktur och innehållsflöden** innan implementeringen startar.
* **Anpassa så mycket som behövs, men så lite som möjligt.** MSM har stöd för en hög grad av anpassning (t.ex. utrullningskonfigurationer), men oftast är det bäst att använda webbplatsens prestanda, tillförlitlighet och uppgraderingsbarhet för att minimera anpassningar.
* Upprätta en **styrningsmodell** tidigt och utbilda användarna därefter för att säkerställa framgång. Ett bra tillvägagångssätt från styrningssynpunkt är att **minimera den auktoritet som lokala innehållsproducenter måste** tilldela/koppla innehåll till andra lokala användare och deras respektive kopior. Detta beror på att icke-styrda, kedjade arv kan öka komplexiteten i en MSM-struktur avsevärt och påverka dess prestanda och tillförlitlighet.

* När det finns en plan för er struktur, innehållsflöden, automatisering och styrning - **skapa prototyper och testa systemet** noggrant innan du börjar implementera live.
* Kom ihåg att **Adobe Consulting och ledande systemintegratörer** har djupgående upplevelseplanering och implementering av innehållsautomatisering med MSM, så att de kan hjälpa er att komma igång med ert MSM-projekt och under hela dess implementering.

>[!NOTE]
>
>Mer information om hur du arbetar med MSM finns i kunskapsbasartiklarna:
>
>* [Vanliga frågor om MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Felsökning av MSM-problem](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)
>



>[!NOTE]
>
>Du kan också använda [referenskomponenten](/help/sites-authoring/default-components-foundation.md#reference) för att återanvända en sida eller ett stycke. Kom dock ihåg:
>
>* MSM är flexiblare och ger detaljerad kontroll över vilket innehåll som synkroniseras och när.
>* [Kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) rekommenderas nu framför grundkomponenterna.
>



## Live Copy-källor och layoutkonfigurationer {#live-copy-sources-and-blueprint-configurations}

Kom ihåg att en live-kopia kan skapas med [vanliga sidor](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) eller en [ritningskonfiguration](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Båda är giltiga användningsfall.

Ytterligare fördelar med att använda en ritkonfiguration är att de

* Tillåt författaren att använda alternativet **Rollout** på en ritning - för att (explicit) överföra ändringar till live-kopior som ärver från den här ritningen.
* Tillåt författaren att använda **Skapa webbplats**; på så sätt kan användaren enkelt välja språk och konfigurera strukturen för live-kopian.
* Definiera en standardkonfiguration för utrullning för live-kopior som har en relation till ritningen.

Om det inte finns någon referens till en ritningskonfiguration kan rollouts bara initieras från själva live-kopiorna, vilket i själva verket leder till att innehållet hämtas från källan.

När du skapar en ny webbplats med en live-kopia är det fördelaktigt att skapa designkonfigurationer för att säkerställa att hela MSM-funktionsuppsättningen är tillgänglig.

## Komponenter- och behållarsynkronisering {#components-and-container-synchronization}

I allmänhet gäller följande som utrullningsregel i MSM för synkronisering av komponenter:

* Komponenter introduceras med synkronisering av alla resurser som ingår i planen.
* Behållare synkroniserar bara den aktuella resursen.

Detta innebär att komponenterna behandlas som en sammanställning och att själva komponenten och alla dess underordnade komponenter i en utrullning ersätts med de i ritningarna. Det innebär att om en resurs läggs till lokalt i en sådan komponent, kommer den att gå förlorad i innehållet i ritningen vid utrullning.

För att ge stöd åt kapsling av komponenter så att lokalt tillagda komponenter bibehålls i en utrullning måste komponenten deklareras som en behållare. Som ett exempel deklareras standardparsysen som en behållare så att den kan hantera lokalt tillagt innehåll.

>[!NOTE]
>
>Lägg till egenskapen `cq:isContainer` i komponenten för att ange den som en behållare.

## Skapa webbplats {#create-site}

Observera att AEM har två huvudmetoder för att skapa live-kopior:

* När du [skapar en Live-kopia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Detta kan betraktas som ett mer allmänt tillvägagångssätt, vilket gör att du kan skapa live-kopior från vilken sida som helst. Innehållsstrukturen för en live-kopia matchar källan exakt.

* När en plats [skapas](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Detta är ett mer specialiserat tillvägagångssätt, främst för att skapa webbplatser med en flerspråkig struktur.

Tänk på följande när du skapar en plats:

* Om du vill skapa en ny plats behöver du en [ritningskonfiguration](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Om du vill att språksökvägar ska kunna väljas på en ny plats måste motsvarande språkrörelser finnas i planen (källa).
* När en [ny webbplats har skapats som en live-kopia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (med **Skapa** och sedan **Webbplats**) är de två första nivåerna i den här live-kopian *oanvändbara*. Sidans underordnade hör inte till live-relationen, men en utrullning kommer ändå att gå ned om en live-relation som matchar utlösaren hittas.

   Det hjälper till att undvika:

   * manuellt lägga till språk i planen (under den första nivån)
   * manuellt lägga till innehåll direkt under språkroten,
   * leder inte till att det nya innehållet automatiskt överförs till den aktiva kopian vid utrullning.

## MSM och flerspråkiga webbplatser {#msm-and-multilingual-websites}

MSM kan hjälpa till att skapa flerspråkiga webbplatser på två sätt:

* När du skapar språkmallar.

   * Även om själva MSM **inte tillhandahåller innehållsöversättning** kan det integreras med översättningsanslutningar från tredje part som gör det. Observera att:

      * Med MSM kan du avbryta arv på sid- och/eller komponentnivå. Detta förhindrar att översatt innehåll skrivs över (från en live-kopia, med ännu inte översatt innehåll från en ritning) vid nästa utrullning.
      * Vissa översättningsanslutningar från tredje part automatiserar hanteringen av MSM-arv.

         Kontakta översättningstjänsten för mer information.

      * Ett annat sätt att skapa och översätta språkmallar är att använda språkkopior i kombination med AEM:s färdiga ramverk för översättningsintegrering.

* När du distribuerar innehåll från språkmallsidor.

   * Till exempel, från den franska huvudpersonen till landsspecifika webbplatser, som Frankrike/Frankrike, Kanada/franska, Schweiz/franska.

Mer information finns i [Översätta innehåll för flerspråkiga platser](/help/sites-administering/translation.md) och [Översättningsmetoder](/help/sites-administering/tc-bp.md).

## Strukturändringar och utrullningar {#structure-changes-and-rollouts}

Ändringar av innehållsstrukturen i ett utkast/källträd återspeglas på olika sätt i en live-kopia. Detta beror på ändringstypen:

* **Om du skapar** nya sidor i en plan skapas motsvarande sidor i live-kopior efter utrullningen med standardkonfigurationen.

* **Om du tar bort** sidor i en plan kommer motsvarande sidor att tas bort från live-kopior efter utrullning med standardkonfigurationen.

* **Om du flyttar** sidor i en plan kommer motsvarande sidor **inte** att flyttas i live-kopior efter utrullning med standardkonfigurationen:

   * Orsaken till detta är att en sidflyttning implicit inkluderar en sidborttagning. Detta kan eventuellt leda till oväntat beteende vid publicering, eftersom om du tar bort sidor på författaren inaktiveras motsvarande innehåll automatiskt vid publicering. Detta kan också få en &quot;spara på&quot;-effekt på relaterade objekt som länkar, bokmärken och andra.
   * Innehållsarv i respektive live-kopia uppdateras för att återspegla den nya platsen för deras källor i planen.
   * Om du vill förverkliga en sidövergång från en plan till dynamiska kopior bör du tänka på följande bästa tillvägagångssätt:

>[!NOTE]
>
>Detta fungerar bara med utlösaren [](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)Vid utrullning.

* Skapa en anpassad utrullningskonfiguration:

   * Den nya konfigurationen måste innehålla åtgärden:

      `PageMoveAction`

      Lägg inte till andra åtgärder i den här konfigurationen.

* Placera den nya konfigurationen:

   * Om du vill flytta sidan helt och hållet och ta bort respektive sidor på den gamla platsen i den aktiva kopian:

      * Placera den nyskapade konfigurationen före standardkonfigurationen för utrullning.

         Standardkonfigurationen för utrullning tar bort sidorna på den gamla platsen.
   * Så här flyttar du ut sidan samtidigt som du behåller respektive sidor på den gamla platsen i live-kopiorna (duplicerar i stort sett innehållet):

      * Placera den nyskapade konfigurationen efter standardkonfigurationen för utrullning.

         Detta säkerställer att inget innehåll tas bort i den aktiva kopian eller inaktiveras från publiceringen.


## Anpassa utrullningar {#customizing-rollouts}

MSM-utrullningskonfigurationer är mycket anpassningsbara. Du bör vara medveten om att automatisering av utrullningar kan få omfattande konsekvenser. Som en god praxis bör du planera *mycket* noggrant innan, till exempel:

* automatisera utrullningar, t.ex. med [utlösarna](#onmodify)onModify,
* anpassa [nodtyper/egenskaper](#node-types-properties),
* starta efterföljande arbetsflöden,
* och/eller aktivering av innehåll som en del av utrullningar.

### onModify {#onmodify}

När du använder [utlösaren](/help/sites-administering/msm-sync.md#rollout-triggers) bör `onModify` du tänka på följande:

* Automatisering av utrullningar med `onModify` utlösare kan ha en negativ inverkan på redigeringsprestanda eftersom de utlöser rollout efter *varje* sidändring.

* Resultatet av utrullningen kan skilja sig från det förväntade:

   * Du kan inte ange ordningen för ändringshändelserna som skapas.
   * Den händelsebaserade arkitekturen kan inte garantera sekvensen för de händelser som skickas till utrullningshanteraren.

* Om en sådan utrullningskonfiguration används kan konflikter uppstå om samma resurs uppdateras samtidigt.

Därför rekommenderar vi att du *endast* använder `onModify` utlösare om fördelarna med automatisk utrullning är större än eventuella prestandaproblem.

### Nodtyper/egenskaper {#node-types-properties}

Kom ihåg följande:

* Förutom att anpassa utrullningsåtgärder kan MSM även anpassa nodegenskaper som introduceras. Med [MSM OSGi-konfigurationen kan du undanta nodtyper](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) från kopiering från källan till live-kopian.

## Ytterligare information {#further-information}

Här och på följande sidor finns de relaterade frågorna:

* [Skapa och synkronisera Live-kopior](/help/sites-administering/msm-livecopy.md)
* [Översiktskonsol för Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Konfigurera Live Copy-synkronisering](/help/sites-administering/msm-sync.md)
* [MSM-utrullningskonflikter](/help/sites-administering/msm-rollout-conflicts.md)

