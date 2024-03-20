---
title: Prestandaträd
description: Lär dig mer om hur du felsöker prestandaproblem i AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: f2f968b8-b21c-487d-bc0d-ed60903bc4bf
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---

# Prestandaträd{#performance-tree}

## Omfång {#scope}

Följande diagram ger vägledning om hur du felsöker prestandaproblem. Den är uppdelad i fem avsnitt för enklare läsning.

Varje steg i diagrammet är länkat till en dokumentationsresurs eller en rekommendation.

## Krav och antaganden {#prerequisites-and-assumptions}

Antagandet är att ett prestandaproblem observeras på en viss sida (antingen en AEM konsol eller en webbsida) och kan återges på ett enhetligt sätt. Att kunna testa eller övervaka prestanda är en förutsättning innan undersökningen inleds.

Analysen börjar med steg 0. Målet är att avgöra vilken enhet (Dispatcher, extern värd eller AEM) som ansvarar för prestandaproblemet och sedan avgöra vilket område (server eller nätverk) som ska undersökas.

### Avsnitt 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### Avsnitt 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### Avsnitt 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### Avsnitt 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Avsnitt 5 {#section-4}

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
   <td><p>Du kan använda standardanalys av HTTP-begäran i webbläsaren för att analysera förfrågningsflödet. Mer information om hur du gör den här analysen i Chrome finns i:<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developer.chrome.com/docs/devtools/</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 2</strong></td>
   <td>Kommer förfrågningar från externa värdar?</td>
   <td>Du kan använda standardanalys av HTTP-begäran i webbläsaren för att analysera förfrågningsflödet. Se länkarna ovan om hur du gör analysen i Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 3</strong></td>
   <td>Kan förfrågningarna cachelagras?</td>
   <td>Mer information om tillgängliga förfrågningar och allmänna råd om prestandaoptimering för Dispatcher finns i <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Prestandaoptimering för Dispatcher</a>.</td>
  </tr>
  <tr>
   <td><strong>Steg 4</strong></td>
   <td>Kommer förfrågningar från Dispatcher?</td>
   <td><p>Om du vill se om begäranden cachelagras på rätt sätt kontrollerar du <a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#debugging">Felsökningsdokumentation för Dispatcher</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 5</strong></td>
   <td>Försöker Dispatcher autentisera varje begäran via AEM?</td>
   <td>Kontrollera om Dispatcher skickar <code>HEAD</code> begäranden om AEM för autentisering innan den cachelagrade resursen levereras. Leta efter <code>HEAD</code> begäranden i AEM <code>access.log</code>. Mer information finns i <a href="/help/sites-deploying/configure-logging.md">Loggning</a>.<br /> </td>
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
   <td><br /> <p>Använd <a href="/help/sites-developing/tough-day.md">Tålig dag</a> för att återskapa"verkliga" förhållanden från produktionsinstanserna. Om det här scenariot inte är realistiskt för ditt utvecklingsområde måste du testa produktionsinstansen (eller en identisk mellanlagringsmodell) i ett annat nätverkskontext.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 9</strong></td>
   <td>Är serverns geografiska plats långt från användarna?</td>
   <td>Flytta servern närmare användarna.</td>
  </tr>
  <tr>
   <td><strong>Steg 10 och 29</strong></td>
   <td>Undersök nätverkslager</td>
   <td><p>Undersök nätverkslagret för problem med mättnad och fördröjning.</p> <p>För författarnivån rekommenderas att fördröjningen inte överstiger 100 millisekunder.</p> <p>Mer information om tips för prestandaoptimering finns i <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">den här sidan</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Steg 11</strong></td>
   <td>Flytta servern närmare eller lägg till en per region</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 12</strong></td>
   <td>Felsök AEM server</td>
   <td>Mer information finns i följande delsteg i diagrammet.</td>
  </tr>
  <tr>
   <td><strong>Steg 13</strong></td>
   <td>Kontrollera maskinvarukraven</td>
   <td>Läs dokumentationen på <a href="/help/managing/hardware-sizing-guidelines.md">Riktlinjer för maskinvarans storlek</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 14</strong></td>
   <td>Kontrollera om det finns vanliga orsaker till prestandaproblem</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 15</strong></td>
   <td>Hitta långsamma förfrågningar</td>
   <td><p>Du kan söka efter långsamma begäranden genom att analysera <code>request.log</code> eller genom att använda <code>rlog.jar</code>.</p> <p>Mer information om hur du använder rlog.jar finns på den här sidan.</p> <p>Se <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Söka efter förfrågningar med lång varaktighet med rlog.jar</a>.<br /> </p> <p> </p> </td>
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
   <td>Se <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Analyserar specifika scenarier</a> i avsnittet Prestandaoptimering.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 19</strong></td>
   <td>100 % CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html</a></td>
  </tr>
  <tr>
   <td><strong>Steg 20</strong></td>
   <td>Slut på minne</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Slut på minne</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">Mitt program orsakar fel av typen slut på minne</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html">Analysera minnesproblem.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 21</strong></td>
   <td>Skiva-I/O</td>
   <td><p>Se <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">Skiva-I/O</a> i övervakningsdokumentationen.</p> </td>
  </tr>
  <tr>
   <td><strong>Steg 22 och 22.1</strong></td>
   <td>Cachenivåer</td>
   <td>Se <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Beräkna Dispatcher-cachens förhållande</a>.<br /> <br /> </td>
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
     <li><a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">Tips för prestandajustering</a></li>
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
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Metodtips för hantering av flera webbplatser</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 27</strong></td>
   <td>Resursjustering</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Resurssynkroniseringstjänst</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Flera DAM-instanser</a></li>
     <li>Tipsartikel för prestandajustering <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">här</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 28</strong></td>
   <td>Oavslutade sessioner</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Söker efter oavslutade JCR-sessioner</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Steg 30</strong></td>
   <td>Flytta Dispatcher närmare (lägg till en per region?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Steg 31</strong></td>
   <td>Använd CDN framför Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Använda Dispatcher med ett CDN</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 32</strong></td>
   <td>Avlasta AEM server med sessionshantering på Dispatcher-nivå</td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">Aktivera säkra sessioner</a></p> </td>
  </tr>
  <tr>
   <td><strong>Steg 33</strong></td>
   <td>Gör förfrågningar tillgängliga</td>
   <td>
    <ol>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html">Allmän Dispatcher-konfiguration</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">Konfigurera Dispatcher Cache</a></li>
    </ol> <p>Så här förbättrar du cacheförhållandet: gör förfrågningar cachelagrade (Bästa tillvägagångssätt för Dispatcher)</p> <p>Titta också på inställningarna nedan för att optimera dina cachelagringskonfigurationer<br /> </p>
    <ol>
     <li>Ange en regel utan cache för HTTP-begäran som inte är GET</li>
     <li>Konfigurera frågesträngar som inte ska kunna cachelagras</li>
     <li>Cachelagra inte URL:er som saknar tillägg</li>
     <li>Cacheautentiseringsrubriker (möjligt sedan Dispatcher version 4.1.10)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Steg 34</strong></td>
   <td>Uppgradera Dispatcher-version</td>
   <td><p>Du kan hämta den senaste Dispatcher-versionen på den här platsen:</p> <p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html">Följ länk</a></p> </td>
  </tr>
  <tr>
   <td><strong>Steg 35</strong></td>
   <td>Konfigurera Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html">Konfigurera Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 36</strong></td>
   <td>Kontrollera cacheminnets ogiltigförklaring</td>
   <td><br />
    <ul>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">Cacheinvalidering för författarnivån.</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">Cacheinvalidering för publiceringsnivån.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Steg 37 och 38</strong></td>
   <td>Lazyladdning</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">Se Gem Session om AEM webbprestanda.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 39</strong></td>
   <td>Använd pre-connect för att minska anslutningens belastning</td>
   <td>Se Gem-sessionen ovan. Ytterligare föranslutningsdokumentation på W3c:<a href="https://html.spec.whatwg.org/#linkTypes"> https://html.spec.whatwg.org/#linkTypes</a></td>
  </tr>
  <tr>
   <td><strong>Steg 40 och 41</strong><br /> </td>
   <td>Latens och svarstid för externa värdar</td>
   <td>Undersök latens och svarstid för externa värdar.</td>
  </tr>
  <tr>
   <td><strong>Steg 45<br /> och 47</strong><br /> </td>
   <td>Använda HTTP/2</td>
   <td>Se Gem Session för steg 37, 38 och 39. Du kan även checka ut <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">this</a> foruminlägg om HTTP/2-stöd.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 49</strong></td>
   <td>Minska nyttolastens storlek</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Aktivera Gzip</a> och <a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">minska bildstorleken</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Steg 42 och 43</strong></td>
   <td>Håll dig uppdaterad</td>
   <td><p>Är <code>Keep-Alive</code> finns det en rubrik i de olika begärandena att återanvända anslutningar? I annat fall innebär det att varje begäran leder till en annan anslutningsanläggning, vilket medför onödiga kostnader. (Standardanalys av HTTP-begäran i webbläsaren)</p> <p>Du kan kontrollera <a href="/help/sites-administering/proxy-jar.md">Proxyserververktyget</a> om du vill kontrollera om det finns anslutningar som inte fungerar.<br /> </p> </td>
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
     <li>Sammanfoga resurser (bilder, CSS-sprites, JSON)<br /> </li>
     <li>Inbäddning av klienter:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Skapar klientbiblioteksmappar</a> - se rubriken Använda inbäddning för att minimera förfrågningar</li>
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
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>
