---
title: Felsöka Dynamic Media - Scene7-läge
description: Felsök Dynamic Media när det körs i Scene7-läge.
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
source-git-commit: d5824078ca3e1ff2b48874446aaebe3fdd60cfdc
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---

# Felsöka Dynamic Media - Scene7-läge{#troubleshooting-dynamic-media-scene-mode}

I följande dokument beskrivs felsökning för Dynamic Media som körs **dynamicmedia_scene7** körningsläge.

## Installation och konfiguration {#setup-and-configuration}

Kontrollera att Dynamic Media har konfigurerats korrekt genom att göra följande:

* Kommandot Start innehåller `-r dynamicmedia_scene7` argument för körningsläge.
* Alla kumulativa Adobe Experience Manager 6.4-korrigeringspaket (CFP) har installerats först *före* alla Dynamic Media funktionspaket.
* Tillvalspaket 18912 är installerat.

   Det här tillvalspaketet är till för FTP-stöd eller om du migrerar resurser till Dynamic Media från Dynamic Media Classic.

* Navigera till användargränssnittet för Cloud Services och bekräfta att det tilldelade kontot visas under **[!UICONTROL Available Configurations]**.
* Se till att `Dynamic Media Asset Activation (scene7)` replikeringsagenten är aktiverad.

   Den här replikeringsagenten finns under Agenter på författare.

## Allmänt (alla resurser) {#general-all-assets}

Här följer några allmänna tips och tricks för alla resurser.

### Egenskaper för resurssynkroniseringsstatus {#asset-synchronization-status-properties}

Följande resursegenskaper kan granskas i CRXDE Lite för att bekräfta att synkroniseringen av resursen lyckades från Experience Manager till Dynamic Media:

| **Egenskap** | **Exempel** | **Beskrivning** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | En allmän indikator på att noden är länkad till Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** eller feltext | Status för överföring av resurs till Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Måste fyllas i för att URL:er ska kunna genereras till Dynamic Media fjärråtkomst. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **framgång** eller **misslyckades:`<error text>`** | Synkroniseringsstatus för uppsättningar (snurra uppsättningar, bilduppsättningar o.s.v.), bildförinställningar, visningsförinställningar, uppdateringar av bildscheman för en resurs eller bilder som har redigerats. |

### Synkroniseringsloggning {#synchronization-logging}

Synkroniseringsfel och problem loggas in `error.log` (Experience Manager serverkatalog `/crx-quickstart/logs/`). Tillräcklig loggning finns för att fastställa orsaken till de flesta problemen, men du kan öka loggningen till DEBUG på `com.adobe.cq.dam.ips` genom Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) för att samla in mer information.

### Flytta, kopiera, ta bort {#move-copy-delete}

Gör följande innan du utför någon av åtgärderna Flytta, Kopiera eller Ta bort:

* För bilder och videoklipp bekräftar du att en `<object_node>/jcr:content/metadata/dam:scene7ID` värdet finns innan du utför åtgärderna flytta, kopiera eller ta bort.
* Bekräfta att en `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` värdet finns innan du utför åtgärderna flytta, kopiera eller ta bort.
* Om metadatavärdet ovan saknas måste du överföra resurserna igen innan du kan flytta, kopiera eller ta bort åtgärder.

### Versionskontroll {#version-control}

När du ersätter en befintlig Dynamic Media-resurs (samma namn och plats) kan du behålla båda resurserna eller ersätta/skapa en version:

* Om du behåller båda skapas en resurs med ett unikt namn för den publicerade resursens URL. Till exempel: `image.jpg` är den ursprungliga tillgången och `image1.jpg` är den nyligen överförda resursen.

* Det går inte att skapa en version i Dynamic Media - leverans i Scene7-läge. Den nya versionen ersätter den befintliga mediefilen som levereras.

## Bilder och uppsättningar {#images-and-sets}

Om du har problem med bilder och uppsättningar kan du läsa följande felsökningsguide.

<table>
 <tbody>
  <tr>
   <td><strong>Problem</strong></td>
   <td><strong>Felsöka</strong></td>
   <td><strong>Lösning</strong></td>
  </tr>
  <tr>
   <td>Det går inte att komma åt knappen för kopiera URL/bädda in i resursens detaljvy</td>
   <td>
    <ol>
     <li><p>Gå till CRX/DE:</p>
      <ul>
       <li>Kontrollera om förinställningen i JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> definierad. Den här platsen gäller om du har uppgraderat från Experience Manager 6.x till 6.4 och valt att inte migrera. Annars är platsen <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Kontrollera att resursen i JCR har <code>dam:scene7FileStatus</code><strong> </strong>under Metadata visas som <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Uppdatera sida/navigera till en annan sida och gå tillbaka (JSP för sidorälar måste kompileras om)</p> <p>Om det inte fungerar:</p>
    <ul>
     <li>Publicera resurs.</li>
     <li>Ladda upp resursen igen och publicera den.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Resursväljaren i set editor fastnade i permanent inläsning</td>
   <td><p>Känt fel som ska åtgärdas i 6.4</p> </td>
   <td><p>Stäng väljaren och öppna den igen.</p> </td>
  </tr>
  <tr>
   <td><strong>Välj</strong> knappen är inte aktiv när du har markerat en resurs som en del av redigeringen av en uppsättning</td>
   <td><p> </p> <p>Känt fel som ska åtgärdas i 6.4</p> <p> </p> </td>
   <td><p>Välj först en annan mapp i resursväljaren och gå tillbaka och välj resursen.</p> </td>
  </tr>
  <tr>
   <td>Carousel hotspot flyttas runt efter växling mellan bildrutor</td>
   <td><p>Kontrollera att alla bildrutor har samma storlek.</p> </td>
   <td><p>Använd endast bilder med samma storlek för karusellen.</p> </td>
  </tr>
  <tr>
   <td>Bilden förhandsvisas inte med Dynamic Media Viewer</td>
   <td><p>Kontrollera att resursen innehåller <code>dam:scene7File</code> i metadataegenskaperna (CRXDE Lite)</p> </td>
   <td><p>Kontrollera att alla resurser har avslutat bearbetningen.</p> </td>
  </tr>
  <tr>
   <td>Den överförda resursen visas inte i resursväljaren</td>
   <td><p>Kontrollera att resursen har en egenskap <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Kontrollera att alla resurser har avslutat bearbetningen.</p> </td>
  </tr>
  <tr>
   <td>Banderoll på kortvyspel <strong>Nytt</strong> när resursen inte har börjat bearbetas</td>
   <td>Kontrollera resurs <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> det har inte hämtats av arbetsflödet.</td>
   <td>Vänta tills resursen har hämtats av arbetsflödet.</td>
  </tr>
  <tr>
   <td>Bilder eller uppsättningar visar inte visningsprogrammets URL eller inbäddningskod</td>
   <td>Kontrollera om visningsförinställningen har publicerats.</td>
   <td><p>Gå till <strong>verktyg</strong> &gt; <strong>Resurser</strong> &gt; <strong>Förinställningar för visningsprogram</strong> och publicera visningsförinställningen.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

Om du har problem med video kan du läsa följande felsökningsguide.

<table>
 <tbody>
  <tr>
   <td><strong>Problem</strong></td>
   <td><strong>Felsöka</strong></td>
   <td><strong>Lösning</strong></td>
  </tr>
  <tr>
   <td>Videon kan inte förhandsgranskas</td>
   <td>
    <ul>
     <li>Kontrollera att mappen har tilldelats en videoprofil (om filformatet inte stöds). Om det inte stöds visas bara en bild.</li>
     <li>Videoprofilen måste innehålla mer än en kodningsförinställning för att generera en AVS-uppsättning (en kodning behandlas som videoinnehåll för MP4-filer). för filer som inte stöds, behandlas på samma sätt som obearbetade).</li>
     <li>Kontrollera att videon har bearbetats klart genom att bekräfta <code>dam:scene7FileAvs</code> av <code>dam:scene7File</code> i metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Tilldela en videoprofil till mappen.</li>
     <li>Redigera videoprofilen så att den innehåller fler än en kodningsförinställning.</li>
     <li>Vänta tills videon har bearbetats klart.</li>
     <li>Kontrollera att arbetsflödet för videokodning inte körs när du läser in videon igen.<br /> </li>
     <li>Ladda upp videon igen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Video är inte kodad</td>
   <td>
    <ul>
     <li>Kontrollera att körningsläget är <code>dynamicmedia_scene7</code>.</li>
     <li>Kontrollera om Dynamic Media molntjänst är konfigurerad.</li>
     <li>Kontrollera om en videoprofil är kopplad till mappen för överföring.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Kontrollera din Experience Manager-instans med <code>-r dynamicmedia_scene7</code></li>
     <li>Kontrollera att Dynamic Media Configuration under Cloud Services är korrekt konfigurerad.</li>
     <li>Kontrollera att mappen har en videoprofil. Kontrollera även videoprofilen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Videobearbetning tar för lång tid</td>
   <td><p>Så här avgör du om videokodning fortfarande pågår eller om den har försatts i ett feltillstånd:</p>
    <ul>
     <li>Kontrollera videostatus <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Övervaka videon från arbetsflödeskonsolen <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Flikarna Instanser, Arkiv och Fel.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Videoåtergivning saknas</td>
   <td><p>När video överförs, men det inte finns några kodade återgivningar:</p>
    <ul>
     <li>Kontrollera att mappen har tilldelats en videoprofil.</li>
     <li>Kontrollera att videon har bearbetats klart genom att bekräfta <code>dam:scene7FileAvs</code> i metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Tilldela en videoprofil till mappen.</li>
     <li>Vänta tills videon har bearbetats klart.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Tittare {#viewers}

Om du har problem med visningsprogram kan du läsa följande felsökningsguide.

### Problem: Visningsförinställningar publiceras inte {#viewers-not-published}

**Felsöka**

1. Gå till diagnostiksidan för provhanteraren: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Lägg märke till beräknade värden. När du arbetar korrekt ser du följande: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Det kan ta ca 10 minuter efter konfigureringen av Dynamic Media molninställningar för de visningsprogramresurser som ska synkroniseras.

1. Om det finns oaktiverade resurser kvar väljer du något av **Visa alla oaktiverade resurser** för att se information.

**Lösning**

1. Navigera till förinställningslistan för visningsprogrammet i administratörsverktygen: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Markera alla förinställningar för visningsprogram och välj sedan **Publicera**.
1. Navigera tillbaka till exempelhanteraren och observera att antalet oaktiverade resurser nu är noll.

### Problem: En förinställd teckning i visningsprogrammet returnerar 404 från Förhandsgranska i resursinformation eller Kopiera URL/Bädda in kod {#viewer-preset-404}

**Felsöka**

Gör följande i CRXDE Lite:

1. Navigera till `<sync-folder>/_CSS/_OOTB` i din Dynamic Media-synkroniseringsmapp (till exempel `/content/dam/_CSS/_OOTB`).
1. Hitta metadatanoden för den problematiska resursen (till exempel `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Kontrollera om det finns `dam:scene7*` egenskaper. Om resursen synkroniserades och publicerades korrekt visas `dam:scene7FileStatus` anges till **PublishComplete**.
1. Försök att begära teckningen direkt från Dynasmic Media genom att sammanfoga värdena för följande egenskaper och stränglitteraler:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Exempel: 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Lösning**

Om exempelmaterialet eller den förinställda teckningen i visningsprogrammet inte har synkroniserats eller publicerats startar du om hela kopierings-/synkroniseringsprocessen:

1. Gå till CRXDE Lite.
1. Ta bort `<sync-folder>/_CSS/_OOTB`.
1. Navigera till CRX Package Manager: `https://localhost:4502/crx/packmgr/`.
1. Sök efter visningsprogrampaket i listan; börjar med `cq-dam-scene7-viewers-content`.
1. Välj **Installera om**.
1. Gå till konfigurationssidan för Dynamic Media under Cloud Services och öppna sedan konfigurationsdialogrutan för din Dynamic Media - S7-konfiguration.
1. Gör inga ändringar, markera **Spara**.
Denna sparåtgärd aktiverar logiken igen för att skapa och synkronisera exempelresurserna, CSS-förinställningen för visningsprogrammet och teckningen.

### Problem: Bildförhandsvisningen läses inte in vid redigering av visningsförinställningar {#image-preview-not-loading}

**Lösning**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och navigerar sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. Navigera till mappen med exempelinnehåll på följande plats i den vänstra listen:

   `/content/dam/_DMSAMPLE`

1. Ta bort `_DMSAMPLE` mapp.
1. Navigera till mappen Presets på följande plats i den vänstra listen:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Ta bort `viewer` mapp.
1. I närheten av det övre vänstra hörnet på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.
1. I det övre vänstra hörnet på CRXDE Lite-sidan väljer du **Tillbaka hem** ikon.
1. Återskapa en [Dynamic Media Configuration in Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
