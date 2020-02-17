---
title: Omstrukturering av anläggningstillgångar i AEM 6.5
seo-title: Omstrukturering av anläggningstillgångar i AEM 6.5
description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.5 for Sites.
seo-description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.5 for Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Omstrukturering av anläggningstillgångar i AEM 6.5 {#sites-repository-restructuring-in-aem}

Som beskrivs på den överordnade [databasomstruktureringen på sidan AEM 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till AEM 6.5 använda den här sidan för att bedöma arbetsinsatsen i samband med databasändringar som påverkar AEM Sites Solution. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Med 6.5-uppgradering**

* [ContextHub-segment](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Före framtida uppgradering**

* [Adobe Analytics Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Klassisk Microsoft Word till Web Page Designs](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Konfigurationer för emulatorn för mobila enheter](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Designkonfigurationer för hantering av flera webbplatser](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Körningskonfigurationer för flera platshanterare](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [E-postmall för sidhändelseavisering](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Sidställningar](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [LESS-responsivt rutnät](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Statiska malldesigner](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Klientbibliotek för Adobe Target-integrering](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Klientbibliotek för WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Med 6.5-uppgradering {#with-upgrade}

### ContextHub-segment {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om nya eller ändrade ContextHub-segment ska redigeras i källkontrollen i stället för att redigeras i AEM, måste de migreras till den nya platsen:</p>
    <ol>
     <li>Kopiera nya eller ändrade ContextHub-segment från föregående plats till rätt nya plats (/<code>apps</code>, <code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Uppdatera referenser till ContextHub-segment på föregående plats till de migrerade ContextHub-segmenten på de nya platserna (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>Följande QueryBuilder-fråga hittar alla referenser till ContextHub-segment i de föregående platserna.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> Detta kan utföras via <br /> AEM QueryBuilder-felsökningsgränssnittet <a href="/help/sites-developing/querybuilder-api.md" target="_blank"></a>. Observera att detta är en genomgående fråga, så kör den inte mot produktionen och se till att genomströmningsgränserna justeras efter behov.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>ContextHub-segment beständiga till föregående platsvisning som skrivskyddade i <strong>AEM &gt; Personalisering &gt; Publiker</strong>.</p> <p>Om ContextHub-segment ska kunna redigeras i AEM måste de migreras till den nya platsen (<code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>). Alla nya ContentHub-segmentsegment som skapas i AEM bevaras på den nya platsen (<code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>).</p> <p>Sidegenskaperna för AEM-platser tillåter bara att antingen föregående plats (<code>/etc</code>) eller en ny plats (<code>/apps</code>, <code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>) markeras, vilket innebär att ContextHub-segment måste migreras i enlighet med detta.</p> <p>Alla oanvända ContextHub-segment från AEM-referenswebbplatser kan tas bort och inte migreras till den nya platsen:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoor</li>
    </ul> <p>Obs! Om ClientContext används bör du konvertera till ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Före framtida uppgradering {#prior-to-upgrade}

### Adobe Analytics Client Libraries {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>All anpassad användning av dessa klientbibliotek ska referera till klientbiblioteket efter kategori och inte efter sökväg:</p>
    <ol>
     <li>Alla referenser till klientbiblioteket per sökväg på platsen Föregående bör uppdateras så att <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM:s referensramverk</a>för klientbibliotek används.</li>
     <li>Om AEM:s referensramverk för klientbibliotek inte kan användas kan den absoluta sökvägen för klientbiblioteken refereras via AEM:s klientbiblioteksproxyserver.
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Redigering av dessa klientbibliotek stöds aldrig.</p> <p>Om du vill hämta kategorierna i klientbiblioteket går du till varje <code>cq:ClientLIbraryFolder</code> nod via CRXDELite och kontrollerar egenskapen categories.</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Klassisk Microsoft Word till Web Page Designs {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Konvertera CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i egenskapen cq:designPath.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-reglerna så att klientbibliotek kan hanteras via <code>/etc.clientlibs/</code> proxyservern.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor:</p>
    <ul>
     <li>Flytta inte bort redigerbara designer <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Konfigurationer för emulatorn för mobila enheter {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>Alla nya konfigurationer för emulatorn för mobila enheter måste migreras till den nya platsen.
    <ol>
     <li>Kopiera alla nya konfigurationer för emulatorn för mobila enheter från den tidigare platsen till den nya platsen (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>För alla AEM Sites Pages som är beroende av dessa konfigurationer för emulatorn för mobila enheter uppdaterar du sidans <span class="code"><code>
        jcr
       </code><code>
        :content
       </code></span> nod: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>För redigerbara mallar som är beroende av dessa konfigurationer för emulatorn för mobila enheter uppdaterar du de redigerbara mallarna och pekar på <span class="code"><code>
        cq
       </code>:
       till <code>
        deviceGroups
       </code></span> den nya platsen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Upplösningen för emulatorkonfigurationer för mobila enheter är följande:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Designkonfigurationer för hantering av flera webbplatser {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/apps/msm</code> (Kunddesignkonfigurationer)</p> <p><code>/libs/msm</code> (Utanför box-designkonfigurationer för skärmar, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade utkastkonfigurationer för Multi-site Manager måste migreras till den nya platsen (<code>/apps</code>).</p>
    <ol>
     <li>Kopiera alla nya eller ändrade Multi-site Manager-utkastkonfigurationer från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Ta bort alla migrerade layoutkonfigurationer för flerplatshanteraren från föregående plats.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Alla layoutkonfigurationer för hantering av flera webbplatser som tillhandahålls av AEM finns på den nya platsen i <code>/libs</code>.</p> <p>Innehållet refererar inte till blå konfigurationer för Multi-site Manager och det finns därför inga innehållsreferenser att justera.</p> </td>
  </tr>
 </tbody>
</table>

### Körningskonfigurationer för flera platshanterare {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade implementeringar av Multi-site Manager-hanteraren måste migreras till den nya platsen.</p>
    <ol>
     <li>Kopiera alla nya eller ändrade Multi-site Manager Rollout-konfigurationer från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Uppdatera alla referenser på AEM Pages till Multi-site Manager Rollout Configurations på den tidigare platsen för att peka på deras motsvarigheter på de nya platserna (<code>/libs</code> eller <code>/apps</code>).</li>
    </ol> <p>Ta bort migrerade utrullningskonfigurationer för hantering av flera platser från föregående plats.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Om det inte går att ta bort migrerade flerplatshanterarens utrullningskonfigurationer från den tidigare platsen visas dubblettalternativ för AEM-författare.</td>
  </tr>
 </tbody>
</table>

### E-postmall för sidhändelseavisering {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>De enda e-postmallar för sidhändelseavisering som stöds är stöd för nya språk.</p> <p>Mall för e-postmallsupplösning för sidhändelser sker i följande ordning:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Alla nya eller ändrade e-postmallar för sidhändelseavisering måste migreras till den nya platsen under <code>/apps</code>:</p>
    <ol>
     <li>Kopiera alla nya eller ändrade e-postmallar för sidhändelseavisering från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Ta bort alla migrerade e-postmallar för sidhändelseavisering från föregående plats.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Sidställningar {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><span class="code">/libs/settings/ <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/ <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>För scener som skapas under den föregående platsen används det äldre scenarioramverket och kan inte migreras till den nya platsen. Om du vill anpassa till den nya platsen måste alla äldre ställningar utvecklas på nytt med det scenkodsramverk som stöds.</td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### LESS-responsivt rutnät {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla referenser till föregående plats i anpassade LESS-filer måste uppdateras för import från den nya platsen.</p>
    <ul>
     <li>Uppdatera alla refererande anpassade LESS-filer som refererar till grid_base.less på platsen Previous för att referera till den nya platsen.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Om du refererar till en icke-befintlig <code>grid_base.less</code> fil fungerar inte layoutläget i sidredigeraren och mallredigeraren, och sidlayouten avbryts.</td>
  </tr>
 </tbody>
</table>

### Statiska malldesigner {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Konvertera CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i <code>cq:designPath</code> egenskapen via <strong>AEM &gt; Platser &gt; Anpassade webbplatssidor &gt; Sidegenskaper &gt; fliken Avancerat &gt; Designfält</strong>.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-reglerna så att klientbibliotek kan hanteras via <code>/etc.clientlibs/</code> proxyservern.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor:</p>
    <ul>
     <li>Flytta inte bort redigerbara designer <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Rekommenderat tillvägagångssätt är att bygga AEM-webbplatser och -sidor med hjälp av redigerbara mallar som använder strukturinnehåll och -profiler i stället för Designs.</td>
  </tr>
 </tbody>
</table>

### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>All anpassad användning av dessa klientbibliotek bör referera till klientbiblioteket efter kategori och inte efter sökväg.</p>
    <ol>
     <li>Alla referenser till klientbiblioteket per sökväg på platsen Föregående bör uppdateras så att <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM:s referensramverk</a>för klientbibliotek används.</li>
     <li>Om AEM:s referensramverk för klientbibliotek inte kan användas kan den absoluta sökvägen för klientbiblioteken refereras via AEM:s klientbiblioteksproxyserver:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Redigering av dessa klientbibliotek stöds aldrig.</p> <p>Om du vill hämta kategorierna i klientbiblioteket går du till varje cq:ClientLibraryFolder-nod via CRXDELite och kontrollerar egenskapen categories:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Klientbibliotek för Adobe Target-integrering {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>All anpassad användning av dessa klientbibliotek bör referera till klientbiblioteket efter kategori och inte efter sökväg.</p>
    <ol>
     <li>Alla referenser till klientbiblioteket per sökväg på platsen Föregående bör uppdateras så att <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM:s referensramverk</a>för klientbibliotek används.</li>
     <li>Om AEM:s referensramverk för klientbibliotek inte kan användas kan den absoluta sökvägen för klientbiblioteken refereras via AEM:s klientbiblioteksproxyserver:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Redigering av dessa klientbibliotek stöds aldrig.</p> <p>Om du vill hämta kategorierna i klientbiblioteket går du till varje cq:ClientLibraryFolder-nod via CRXDELite och kontrollerar egenskapen categories:</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Klientbibliotek för WCM Foundation {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>All anpassad användning av dessa klientbibliotek bör referera till klientbiblioteket efter kategori och inte efter sökväg.</p>
    <ol>
     <li>Alla referenser till klientbiblioteket per sökväg på platsen Föregående bör uppdateras så att <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM:s referensramverk</a>för klientbibliotek används.</li>
     <li>Om AEM:s referensramverk för klientbibliotek inte kan användas kan den absoluta sökvägen för klientbiblioteken refereras via AEM:s klientbiblioteksproxyserver.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Redigering av dessa klientbibliotek stöds aldrig.</p> <p>Om du vill hämta kategorierna i klientbiblioteket går du till varje <code>cq:ClientLIbraryFolder</code> nod via CRXDELite och kontrollerar egenskapen categories:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

