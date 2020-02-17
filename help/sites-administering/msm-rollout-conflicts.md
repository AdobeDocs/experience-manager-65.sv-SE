---
title: MSM-utrullningskonflikter
seo-title: MSM-utrullningskonflikter
description: Lär dig hur du hanterar driftsättningskonflikter i Multi Site Manager.
seo-description: Lär dig hur du hanterar driftsättningskonflikter i Multi Site Manager.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
translation-type: tm+mt
source-git-commit: 47b69098a45f774501ebb62ee1a14a8d209ad101

---


# MSM-utrullningskonflikter{#msm-rollout-conflicts}

Konflikter kan uppstå om nya sidor med samma sidnamn skapas både i den blå grenen och i en beroende livekopiegren.

Sådana konflikter måste hanteras och lösas vid utrullning.

## Konflikthantering {#conflict-handling}

När det finns sidor som är i konflikt (i grenarna utkast och live copy) kan du med MSM definiera hur (eller till och med om) de ska hanteras.

För att säkerställa att utrullningen inte blockeras kan möjliga definitioner omfatta:

* vilken sida (utkast eller live-kopia) som ska ha prioritet under utrullningen,
* vilka sidor som ska namnändras (och hur),
* hur detta påverkar publicerat innehåll.

   Standardbeteendet för AEM (färdiga) är att publicerat innehåll inte påverkas. Om en sida som skapades manuellt i en livekopiegren har publicerats kommer det innehållet fortfarande att publiceras efter konflikthanteringen och utrullningen.

Förutom standardfunktionerna kan anpassade konflikthanterare läggas till för att implementera olika regler. Detta kan även möjliggöra publiceringsåtgärder som en enskild process.

### Exempelscenario {#example-scenario}

I följande avsnitt använder vi exemplet med en ny sida `b`som har skapats både i grenen för utkast och live-kopia (skapas manuellt) för att illustrera olika metoder för konfliktlösning:

* skiss: `/b`

   En mallsida; med 1 underordnad sida, bp-level-1.

* live copy: `/b`

   En sida som har skapats manuellt i den aktiva kopiegrenen; med 1 underordnad sida, `lc-level-1`.

   * Aktiveras vid publicering som `/b`, tillsammans med den underordnade sidan.

**Före utrullning**

<table>
 <tbody>
  <tr>
   <td><strong>utkast före utrullning</strong></td>
   <td><strong>live copy före utrullning</strong></td>
   <td><strong>publicera före lansering</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (skapat i en skissgren, klar för utrullning)<br /> </td>
   <td><code>b</code> <br /> (skapat manuellt i en förgrening för live-kopia)<br /> </td>
   <td><code>b</code> <br /> (innehåller innehållet på sidan b som skapades manuellt i den aktiva kopiegrenen)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (skapat manuellt i en förgrening för live-kopia)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (innehåller innehållet på sidan<br /> med underordnad nivå-1 som skapades manuellt i den aktiva kopiegrenen)</td>
  </tr>
 </tbody>
</table>

## Utrullningshanteraren och konflikthantering {#rollout-manager-and-conflict-handling}

Med utrullningshanteraren kan du aktivera eller inaktivera konflikthantering.

Detta görs med [OSGi-konfigurationen](/help/sites-deploying/configuring-osgi.md) av WCM-rullningshanteraren **för** Dag:

* **Hantera konflikt med manuellt skapade sidor**:

   ( `rolloutmgr.conflicthandling.enabled`)

   Ange som true om rullningshanteraren ska hantera konflikter från en sida som skapats i live-kopian med ett namn som finns i ritningen.

AEM har [fördefinierat beteende när konflikthantering har inaktiverats](#behavior-when-conflict-handling-deactivated).

## Konflikthanterare {#conflict-handlers}

AEM använder konflikthanterare för att lösa eventuella sidkonflikter som uppstår när innehåll distribueras från en ritning till en live-kopia. Att byta namn på sidor är en (vanlig) metod för att lösa sådana konflikter. Mer än en konflikthanterare kan vara användbar för att tillåta ett urval av olika beteenden.

AEM ger:

* Konflikthanteraren [som](#default-conflict-handler)standard:

   * `ResourceNameRolloutConflictHandler`

* Möjligheten att implementera en [anpassad hanterare](#customized-handlers).
* Den rangordningsmekanism som gör att du kan ange prioriteten för varje enskild hanterare. Tjänsten med högst rankning används.

### Standardhanterare för konflikter {#default-conflict-handler}

Standardkonflikthanteraren:

* Anropas `ResourceNameRolloutConflictHandler`

* Med den här hanteraren får plantryckssidan företräde.
* Tjänstrankningen för hanteraren är låg (&quot;dvs. under standardvärdet för `service.ranking` egenskapen) eftersom antagandet är att anpassade hanterare behöver en högre rankning. Rankningen är dock inte den absolut minsta nivån för att garantera flexibilitet vid behov.

Den här konflikthanteraren ger prioritet åt ritningen. Den aktiva kopieringssidan `/b` flyttas (inom den aktiva kopiegrenen) till `/b_msm_moved`.

* live copy: `/b`

   Flyttas (inom den aktiva kopian) till `/b_msm_moved`. Detta fungerar som en säkerhetskopia och säkerställer att inget innehåll går förlorat.

   * `lc-level-1` flyttas inte.

* skiss: `/b`

   Går ut på live-kopieringssidan `/b`.

   * `bp-level-1` har rullats ut i livecopy.

**Efter utrullning**

<table>
 <tbody>
  <tr>
   <td><strong>skiss efter utrullning</strong></td>
   <td><strong>live copy efter utrullning</strong><br /> </td>
   <td></td>
   <td><strong>live copy efter utrullning</strong><br /> <br /><br /> </td>
   <td><strong>publicera efter utrullning</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (har innehållet på den plana sidan b som lanserades)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (har innehållet på sidan b som skapades manuellt i den aktiva kopiegrenen)</td>
   <td><code>b</code> <br /> (Ingen ändring.) innehåller innehållet på originalsidan b som skapades manuellt i den aktiva kopiegrenen och nu kallas b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (ingen ändring)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (ingen ändring)</td>
  </tr>
 </tbody>
</table>

### Anpassade hanterare {#customized-handlers}

Med anpassade konflikthanterare kan du implementera egna regler. Med servicerangordningsmekanismen kan du även definiera hur de interagerar med andra hanterare.

Anpassade konflikthanterare kan:

* Namnge efter behov.
* utvecklas/konfigureras enligt dina krav, Du kan t.ex. utveckla en hanterare så att den aktiva kopieringssidan ges företräde.
* Kan utformas för att konfigureras med [OSGi-konfigurationen](/help/sites-deploying/configuring-osgi.md). särskilt

   * **Servicerangordning**:

      Definierar ordningen som är relaterad till andra konflikthanterare ( `service.ranking`).

      Standardvärdet är 0.

### Beteende vid inaktiverad konflikthantering {#behavior-when-conflict-handling-deactivated}

Om du manuellt [inaktiverar konflikthantering](#rollout-manager-and-conflict-handling) utför inte AEM någon åtgärd på sidor som är i konflikt (sidor som inte är i konflikt rullas ut som förväntat).

>[!CAUTION]
>
>AEM ger ingen indikation på att konflikter ignoreras eftersom detta beteende måste konfigureras explicit, så det antas att det är det obligatoriska beteendet.

I det här fallet har live-kopian företräde. Den blå sidan `/b` kopieras inte och den aktiva kopieringssidan `/b` lämnas orörd.

* skiss: `/b`

   Kopieras inte alls, men ignoreras.

* live copy: `/b`

   Står detsamma.

<table>
 <caption>
   Efter utrullning
 </caption>
 <tbody>
  <tr>
   <td><strong>skiss efter utrullning</strong></td>
   <td><strong>live copy efter utrullning</strong><br /> <br /><br /> </td>
   <td><strong>publicera efter utrullning</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (Ingen ändring.) har innehållet på sidan b som skapades manuellt i den aktiva kopiegrenen)</td>
   <td><code>b</code> <br /> (Ingen ändring.) innehåller innehållet på sidan b som skapades manuellt i den aktiva kopiegrenen)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (ingen ändring)</td>
   <td><code> /lc-level-1</code> <br /> (ingen ändring)</td>
  </tr>
 </tbody>
</table>

### Servicerangordning {#service-rankings}

Tjänstrankningen [OSGi](https://www.osgi.org/) kan användas för att definiera prioriteten för enskilda konflikthanterare.
