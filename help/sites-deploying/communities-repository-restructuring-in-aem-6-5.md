---
title: Repositionsomstrukturering för AEM Communities i 6.4
description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.4 for Communities.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Repositionsomstrukturering för AEM Communities i 6.5 {#repository-restructuring-for-aem-communities-in}

Så som beskrivs på den överordnade sidan [Databasomstrukturering på sidan AEM 6.4](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till AEM 6.5 använda den här sidan för att utvärdera arbetsinsatsen som är kopplad till databasändringar som påverkar AEM Communities-lösningen. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Med 6.5-uppgradering**

* [E-postmeddelandemallar](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Prenumerationskonfigurationer](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Före framtida uppgradering**

* [Konfigurationer för märkning](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Konsoldesigner för klassiska communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook Social Login Configurations](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Konfigurationer av språkalternativ](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest Social Login Configurations](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Bedömningskonfigurationer](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Konfigurationer för social inloggning för twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Diverse](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Med 6.5-uppgradering {#with-upgrade}

### E-postmeddelandemallar {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Manuell migrering krävs om du vill gå till en ny sökväg under <code>/apps/settings</code>. Du kan använda konfigurationshanteraren för Granite för att utföra migreringen.</p> <p>Du kan utföra migreringen genom att ange egenskapen <code>mergeList</code> till <code>true</code> på noden <code>/libs/settings/community/subscriptions</code> och lägga till en underordnad <code>nt:unstructured</code>-nod.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Prenumerationskonfigurationer {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Manuell migrering krävs om du vill gå till en ny sökväg under <code>/apps/settings</code>. Du kan använda konfigurationshanteraren för Granite för att utföra migreringen.</p> <p>Du kan utföra migreringen genom att ange egenskapen <code>mergeList</code> till <code>true</code> på noden <code>/libs/settings/community/subscriptions</code> och lägga till en underordnad <code>nt:unstructured</code>-nod.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Konfigurationer för watchwords {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>Det finns en aktivitet för Azure-migrering som rensar webbgruppskonfigurationerna.<br /> <p>Uppgiften flyttar bevakningsord från <code>/etc/watchwords</code> till <code>/conf/global/settings/community/watchwords</code>.</p> <p>Om anpassade bevakningsord lagras i SCM bör de distribueras till <code>/apps/settings/...</code> och du måste se till att det inte finns någon överliggande <code>/conf/global/settings/...</code>-konfiguration som har företräde.</p> <p>Migreringsaktiviteten tar bort <code>/etc</code> platser.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

## Före framtida uppgradering {#prior-to-upgrade}

### Konfigurationer för märkning {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><strong>Badge Rules:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Bilder:</strong></p> <p>För standardbilder: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>För anpassade bilder: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Manuell migrering krävs.</p> <p>Om instansen har anpassat reglerna för märkning/poängsättning finns det inget automatiskt sätt att placera alla regler under en bucket. Kundernas inmatningar behöver den konf-bucket (global eller platsspecifik) som du vill använda för din webbplats.</p> <p>Det finns inget tillgängligt gränssnitt för att konfigurera märkning och poängsättning för en plats.</p> <p>Så här anpassar du dig till den nya databasstrukturen:</p>
    <ol>
     <li>Skapa en platskontextbucket med <strong>Configuration Browser</strong> under <strong>Tools</strong></li>
     <li>Gå till platsroten</li>
     <li>Ange <code>cq:confproperty</code> till den bucketsökväg där du vill lagra alla dina inställningar. Samma sak kan anges via webbplatsen <strong>Redigera guide - Ange molnkonfigurationsindata</strong>.</li>
     <li>Flytta relevanta regler för märkning och poängsättning från <code>/etc/community/*</code> till webbplatskontextgruppen som skapades i föregående steg.</li>
     <li>Justera egenskaperna för badging-regler och bedömningsregler i platsroten för att få relativa referenser till nya regelplatser.
      <ol>
       <li>Om till exempel egenskapen för <code>cq:conf = /conf/we-retail</code> flyttas <code>badgingRules [] = community/badging/rules</code> om regler nu till den nya bucket.</li>
      </ol> </li>
     <li>På samma sätt kan du justera referenserna för poängregler i en nod med en badging-regel så att de har en relativ sökväg.</li>
    </ol> <p> </p> <p>Rensa slutligen genom att ta bort resursen <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Konsoldesigner för klassiska communities {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Facebook Social Login Configurations {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya Facebook Cloud-konfigurationer måste migreras till den nya platsen.</p>
    <ol>
     <li>Migrera befintliga konfigurationer på den föregående platsen till den nya platsen.
      <ol>
       <li>Återskapa nya Facebook Social Login Configurations manuellt via redigeringsgränssnittet för AEM på <strong>Verktyg &gt; Cloud Service &gt; Facebook Social Login Configuration</strong>.<br /> eller <br /> </li>
       <li>Kopiera alla nya Facebook Cloud-konfigurationer från föregående plats till lämplig ny plats, under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Uppdatera valfri AEM Communities-platsrot så att den refererar till den nya konfigurationen för Facebook Social Login genom att ange egenskapen <code>[cq:Page]/jcr:content@cq:conf</code> till den absoluta sökvägen i den nya platsen.</li>
     <li>Avassociera den gamla Facebook Connect-Cloud Servicen från alla AEM Communities webbplatsrötter som har uppdaterats för att referera till den nya platsen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Konfigurationer av språkalternativ {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Pinterest Social Login Configurations {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya Pinterest Cloud-konfigurationer måste migreras till den nya platsen.</p>
    <ol>
     <li>Migrera befintliga konfigurationer på den föregående platsen till den nya platsen.
      <ol>
       <li>Återskapa nya Pinterest Social Login Configurations manuellt via redigeringsgränssnittet för AEM på <strong>Verktyg &gt; Cloud Service &gt; Pinterest Social Login Configuration</strong>.<br /> eller</li>
       <li>Kopiera alla nya Pinterest Cloud-konfigurationer från föregående plats till lämplig ny plats under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Uppdatera valfri AEM Communities-platsrot så att den refererar till den nya konfigurationen för Pinterest Social Login genom att ställa in egenskapen <code>[cq:Page]/jcr:content@cq:conf</code> på den absoluta sökvägen i den nya platsen.</li>
     <li>Avassociera den gamla Pinterest Connect-Cloud Servicen från alla AEM Communities webbplatsrötter som har uppdaterats för att referera till den nya platsen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Bedömningskonfigurationer {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Om du vill anpassa till den nya databasstrukturen kan poängsättningsreglerna lagras i <code>/apps/settings/</code> eller /<code>conf/.../settings</code></p>
    <ol>
     <li>För <code>/apps/settings</code> fungerar detta som globala regler eller standardregler som hanteras i SCM.</li>
    </ol> <p>Skapa kontextmedvetna konfigurationer i <code>/conf/</code> med CRXDELite:</p>
    <ol>
     <li>Skapa konfigurationerna på önskad <code>/conf/.../settings</code>-plats<br /> </li>
     <li>Egenskapen <code>cq:conf </code> måste ha angetts för webbgruppsplatsen.
      <ol>
       <li>Om <code>cq:conf</code> inte anges läses bedömningsreglerna direkt från den angivna sökvägen för egenskapen <code>scoringRules</code> i platsens rotnod, till exempel: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Rensa: Ta bort resursen <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

### Konfigurationer för social inloggning för twitter {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Alla nya Twitter Cloud-konfigurationer måste migreras till den nya platsen.</p>
    <ol>
     <li>Migrera befintliga konfigurationer på den föregående platsen till den nya platsen.
      <ol>
       <li>Återskapa nya Twitter för konfiguration för social inloggning manuellt via redigeringsgränssnittet för AEM på <strong>Verktyg &gt; Cloud Service &gt; Twitter konfiguration för social inloggning</strong>.<br /> eller <br /> </li>
       <li>Kopiera alla nya Twitter Cloud-konfigurationer från föregående plats till lämplig ny plats, under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Uppdatera en AEM Communities-platsrot så att den refererar till den nya Twitternas konfiguration för social inloggning genom att ange egenskapen <code>[cq:Page]/jcr:content@cq:conf</code> till den absoluta sökvägen i den nya platsen.</li>
     <li>Koppla inte bort den gamla Twitter Connect-Cloud Servicen från några av AEM Communities webbplatsrötter som har uppdaterats för att referera till den nya platsen.</li>
    </ol> </td>
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
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Adobe har tillhandahållit ett migreringsverktyg på:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>De befintliga anpassade mallarna skulle gå över till <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
