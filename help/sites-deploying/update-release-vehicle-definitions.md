---
title: Uppdatera definitioner för frisläppningsfordon
seo-title: Uppdatera definitioner för frisläppningsfordon
description: I den här artikeln beskrivs de olika typerna av AEM-versioner, inklusive fullständiga versioner, funktionspaket och servicepaket.
seo-description: I den här artikeln beskrivs de olika typerna av AEM-versioner, inklusive fullständiga versioner, funktionspaket och servicepaket.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# AEM Update Release Vehicle Definitions{#update-release-vehicle-definitions}

Det här dokumentet innehåller information om de olika typerna av Adobe Experience Manager-versioner (AEM), inklusive fullständiga releaser, funktionspaket och servicepaket som Adobe levererar till sina kunder.

>[!Note]
>
>Information om releaseschema för AEM-uppdateringsreleaser finns i [AEM-uppdateringsöversikt](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## Fullversion {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td>
    <ul>
     <li>Schemalagd release</li>
     <li>Stöder uppgraderingssökvägar för specifika versioner, som definieras i versionsinformationen</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td>
    <ul>
     <li>Versionsnummer för större releaser ökar baserat på formeln X+1.Y.Z. </li>
     <li>Versionsnummer för mindre releaser ökar baserat på formeln X.Y+1.Z</li>
    </ul> <p>Där X är det primära versionsnumret, är Y det sekundära versionsnumret och Z korrigeringsnumret.</p> </td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td>
    <ul>
     <li>Nya funktioner</li>
     <li>Förbättringar</li>
     <li>Felkorrigeringar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td>
    <ul>
     <li>Versionsinformation finns på dokumentationsportalen</li>
     <li>Dokumentation om funktioner, förbättringar och felkorrigeringar finns på dokumentationsportalen</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Årsvis</td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Levereras som ett fristående installationsprogram</li>
     <li>Finns på licenswebbplatsen och webbplatsen för Managed Services Licensing</li>
     <li>Kan kräva migrering av innehållsdatabas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>Fullt validerad av kvalitetskontrollen</td>
  </tr>
 </tbody>
</table>

## Service Pack {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td>
    <ul>
     <li>Schemalagd release</li>
     <li>Det går inte att återställa</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td>
    <ul>
     <li>Patch release number is a single digit number</li>
     <li>Efter installationen ökar korrigeringssiffran för det installerade versionsnumret baserat på formeln X.Y.Z.SPx</li>
     <li>Där X är det primära versionsnumret, är Y det sekundära versionsnumret och Z korrigeringsnumret. x är service pack-numret.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td>
    <ul>
     <li>Nya funktioner</li>
     <li>Förbättringar</li>
     <li>Felkorrigeringar</li>
     <li>Funktionspaket för gemensamma intressen (om sådana finns)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td>
    <ul>
     <li>Versionsinformation finns på dokumentationsportalen</li>
     <li>Dokumentation om funktioner, förbättringar, felkorrigeringar på dokumentationsportalen</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Kvartalsvis</td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Levereras som ett paket</li>
     <li>Finns på paketresurs</li>
     <li>Kräver befintlig funktionell installation</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>
    <ul>
     <li>Alla korrigeringar QA har validerats</li>
     <li>Total paketsäkerhet med automatiserade körningar</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Kumulativt korrigeringspaket {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td>
    <ul>
     <li>Enstaka leveransmodell för frisläppningsfixar</li>
     <li>Aggregator-innehållspaket som innehåller innehållspaket för enskilda komponenter</li>
     <li>Bestruket finpapper är en överrullning av snabbkorrigeringar och inga förbättringar ingår i den.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>Där X är det primära versionsnumret, är Y det sekundära versionsnumret och Z korrigeringsnumret. x är det kumulativa Service Pack-numret.</p> </td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td><p>CFP är ett kumulativt korrigeringspaket som innehåller korrigeringar av alla komponenter under angivna datum. Om en kund till exempel tillämpar CFP3, blir CFP3 = CFP1 + CFP2.</p> </td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td>Versionsinformation finns på dokumentationsportalen</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Kvateralt</td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Levereras som ett paket</li>
     <li>Finns på paketresurs</li>
     <li>Beroende på det senaste Service Pack-versionen</li>
     <li>Den gemensamma fiskeripolitiken är självständig. Kunderna behöver inte bekymra sig om att hitta/lösa beroenden. CFP bör installeras på senaste lanserade Service Pack.</li>
     <li>CFP kan installeras som ett enda paket, vilket förbättrar kundupplevelsen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>QA validerat på integreringsnivå och regressionstestning</td>
  </tr>
 </tbody>
</table>

## Eak Cumulative Fix Pack {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td>
    <ul>
     <li>Liknar en vanlig bestruket finpapper, men innehåller endast ekrelaterade korrigeringar</li>
     <li>COFP är självberoende (inga beroenden). Kunderna behöver inte bekymra sig om att hitta/lösa beroenden. [1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td>oak &lt;version&gt;</td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td>COFP är ett kumulativt korrigeringspaket som innehåller korrigeringar av alla Oak-komponenter för en viss 1.x-version. Om kunden t.ex. använder COHF 1.x.3, så COHF 1.x.3. = COHF 1.x.1 + COHF 1.x.2.</td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td><p>Vid behov</p> </td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Installationsprocessen för COFP har förenklats för att förbättra kundupplevelsen. (Kunderna kan bara installera ett enda paket för alla komponenter).</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td><p>Kvalitetsvaliderade</p> </td>
  </tr>
 </tbody>
</table>

## Snabbkorrigering {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td><p>Paket som innehåller en eller flera filer som skapats för att åtgärda en produktdefekt som avsevärt försämrar viktiga tjänster eller som i hög grad påverkar verksamheten. </p> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td>cq-&lt;Release Version&gt;-hotfix-&lt;hotfix ID&gt;-&lt;hotfix-version&gt;</td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td>Innehåller korrigeringar för ett specifikt problem</td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td>Versionsinformation om de offentliga snabbkorrigeringarna är endast tillgängliga baserat på kundens begäran via AEM Support Portal.</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Vid behov</td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Levereras som ett paket</li>
     <li>Finns på paketresurs</li>
     <li>Beroende på det senaste Service Pack-versionen</li>
     <li>De flesta snabbkorrigeringar är fristående, om inte annat anges. Kan installeras i valfri ordning. Kan verifieras via fliken Paketdelningsinformation i elementet Beroenden.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>
    <ul>
     <li>Validerad av Kundtjänst</li>
     <li>AEM-snabbkorrigeringar har inte samma kvalitetssäkring som servicepaket eller produktreleaser. Därför bör de först valideras i en testmiljö som en del av kvalitetsdistributionsprocesserna.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Övertäckning {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td>överlägg-&lt;biljett-ID&gt;</td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td>Felkorrigering för en JS- eller JSP-fil</td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td>Inget</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Vid behov</td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Levereras som paket av AEM Customer Care</li>
     <li>Ingår inte nödvändigtvis i Service Pack eller fullständiga versioner</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>Validerad av Kundtjänst</td>
  </tr>
 </tbody>
</table>

## Funktionspaket {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definition</strong></td>
   <td>
    <ul>
     <li>Funktionspaket är tilläggsfunktioner och levereras via Service Pack. Om en AEM-version har släppt sitt senaste Service Pack kommer Adobe inte att leverera något funktionspaket till den i framtiden.</li>
     <li>FP:er innehåller produktförbättringar, som planeras för en senare produktrelease, men levereras i ett tidigt skede baserat på beslut av Adobes produktledning.</li>
     <li>Funktionerna sammanfogas alltid med nästa större release och backporteras sedan till den AEM-version som kunden behöver</li>
     <li>Funktionspaket för gemensamt intresse och GA sammanfogas i nästa servicepaket</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Namngivning</strong></td>
   <td>cq-&lt;Release Version&gt;-featurepack-&lt;featurepack ID&gt;-&lt;featurepack version&gt;</td>
  </tr>
  <tr>
   <td><strong>Inkluderingar</strong></td>
   <td>
    <ul>
     <li>Nya funktioner</li>
     <li>Förbättringar</li>
     <li>Felkorrigeringar (stegvisa produktuppdateringar)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dokumentation</strong></td>
   <td>Dokumentation finns på helpx.adobe.com.</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Varierar med produktområdet</td>
  </tr>
  <tr>
   <td><strong>Tillgänglighet och installation</strong></td>
   <td>
    <ul>
     <li>Levereras via servicepaket</li>
     <li>Finns på paketresurs. Kunderna godkänner Adobes villkor via paketresursen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>Funktionspaket för allmän tillgänglighet är QA-validerade</td>
  </tr>
 </tbody>
</table>

* [1]: OAK-korrigeringar levereras inte som enskilda snabbkorrigeringar. De ingår dock i den följande snabbkorrigeringen Cumulative Oak. Om det behövs kan en diagnostisk version av den senaste offertförfrågan göras tillgänglig. Förutsättningen är att kunden har den senaste COFP som körs. Diagnostiska byggen ger bara samma kvalitetssäkring som en snabbkorrigering. Därför ger de inte samma kvalitetssäkring som ett kumulativt korrigeringspaket, Service Pack eller produktrelease. Den slutliga lösningen levereras med nästa gemensamma fiskeripolitik.

