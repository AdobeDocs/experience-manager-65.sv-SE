---
title: Omstrukturering av e-handelslager i AEM 6.5
seo-title: Omstrukturering av e-handelslager i AEM 6.5
description: Lär dig hur du gör nödvändiga ändringar för att migrera till den nya databasstrukturen i AEM 6.5 för e-handel.
seo-description: Lär dig hur du gör nödvändiga ändringar för att migrera till den nya databasstrukturen i AEM 6.5 för e-handel.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Uppgraderar
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Omstrukturering av databas för e-handel i AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Som beskrivs på den överordnade sidan [Databasomstrukturering på AEM 6.5](/help/sites-deploying/repository-restructuring.md) bör kunder som uppgraderar till AEM 6.5 använda den här sidan för att bedöma arbetsinsatsen i samband med databasändringar som påverkar AEM e-handelslösning. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

## Med 6.5-uppgradering {#with-upgrade}

### Produkt-, order-, samlings-, klassificerings-, leveranssätt- och betalningsmetoder - data {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Föregående plats</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Ny plats(er)</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Omstruktureringsvägledning</strong></td>
   <td><p>Du kan använda en <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Lazy Migration</a>-åtgärd för att migrera e-handelsdata.</p> <p>Följande steg utförs:</p>
    <ul>
     <li>justerar referenser till gammal plats så att de pekar på ny plats</li>
     <li>flyttar innehåll från den gamla platsen till den nya</li>
     <li>tar bort gammal plats för att till slut aktivera användningen av ny plats i hela systemet</li>
    </ul> <p>Platserna som ska täckas av uppgiften är:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>För större kataloger rekommenderar vi att du kör migreringsaktiviteten för e-handel separat genom att skicka följande Java-systemegenskap till AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Efter migreringen AEM en omstart krävs.</p> </td>
  </tr>
  <tr>
   <td><strong>Anteckningar</strong></td>
   <td>Ej tillämpligt<br /> </td>
  </tr>
 </tbody>
</table>

