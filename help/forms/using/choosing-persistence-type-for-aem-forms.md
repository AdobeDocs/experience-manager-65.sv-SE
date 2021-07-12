---
title: Välja en beständig typ för en AEM Forms-installation
seo-title: Välja en beständig typ för en AEM Forms-installation
description: Välj en beständig typ klokt. Det hjälper er att bygga en effektiv och skalbar AEM Forms-miljö.
seo-description: Välj en beständig typ klokt. Det hjälper er att bygga en effektiv och skalbar AEM Forms-miljö.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# Välja en beständig typ för en AEM Forms-installation {#choosing-a-persistence-type-for-an-aem-forms-installation}

Välj en beständig typ klokt. Det hjälper er att bygga en effektiv och skalbar AEM Forms-miljö.

Persistence är ett sätt att lagra innehåll på de fysiska lagren. Den definierar den faktiska datastrukturen och lagringsmekanismen för data. MicroKernels fungerar som persistencehanterare i AEM Forms. AEM Forms stöder persistence (MicroKernals) av typen tarMK, MongoMK och RDBMK. Du kan välja en beständighetstyp för AEM Forms beroende på syfte och distributionstyp (Single-Server, Farm eller Cluster) för en AEM Forms-instans.

>[!NOTE]
>
>LiveCycle ES4 SP1 använder tarPM-beständighet för att lagra innehåll.

I följande tabell visas alla beständighetstyper som stöds tillsammans med olika parametrar som hjälper dig att välja en beständig typ för din miljö:

<table>
 <tbody>
  <tr>
   <th><strong>Installationstyp / Kostnad</strong></th>
   <th><strong>tarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Fristående installation</strong></th>
   <td>Stöds<br /> </td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <th><strong>Klusterinställning</strong></th>
   <td>Stöds ej</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <th><strong>Licenskostnad</strong></th>
   <td>Ingår i AEM </td>
   <td>Separat licens krävs</td>
   <td>Separat licens krävs</td>
  </tr>
 </tbody>
</table>

tarMK är utformat för prestanda, medan MongoMK och RDBMK är utformade för skalbarhet. Adobe rekommenderar starkt att TjäraMK används som standardbeständighetsteknik för alla AEM Forms-distributionsscenarier, både för författare- och publiceringsinstanser, utom i de fall som beskrivs i avsnittet [Välja Mongo eller en relationsdatabasmikrokärna över TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

En lista över mikrokärnor som stöds finns i [AEM Forms on OSGi Technical Requirements](/help/sites-deploying/technical-requirements.md) eller [AEM Forms on JEE supported platform combinations](/help/forms/using/aem-forms-jee-supported-platforms.md)-artiklar.

## Välja Mongo eller en relationsdatabasmikrokärna över tarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

En skalbar (klustrad) AEM Forms-miljö är en uppsättning med två eller flera horisontellt konfigurerade aktiva författarinstanser. Du kan välja att köra mer än en författarinstans om en enda server med stöd för alla samtidiga redigeringsaktiviteter inte längre är hållbar.

Endast beständighetstypen MongoMK och RDBMK stöds för en skalbar (klustrad) AEM Forms i JEE-miljö. Antalet servrar eller storleken på den skalbara miljön varierar för varje installation. En lista med överväganden och exempel finns i [Recommended Deployments](/help/sites-deploying/recommended-deploys.md) och [Architecture and deployment topologies for AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). Du kan även kontakta AEM Forms support för mer information om kapacitetsplanering för AEM Forms med RDBMK och tarMK.
