---
title: Uppdatera definitioner för frisläppningsfordon
seo-title: Uppdatera definitioner för frisläppningsfordon
description: I den här artikeln beskrivs de olika typerna av AEM, inklusive fullständiga versioner, funktionspaket och servicepaket.
seo-description: I den här artikeln beskrivs de olika typerna av AEM, inklusive fullständiga versioner, funktionspaket och servicepaket.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Definitioner av AEM Uppdatera utgivningsfordon{#update-release-vehicle-definitions}

Det här dokumentet innehåller information om de olika typerna av Adobe Experience Manager (AEM)-releaser, inklusive fullständiga releaser, funktionspaket och servicepaket som Adobe levererar till sina kunder.

>[!NOTE]
>
>Information om releaseschema för AEM finns i [AEM uppdateringsreleaser](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

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
     <li>Finns på licenswebbplatsen och Managed Services Licensing Website</li>
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

## Kumulativt korrigeringspaket  {#cumulative-fix-pack-aem}

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
     <li>Levereras som paket av AEM kundtjänst</li>
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
     <li>Funktionspaket är tilläggsfunktioner och levereras via Service Pack. Om en AEM har släppt sitt senaste Service Pack kommer Adobe inte att leverera något funktionspaket till den i framtiden.</li>
     <li>FP:er innehåller produktförbättringar, som planeras för en senare produktrelease, men levereras tidigt baserat på beslut av Adobe Product Management.</li>
     <li>Funktioner sammanfogas alltid med nästa större release och backporteras sedan till den AEM versionen som kunden behöver</li>
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
     <li>Finns på paketresurs. Kunderna godkänner Adobe och villkor via paketresursen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Testnivå</strong></td>
   <td>Funktionspaket för allmän tillgänglighet är QA-validerade</td>
  </tr>
 </tbody>
</table>

* [1]: OAK-korrigeringar levereras inte som enskilda snabbkorrigeringar. De ingår dock i den följande snabbkorrigeringen Cumulative Oak. Om det behövs kan en diagnostisk version av den senaste offertförfrågan göras tillgänglig. Förutsättningen är att kunden har den senaste COFP som körs. Diagnostiska byggen ger bara samma kvalitetssäkring som en snabbkorrigering. Därför ger de inte samma kvalitetssäkring som ett kumulativt korrigeringspaket, Service Pack eller produktrelease. Den slutliga lösningen levereras med nästa gemensamma fiskeripolitik.

