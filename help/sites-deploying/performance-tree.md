---
title: Prestandaträd
seo-title: Prestandaträd
description: Lär dig mer om de steg som behöver vidtas för att felsöka prestandaproblem i AEM.
seo-description: Lär dig mer om de steg som behöver vidtas för att felsöka prestandaproblem i AEM.
uuid: ab0624f7-6b39-4255-89e0-54c74b54cd98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 5febbb1e-795c-49cd-a8f4-c6b4b540673d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prestandaträd{#performance-tree}

## Scope {#scope}

Bilden nedan är avsedd att ge vägledning om vilka åtgärder som behöver vidtas för att felsöka prestandaproblem. Den delas upp i fem avsnitt för enklare läsning.

Varje steg i diagrammet är länkat till en dokumentationsresurs eller en rekommendation.

## Förutsättningar och antaganden {#prerequisites-and-assumptions}

Antagandet är att ett prestandaproblem observeras på en viss sida (antingen en AEM-konsol eller en webbsida) och kan återges på ett enhetligt sätt. Att kunna testa eller övervaka prestanda är en förutsättning innan undersökningen inleds.

Analysen börjar med steg 0. Målet är att avgöra vilken enhet (avsändare, extern värd eller AEM) som ansvarar för prestandaproblemet och sedan avgöra vilket område (server eller nätverk) som ska undersökas.

### Section 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### Section 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### Section 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### Section 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Section 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## Referenslänkar {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>Steg</strong></td>
   <td><strong>Titel</strong></td>
   <td><strong>Resurser</strong></td>
  </tr>
  <tr>
   <td><strong>Steg 0</strong></td>
   <td>Analysera flödet för förfrågningar</td>
   <td><p>Du kan använda standardanalys av HTTP-begäran i webbläsaren för att analysera förfrågningsflödet. Mer information om hur du gör detta i Chrome finns i:<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading</a><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing"><br /> https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 2</strong></td>
   <td>Kommer förfrågningar från externa värdar?</td>
   <td>Du kan använda standardanalys av HTTP-begäran i webbläsaren för att analysera förfrågningsflödet. Se länkarna ovan om hur du gör detta i Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 3</strong></td>
   <td>Kan förfrågningarna cachelagras?</td>
   <td>Mer information om tillgängliga begäranden och allmänna råd om prestandaoptimering för Dispatcher finns i <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Prestandaoptimering</a>för Dispatcher.</td>
  </tr>
  <tr>
   <td><strong>Steg 4</strong></td>
   <td>Kommer förfrågningar från Dispatcher?</td>
   <td><p>Kontrollera felsökningsdokumentationen <a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#debugging">för</a> Dispatcher för att se om begäranden har cachelagrats på rätt sätt.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 5</strong></td>
   <td>Försöker Dispatcher autentisera varje begäran via AEM?</td>
   <td>Kontrollera om avsändaren skickar <code>HEAD</code> begäranden till AEM för autentisering innan den cachelagrade resursen levereras. Du kan göra detta genom att söka efter <code>HEAD</code> förfrågningar i AEM <code>access.log</code>. For more information, see <a href="/help/sites-deploying/configure-logging.md">Logging</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 6</strong></td>
   <td>Är den geografiska platsen för Dispatcher långt från användarna?</td>
   <td>Flytta Dispatcher närmare användarna.</td>
  </tr>
  <tr>
   <td><strong>Steg 7</strong></td>
   <td>Går nätverkslagret för Dispatcher bra?</td>
   <td><br /> Undersök nätverkslagret för problem med mättnad och fördröjning.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 8</strong></td>
   <td>Kan långsamheten reproduceras med en lokal instans?</td>
   <td><br /> <p>Använd <a href="/help/sites-developing/tough-day.md">Tough Day</a> för att replikera verkliga förhållanden från produktionsinstanserna. Om detta inte är realistiskt för utvecklingens hastighet måste du testa produktionsinstansen (eller en identisk mellanlagringsmodell) i en annan nätverkskontext.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 9</strong></td>
   <td>Är serverns geografiska plats långt från användarna?</td>
   <td>Flytta servern närmare användarna.</td>
  </tr>
  <tr>
   <td><strong>Steg 10 och 29</strong></td>
   <td>Undersök nätverkslager</td>
   <td><p>Undersök nätverkslagret för problem med mättnad och fördröjning.</p> <p>För författarnivån rekommenderas att fördröjningen inte överstiger 100 millisekunder.</p> <p>Mer information om tips för prestandaoptimering finns på <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">den här sidan</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Steg 11</strong></td>
   <td>Flytta servern närmare eller lägg till en per region</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 12</strong></td>
   <td>Felsök AEM-server</td>
   <td>Mer information finns i följande delsteg i diagrammet.</td>
  </tr>
  <tr>
   <td><strong>Steg 13</strong></td>
   <td>Kontrollera maskinvarukraven</td>
   <td>Läs dokumentationen om riktlinjer för <a href="/help/managing/hardware-sizing-guidelines.md">maskinvarans storlek</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 14</strong></td>
   <td>Kontrollera om det finns vanliga orsaker till prestandaproblem</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 15</strong></td>
   <td>Hitta långsamma förfrågningar</td>
   <td><p>Du kan kontrollera om det finns långsamma förfrågningar genom att analysera dem <code>request.log</code> eller genom att använda <code>rlog.jar</code>.</p> <p>Mer information om hur du använder rlog.jar finns på den här sidan.</p> <p>Se <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Använda rlog.jar för att söka efter begäranden med lång varaktighet</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 16</strong></td>
   <td>Profilserver</td>
   <td><p>Mer information om profileringsverktyg som du kan använda med AEM finns i <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">Verktyg för övervakning och analys av prestanda</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 17</strong></td>
   <td>Hitta långsamma metoder i profilering</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 18</strong></td>
   <td>Vanliga scenarier för profilering</td>
   <td>Se <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Analysera specifika scenarier</a> i avsnittet Prestandaoptimering.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 19</strong></td>
   <td>100 % CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://helpx.adobe.com/experience-manager/6-3/sites-deploying/monitoring-and-maintaining.html#MonitoringPerformance</a></td>
  </tr>
  <tr>
   <td><strong>Steg 20</strong></td>
   <td>Slut på minne</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Slut på minne</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">Mitt program orsakar fel av typen slut på minne</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html">Analysera minnesproblem i hjälpen.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 21</strong></td>
   <td>Skiva-I/O</td>
   <td><p>Se avsnittet <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">Skiva-I/O</a> i dokumentationen Övervakning och underhåll.</p> </td>
  </tr>
  <tr>
   <td><strong>Steg 22 och 22.1</strong></td>
   <td>Cachenivåer</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio"> Se </a>Beräkna Dispatcher-cachens förhållande<br />. <br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 23</strong></td>
   <td>Långsamma frågor</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Metodtips för frågor och indexering</a></td>
  </tr>
  <tr>
   <td><strong>Steg 24</strong></td>
   <td>Databasjustering</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">Tips för prestandajustering</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">Konfigurera för prestanda</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">Justering av databasprestanda</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Steg 25</strong></td>
   <td>Arbetsflöden som körs</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">Samtidig bearbetning av arbetsflöden</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">Konfigurera kön för ett specifikt arbetsflöde</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">Vanlig tömning av arbetsflödesinstanser</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">Övergående arbetsflöden</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 26</strong></td>
   <td>MSM-infrastruktur</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Bästa praxis för hantering av flera webbplatser</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 27</strong></td>
   <td>Resursjustering</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Resurssynkroniseringstjänst</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Flera DAM-instanser</a></li>
     <li>Artiklar om prestandajustering <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">här</a> och <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">här</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 28</strong></td>
   <td>Oavslutade sessioner</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Söker efter oavslutade JCR-sessioner</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 30</strong></td>
   <td>Flytta dispatchern närmare (lägg till en per region?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 31</strong></td>
   <td>Använd CDN framför dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Använda Dispatcher med ett CDN</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 32</strong></td>
   <td>Använd sessionshantering på dispatchernivå för att avlasta AEM-server</td>
   <td><p><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">Aktivera säkra sessioner</a></p> </td>
  </tr>
  <tr>
   <td><strong>Steg 33</strong></td>
   <td>Gör förfrågningar tillgängliga</td>
   <td>
    <ol>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html">Allmän Dispatcher-konfiguration</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">Konfigurera Dispatcher Cache</a></li>
    </ol> <p>Hur man förbättrar cachekvoten, gör förfrågningar cachelagrade (god praxis vid utsändning)</p> <p>Ta även hänsyn till inställningarna nedan för att optimera dina cachelagringskonfigurationer<br /> </p>
    <ol>
     <li>Ange en regel utan cache för HTTP-begäran som inte är GET</li>
     <li>Konfigurera frågesträngar som inte ska kunna cachelagras</li>
     <li>Cachelagra inte URL:er som saknar tillägg</li>
     <li>Cacheautentiseringsrubriker (möjligt sedan Dispatcher version 4.1.10)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 34</strong></td>
   <td>Uppgradera dispatcherversion</td>
   <td><p>Du kan hämta den senaste Dispatcher-versionen på den här platsen:</p> <p><a href="https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html">Följ länk</a></p> </td>
  </tr>
  <tr>
   <td><strong>Steg 35</strong></td>
   <td>Konfigurera dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html">Konfigurera Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 36</strong></td>
   <td>Kontrollera cacheminnets ogiltigförklaring</td>
   <td><br />
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">Cacheinvalidering för författarnivån.</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">Cacheinvalidering för publiceringsnivån.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Steg 37 och 38</strong></td>
   <td>Lazyladdning</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">Se Gem-sessionen om AEM Web Performance.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 39</strong></td>
   <td>Använd pre-connect för att minska anslutningens belastning</td>
   <td>Se Gem Session som anges ovan. <a href="https://www.w3.org/TR/resource-hints/#dfn-preconnect"> Dessutom kan du föransluta ytterligare dokumentation på W3c: https://www.w3.org/TR/resource-hints/#dfn-preconnect</a></td>
  </tr>
  <tr>
   <td><strong>Steg 40 och 41</strong><br /> </td>
   <td>Latens och svarstid för externa värdar</td>
   <td>Undersök latens och svarstid för externa värdar.</td>
  </tr>
  <tr>
   <td><strong>Steg 45<br /> och 47</strong><br /> </td>
   <td>Använda HTTP/2</td>
   <td>Se Gem Session för steg 37, 38 och 39. Se även <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">det här</a> foruminlägget om stöd för HTTP/2.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 49</strong></td>
   <td>Minska nyttolastens storlek</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Aktivera Gzip</a> och <a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">minska bildstorleken</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 42 och 43</strong></td>
   <td>Behåll</td>
   <td><p>Finns rubriken <code>Keep-Alive</code> i de olika begärandena att återanvända anslutningar? I annat fall skulle det innebära att varje begäran leder till en annan anslutningsanläggning, vilket medför onödiga kostnader. (Standardanalys av HTTP-begäran i webbläsaren)</p> <p>Du kan kontrollera <a href="/help/sites-administering/proxy-jar.md">proxyserververktyget</a> för att se om det finns några anslutningar som inte fungerar.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 44</strong></td>
   <td>Hur många förfrågningar görs?</td>
   <td>Utför standardanalys av HTTP-begäran i webbläsaren.</td>
  </tr>
  <tr>
   <td><strong>Steg 46</strong></td>
   <td>Minska antalet förfrågningar</td>
   <td>
    <ol>
     <li>Sammanfoga resurser (bilder, CSS-sprites, JSON osv.)<br /> </li>
     <li>Inbäddning av klienter:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Skapa klientbiblioteksmappar</a> - se rubriken Använda inbäddning för att minimera begäranden</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 48</strong></td>
   <td>Vilken är nyttolastens storlek?</td>
   <td>Standardanalys av HTTP-begäran i webbläsaren</td>
  </tr>
  <tr>
   <td><strong>Steg 50 och 51</strong></td>
   <td>JS-kodblockering</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">https://docs.adobe.com/ddc/en/gems/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>

