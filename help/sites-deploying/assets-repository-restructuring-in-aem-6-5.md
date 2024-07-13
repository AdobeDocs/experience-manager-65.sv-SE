---
title: Omstrukturering av Assets-lager i AEM 6.5
description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i Adobe Experience Manager (AEM) 6.5 för Assets.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Omstrukturering av Assets-lager i AEM 6.5 {#assets-repository-restructuring-in-aem}

Så som beskrivs på den överordnade sidan [Databasomstrukturering på sidan AEM 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till Adobe Experience Manager (AEM) 6.5 använda den här sidan för att utvärdera arbetsinsatsen som är kopplad till databasändringar som påverkar AEM Assets-lösningen. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

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
   <td>/var/dam/Jobb</td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om någon anpassad kod är beroende av den här platsen, d.v.s., är koden uttryckligen beroende av den här sökvägen. Koden måste uppdateras för att kunna använda den nya platsen innan du uppgraderar. Helst används Java™-API:er när de är tillgängliga för att minska beroendet av en viss sökväg i JCR-läsaren.</p> <p>Temporär plats för en ZIP-fil som klienten kan hämta. Det finns ingen anledning att uppdatera sedan när kunden begär att få hämta resursen. Den genererar en fil på den nya platsen.</p> </td>
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
     <li>E-postmallen <code>/libs/settings/dam/notification</code> ska kopieras från <strong><code>/etc/notification/email/default</code></strong> till <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Eftersom målet är i <strong> <code>/apps</code></strong> bör den här ändringen bevaras i SCM.</li>
      </ol> </li>
     <li>Ta bort mappen: <strong><code>/etc/dam/notification/email/default</code></strong> när e-postmallarna i den har flyttats.<br />
      <ol>
       <li>Om inga uppdateringar gjordes av e-postmallen under <strong> <code>/etc/notification/email/default</code></strong> kan mappen tas bort eftersom den ursprungliga e-postmallen finns under <strong><code>/libs/settings/notification/email/default</code></strong> som en del av installationen av AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
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
   <td><p>Utför följande åtgärder för alla designer som hanteras i SCM och som inte skrivs till under körning via designdialogrutor för att anpassa sig till den senaste modellen:</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen under <code>/apps</code>.</li>
     <li>Konvertera alla CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i egenskapen <code>cq:designPath</code> genom att <strong>AEM &gt; DAM-administratör &gt; Resursdelningssida &gt; Sidegenskaper &gt; fliken Avancerat &gt; Designfält</strong>.</li>
     <li>Om du vill använda den nya kategorin Klientbibliotek uppdaterar du alla sidor som refererar till den tidigare platsen. Detta kräver att implementeringskoden för sidan uppdateras.</li>
     <li>Uppdatera Dispatcher-reglerna så att du kan tillåta servering av klientbibliotek via proxyservern <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Flytta inte redigerbara designer från <code>/etc</code> för designer som inte hanteras i SCM och som ändras vid körning via designdialogrutor.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
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
   <td><p>Om e-postmallarna (<strong>downloader</strong> eller <strong>transientworkflowComplete</strong>) har ändrats följer du nedanstående procedur för att anpassa till den nya strukturen:</p>
    <ol>
     <li>Den uppdaterade e-postmallen ska kopieras från <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> till <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Eftersom målet är i <strong> <code>/apps</code></strong> bör den här ändringen bevaras i SCM.</li>
      </ol> </li>
     <li>Ta bort mappen: <code>/etc/dam/workflow/notification/email/downloadasset </code>när e-postmallarna i den har flyttats.<br />
      <ol>
       <li>Om inga uppdateringar gjordes av e-postmallen under <strong> <code>/etc</code></strong> kan mappen tas bort eftersom den ursprungliga e-postmallen finns under <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> som en del av AEM 6.4-installationen.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> stöds tekniskt för sökning (har företräde före /apps via vanlig Sling CAConfig-sökning, men efter <code>/etc</code>) kan mallen placeras i <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Detta rekommenderas dock inte eftersom det inte finns något användargränssnitt som underlättar redigeringen av e-postmallen.</td>
  </tr>
 </tbody>
</table>

### Exempel på DRM-licenser {#example-drm-licenses}

| **Föregående plats** | `/etc/dam/drm/licenses/` |
|---|---|
| **Ny(a) plats(er)** | `/libs/settings/dam/drm` |
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
       <li>Eftersom målet är i <strong><code>/apps</code></strong> bör den här ändringen bevaras i SCM.</li>
      </ol> </li>
     <li>Ta bort mappen: <strong><code>/etc/dam/adhocassetshare</code></strong> när e-postmallarna i den har flyttats.<br />
      <ol>
       <li>Om inga uppdateringar gjordes av e-postmallen under <strong> <code>/etc</code></strong> kan mappen tas bort eftersom den ursprungliga e-postmallen finns under <strong><code>/libs/settings/dam/adhocassetshare</code></strong> som en del av AEM 6.4-installationen.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><code>/conf/global/settings/dam/adhocassetshare</code> stöds tekniskt för sökning (det har företräde före <code>/apps</code> via den vanliga Sling CAConfig-sökningen, men efter <code>/etc</code>), men mallen kan placeras i <code>/conf/global/settings/dam/adhocassetshare</code>. Detta rekommenderas dock inte eftersom det inte finns något användargränssnitt som underlättar redigeringen av e-postmallen</td>
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
       <li>Endast kopiera nya eller ändrade skript som oförändrade skript som tillhandahålls av AEM är tillgängliga via <strong><code>/libs/settings</code></strong> i AEM 6.5</li>
      </ol> </li>
     <li>Hitta alla arbetsflödesmodeller som använder WF-steget för medieextraheringsprocessen och
      <ol>
       <li>Uppdatera sökvägarna i konfigurationen så att de pekar explicit på rätt skript under <strong> <code>/apps/settings/dam/indesign/scripts</code></strong> eller <strong><code>/libs/settings/dam/indesign/scripts</code></strong> efter behov för varje instans av arbetsflödessteget.</li>
      </ol> </li>
     <li>Ta bort <strong> <code>/etc/dam/indesign/scripts</code></strong> helt.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Vi rekommenderar att anpassade skript lagras under <code>/apps</code>, eftersom det är platsen där koden ska lagras.</td>
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
   <td><p>Anpassningar på projektnivå måste klippas ut och klistras in under motsvarande <code>/apps</code>- eller <code>/conf</code>-sökvägar.</p> <p>Så här anpassar du dig till databasstrukturen i AEM 6.4:</p>
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
     <li>kör ett migreringsskript så att du kan flytta noden från <code>/etc</code> till <code>/conf</code>. Skriptet finns på <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>eller så kan du redigera konfigurationen och de sparas automatiskt på den nya platsen.</li>
    </ul> <p>Du behöver inte justera deras copyURL/embed-kod så att den pekar på <code>/conf</code>. Den befintliga begäran till <code>/etc</code> dirigeras om till rätt innehåll från <code>/conf</code>.</p> </td>
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
   <td><p>Justera alla referenser så att de pekar på de nya resurserna under <code>/libs</code> med hjälp av prefixet <code>/etc.clientlibs/</code> allow.</p> <p>Rensa slutligen genom att ta bort mapparna för de migrerade klientlibs från <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>
