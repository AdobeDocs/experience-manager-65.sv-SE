---
title: Omstrukturering av tillgångar i AEM 6.5
seo-title: Omstrukturering av tillgångar i AEM 6.5
description: Lär dig hur du gör nödvändiga ändringar för att migrera till den nya databasstrukturen i AEM 6.5 for Assets.
seo-description: Lär dig hur du gör nödvändiga ändringar för att migrera till den nya databasstrukturen i AEM 6.5 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Omstrukturering av tillgångar i AEM 6.5 {#assets-repository-restructuring-in-aem}

Som beskrivs på den överordnade [databasomstruktureringen på sidan AEM 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till AEM 6.5 använda den här sidan för att bedöma arbetsinsatsen i samband med databasändringar som påverkar AEM Assets-lösningen. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Med 6.5-uppgradering**

* [Diverse](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Före framtida uppgradering**

* [E-postmeddelandemall för tillgångs-/samlingshändelse](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Klassisk resursdelningsdesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Ladda ned mall för e-postmeddelanden om tillgångar](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Exempel på DRM-licenser](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [E-postmeddelandemall för länkdelning](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign Workflow Scripts](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Konfigurationer för videoomkodning](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Diverse](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Med 6.5-uppgradering {#with-upgrade}

### Diverse {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td>/etc/dam/job</td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td>/var/dam/job</td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om någon anpassad kod är beroende av den här platsen (t.ex. koden uttryckligen bygger på denna sökväg) måste koden uppdateras för att kunna använda den nya platsen innan den uppgraderas, Helst används Java-API:er när de är tillgängliga för att minska beroenden av en viss sökväg i JCR-läsaren.</p> <p>Temporär plats för ZIP-filen som klienten kan hämta. Det finns ingen anledning att uppdatera sedan när kunden begär att få hämta resursen. Filen genereras på den nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

## Före framtida uppgradering {#prior-to-upgrade}

### E-postmeddelandemall för tillgångs-/samlingshändelse {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om e-postmallarna har ändrats av kunden utför du följande åtgärder för att anpassa dem till den nya databasstrukturen:</p>
    <ol>
     <li>E- <code>/libs/settings/dam/notification</code> postmallen ska kopieras från <strong><code>/etc/notification/email/default</code></strong> till <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Eftersom målet finns i<strong> den här <code>/apps</code></strong> ändringen bör sparas i SCM.</li>
      </ol> </li>
     <li>Ta bort mappen: <strong><code>/etc/dam/notification/email/default</code></strong> efter att e-postmallarna har flyttats.<br />
      <ol>
       <li>Om inga uppdateringar gjordes av e-postmallen under<strong> <code>/etc/notification/email/default</code></strong>kan mappen tas bort eftersom den ursprungliga e-postmallen finns under <strong><code>/libs/settings/notification/email/default</code></strong> AEM 4-installationen.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Klassisk resursdelningsdesign {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Utför följande åtgärder för alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor för att anpassa sig till den senaste modellen:</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen under <code>/apps</code>.</li>
     <li>Konvertera CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i <code>cq:designPath</code> egenskapen via <strong>AEM &gt; DAM Admin &gt; Resursdelningssida &gt; Sidegenskaper &gt; fliken Avancerat &gt; Designfält</strong>.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används. Detta kräver uppdatering av koden för implementering av sidan.</li>
     <li>Uppdatera Dispatcher-reglerna så att klientbibliotek kan hanteras via <code>/etc.clientlibs/</code> proxyservern.</li>
    </ol> <p>För alla designer som inte hanteras i SCM, och som modifieras vid körning via designdialogrutor, ska du inte flytta bort författarskapande designer <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Ladda ned mall för e-postmeddelanden om tillgångar {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om e-postmallarna (<strong>nedladdningstillgång</strong> eller <strong>tillfälligt arbetsflöde slutfört</strong>) har ändrats följer du nedanstående procedur för att anpassa sig till den nya strukturen:</p>
    <ol>
     <li>Den uppdaterade e-postmallen ska kopieras från <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> till <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Eftersom målet finns i<strong> den här <code>/apps</code></strong> ändringen bör sparas i SCM.</li>
      </ol> </li>
     <li>Ta bort mappen: <code>/etc/dam/workflow/notification/email/downloadasset </code>efter att e-postmallarna har flyttats.<br />
      <ol>
       <li>Om inga uppdateringar gjordes av e-postmallen under<strong> <code>/etc</code></strong>kan mappen tas bort eftersom den ursprungliga e-postmallen finns under <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> installationen av AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Även om <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> det finns tekniskt stöd för sökning (har företräde före /apps via vanlig Sling CAConfig-sökning, men efter <code>/etc</code>) kan mallen placeras i <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Detta rekommenderas dock inte eftersom det inte finns något användargränssnitt som underlättar redigeringen av e-postmallen.</td>
  </tr>
 </tbody>
</table>

### Exempel på DRM-licenser {#example-drm-licenses}

| **Föregående plats** | `/etc/dam/drm/licenses/` |
|---|---|
| **Ny plats(er)** | `/libs/settings/dam/drm` |
| **Omstruktureringsvägledning** | Ej tillämpligt |
| **Anteckningar** | Ej tillämpligt |

### E-postmeddelandemall för länkdelning {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om e-postmallen ändrades av kunden så justeras den efter den nya databasstrukturen:</p>
    <ol>
     <li>Den uppdaterade e-postmallen ska kopieras från <strong><code>/etc/dam/adhocassetshare</code></strong> till <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Eftersom målet finns i<strong> den här <code>/apps</code></strong> ändringen bör sparas i SCM.</li>
      </ol> </li>
     <li>Ta bort mappen: <strong><code>/etc/dam/adhocassetshare</code></strong> efter att e-postmallarna har flyttats.<br />
      <ol>
       <li>Om inga uppdateringar gjordes av e-postmallen under<strong> <code>/etc</code></strong>kan mappen tas bort eftersom den ursprungliga e-postmallen finns under <strong><code>/libs/settings/dam/adhocassetshare</code></strong> installationen av AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Mallen <code>/conf/global/settings/dam/adhocassetshare</code> stöds tekniskt för sökning (den har företräde före <code>/apps</code> vanlig Sling CAConfig-sökning, men efter <code>/etc</code>), men kan placeras i <code>/conf/global/settings/dam/adhocassetshare</code>. Detta rekommenderas dock inte eftersom det inte finns något användargränssnitt som underlättar redigeringen av e-postmallen</td>
  </tr>
 </tbody>
</table>

### InDesign Workflow Scripts {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Så här justerar du den nya databasstrukturen:</p>
    <ol>
     <li>Kopiera alla anpassade eller ändrade skript från <strong><code>/etc/dam/indesign/scripts</code></strong> till <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>Endast kopiera nya eller ändrade skript som oförändrade skript från AEM är tillgängliga via <strong><code>/libs/settings</code></strong> AEM 6.5</li>
      </ol> </li>
     <li>Hitta alla arbetsflödesmodeller som använder WF-steget för medieextraheringsprocessen och
      <ol>
       <li>För varje instans av arbetsflödessteget ska du uppdatera sökvägarna i config så att de pekar explicit på rätt skript under<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> eller <strong><code>/libs/settings/dam/indesign/scripts</code></strong> efter behov.</li>
      </ol> </li>
     <li>Ta bort<strong> <code>/etc/dam/indesign/scripts</code></strong> helt.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Vi rekommenderar att du lagrar anpassade skript under <code>/apps</code>, eftersom det är platsen där koden ska lagras.</td>
  </tr>
 </tbody>
</table>

### Konfigurationer för videoomkodning {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Anpassningar på projektnivå måste klippas ut och klistras in under motsvarande <code>/apps</code> eller <code>/conf</code> tillämpliga sökvägar.</p> <p>Så här anpassar du dig till databasstrukturen för AEM 6.4:</p>
    <ol>
     <li>Kopiera ändrade videokonfigurationer från <code>/etc/dam/video</code> till <code>/apps/settings/dam/video</code></li>
     <li>Ta bort <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Förinställningskonfigurationer för visningsprogram {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För den som visas i rutan Visningsförinställning är den bara tillgänglig på den nya platsen.</p> <p>För förinställningen för Anpassat visningsprogram:</p>
    <ul>
     <li>måste du köra ett migreringsskript för att flytta noden från <code>/etc</code> till <code>/conf</code>. Skriptet finns på <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>eller så kan du redigera konfigurationen så sparas de automatiskt på den nya platsen.</li>
    </ul> <p>Observera att du inte behöver justera deras copyURL/embed-kod så att den pekar på <code>/conf</code>. Den befintliga begäran <code>/etc</code> dirigeras om till rätt innehåll från <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Diverse {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Justera alla referenser så att de pekar på de nya resurserna under <code>/libs</code> med hjälp av prefixet Tillåt <code>/etc.clientlibs/</code> .</p> <p>Rensa slutligen genom att ta bort mapparna för de migrerade klientlibs från <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

