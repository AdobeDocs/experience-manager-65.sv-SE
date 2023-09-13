---
title: Omstrukturering av e-handelslager i AEM 6.5
description: Lär dig hur du gör nödvändiga ändringar för att migrera till den nya databasstrukturen i AEM 6.5 för e-handel.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Omstrukturering av e-handelslager i AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Enligt beskrivning på överordnad [Omstrukturering av lager i AEM 6.5](/help/sites-deploying/repository-restructuring.md) på denna sida bör kunder som uppgraderar till AEM 6.5 använda denna sida för att bedöma arbetsinsatsen i samband med databasändringar som påverkar AEM e-handelslösning. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

## Med 6.5-uppgradering {#with-upgrade}

### Produkt-, order-, samlings-, klassificerings-, leveranssätt- och betalningsmetoder {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nya platser</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Du kan använda en <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Lazy Migration</a> uppgift att migrera e-handelsdata.</p> <p>Följande steg utförs:</p>
    <ul>
     <li>justerar referenser till den gamla platsen så att de pekar på den nya platsen</li>
     <li>flyttar innehåll från den gamla platsen till den nya</li>
     <li>tar bort den gamla platsen för att till slut aktivera användningen av den nya platsen i hela systemet</li>
    </ul> <p>Platserna som ska täckas av uppgiften är:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>För större kataloger rekommenderar Adobe att du kör migreringsaktiviteten för e-handel separat genom att skicka följande Java™-systemegenskap till AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Starta om AEM efter migreringen.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>
