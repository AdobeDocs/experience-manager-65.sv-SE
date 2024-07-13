---
title: Omstrukturering av de gemensamma tillgångarna i AEM 6.5
description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.5 som är gemensamma för alla AEM.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
solution: Experience Manager, Experience Manager Sites
feature: Upgrading
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 0%

---

# Omstrukturering av de gemensamma tillgångarna i AEM 6.5 {#common-repository-restructuring-in-aem}

Så som beskrivs på den överordnade sidan [Databasomstrukturering på sidan AEM 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till AEM 6.5 använda den här sidan för att bedöma arbetsinsatsen som är kopplad till databasändringar som kan påverka alla lösningar. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Med 6.5-uppgradering**

* [ContextHub-konfigurationer](#contexthub-6.5)
* [Arbetsflödesinstanser](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Arbetsflödesmodeller](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Arbetsflödeskörare](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Arbetsflödesskript](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Före framtida uppgradering**

* [ContextHub-konfigurationer](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Klassisk Cloud Service Designs](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Designer för klassiska instrumentpaneler](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Designer för klassiska rapporter](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Standarddesigner](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Adobe DTM JavaScript Endpoint](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe DTM-webbhook-slutpunkt](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Inkorgsuppgifter](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Designkonfigurationer för hantering av flera webbplatser](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Konfigurationer för instrumentpanelswidgetar för AEM projekt](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [E-postmall för replikeringsmeddelande](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Taggar](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Cloud Services för översättning](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Översättningsspråk](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Översättningsregler](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Klientbibliotek för översättningswidget](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Webbkonsol för träaktivering](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Service för leverantörsöversättningskonnektor](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [E-postmallar för arbetsflödesmeddelanden](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Med 6.5-uppgradering {#with-upgrade}

### ContextHub-konfigurationer {#contexthub-6.5}

Från och med AEM 6.4 finns det ingen standardkonfiguration för ContextHub. Därför bör `cq:contextHubPathproperty` anges på platsens rotnivå för att ange vilken konfiguration som ska användas.

1. Navigera till platsens rot.
1. Öppna sidegenskaperna för rotsidan och välj fliken Personalization.
1. I fältet Contexthub Path anger du din egen konfigurationssökväg för ContextHub.

I ContextHub-konfigurationen måste dessutom `sling:resourceType` uppdateras så att den är relativ och inte absolut.

1. Öppna egenskaperna för ContextHub-konfigurationsnoden i CRX DE Lite, till exempel `/apps/settings/cloudsettings/legacy/contexthub`
1. Ändra `sling:resourceType` från `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` till `granite/contexthub/cloudsettings/components/baseconfiguration`

Det innebär att `sling:resourceType` för ContextHub-konfigurationen måste vara relativ i stället för absolut.

### Arbetsflödesmodeller {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade arbetsflödesmodeller måste migreras till /conf/global/workflow/models.</p>
    <ol>
     <li>Distribuera de ändrade arbetsflödesmodellerna till en lokal AEM 6.5-utvecklingsinstans, så att de finns på platsen Previous.</li>
     <li>Redigera arbetsflödesmodellen med AEM Workflow Model Editor på AEM &gt; Verktyg &gt; Arbetsflöde &gt; Modeller.</li>
     <li>Vid migrering av AEM medföljande arbetsflödesmodeller
      <ol>
       <li>När modellredigeraren för arbetsflöde är öppen ändrar du webbläsarens adress-URL och ersätter sökvägssegmentet /libs/settings/workflow/models med /etc/workflow/models.
        <ul>
         <li>Ändra till exempel: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> till <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Aktivera redigeringsläget i arbetsflödesmodellredigeraren, som kopierar arbetsflödesmodelldefinitionen till /conf/global/workflow/models.</li>
     <li>Markera knappen Synkronisera om du vill synkronisera ändringarna till arbetsflödesmodellen för körning under /var/workflow/models.</li>
     <li>Exportera både arbetsflödesmodellen (/conf/global/workflow/models/&lt;workflow-model&gt;) och körningsarbetsflödesmodellen (/var/workflow/models/&lt;workflow-model&gt;) och integrera i AEM.
      <ol>
       <li>Exempel:
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code><br /> och </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Arbetsflödesmodellens upplösning sker i följande ordning:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Alla anpassningar av AEM arbetsflödesmodeller som finns kvar på platsen Föregående måste flyttas till /conf/global/settings/workflow/models om de ska behållas, annars ersätts de av den AEM arbetsflödesmodelldefinitionen i /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Arbetsflödesinstanser {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Ingen åtgärd krävs för att justera mot den nya platsen.</p> <p>Historiska arbetsflödesinstanser kan tryggt fortsätta finnas på den tidigare platsen, och nya arbetsflödesinstanser skapas på den nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Alla explicita sökvägsreferenser i
    Koden <code>
     custom
    </code> till föregående plats ska även ta hänsyn till den nya platsen. Vi rekommenderar att koden ändras så att den använder API:erna för AEM arbetsflöde.</td>
  </tr>
 </tbody>
</table>

### Arbetsflödeskörare {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade arbetsflödesstartare måste migreras till <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Kopiera alla nya eller ändrade arbetsflödeskonfigurationer från den tidigare platsen till den nya platsen (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Arbetsflödets startupplösning inträffar i följande ordning:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Alla anpassningar av AEM tillhandahållna Workflow Launcher som finns kvar på platsen Previous måste flyttas till den nya platsen (<code>/conf/global/settings/workflow/launcher</code>) om de ska behållas, annars ersätts de av den AEM arbetsflödesljudsdefinitionen i <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Arbetsflödesskript {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade arbetsflödesskript måste migreras till den nya platsen och de refererande arbetsflödesmodellerna uppdateras för att återspegla den nya platsen.</p>
    <ol>
     <li>Kopiera alla nya eller ändrade arbetsflödesskript från föregående plats till den nya platsen.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> bör upprätthållas i SCM.</li>
      </ul> </li>
     <li>Uppdatera alla referenser till arbetsflödesskripten på föregående plats i arbetsflödesmodeller så att de pekar på de nya platserna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>AEM 6.4 SP1, när den släpps, gör att omstruktureringen kan skjutas upp till 6.5
     <code>
      upgrade
     </code>.</p> <p>Om man uppgraderar till AEM 6.4 innan AEM 6.4 SP1 släpps bör denna omstrukturering genomföras som en del av uppgraderingsprojektet. Om du inte gör det kommer redigering och sparande av arbetsflödessteg som refererar till skript på den föregående platsen att ta bort skriptreferensen för arbetsflöde från arbetsflödessteget helt och hållet, och endast arbetsflödesskript på nya platser kommer att vara tillgängliga i listrutan för skriptval.</p> </td>
  </tr>
 </tbody>
</table>

## Före framtida uppgradering {#prior-to-upgrade}

### ContextHub-konfigurationer {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade ContextHub-konfigurationer måste migreras till den nya platsen och de refererande AEM Sites-sidorna måste uppdateras för att återspegla den nya platsen.</p>
    <ol>
     <li>Kopiera nya eller ändrade ContextHub-konfigurationer från föregående plats till den nya platsen.</li>
     <li>Associera de tillämpliga AEM med AEM innehållshierarkier.
      <ol>
       <li><strong>AEM Sites sidhierarkier via AEM Sites &gt; Sida &gt; Sidegenskaper &gt; fliken Avancerat &gt; Molnkonfiguration</strong>.</li>
      </ol> </li>
     <li>Avassociera migrerade äldre ContextHub-konfigurationer från de tidigare AEM innehållshierarkierna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Klassisk Cloud Service Designs {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Konvertera alla CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span> -egenskap.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-regler så att klientbibliotek kan visas via /etc.clientlibs/.. proxyserver.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor.</p>
    <ul>
     <li>Flytta inte designerbara designer från <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Designer för klassiska instrumentpaneler {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (/appar).</li>
     <li>Konvertera alla CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i dialogrutan
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> -egenskap.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-regler så att klientbibliotek kan visas via /etc.clientlibs/.. proxyserver.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor.</p>
    <ul>
     <li>Flytta inte designerbara designer från <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Designer för klassiska rapporter {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (/appar).</li>
     <li>Konvertera alla CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i dialogrutan
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> -egenskap.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-regler så att klientbibliotek kan visas via /etc.clientlibs/.. proxyserver.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor.</p>
    <ul>
     <li>Flytta inte designerbara designer från <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Standarddesigner {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (/appar).</li>
     <li>Konvertera alla CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i dialogrutan
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> -egenskap.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-regler så att klientbibliotek kan visas via /etc.clientlibs/.. proxyserver.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor.</p>
    <ul>
     <li>Flytta inte designerbara designer från <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Adobe DTM JavaScript Endpoint {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Ingen åtgärd krävs.</p> <p>Den offentliga föregående platsen fungerar som en proxyslutpunkt för den privata nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Adobe DTM-webbhook-slutpunkt {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Ingen åtgärd krävs.</p> <p>Den offentliga föregående platsen fungerar som en proxyslutpunkt för den privata nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Inkorgsuppgifter {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>Använd <strong>underhållsaktiviteten Rensa inkorg</strong> för att ta bort gamla uppgifter från föregående plats efter behov.</td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Ingen åtgärd krävs för att migrera uppgifter till den nya platsen.</p>
    <ul>
     <li>Uppgifter som finns på den föregående platsen är fortfarande tillgängliga och fungerar.</li>
     <li>Nya uppgifter skapas på den nya platsen.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Designkonfigurationer för hantering av flera webbplatser {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>Föregående plats</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>
    <ol>
     <li>Kopiera anpassade konfigurationer från <code>/etc/blueprints</code> till <code>/apps/msm</code>.</li>
     <li>Ta bort <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Konfigurationer för instrumentpanelswidgetar för AEM projekt {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade AEM Project Dashboard Gadget Configurations måste migreras till den nya platsen (<code>/apps</code>).</p>
    <ol>
     <li>Kopiera alla nya eller ändrade Gadget-konfigurationer för AEM Project Dashboard från föregående plats till den nya platsen (<code>/apps</code>).
      <ol>
       <li>Kopiera inte oförändrade AEM Project Dashboard Gadget Configurations eftersom dessa nu finns på den nya platsen (<code>/libs</code>).</li>
      </ol> </li>
     <li>Uppdatera alla AEM projektmallar som refererar till föregående plats så att de pekar på rätt ny plats.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Om kompatibilitetspaketet AEM 6.4 används måste databasjusteringsaktiviteterna utföras när kompatibilitetspaketet tas bort.</td>
  </tr>
 </tbody>
</table>

### E-postmall för replikeringsmeddelande {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade e-postmallar för replikeringsmeddelanden måste migreras till den nya platsen (<code>/apps</code>)</p>
    <ol>
     <li>Kopiera alla nya eller ändrade e-postmallar för replikeringsmeddelanden från föregående plats till den nya platsen (<code>/apps</code>).</li>
     <li>Ta bort alla e-postmallar för migrerade replikeringsmeddelanden från den tidigare platsen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>De enda nya e-postmallar för replikeringsmeddelanden som stöds är stöd för nya språk.</p> <p>Lösning av e-postmallar för replikeringsmeddelanden sker i följande ordning:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Taggar {#tags}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla taggar måste migreras till <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Kopiera alla taggar från föregående plats till den nya platsen.</li>
     <li>Ta bort alla taggar från föregående plats.</li>
     <li>Via AEM webbkonsol startar du om paketet Day Communique 5 Tagging OSGi på <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> för att AEM att identifiera den nya platsen innehåller innehåll och ska användas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Om du startar om paketet Day Communique Tagging OSGi registreras den nya platsen endast som taggrot om den föregående platsen är tom.</p> <p>Referenser till föregående plats fortsätter att fungera efter migrering till Ny plats för alla funktioner som använder AEM TagManager API för taggupplösning.</p> <p>All anpassad kod som uttryckligen refererar till sökvägen <code>/etc/tags</code> måste uppdateras till <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, eller helst skrivs om för att använda Java-API:t TagManager tillsammans med den här migreringen.</p> </td>
  </tr>
 </tbody>
</table>

### Cloud Services för översättning {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya översättningsadresser måste migreras till den nya Cloud Servicen (<code>/apps</code>, <code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrera befintliga konfigurationer på föregående plats till den nya platsen.
      <ul>
       <li>Återskapa nya översättningskonfigurationer manuellt via redigeringsgränssnittet för AEM på <strong>Verktyg &gt; Cloud Service &gt; Översättningskonfigurationer</strong>.<br /> ELLER </li>
       <li>Kopiera alla nya konfigurationer av översättningsadresser från den tidigare Cloud Servicen till den nya platsen (<code>/apps</code>, <code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associera de tillämpliga AEM med AEM innehållshierarkier.
      <ol>
       <li>AEM Sites sidhierarkier via <strong>AEM Sites &gt; Sida &gt; Sidegenskaper &gt; fliken Avancerat &gt; Molnkonfiguration</strong>.</li>
       <li>AEM Experience Fragment-hierarkier via <strong>AEM Experience Fragments &gt; Experience Fragment &gt; Properties &gt; Cloud Services Tab &gt; Cloud Configuration</strong>.</li>
       <li>AEM Experience Fragment Folder-hierarkier via <strong>AEM Experience Fragments &gt; Folder &gt; Properties &gt; Cloud Services tab &gt; Cloud Configuration</strong>.<br /> </li>
       <li>AEM Assets mapphierarkier via <strong>AEM Assets &gt; Mapp &gt; Mappegenskaper &gt; fliken Cloud Service &gt; Konfiguration</strong>.</li>
       <li>AEM projekt via <strong>AEM Projekt &gt; Projekt &gt; Projektegenskaper &gt; fliken Avancerat &gt; Molnkonfiguration</strong>.</li>
      </ol> </li>
     <li>Avassociera migrerade äldre översättningshierarkier från de tidigare AEM innehållshierarkierna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Översättningens Cloud Service visas i följande ordning:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>Migrerade översättningsfunktioner måste vara kompatibla med AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Översättningsspråk {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya eller ändrade definitioner av översättningsspråk kräver en migrering av alla definitioner av översättningsspråk till den nya platsen (<code>/apps</code>).</p>
    <ol>
     <li>Om några tillägg eller ändringar har gjorts i översättningsspråksdefinitionerna kopierar du alla definitioner för översättningsspråk från föregående plats till den nya platsen (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Sökvägsupplösning för översättningsspråk sker i följande ordning:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Den här upplösningen stöder inte en sammanfogningsövertäckning, vilket innebär att den lösta sökvägen måste innehålla alla språk som stöds och inte ärver språk som stöds från upplösningar i högre ordning.</p> </td>
  </tr>
 </tbody>
</table>

### Översättningsregler {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>En ändrad XML-fil för översättningsregler måste migreras till den nya platsen (<code>/apps</code> eller <code>/conf/global</code>).</p> <p>1. Kopiera den ändrade XML-filen för översättningsregler från föregående plats till den nya platsen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>XML-upplösningen för replikeringsöversättningsregler sker i följande ordning:</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Klientbibliotek för översättningswidget {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>För alla designer som hanteras i SCM och som inte skrivs till vid körning via designdialogrutor.</p>
    <ol>
     <li>Kopiera designen från föregående plats till den nya platsen (/appar).</li>
     <li>Konvertera alla CSS-, JavaScript- och statiska resurser i designen till ett <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">klientbibliotek</a> med <code>allowProxy = true</code>.</li>
     <li>Uppdatera referenser till föregående plats i dialogrutan
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> -egenskap.</li>
     <li>Uppdatera alla sidor som refererar till föregående plats så att den nya kategorin Klientbibliotek används (detta kräver uppdatering av koden för sidimplementering).</li>
     <li>Uppdatera AEM Dispatcher-regler så att klientbibliotek kan visas via /etc.clientlibs/.. proxyserver.</li>
    </ol> <p>För alla designer som INTE hanterats i SCM och som ändrats under körning via designdialogrutor.</p>
    <ul>
     <li>Flytta inte designerbara designer från <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>

### Webbkonsol för träaktivering {#tree-activation-web-console}

| **Föregående plats** | `/etc/replication/treeactivation` |
|---|---|
| **Ny(a) plats(er)** | `/libs/replication/treeactivation` |
| **Omstruktureringsvägledning** | Ingen åtgärd krävs. |
| **Anteckningar** | Webbkonsolen Trädaktivering är nu tillgänglig via **Verktyg > Distribution > Replikering > Aktivera träd**. |

{style="table-layout:auto"}

### Cloud Service för leverantörsöversättningskonnektor {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya Cloud Service för leverantörsöversättningsanslutning måste migreras till den nya platsen (<code>/apps</code>, <code>/conf/global</code> eller <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrera befintliga konfigurationer på den föregående platsen till den nya platsen.
      <ul>
       <li>Skapa manuellt nya konfigurationer av leverantörsöversättningens koppling-Cloud Service via <strong>AEM redigeringsgränssnittet på Verktyg &gt; Cloud Service &gt; ÖversättningsCloud Service</strong>.<br /> ELLER </li>
       <li>Kopiera alla nya konfigurationer för leverantörsöversättningsanslutning från den tidigare Cloud Servicen till den nya platsen (<code>/apps</code>, <code>/conf/global </code> eller <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associera de tillämpliga AEM med AEM innehållshierarkier.
      <ol>
       <li>AEM Sites sidhierarkier via <strong>AEM Sites &gt; Sida &gt; Sidegenskaper &gt; fliken Avancerat &gt; Molnkonfiguration</strong>.</li>
       <li>AEM Experience Fragment-hierarkier via <strong>AEM Experience Fragments &gt; Experience Fragment &gt; Properties &gt; Cloud Services Tab &gt; Cloud Configuration</strong>.</li>
       <li>AEM Experience Fragment Folder-hierarkier via <strong>AEM Experience Fragments &gt; Folder &gt; Properties &gt; Cloud Services tab &gt; Cloud Configuration</strong>.</li>
       <li>AEM Assets mapphierarkier via <strong>AEM Assets &gt; Mapp &gt; Mappegenskaper &gt; fliken Cloud Service &gt; Konfiguration</strong>.</li>
       <li>AEM projekt via <strong>AEM Projekt &gt; Projekt &gt; Projektegenskaper &gt; fliken Avancerat &gt; Molnkonfiguration</strong>.</li>
      </ol> </li>
     <li>Avassociera migrerade äldre översättningshierarkier från de tidigare AEM innehållshierarkierna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Översättningens Cloud Service visas i följande ordning:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### E-postmallar för arbetsflödesmeddelanden {#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla ändrade e-postmallar för arbetsflödesmeddelanden måste migreras till den nya platsen (<code>/conf/global</code>).</p>
    <ol>
     <li>Kopiera ändrade e-postmallar för arbetsflödesmeddelanden från föregående plats till den nya platsen.</li>
     <li>Ta bort migrerade e-postmallar för arbetsflödesmeddelanden från föregående plats.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Lösning av e-postmall för arbetsflödesmeddelande sker i följande ordning:</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Arbetsflödespaket {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Befintliga arbetsflödespaket på den tidigare platsen bör migreras till den nya platsen.</p>
    <ol>
     <li>Ta bort alla arbetsflödespaket på den föregående platsen som inte refereras av annat innehåll och som annars inte behövs.</li>
     <li>Flytta eventuella arbetsflödespaket på den föregående platsen som inte refereras av annat innehåll, men som i övrigt krävs på den nya platsen.</li>
     <li>Lämna eventuella arbetsflödespaket som refereras av annat innehåll på föregående plats.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td><p>Arbetsflödespaket som skapats via den klassiska användargränssnittskonsolen bevaras på den tidigare platsen, medan alla andra bevaras på den nya platsen.</p> <p>Arbetsflödespaket som lagras på en tidigare eller mindre plats kan hanteras via den klassiska UI Miscadmin-konsolen.</p> </td>
  </tr>
 </tbody>
</table>
