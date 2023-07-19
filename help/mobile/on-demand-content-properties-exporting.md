---
title: Exportera innehåll med hjälp av innehållsegenskaper
seo-title: Using Content Properties to Export Content
description: På följande sida visas Appegenskaper och -noder.
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Exportera innehåll med hjälp av innehållsegenskaper{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Apparna representeras som *cq:Sidor* AEM.

De delar samma gemensamma egenskaper som finns i *cq:Page* utöver de andra som visas nedan och som representerar egenskaper som stöder integrering.

## Appegenskaper {#app-properties}

Följande tabell visar **Programegenskaper och noder**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String:Path</td>
   <td><p>Sökväg till en konfigurerad Mobile On-Demand-Cloud Service. Används för AEM Mobile till Mobile On-Demand-åtgärder (API-anrop)</p> <p>Den här associationen konfigureras via panelen Hantera anslutning när en författare väljer en Cloud Service för mobil på begäran att koppla appen till.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>Sökväg till programmets exportkonfigurationer. Exportkonfigurationen är en mapp med två underordnade konfigurationsmallar för ContentSync-export.</p> <p><i>dps-article</i>: ContentSync-exportkonfiguration för att exportera artikelinnehåll</p> <p><i>dps-HTMLResources</i>: Konfiguration av ContentSync-export för att exportera delade resurser för program/artikel</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Sträng</td>
   <td><p>ID/URI för det Mobile On-Demand-projekt som den här appen är länkad/bunden till.</p> <p>Den här associationen konfigureras via panelen Hantera anslutning när en författare väljer projektet från en lista över tillgängliga projekt för den associerade Cloud Servicen Mobile On-Demand.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>Sträng</td>
   <td>Programtitel.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>Sträng</td>
   <td>Innehållstyp.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>Datum</td>
   <td>Datum för senaste överföring av delade resurser från AEM till AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>ID för den användare som senast överförde begäran om delade resurser från AEM till AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>String:Path</td>
   <td>Sökväg till en instrumentpanelskonfiguration. Sökvägen kan vid behov omdirigeras till en anpassad instrumentpanelskonfiguration.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String:Path</td>
   <td><p>Sökväg till en cq:Component som är eller utökar <i>mobileapps/core/components/instance.</i></p> <p>Detta medför att det finns och återges i Apps-katalogen.</p> </td>
  </tr>
 </tbody>
</table>

Du kan använda ***Innehållsegenskaper*** för att skapa innehåll. Se följande resurser för att skapa och exportera artiklar och delade resurser:

* [Innehållsegenskaper](/help/mobile/content-properties.md)
* [Skapar artikelexportkonfiguration](/help/mobile/creating-article-export-configuration.md)
* [Skapar exportkonfiguration för delade resurser](/help/mobile/creating-shared-resources-export-configuration.md)
