---
title: Omstrukturering av Dynamic Media-arkiv i AEM 6.5
seo-title: Omstrukturering av Dynamic Media-arkiv i AEM 6.5
description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.5 för Dynamic Media.
seo-description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.5 för Dynamic Media.
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
feature: Uppgraderar
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---


# Omstrukturering av Dynamic Media-arkiv i AEM 6.5 {#dynamic-media-repository-restructuring-in-aem}

Som beskrivs på den överordnade sidan [Databasomstrukturering på AEM 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till AEM 6.5 använda den här sidan för att bedöma arbetsinsatsen i samband med databasändringar som påverkar Dynamic Media-lösningen. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Före framtida uppgradering**

* [Anpassade konfigurationer för adaptiv videokodning](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media (DMS7) Cloud-konfiguration](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Konfiguration av Dynamic Media (DM Hybrid) Cloud Service](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube Cloud Service Configuration](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Diverse](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Före framtida uppgradering {#prior-to-upgrade}

### Anpassade adaptiva videokodningskonfigurationer {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Du kan köra följande migreringsskript för att migrera till den nya platsen:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Du kan också redigera konfigurationen i AEM och ändringarna sparas på den nya platsen.</p> </td>
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
   <td><strong>Ny plats(er)</strong></td>
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

### Dynamic Media (DM Hybrid) Cloud Service configuration {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
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

### Dynamic Media - YouTube Cloud Service configuration {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>1. Avpublicera alla videoklipp från YouTube<br /> 2. Skapa YouTube-konfigurationen med nya TouchUI (från <code>/conf</code>), inklusive kopiering av alla kanaler från den gamla platsen<br /> 3. Publicera alla videor på YouTube.</p> <p>Det här arbetsflödet ger nya YouTube-URL:er. Om du inte avpublicerar innan du skapar en ny TouchUI YouTube-konfiguration har du flera YouTube-URL:er listade under Egenskaper eftersom de återskapade kanalerna kommer att publiceras igen om du får chansen. Det innebär att du har oanvändbara URL:er som listas under Egenskaper.</p> </td>
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
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Kunden kan köra migreringsskriptet nedan.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Du kan också redigera konfigurationen i AEM och ändringarna sparas på den nya platsen.</p> </td>
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
   <td><strong>Ny plats(er)</strong></td>
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

