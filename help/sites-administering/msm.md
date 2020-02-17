---
title: '"Återanvända innehåll: Multi Site Manager och Live Copy"'
seo-title: '"Återanvända innehåll: Multi Site Manager och Live Copy"'
description: Lär dig hur du återanvänder innehåll med Live-kopior och Multi Site Manager.
seo-description: Lär dig hur du återanvänder innehåll med Live-kopior och Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Återanvända innehåll: Multi Site Manager och Live Copy{#reusing-content-multi-site-manager-and-live-copy}

Med Multi Site Manager (MSM) kan du använda samma platsinnehåll på flera platser. MSM använder sin Live Copy-funktion för att uppnå detta:

* Med MSM kan man

   * Skapa innehåll en gång och sedan
   * Kopiera innehållet till och återanvänd innehållet i andra områden ([live-kopior](#live-copies)) av samma eller andra webbplatser.

* MSM upprätthåller sedan (live)-relationerna mellan källinnehållet och dess livekopior så att:

   * När du gör ändringar i källinnehållet synkroniseras källkopiorna och livekopiorna (så att ändringarna även tillämpas på livekopiorna).
   * Du kan justera innehållet i live-kopiorna genom att koppla från den aktiva relationen för enskilda undersidor och/eller komponenter. Om du gör det tillämpas inte längre ändringar i källan på den aktiva kopian.

Här och på följande sidor finns de relaterade frågorna:

* [Skapa och synkronisera Live-kopior](/help/sites-administering/msm-livecopy.md)
* [Översiktskonsol för Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Konfigurera Live Copy-synkronisering](/help/sites-administering/msm-sync.md)
* [MSM-utrullningskonflikter](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM Best Practices](/help/sites-administering/msm-best-practices.md)

## Möjliga scenarier {#possible-scenarios}

Det finns många användningsfall för MSM och live-kopior, och vissa scenarier är:

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
   >Se [Översätta innehåll för flerspråkiga platser](/help/sites-administering/translation.md) om du vill utöka ett sådant exempel.

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

   Eller så kan du använda MSM för att skapa versioner av en viss underavdelning, t.ex. en underavdelning till supporten som innehåller information om olika versioner av en viss produkt, där basinformationen är konstant och endast de uppdaterade funktionerna behöver ändras:

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
   >I ett sådant scenario är det alltid frågan om man ska göra en enkel kopia eller använda direktkopior.
   >
   >Balansen är:
   >
   >  * Hur mycket av det centrala innehållet som behöver uppdateras över flera versioner.
   >
   >Mot:
   >
   >  * Hur mycket av de enskilda kopiorna behöver justeras.


## MSM från användargränssnittet {#msm-from-the-ui}

MSM är direkt tillgängligt i användargränssnittet med hjälp av olika alternativ från rätt konsol. Så här gör du en introduktion:

* **Skapa plats** (**platser**)

   * MSM hjälper er att hantera flera webbplatser som delar gemensamt innehåll; webbplatser tillhandahålls till exempel ofta för internationella målgrupper så att det mesta av innehållet är gemensamt i alla länder, med en delmängd av innehållet som är specifikt för varje enskilt land. Med MSM kan du [skapa live-kopior som automatiskt uppdaterar en eller flera webbplatser baserat på källplatsen](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Detta hjälper er också att genomdriva en gemensam basstruktur, använda det gemensamma innehållet på flera webbplatser, bibehålla en gemensam design och känsla och fokusera på att hantera det innehåll som faktiskt skiljer sig åt mellan webbplatserna.
   * Kräver en fördefinierad ritningskonfiguration för att ange källan.
   * Skapar en live-kopia av (fördefinierad) källan.
   * Förser användaren med knappen **Rollout** .

* **Skapa Live-kopia** (**webbplatser**)

   * Med MSM kan ni [skapa en tillfällig (engångs) live kopia av en enskild sida eller underavdelning till en webbplats](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page). till exempel duplicera en underavdelning för att ge information om en ny/uppdaterad version av en produkt.
   * Skapar en ad hoc live-kopia (ingen plantryckskonfiguration krävs).
   * Kan användas för att (omedelbart) skapa en live-kopia av valfri sida/gren.
   * Kräver **synkronisering** (aktiverar inte **utrullningsknappen** ).

* **Visa egenskaper** (**platser**)

   * Om det är lämpligt kan du med det här alternativet [övervaka din livekopia](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) genom att ange information om **Live** Copy eller **Blueprint**.

* **Referenser** (**platser**)

   * På [fliken Referenser](/help/sites-authoring/basic-handling.md#references) finns information om **Live-kopior** samt tillgång till lämpliga åtgärder.

* **Översikt över** Live-kopia (**webbplatser**)

   * Med den här konsolen kan du [visa och hantera din ritning och dess live-kopior](/help/sites-administering/msm-livecopy-overview.md).

* **Utskrifter** (**verktyg** - **webbplatser**)

   * Med den här konsolen kan du [skapa och hantera dina ritningskonfigurationer](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>Aspekter på MSM-funktioner används i flera andra AEM-funktioner (till exempel Launches, Catalog). i dessa fall hanteras den aktiva kopian av den funktionen.

### Villkor {#terms-used}

Som en introduktion ger följande tabell en översikt över de viktigaste termerna som används med medlemsstaterna. dessa kommer att beskrivas mer ingående i de följande avsnitten och sidorna:

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
   <td>Effektiv definition av arvet för en viss resurs. anslutningen mellan källan och live-kopiorna.<br /> </td>
   <td>Ser till att ändringar i källan kan synkroniseras med live-kopian.</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>Synonym med Källa.</td>
   <td>Kan definieras av en ritningskonfiguration.</td>
  </tr>
  <tr>
   <td><strong>Konfiguration av utkast</strong></td>
   <td>Fördefinierad konfiguration som anger en källsökväg.</td>
   <td>När en ritningssida refereras i en ritningskonfiguration blir kommandot Överrullning tillgängligt.</td>
  </tr>
  <tr>
   <td><strong>Synkronisering</strong></td>
   <td>Den generiska termen för synkronisering av innehåll mellan källan och live-kopiorna (av både <strong>utrullning</strong> och <strong>synkronisering</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Utrullning</strong><br /> </td>
   <td>Synkroniserar från källan till livecopy.<br /> Kan utlösas av en författare (på en ritningssida) eller av en systemhändelse (som definieras av utrullningskonfigurationen).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Konfiguration av utrullning</strong></td>
   <td>Regler som bestämmer vilka egenskaper som ska synkroniseras, hur och när.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Synkronisera</strong></td>
   <td>En manuell begäran om synkronisering, gjord från livecopy-sidorna.</td>
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
    </ul> <p>Återställ påverkar alla ändringar som du har gjort i sidegenskaperna, styckesystemet och komponenterna.</p> </td>
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
>Se [Översikt över Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) för objektnamnen.

## Live-kopior {#live-copies}

En MSM-live kopia är en kopia av specifikt webbplatsinnehåll för vilket en direktrelation med den ursprungliga källan upprätthålls:

* Den aktiva kopian ärver innehåll från sin källa.
* Synkroniseringen utför den faktiska överföringen av innehåll när ändringar görs i källan.
* En live-kopia kan betraktas som antingen:

   * Grund: en sida
   * Djup: sidan tillsammans med dess underordnade sidor

* Synkroniseringsregler, som kallas rollout-konfigurationer, avgör vilka egenskaper som synkroniseras och när synkroniseringen sker.

I föregående exempel `/content/we-retail/language-masters/en` är den globala huvudwebbplatsen på engelska. För att återanvända innehållet på den här webbplatsen skapas MSM-kopior:

* Innehållet nedan `/content/we-retail/language-masters/en` är källan.

* Innehållet nedan `/content/we-retail/language-masters/en` kopieras under `/content/we-retail/us/en/`-, `/content/we-retail/gb/en`- `/content/we-retail/ca/en`och `/content/we-retail/au/en` noderna. Det här är live-kopiorna.

* Författare gör ändringar på sidorna nedan `/content/we-retail/language-masters/en`.
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

   * Länka live-kopians resurs med dess plan/källa.
   * Används vid arv och utrullning.

* Ändringarna kan [synkroniseras](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) efter behov.

![chlimage_1-367](assets/chlimage_1-367.png)

#### Live Copy med icke-Live-Copy-sidor {#live-copy-with-non-live-copy-pages}

När du skapar en live-kopia i AEM kan du se och navigera genom livekopiegrenen - och använda de vanliga AEM-funktionerna i livekopiegrenen. Det innebär att du (eller en process) kan skapa nya resurser (sidor och/eller stycken) inuti den aktiva kopiegrenen (t.ex. `myCanadaOnlyProduct`).

* Sådana resurser har ingen aktiv relation till käll-/ritningssidorna och är inte synkroniserade.
* Scenarier kan inträffa som MSM hanterar som specialfall. När du till exempel (eller en process) skapar en sida med samma position och namn i både källans/ritytans och live-kopians grenar. Mer information finns i [MSM-utrullningskonflikter](/help/sites-administering/msm-rollout-conflicts.md) .

![chlimage_1-368](assets/chlimage_1-368.png)

#### Kapslade Live-kopior {#nested-live-copies}

När du (eller en process) skapar en [ny sida i en befintlig live-kopia](#live-copy-with-non-live-copy-pages) kan den nya sidan också ställas in som en live-kopia av en annan plan. Det här kallas en kapslad Live-kopia, där beteendet för den andra (inre) aktiva kopian påverkas av den första (yttre) aktiva kopian på följande sätt:

* En djup utrullning som utlöses för live-kopian på den översta nivån kan fortsätta till den kapslade live-kopian (till exempel om utlösaren matchar).
* Alla länkar mellan källorna skrivs om i de publicerade kopiorna.

   Till exempel skrivs länkar från den andra till den första utkast om som länkar från den kapslade/andra live-kopian till den första live-kopian.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Om du flyttar/byter namn på en sida i en livekopiegren behandlas detta som en kapslad livekopia så att AEM kan spåra relationerna.

#### Skiktade Live-kopior {#stacked-live-copies}

En live-kopia kallas för en staplad Live-kopia när den skapas som underordnad till en ytlig live-kopia. Det fungerar på samma sätt som en [kapslad Live-kopia](#nested-live-copies).

### Källa-, utkast- och designkonfigurationer {#source-blueprints-and-blueprint-configurations}

Alla sidor eller sidgrenar kan användas som källa för en live-kopia.

Med MSM kan du även definiera en ritningskonfiguration som anger en källsökväg. Fördelarna med att använda en designkonfiguration är att de

* Tillåt författaren att använda alternativet **Rollout** på en ritning - för att (explicit) överföra ändringar till live-kopior som ärver från den här ritningen.
* Tillåt författaren att använda **Skapa webbplats**; på så sätt kan användaren enkelt välja språk och konfigurera strukturen för live-kopian.
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

* En [utrullningskonfiguration](#rollout-configurations) kan definieras så att specifika [händelser](/help/sites-administering/msm-sync.md#rollout-triggers) kan leda till att en utrullning sker automatiskt.
* När du skapar en ritningssida kan du använda kommandot [Rollout](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) för att göra ändringar i den aktiva kopian.

   **Kommandot Rollout** är tillgängligt på en ritningssida som en ritningskonfiguration refererar till.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* När du redigerar en live-kopieringssida kan du använda kommandot [Synkronisera](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) för att dra ändringar från källan till live-kopian.

   Kommandot **Synkronisera** är alltid tillgängligt på live-kopieringssidan (oavsett om käll-/plantryckssidan omfattas av en plantryckskonfiguration).

   ![chlimage_1-371](assets/chlimage_1-371.png)

### Konfigurationer för utrullning {#rollout-configurations}

En utrullningskonfiguration definierar när och hur en live-kopia synkroniseras med källinnehållet. En utrullningskonfiguration består av en utlösare och en eller flera synkroniseringsåtgärder:

* **Utlösare**

   En utlösare är en händelse som gör att live-åtgärdssynkroniseringen utförs, till exempel aktiveringen av en källsida. MSM definierar de utlösare som du kan använda.

* **Synkroniseringsåtgärder**

   Arbetas på live-kopian för att synkronisera den med källan. Exempelåtgärder är att kopiera innehåll, ordna underordnade noder och aktivera live-kopieringssidan. MSM tillhandahåller ett antal synkroniseringsåtgärder.

   >[!NOTE]
   >
   >Du kan skapa anpassade åtgärder för instansen med Java API.

Utrullningskonfigurationer kan återanvändas så att fler än en live-kopia kan använda samma utrullningskonfiguration. Flera [utrullningskonfigurationer](/help/sites-administering/msm-sync.md#installed-rollout-configurations) ingår i en standardinstallation.

### utrullningskonflikter {#rollout-conflicts}

Utrullningar kan bli komplicerade, särskilt när författare redigerar innehåll i både källan och den aktiva kopian, så det är praktiskt att känna till hur AEM hanterar eventuella [konflikter som kan uppstå under utrullning](/help/sites-administering/msm-rollout-conflicts.md).

### Inaktivera och avbryta arv och synkronisering {#suspending-and-cancelling-inheritance-and-synchronization}

Varje sida och komponent i en live-kopia kopplas till sin källsida och komponent via en live-relation. Live-relationen konfigurerar synkroniseringen av live-kopieinnehåll från källan.

Du kan **pausa** arvet av live-kopior för en live-kopieringssida så att du kan ändra sidegenskaper och komponenter. När du gör uppehåll i arv synkroniseras inte längre sidegenskaperna och komponenterna med källan.

När du redigerar en enskild sida kan författare **avbryta arv** för en komponent. När arvet avbryts pausas direktrelationen och synkronisering sker inte för den komponenten. Att avbryta arv och synkronisering är användbart när underavsnitt av innehållet behöver anpassas.

### Koppla loss en Live-kopia {#detaching-a-live-copy}

Du kan också [koppla loss en live-kopia](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) från sin plan för att ta bort alla anslutningar.

>[!CAUTION]
>
>Frigör är permanent och icke-reversibel.

Koppla loss permanent tar bort den aktiva relationen mellan en live-kopia och dess planeringssida. Alla MSM-relevanta egenskaper tas bort från den aktiva kopian och de aktiva kopieringssidorna blir en fristående kopia.

>[!NOTE]
>
>Mer information finns i [Koppla loss en Live-kopia](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) . inklusive den inverkan som detta har på underordnade och överordnade sidor.

## Standardsteg för att använda MSM {#standard-steps-for-using-msm}

Följande steg beskriver standardproceduren för användning av MSM för att återanvända innehåll och synkronisera ändringar i live-kopior.

1. Utveckla innehållet på källwebbplatsen.
1. Bestäm vilken utrullningskonfiguration som ska användas.

   1. MSM [installerar flera utrullningskonfigurationer](/help/sites-administering/msm-sync.md#installed-rollout-configurations) som kan uppfylla ett antal användningsfall.
   1. Du kan också [skapa en utrullningskonfiguration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) om det behövs.

1. Bestäm var du behöver [ange vilka rollout-konfigurationer som ska användas](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) och konfigureras efter behov.
1. Om det behövs kan du [skapa en designkonfiguration](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) som identifierar källinnehållet i live-kopian.
1. [Skapa en live-kopia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. Ändra källinnehållet efter behov. Ni bör använda den normala process för granskning och godkännande av innehåll som er organisation har etablerat.
1. [Rulla ut](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) planen eller [synkronisera live-kopian](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) med ändringarna.

## Anpassa MSM {#customizing-msm}

MSM tillhandahåller verktyg så att implementeringen kan anpassas till de stora svårigheter som kan uppstå när du delar innehåll:

* **Anpassade utrullningskonfigurationer**
   [Skapa en utrullningskonfiguration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) när de installerade utrullningskonfigurationerna inte uppfyller dina krav. Du kan använda alla tillgängliga utlösare och synkroniseringsåtgärder.

* **Anpassade synkroniseringsåtgärder**
   [Skapa en anpassad synkroniseringsåtgärd](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) när de installerade åtgärderna inte uppfyller dina specifika programkrav. MSM tillhandahåller ett Java-API för att skapa anpassade synkroniseringsåtgärder.

## Bästa praxis {#best-practices}

Sidan [MSM Best Practices](/help/sites-administering/msm-best-practices.md) innehåller viktig information om implementeringen.
