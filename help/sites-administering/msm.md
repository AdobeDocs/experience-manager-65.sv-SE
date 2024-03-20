---
title: "Återanvända innehåll: Multi Site Manager och Live Copy"
description: Lär dig hur du återanvänder innehåll med Live-kopior och Multi Site Manager.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 0%

---

# Återanvända innehåll: Multi Site Manager och Live Copy{#reusing-content-multi-site-manager-and-live-copy}

Med Multi Site Manager (MSM) kan du använda samma platsinnehåll på flera platser. MSM använder sin Live Copy-funktion för att uppnå detta:

* Med MSM kan man

   * Skapa innehåll en gång och sedan
   * Kopiera innehållet till och återanvända innehållet i andra områden ([live-kopior](#live-copies)) på samma eller andra webbplatser.

* MSM upprätthåller sedan (live)-relationerna mellan källinnehållet och dess livekopior så att:

   * När du ändrar källinnehållet synkroniseras källkopiorna och livekopiorna (så att ändringarna även tillämpas på livekopiorna).
   * Du kan justera innehållet i live-kopiorna genom att koppla från den aktiva relationen för enskilda undersidor, komponenter eller båda. På så sätt tillämpas inte längre ändringar i källan på den aktiva kopian.

Här och på följande sidor finns de relaterade frågorna:

* [Skapa och synkronisera Live-kopior](/help/sites-administering/msm-livecopy.md)
* [Översiktskonsol för Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Konfigurera Live Copy-synkronisering](/help/sites-administering/msm-sync.md)
* [MSM-utrullningskonflikter](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM Best Practices](/help/sites-administering/msm-best-practices.md)

## Möjliga scenarier {#possible-scenarios}

Det finns många användningsfall för MSM och live-kopior. Exempel:

* **Multinationals - Global till lokalt företag**

  Ett typiskt användningsfall som MSM stöder är att återanvända innehåll på flera multinationella webbplatser på samma språk. På så sätt kan kärninnehållet återanvändas, samtidigt som nationella variationer tillåts.

  Exempelvis skapas den engelska delen av exemplet med referensplatsen We.Retail för kunder i USA. Det mesta av innehållet på den här webbplatsen kan också användas för andra webbsidor.Butikssajter som passar för engelsktalande kunder i olika länder och kulturer. Kärninnehållet är detsamma på alla webbplatser, och regionala justeringar kan göras.

  Följande struktur kan användas för webbplatser för USA, Storbritannien, Kanada och Australien:

  ```xml
  /content
      |- we.retail
          |- language-masters
              |- en
      |- we.retail
          |- us
              |- en
      |- we.retail
          |- gb
              |- en
      |- we.retail
          |- ca
              |- en
      |- we.retail
          |- au
              |- en
  ```

  >[!NOTE]
  >
  >MSM översätter inte innehållet. Den används för att skapa den struktur som krävs och distribuera innehållet.
  >
  >
  >Se [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md) om du vill utöka ett sådant exempel.

* **Nationell myndighet - chef för de regionala avdelningarna**

  Ett företag med ett nätverk av återförsäljare kan också vilja ha separata webbplatser för sina enskilda återförsäljare - var och en är en variation av huvudwebbplatsen som huvudkontoret tillhandahåller. Detta kan gälla ett enskilt företag med flera regionala kontor eller ett nationellt franchisystem som består av en central franchisor och flera lokala franchisetagare.

  Huvudkontoret kan tillhandahålla viktig information, medan de regionala enheterna kan lägga till lokal information, som kontaktuppgifter, öppettider och händelser.

  ```xml
  /content
      |- head-office-Berlin
      |- branch-Hamburg
      |- branch-Stuttgart
      |- branch-Munich
      |- branch-Frankfurt
  ```

* **Flera versioner**

  Du kan också använda MSM för att skapa versioner av en viss underavdelning. En underwebbplats till support som innehåller information om olika versioner av en viss produkt, där basinformationen är konstant och endast de uppdaterade funktionerna måste ändras:

  ```xml
  /content
      |- support
          |- product X
              |- v5.0
              |- v4.0
              |- v3.0
              |- v2.0
              |- v1.0
  ```

  >[!NOTE]
  >
  >I så fall måste du bestämma om du ska göra en enkel kopia eller använda live-kopior.
  >
  >Balansen är:
  >
  >  * Hur mycket av det centrala innehållet behöver uppdateras över de olika versionerna.
  >
  >Mot:
  >
  >  * Hur mycket av de enskilda kopiorna måste justeras.

## MSM från användargränssnittet {#msm-from-the-ui}

MSM är direkt tillgängligt i användargränssnittet med hjälp av olika alternativ från rätt konsol. Så här gör du en introduktion:

* **Skapa webbplats** (**Webbplatser**)

   * Med MSM kan du hantera flera webbplatser som delar gemensamt innehåll. Till exempel tillhandahålls webbplatser ofta för internationella målgrupper så att det mesta av innehållet är gemensamt i alla länder, med en delmängd av innehållet som är specifikt för varje enskilt land. Med MSM kan du [skapa live-kopior som automatiskt uppdaterar en eller flera webbplatser baserat på din källwebbplats](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Detta hjälper er också att genomdriva en gemensam basstruktur, använda det gemensamma innehållet på flera webbplatser, bibehålla en gemensam design och känsla samt fokusera på att hantera innehållet som faktiskt skiljer sig åt mellan webbplatserna.
   * Den kräver en fördefinierad ritningskonfiguration för att ange källan.
   * Skapar en live-kopia av (fördefinierad) källan.
   * Den ger användaren **Utrullning** -knappen.

* **Skapa Live Copy** (**Webbplatser**)

   * Med MSM kan du [skapa en tillfällig (engångs) live-kopia av en enskild sida eller underavdelning till en webbplats](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page), till exempel duplicering av en undergren för att ge information om en ny/uppdaterad version av en produkt.
   * Skapar en ad hoc live-kopia (ingen plantryckskonfiguration krävs).
   * Den kan användas för att (omedelbart) skapa en live-kopia av valfri sida/gren.
   * Kräver **Synkronisera** (ger inte **Utrullning** -knapp).

* **Visa egenskaper** (**Webbplatser**)

   * Om det är lämpligt kan du använda det här alternativet [övervaka din livekopia](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) genom att tillhandahålla information om relaterade **Live Cop** y eller **Blueprint**.

* **Referenser** (**Webbplatser**)

   * The [Referenser](/help/sites-authoring/basic-handling.md#references) järnvägen ger information om **Live-kopior** tillsammans med tillgång till lämpliga åtgärder.

* **Live Copy - översikt** (**Webbplatser**)

   * Med den här konsolen kan du [visa och hantera din plan och dina livekopior](/help/sites-administering/msm-livecopy-overview.md).

* **Blueprints** (**verktyg** - **Webbplatser**)

   * Med den här konsolen kan du [skapa och hantera designkonfigurationer](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM kan användas med både sidor och [Upplevelsefragment](/help/sites-authoring/experience-fragments.md) eftersom dessa fragment ingår i en upplevelse (sida).

>[!NOTE]
>
>Aspekter på MSM-funktioner används i flera andra Adobe Experience Manager-funktioner (AEM) (till exempel Launches, Catalog). I dessa fall hanteras live-kopian av den funktionen.

### Använda termer {#terms-used}

Till att börja med ger följande tabell en översikt över de viktigaste termerna som används i MSM. Dessa beskrivs närmare i de följande avsnitten och sidorna:

<table>
 <tbody>
  <tr>
   <td><strong>Term</strong></td>
   <td><strong>Definition</strong></td>
   <td><strong>Ytterligare information</strong></td>
  </tr>
  <tr>
   <td><strong>Källa</strong></td>
   <td>Originalsidorna.</td>
   <td>Synonymt med skisser och/eller skisser.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>Kopian (av källan), som underhålls av synkroniseringsåtgärder som definieras av rollout-konfigurationerna. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Konfiguration av Live Copy</strong></td>
   <td>Definition av konfigurationsinformationen för en live-kopia.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live-relation</strong><br /> </td>
   <td>Effektiv definition av arvet för en viss resurs, anslutningarna mellan källan och livekopiorna.<br /> </td>
   <td>Ser till att ändringar i källan kan synkroniseras med live-kopian.</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>Synonym med Källa.</td>
   <td>Den kan definieras av en ritningskonfiguration.</td>
  </tr>
  <tr>
   <td><strong>Konfiguration av utkast</strong></td>
   <td>Fördefinierad konfiguration som anger en källsökväg.</td>
   <td>När en ritningssida refereras till i en ritningskonfiguration blir kommandot Rollout tillgängligt.</td>
  </tr>
  <tr>
   <td><strong>Synkronisering</strong></td>
   <td>Den generiska termen för synkronisering av innehåll mellan källan och live-kopiorna (av både <strong>Utrullning</strong> och <strong>Synkronisera</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Utrullning</strong><br /> </td>
   <td>Synkroniserar från källan till live-kopian.<br /> Den kan utlösas av en författare (på en ritningssida) eller av en systemhändelse (som definieras av utrullningskonfigurationen).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Konfiguration av utrullning</strong></td>
   <td>Regler som bestämmer vilka egenskaper som ska synkroniseras, hur och när.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Synkronisera</strong></td>
   <td>En manuell begäran om synkronisering, gjord från live-kopieringssidorna.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Arv</strong></td>
   <td>En live-kopia-sida/komponent ärver innehåll från sin källsida/källkomponent när synkronisering sker.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Gör uppehåll</strong></td>
   <td>Tar tillfälligt bort den aktiva relationen mellan en live-kopia och dess planeringssida.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Koppla loss</strong></td>
   <td>Tar permanent bort den aktiva relationen mellan en live-kopia och dess designsida.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Återställ</strong></td>
   <td><p>Återställ en live-kopia till:</p>
    <ul>
     <li>Ta bort alla annulleringar av arv och<br /> </li>
     <li>Returnera sidan till samma läge som källsidan.</li>
    </ul> <p>Återställ påverkar alla ändringar som du har gjort i sidegenskaper, styckesystem och komponenter.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Grund</strong></td>
   <td>En live-kopia av en enda sida.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Djup</strong></td>
   <td>En live-kopia av en sida, tillsammans med dess underordnade sidor.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se [Översikt över Java™ API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) för objektnamnen.

## Live-kopior {#live-copies}

En MSM-live kopia är en kopia av specifikt webbplatsinnehåll för vilket en direktrelation med den ursprungliga källan upprätthålls:

* Den aktiva kopian ärver innehåll från sin källa.
* Synkroniseringen utför den faktiska överföringen av innehåll när ändringar görs i källan.
* En live-kopia kan betraktas som antingen:

   * Grund: en sida
   * Djup: sidan tillsammans med de underordnade sidorna

* Synkroniseringsregler - rollout configurations - avgör vilka egenskaper som synkroniseras och när synkroniseringen görs.

I föregående exempel `/content/we-retail/language-masters/en` är den globala huvudwebbplatsen på engelska. För att återanvända innehållet på den här webbplatsen skapas MSM-kopior:

* Innehållet nedan `/content/we-retail/language-masters/en` är källan.

* Innehållet nedan `/content/we-retail/language-masters/en` kopieras under `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en`och `/content/we-retail/au/en` noder. Det här är live-kopiorna.

* Författare kan ändra sidor nedan `/content/we-retail/language-masters/en`.
* När MSM aktiveras synkroniseras dessa ändringar med live-kopiorna.

### Live-kopior - komposition {#live-copies-composition}

>[!NOTE]
>
>Diagrammen och beskrivningarna i det här avsnittet representerar ögonblicksbilder av potentiella livekopior. De är inte heltäckande, men ger en översikt som framhäver specifika egenskaper.

När du först skapar en live-kopia återspeglas de valda källsidorna på 1:1-basis i den aktiva kopian. Därefter kan nya resurser (sidor och/eller stycken) också skapas direkt i den aktiva kopian, så det är användbart att känna till dessa variationer och hur de påverkar synkroniseringen. Möjliga kompositioner:

* [Live Copy med icke-Live-Copy-sidor](#live-copy-with-non-live-copy-pages)
* [Kapslade Live-kopior](#nested-live-copies)

Den grundläggande formen av en live-kopia har:

* Live copy-sidor som återspeglar de valda källsidorna på 1:1-basis.
* En konfigurationsdefinition.
* En liverelation definierad för varje resurs:

   * Länka live-kopieresursen med dess plan/källa.
   * Används vid arv och utrullning.

* Ändringar kan [synkroniserad](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) enligt kraven.

![Synkronisera](assets/chlimage_1-367.png)

#### Live Copy med icke-Live-Copy-sidor {#live-copy-with-non-live-copy-pages}

När du skapar en live-kopia i AEM kan du se och navigera genom den aktiva kopieringsgrenen - och använda normal AEM på den aktiva kopieringsgrenen. Det innebär att du (eller en process) kan skapa resurser (sidor, stycken eller både och) inuti den aktiva kopian. Till exempel: `myCanadaOnlyProduct`.

* Sådana resurser har ingen aktiv relation till käll-/ritningssidorna och är inte synkroniserade.
* Scenarier kan inträffa som MSM hanterar som specialfall. När du till exempel (eller en process) skapar en sida med samma position och namn i både källans/ritytans och live-kopians grenar. Information om sådana situationer finns i [MSM-utrullningskonflikter](/help/sites-administering/msm-rollout-conflicts.md) för mer information.

![utrullningskonflikter](assets/chlimage_1-368.png)

#### Kapslade Live-kopior {#nested-live-copies}

När du (eller en process) skapar en [sida i en befintlig live-kopia](#live-copy-with-non-live-copy-pages)kan den nya sidan också skapas som en live-kopia av en annan plan. Det här kallas en kapslad Live-kopia, där beteendet för den andra (inre) aktiva kopian påverkas av den första (yttre) aktiva kopian på följande sätt:

* En djup utrullning som utlöses för live-kopian på den översta nivån kan fortsätta till den kapslade live-kopian (till exempel om utlösaren matchar).
* Eventuella länkar mellan källorna skrivs om i de publicerade kopiorna.

  Till exempel skrivs länkar från den andra till den första utkast om som länkar från den kapslade/andra live-kopian till den första live-kopian.

![Länkar mellan källor](assets/chlimage_1-369.png)

>[!NOTE]
>
>Om du flyttar/byter namn på en sida i en livekopiegren behandlas detta (internt) som en kapslad live-kopia för att AEM ska kunna spåra relationerna.

#### Skiktade Live-kopior {#stacked-live-copies}

En live-kopia kallas för en staplad Live-kopia när den skapas som underordnad till en ytlig live-kopia. Det fungerar på samma sätt som en [Kapslad Live Copy](#nested-live-copies).

### Källa-, utkast- och designkonfigurationer {#source-blueprints-and-blueprint-configurations}

Alla sidor eller sidgrenar kan användas som källa för en live-kopia.

Med MSM kan du dock även definiera en ritningskonfiguration som anger en källsökväg. Fördelarna med att använda en designkonfiguration är att de

* Tillåt författaren att använda **Utrullning** på en plan - att (explicit) överföra ändringar till live-kopior som ärver från den här planen.
* Tillåt författaren att använda **Skapa webbplats**; det gör att användaren enkelt kan välja språk och konfigurera strukturen för live-kopian.
* Definiera en standardkonfiguration för utrullning för live-kopior som har en relation till ritningen.

Källan för en live-kopia kan vara antingen vanliga sidor eller sidor som omfattas av en designkonfiguration - båda är giltiga användningsfall.

Källan utgör utkast för den aktiva kopian. Planen definieras när du antingen:

* [Skapa en designkonfiguration](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

  I konfigurationen definieras (i förväg) de sidor som ska användas för att skapa den aktiva kopian.

* [Skapa en Live-kopia av en sida](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

  De sidor som används för att skapa den aktiva kopian (källsidorna) är de som används som utkast.

  Källsidan kan refereras av en ritningskonfiguration eller inte.

### Utrullning och synkronisering {#rollout-and-synchronize}

En utrullning är den centrala MSM-åtgärden som synkroniserar live-kopior med källan. Du kan utföra rollouts manuellt eller så kan de inträffa automatiskt:

* A [utrullningskonfiguration](#rollout-configurations) kan definieras så att specifika [händelser](/help/sites-administering/msm-sync.md#rollout-triggers) kan orsaka att en utrullning inträffar automatiskt.
* När du skapar en ritningssida kan du använda [Utrullning](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) om du vill göra ändringar i den aktiva kopian.

  **The Rollout** -kommandot är tillgängligt på en ritningssida som en ritningskonfiguration refererar till.

  ![Utrullning](assets/chlimage_1-370.png)

* När du redigerar en live-kopia kan du använda [Synkronisera](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) om du vill dra ändringar från källan till den aktiva kopian.

  The **Synkronisera** -kommandot alltid är tillgängligt på live-kopieringssidan (oavsett om käll-/plantryckssidan omfattas av en ritningskonfiguration).

  ![Synkronisera](assets/chlimage_1-371.png)

### Utrullningskonfigurationer {#rollout-configurations}

En utrullningskonfiguration definierar när och hur en live-kopia synkroniseras med källinnehållet. En utrullningskonfiguration består av en utlösare och en eller flera synkroniseringsåtgärder:

* **Utlösare**

  En utlösare är en händelse som gör att live-åtgärdssynkroniseringen utförs, till exempel aktiveringen av en källsida. MSM definierar de utlösare som du kan använda.

* **Synkroniseringsåtgärder**

  Utfört på den aktiva kopian för att synkronisera den med källan. Exempelåtgärder är att kopiera innehåll, ordna underordnade noder och aktivera live-kopieringssidan. MSM erbjuder flera synkroniseringsåtgärder.

  >[!NOTE]
  >
  >Du kan skapa anpassade åtgärder för instansen med Java™ API.

Utrullningskonfigurationer kan återanvändas så att mer än en live-kopia kan använda samma utrullningskonfiguration. Flera [utrullningskonfigurationer](/help/sites-administering/msm-sync.md#installed-rollout-configurations) ingår i en standardinstallation.

### utrullningskonflikter {#rollout-conflicts}

Utrullningar kan bli komplicerade, särskilt när författare redigerar innehåll i både källan och den aktiva kopian, så det är praktiskt att vara medveten om hur AEM hanterar [konflikter som kan uppstå under utrullning](/help/sites-administering/msm-rollout-conflicts.md).

### Inaktivera och avbryta arv och synkronisering {#suspending-and-cancelling-inheritance-and-synchronization}

Varje sida och komponent i en live-kopia kopplas till sin källsida och komponent via en live-relation. Live-relationen konfigurerar synkroniseringen av live-kopieinnehåll från källan.

Du kan **Gör uppehåll** live-kopiarv för en live-kopieringssida så att du kan ändra sidegenskaper och komponenter. När du gör uppehåll i arv synkroniseras inte längre sidegenskaperna och komponenterna med källan.

När man redigerar en enstaka sida kan man **Avbryt arv** för en komponent. När arvet avbryts pausas direktrelationen och synkronisering sker inte för den komponenten. Att avbryta arv och synkronisering är användbart när underavsnitt av innehållet måste anpassas.

### Koppla loss en Live-kopia {#detaching-a-live-copy}

Du kan också [frigöra en live-kopia](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) från sin plan för att ta bort alla anslutningar.

>[!CAUTION]
>
>Frigör är permanent och icke-reversibel.

Koppla loss permanent tar bort den aktiva relationen mellan en live-kopia och dess planeringssida. Alla MSM-relevanta egenskaper tas bort från den aktiva kopian och de aktiva kopieringssidorna blir en fristående kopia.

>[!NOTE]
>
>Se [Koppla loss en Live-kopia](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) om du vill ha fullständig information, inklusive den relaterade effekten på underordnade och överordnade sidor.

## Standardsteg för att använda MSM {#standard-steps-for-using-msm}

Följande steg beskriver standardproceduren för användning av MSM för att återanvända innehåll och synkronisera ändringar i live-kopior.

1. Utveckla innehållet på källwebbplatsen.
1. Bestäm vilken utrullningskonfiguration som ska användas.

   1. MSM [installerar flera utrullningskonfigurationer](/help/sites-administering/msm-sync.md#installed-rollout-configurations) som kan användas i olika fall.
   1. Om du vill kan du [skapa en utrullningskonfiguration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) vid behov.

1. Bestäm var du måste [ange de utrullningskonfigurationer som ska användas](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) och konfigurera efter behov.
1. Vid behov, [skapa en ritningskonfiguration](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) som identifierar källinnehållet i live-kopian.
1. [Skapa en live-kopia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. Ändra källinnehållet efter behov. Använd den normala process för granskning och godkännande av innehåll som organisationen har etablerat.
1. [Rulla ut](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) ritningen, eller [synkronisera live-kopian](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) med ändringarna.

## Anpassa MSM {#customizing-msm}

MSM tillhandahåller verktyg så att implementeringen kan anpassas till de stora svårigheter som kan uppstå när du delar innehåll:

* **Anpassade utrullningskonfigurationer**
  [Skapa en utrullningskonfiguration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) när de installerade utrullningskonfigurationerna inte uppfyller dina krav. Du kan använda alla tillgängliga utlösare och synkroniseringsåtgärder.

* **Anpassade synkroniseringsåtgärder**
  [Skapa en anpassad synkroniseringsåtgärd](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) när de installerade åtgärderna inte uppfyller dina specifika programkrav. MSM tillhandahåller ett Java™-API för att skapa anpassade synkroniseringsåtgärder.

## Bästa praxis {#best-practices}

The [MSM Best Practices](/help/sites-administering/msm-best-practices.md) sidan innehåller viktig information om implementeringen.
