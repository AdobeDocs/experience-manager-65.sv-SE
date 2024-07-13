---
title: Omstrukturering av Dynamic Media-arkiv i Adobe Experience Manager 6.5
description: Lär dig hur du gör nödvändiga ändringar för att migrera till den nya databasstrukturen i Experience Manager 6.5 för Dynamic Media.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Omstrukturering av Dynamic Media-arkiv i Adobe Experience Manager 6.5 {#dynamic-media-repository-restructuring-in-aem}

Så som beskrivs på den överordnade sidan [Databasomstrukturering i Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till Experience Manager 6.5 använda den här sidan för att utvärdera arbetsinsatsen som är kopplad till databasändringar som påverkar Dynamic Media. Vissa ändringar kräver arbete under uppgraderingsprocessen för Experience Manager 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Före framtida uppgradering**

* [Anpassade konfigurationer för adaptiv videokodning](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media (DMS7) Cloud-konfiguration](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Konfiguration av Dynamic Media (DM Hybrid) Cloud Service](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube Cloud Service Configuration](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Diverse](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Före framtida uppgradering {#prior-to-upgrade}

### Anpassade adaptiva videokodningskonfigurationer  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Du kan köra följande migreringsskript för att migrera till den nya platsen:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Du kan också redigera konfigurationen i användargränssnittet för Experience Manager och ändringarna sparas på den nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7) Cloud-konfiguration {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Kunden kan köra ett migreringsskript på följande plats:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Starta om Dynamic Media OSGi-paketet.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Konfiguration av Dynamic Media-Cloud Service (DM Hybrid) {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Du kan köra migreringsskriptet nedan för att anpassa dig till den senaste modellen:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTube Cloud Service configuration  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>1. Avpublicera alla videoklipp från YouTube<br /> 2. Skapa YouTube Configuration med det nya TouchUI-gränssnittet (från <code>/conf</code>), inklusive kopiering av alla kanaler från den gamla platsen <br /> 3. Publish alla filmer tillbaka till YouTube.</p> <p>Arbetsflödet ger nya YouTube URL:er. Om du inte avpublicerar innan du skapar en TouchUI YouTube-konfiguration har du flera YouTube-URL:er listade under Egenskaper eftersom de återskapade kanalerna publiceras igen, om du får chansen. Den här funktionen innebär att du har oanvändbara URL:er som listas under Egenskaper.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Diverse {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Kunden kan köra migreringsskriptet nedan.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Du kan också redigera konfigurationen i användargränssnittet för Experience Manager och ändringarna sparas på den nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Kunden kan köra migreringsskriptet nedan.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>
