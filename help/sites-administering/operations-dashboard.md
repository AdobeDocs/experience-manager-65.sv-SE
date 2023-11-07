---
title: Instrumentpanel för åtgärder
seo-title: Operations Dashboard
description: Lär dig hur du använder kontrollpanelen för åtgärder i Adobe Experience Manager.
seo-description: Learn how to use the Operations Dashboard.
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: Operations
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '6057'
ht-degree: 0%

---

# Instrumentpanel för åtgärder {#operations-dashboard}

## Introduktion {#introduction}

På kontrollpanelen för åtgärder i AEM 6 kan systemansvariga övervaka AEM systemhälsan snabbt. Den innehåller även automatiskt genererad diagnos om relevanta aspekter av AEM och gör att du kan konfigurera och köra självständig automatisering av underhåll för att avsevärt minska projektdriften och supportärenden. Kontrollpanelen för åtgärder kan utökas med anpassade hälsokontroller och underhållsuppgifter. Data från Operations Dashboard kan dessutom nås från externa övervakningsverktyg via JMX.

**Kontrollpanelen för åtgärder:**

* Är en enklickssystemstatus som hjälper verksamhetstjänsterna att bli effektivare
* Ger en översikt över systemets hälsa på en central plats
* Minskar tiden för att hitta, analysera och åtgärda problem
* Automatisering av underhåll som kan minska projektkostnaderna avsevärt

Den kan nås genom att **verktyg** - **Operationer** på AEM välkomstskärm.

>[!NOTE]
>
>För att få åtkomst till kontrollpanelen för åtgärder måste den inloggade användaren vara en del av användargruppen Operatorer. Mer information finns i dokumentationen om [Administrera användare, grupper och åtkomsträttigheter](/help/sites-administering/user-group-ac-admin.md).

## Hälsorapporter {#health-reports}

I systemet för hälsorapporter finns information om hälsotillståndet i en AEM via Sling Health Checks. Du uppnår detta antingen genom OSGI-, JMX-, HTTP-begäranden (via JSON) eller genom Touch-gränssnittet. Den erbjuder mått och tröskelvärden för vissa konfigurerbara räknare och ibland ger den information om hur problemet kan lösas.

Den har flera funktioner som beskrivs nedan.

## Hälsokontroller {#health-checks}

The **Hälsorapporter** är ett kortsystem som indikerar god eller dålig hälsa i ett visst produktområde. Dessa kort är visualiseringar av Sling Health Checks, som samlar in data från JMX och andra källor och visar bearbetad information igen som MBeans. Dessa MBeans kan också granskas i [JMX-webbkonsol](/help/sites-administering/jmx-console.md), under **org.apache.sling.healthCheck** domän.

Du kommer åt gränssnittet Hälsorapporter via **verktyg** - **Operationer** - **Hälsorapporter** på AEM välkomstskärm eller direkt via följande URL:

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

Kortsystemet visar tre möjliga lägen: **OK**, **VARNING** och **KRITISK**. Lägen är ett resultat av regler och tröskelvärden, som kan konfigureras genom att du håller muspekaren över kortet och sedan klickar på kugghjulsikonen i åtgärdsfältet:

![chlimage_1-117](assets/chlimage_1-117.png)

### Typ av hälsokontroll {#health-check-types}

Det finns två typer av hälsokontroller i AEM 6:

1. Individuella hälsokontroller
1. Sammansatta hälsokontroller

An **Individuell hälsokontroll** är en enda hälsokontroll som motsvarar ett statuskort. Enskilda hälsokontroller kan konfigureras med regler eller tröskelvärden och de kan ge ett eller flera tips och länkar för att lösa identifierade hälsoproblem. Låt oss ta kontrollen &quot;Loggfel&quot; som exempel: om det finns FEL-poster i instansloggarna kan du hitta dem på informationssidan i hälsokontrollen. Längst upp på sidan finns en länk till analysverktyget för loggmeddelanden i avsnittet Diagnosverktyg, där du kan analysera felen mer i detalj och konfigurera om loggarna.

A **Sammansatt hälsokontroll** är en kontroll som sammanställer information från flera enskilda kontroller.

Sammansatta hälsokontroller konfigureras med hjälp av **filtertaggar**. Alla enskilda kontroller som har samma filtertagg grupperas alltså som en sammansatt hälsokontroll. En sammansatt hälsokontroll har bara statusen OK om alla enskilda kontroller som den sammanställer också har OK-status.

### Så här skapar du hälsokontroller {#how-to-create-health-checks}

På kontrollpanelen för åtgärder kan du visualisera resultatet av både individuella och sammansatta hälsokontroller.

### Skapa en enskild hälsokontroll {#creating-an-individual-health-check}

Att skapa en enskild hälsokontroll består av två steg: implementera en hälsokontroll vid enkel inloggning och lägga till en post för hälsokontrollen på kontrollpanelens konfigurationsnoder.

1. Skapa en OSGI-komponent som implementerar Sling HealthCheck-gränssnittet om du vill skapa en Sling-hälsokontroll. Lägg till den här komponenten i ett paket. Komponentens egenskaper identifierar hälsokontrollen fullständigt. När komponenten har installerats skapas en JMX MBean automatiskt för hälsokontrollen. Se [Dokumentation för hälsokontroll vid segmentering](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) för mer information.

   Exempel på en Sling Health Check-komponent, skriven med OSGI-tjänstkomponentsanteckningar:

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >The `MBEAN_NAME` -egenskapen definierar namnet på den böna som genereras för den här hälsokontrollen.

1. När du har skapat en hälsokontroll måste en ny konfigurationsnod skapas för att den ska bli tillgänglig i gränssnittet för kontrollpanelen för åtgärder. I detta steg är det nödvändigt att känna till JMX-namnet på hälsokontrollen ( `MBEAN_NAME` egenskap). Om du vill skapa en konfiguration för hälsokontrollen öppnar du CRXDE och lägger till en nod (av typen **nt:ostrukturerad**) under följande sökväg: `/apps/settings/granite/operations/hc`

   Följande egenskaper ska anges för den nya noden:

   * **Namn:** `sling:resourceType`

      * **Typ:** `String`
      * **Värde:** `granite/operations/components/mbean`

   * **Namn:** `resource`

      * **Typ:** `String`
      * **Värde:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >Resurssökvägen ovan skapas så här: Om huvudnamnet för hälsokontrollen är &quot;test&quot; lägger du till &quot;test&quot; i slutet av sökvägen `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
   >
   >Så den sista banan är följande:
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >Se till att `/apps/settings/granite/operations/hc` path har följande egenskaper inställda på true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >Den här processen instruerar konfigurationshanteraren att sammanfoga de nya konfigurationerna med de befintliga från `/libs`.

### Skapa en sammansatt hälsokontroll {#creating-a-composite-health-check}

En sammansatt hälsokontroll har till uppgift att sammanställa flera enskilda hälsokontroller som delar en uppsättning gemensamma funktioner. Den sammansatta hälsokontrollen för Säkerhet grupperar till exempel alla enskilda hälsokontroller som utför säkerhetsrelaterade kontroller. Det första steget för att skapa en sammansatt kontroll är att lägga till en OSGI-konfiguration. För att den ska kunna visas på kontrollpanelen för åtgärder måste en ny konfigurationsnod läggas till på samma sätt som en enkel kontroll.

1. Gå till Web Configuration Manager i OSGI-konsolen. Öppna `https://serveraddress:port/system/console/configMgr`
1. Sök efter den anropade posten **Apache Sling Composite Health Check**. När du har hittat den bör du tänka på att det redan finns två konfigurationer: en för systemkontrollerna och en annan för säkerhetskontrollerna.
1. Skapa en konfiguration genom att trycka på plusknappen (+) till höger om konfigurationen. Ett nytt fönster visas enligt nedan:

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. Skapa en konfiguration och spara den. En böna skapas med den nya konfigurationen.

   Syftet med varje konfigurationsegenskap är följande:

   * **Namn (hc.name):** Namnet på den sammansatta hälsokontrollen. Ett beskrivande namn rekommenderas.
   * **Taggar (hc.tags):** Taggarna för den här hälsokontrollen. Om den här sammansatta hälsokontrollen är avsedd att ingå i en annan sammansatt hälsokontroll (till exempel i en hierarki av hälsokontroller) lägger du till de taggar som den sammansatta kontrollen är relaterad till.
   * **MBean-namn (hc.mbean.name):** Namnet på den Mbean som ges till JMX MBean för den här sammansatta hälsokontrollen.
   * **Filtertaggar (filter.tags):** Egenskapen som är specifik för sammansatta hälsokontroller. Dessa taggar sammanställs av det sammansatta. Den sammansatta hälsokontrollen aggregerar under sin grupp alla hälsokontroller som har en tagg som matchar någon av filtertaggarna i den här sammansatta sammansättningen. En sammansatt hälsokontroll med till exempel filtertaggarna **test** och **check**, sammanställer alla individuella och sammansatta hälsokontroller som har någon av **test** och **check** taggar i deras taggegenskap ( `hc.tags`).

   >[!NOTE]
   >
   >En ny JMX Mbean skapas för varje ny konfiguration av den sammansatta hälsokontrollen för Apache Sling.**

1. Slutligen måste posten för den sammansatta hälsokontrollen som har skapats läggas till i konfigurationsnoderna för kontrollpanelen för åtgärder. Proceduren är densamma som för individuella hälsokontroller: en nod av typen **nt:ostrukturerad** måste skapas under `/apps/settings/granite/operations/hc`. Egenskapen resource för noden definieras av värdet för **hc.ean.name** i OSGI-konfigurationen.

   Om du till exempel har skapat en konfiguration och ställt in **hc.mbean.name** värde till **diskus** ser konfigurationsnoderna ut så här:

   * **Namn:** `Composite Health Check`

      * **Typ:** `nt:unstructured`

   Med följande egenskaper:

   * **Namn:** `sling:resourceType`

      * **Typ:** `String`
      * **Värde:** `granite/operations/components/mbean`

   * **Namn:** `resource`

      * **Typ:** `String`
      * **Värde:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >Om du skapar enskilda hälsokontroller som logiskt sett hör till en sammansatt kontroll som redan finns på kontrollpanelen som standard, hämtas de automatiskt och grupperas under respektive sammansatta kontroll. Därför behöver du inte skapa en konfigurationsnod för dessa kontroller.
   >
   >Om du till exempel skapar en enskild säkerhetshälsokontroll tilldelar du den värdet **säkerhet**-taggen och den är installerad. Den visas automatiskt under den sammansatta kontrollen Säkerhetskontroller på kontrollpanelen för åtgärder.

### Hälsokontroller som tillhandahålls med AEM {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>zHealthcheck-namn</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Frågeprestanda</td>
   <td><p>Den här hälsokontrollen har förenklats <strong>i AEM 6.4</strong>och kontrollerar nu den nyligen omarbetade <code>Oak QueryStats</code> MBean, mer specifikt <code>SlowQueries </code>-attribut. Om statistiken innehåller långsamma frågor returnerar hälsokontrollen en varning. I annat fall returneras OK-statusen.<br /> </p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=queriesStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Längd på observationskö</td>
   <td><p>Längden på observationskön itererar över alla händelseavlyssnare och bakgrundsobservrar och jämför deras <code>queueSize </code>till sina <code>maxQueueSize</code> och:</p>
    <ul>
     <li>returnerar Kritisk status om <code>queueSize</code> värdet överskrider <code>maxQueueSize</code> värde (d.v.s. när händelser tas bort)</li>
     <li>returnerar Varna om <code>queueSize</code> värdet är över <code>maxQueueSize * WARN_THRESHOLD</code> (standardvärdet är 0,75) </li>
    </ul> <p>Den maximala längden för varje kö kommer från olika konfigurationer (Oak och AEM) och kan inte konfigureras från den här hälsokontrollen. MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=ObservationQueueLengthHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Gränser för genomgång av frågor</td>
   <td><p>Gränser för frågesport kontrollerar <code>QueryEngineSettings</code> MBean, mer specifikt <code>LimitInMemory</code> och <code>LimitReads</code> och returnerar följande status:</p>
    <ul>
     <li>returnerar varningsstatus om en av gränserna är lika med eller högre än <code>Integer.MAX_VALUE</code></li>
     <li>returnerar varningsstatus om en av gränserna är lägre än 10000 (den rekommenderade inställningen från Oak)</li>
     <li>returnerar statusen Kritisk om <code>QueryEngineSettings</code> eller någon av gränserna inte kan hämtas</li>
    </ul> <p>The Mbean for this health check is <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=queryTraversalLimitsBundle,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Synkroniserade klockor</td>
   <td><p>Den här kontrollen gäller endast för <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">dokumentnodestore-kluster</a>. Den returnerar följande status:</p>
    <ul>
     <li>returnerar Warn-status när instansklockorna inte är synkroniserade och går över ett fördefinierat lågt tröskelvärde</li>
     <li>returnerar statusen Kritisk när instansklockorna inte är synkroniserade och går över ett fördefinierat högt tröskelvärde</li>
    </ul> <p>The Mbean for this health check is <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=slingDiscoveryOakSynchronizedClocks,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Asynkrona index</td>
   <td><p>Kontrollen Asynkrona index:</p>
    <ul>
     <li>returnerar Kritisk status om minst ett indexeringsfält misslyckas</li>
     <li>kontrollerar <code>lastIndexedTime</code> för alla indexeringsbanor och
      <ul>
       <li>returnerar Kritisk status om det är mer än 2 timmar sedan </li>
       <li>returnerar varningsstatus om det är mellan 2 timmar och 45 minuter sedan </li>
       <li>returnerar OK-status om det är mindre än 45 minuter sedan </li>
      </ul> </li>
     <li>om inget av dessa villkor uppfylls returneras OK-statusen</li>
    </ul> <p>Både statuströskelvärdena Kritisk och Varna är konfigurerbara. The Mbean for this health check is <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=asyncIndexHealthCheck,type=HealthCheck</a>.</p> <p><strong>Obs! </strong>Den här hälsokontrollen är tillgänglig i AEM 6.4 och har flyttats tillbaka till AEM 6.3.0.1.</p> </td>
  </tr>
  <tr>
   <td>Stora Lucene-index</td>
   <td><p>Den här kontrollen använder data som exponeras av <code>Lucene Index Statistics</code> MBean för att identifiera stora index och returnera:</p>
    <ul>
     <li>en varningsstatus om det finns ett index med mer än 1 miljard dokument</li>
     <li>en kritisk status om det finns ett index med mer än 1,5 miljarder dokument</li>
    </ul> <p>Tröskelvärdena kan konfigureras och MBean för hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=largeIndexHealthCheck,type=HealthCheck.</a></p> <p><strong>Obs! </strong>Den här kontrollen är tillgänglig i AEM 6.4 och har flyttats tillbaka till AEM 6.3.2.0.</p> </td>
  </tr>
  <tr>
   <td>Systemunderhåll</td>
   <td><p>Systemunderhåll är en sammansatt kontroll som returnerar OK om alla underhållsåtgärder körs som de är konfigurerade. Kom ihåg att:</p>
    <ul>
     <li>varje underhållsåtgärd åtföljs av en tillhörande hälsokontroll</li>
     <li>Om en uppgift inte läggs till i ett underhållsfönster returneras Critical-kontrollen</li>
     <li>konfigurera underhållsuppgifterna för granskningslogg och tömning av arbetsflöde eller på annat sätt ta bort dem från underhållsfönstren. Om dessa uppgifter inte är konfigurerade misslyckas de vid den första körningen, så systemunderhållskontrollen returnerar statusen Kritisk.</li>
     <li><strong>Med AEM 6.4</strong>, finns det också en kontroll för <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Lucene Binaries-underhåll</a> uppgift</li>
     <li>på AEM 6.2 och lägre returnerar systemunderhållskontrollen en varningsstatus direkt efter start eftersom aktiviteterna aldrig körs. Från och med 6.3 returneras OK om det första underhållsfönstret inte har nåtts ännu.</li>
    </ul> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=systemchecks,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Replikeringskö</td>
   <td><p>Den här kontrollen itererar över replikeringsagenter och tittar på deras köer. För objektet högst upp i kön kontrolleras hur många gånger agenten försökte replikera på nytt. Om agenten gjorde ett nytt försök att replikera mer än värdet för <code>numberOfRetriesAllowed</code> returnerar den en varning. The <code>numberOfRetriesAllowed</code> parametern kan konfigureras. </p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=replicationQueue,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Försäljningsjobb</td>
   <td>
    <div>
      Sling Jobs kontrollerar antalet jobb som köas i JobManager, jämför det med
     <code>maxNumQueueJobs</code> och
    </div>
    <ul>
     <li>returnerar Critical om mer än <code>maxNumQueueJobs</code> finns i kön</li>
     <li>returnerar Kritisk om det finns aktiva jobb som körs länge och är äldre än 1 timme</li>
     <li>returnerar Kritisk om det finns jobb i kö och den senaste slutförda jobbtiden är äldre än 1 timme</li>
    </ul> <p>Endast parametern för maximalt antal jobb i kö kan konfigureras och har standardvärdet 1 000.</p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=slingJobs,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Begär prestanda</td>
   <td><p>Den här kontrollen tittar på <code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">Sling-mått </a>och:</p>
    <ul>
     <li>returnerar Kritisk om det 75:e percentilvärdet överstiger det kritiska tröskelvärdet (standardvärdet är 500 millisekunder)</li>
     <li>returnerar Varna om det 75:e percentilvärdet överstiger varningströskeln (standardvärdet är 200 millisekunder)</li>
    </ul> <p>MBean för den här hälsokontrollen är<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=requestsStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Loggfel</td>
   <td><p>Den här kontrollen returnerar varningsstatus om loggen innehåller fel.</p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=logErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Diskutrymme</td>
   <td><p>Kontrollen av diskutrymme finns på <code>FileStoreStats</code> MBean, hämtar storleken på nodarkivet och hur mycket diskutrymme som kan användas på partitionen Node Store, och:</p>
    <ul>
     <li>returnerar Varna om det tillgängliga diskutrymmet till databasstorleken är mindre än varningströskeln (standardvärdet är 10)</li>
     <li>returnerar Kritisk om det användbara diskutrymmet till databasstorleken är mindre än det kritiska tröskelvärdet (standardvärdet är 2)</li>
    </ul> <p>Båda tröskelvärdena kan konfigureras. Kontrollen fungerar bara på instanser med ett segmentlager.</p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=DiskSpaceHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Hälsokontroll för schemaläggare</td>
   <td><p>Den här kontrollen returnerar en varning om instansen har Quartz-jobb som körs i mer än 60 sekunder. Tröskelvärdet för acceptabel varaktighet är konfigurerbart.</p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=slingCommonsSchedulerHealthCheck,type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>Säkerhetskontroller</td>
   <td><p>Säkerhetskontrollen är en sammansatt kontroll som sammanställer resultaten av flera säkerhetsrelaterade kontroller. Dessa individuella hälsokontroller tar upp andra problem än checklistan för säkerhet på <a href="/help/sites-administering/security-checklist.md">Dokumentationssida för checklista för säkerhet.</a> Kontrollen är användbar som säkerhetsröktest när instansen startas. </p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=securityCheck,type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>Aktiva paket</td>
   <td><p>Active Bundles kontrollerar statusen för alla paket och:</p>
    <ul>
     <li>returnerar Warn-status om något av paketen inte är aktivt eller (med start, med lat aktivering)</li>
     <li>ignorerar paketens status i ignoreringslistan</li>
    </ul> <p>Parametern för ignoreringslistan kan konfigureras.</p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.hälsokontroll:name=inactiveBundles,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Kontroll av kodcache</td>
   <td><p>En hälsokontroll som verifierar flera JVM-förhållanden som kan utlösa ett CodeCache-fel i Java™ 7:</p>
    <ul>
     <li>returnerar Varna om instansen körs på Java™ 7, med tömning av kodcache aktiverat</li>
     <li>returnerar Varna om instansen körs på Java™ 7 och storleken på den reserverade kodcachen är mindre än ett minimivärde (standardvärdet är 90 MB)</li>
    </ul> <p>The <code>minimum.code.cache.size</code> tröskelvärdet kan konfigureras. Mer information om felet finns i <a href="https://bugs.java.com/bugdatabase/"> och sök sedan på fel ID 8012547</a>.</p> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=codeCacheHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Sökvägsfel för resurssökning</td>
   <td><p>Kontrollerar om det finns några resurser i sökvägen <code>/apps/foundation/components/primary</code> och:</p>
    <ul>
     <li>returnerar Varna om det finns underordnade noder under <code>/apps/foundation/components/primary</code></li>
    </ul> <p>MBean för den här hälsokontrollen är <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=resourceSearchPathErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Konfiguration av hälsokontroll {#health-check-configuration}

Som standard körs hälsokontrollerna var 60:e sekund för en AEM.

Du kan konfigurera **Period** med [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md) **Konfiguration av hälsokontroll av fråga** (com.adobe.granite.queries.impl.hc.QueryHealthCheckMetrics).

## Övervakning med Nagios {#monitoring-with-nagios}

Kontrollpanelen för hälsokontroll kan integreras med Nagios via Granite JMX Mbeans. I följande exempel visas hur du lägger till en kontroll som visar hur mycket minne som används på AEM.

1. Konfigurera och installera Nagios på övervakningsservern.
1. Installera sedan Nagios Remote Plugin Executor (NRPE).

   >[!NOTE]
   >
   >Mer information om hur du installerar Nagios och NRPE på datorn finns i [Nagios-dokumentation](https://library.nagios.com/library/products/nagios-core/manuals//).

1. Lägg till en värddefinition för AEM. Du kan utföra den här uppgiften med webbgränssnittet Nagios XI genom att använda Configuration Manager:

   1. Öppna en webbläsare och peka på Nagios-servern.
   1. Tryck på **Konfigurera** på den översta menyn.
   1. Tryck på **Core Config Manager** under **Avancerad konfiguration**.
   1. Tryck på **Värdar** länk under **Övervakning** -avsnitt.
   1. Lägg till värddefinitionen:

   ![chlimage_1-118](assets/chlimage_1-118.png)

   Nedan visas ett exempel på en värdkonfigurationsfil, om du använder Nagios Core:

   ```xml
   define host {
      address 192.168.0.5
      max_check_attempts 3
      check_period 24x7
      check-command check-host-alive
      contacts admin
      notification_interval 60
      notification_period 24x7
   }
   ```

1. Installera Nagios och NRPE på AEM.
1. Installera [check_http_json](https://github.com/phrawzty/check_http_json) plugin-program på båda servrarna.
1. Definiera ett generiskt JSON-kontrollkommando på båda servrarna:

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. Lägg till en tjänst för använt minne på AEM:

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. Kontrollera din Nagios-instrumentpanel för den nya tjänsten:

   ![chlimage_1-119](assets/chlimage_1-119.png)

## Diagnosverktyg {#diagnosis-tools}

Kontrollpanelen för åtgärder ger även tillgång till diagnosverktyg som kan hjälpa dig att hitta och felsöka rotorsaker till varningarna som kommer från kontrollpanelen för hälsokontroll, samt tillhandahålla viktig felsökningsinformation för systemoperatörer.

Bland de viktigaste funktionerna är:

* En loggmeddelandeanalyserare
* Möjlighet att komma åt stackar och tråddumpar
* Begäranden och frågeprestandaanalyser

Du kan nå skärmen Diagnosverktyg genom att gå till **Verktyg - Åtgärder - diagnostik** på AEM välkomstskärm. Du kan även komma åt skärmen genom att gå direkt till följande URL: `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### Loggmeddelanden {#log-messages}

Loggmeddelandena Användargränssnittet visar alla FELmeddelanden som standard. Om du vill att fler loggmeddelanden ska visas konfigurerar du en loggare med rätt loggnivå.

Loggmeddelandena använder ett tillägg i minnesloggen och är därför inte relaterade till loggfilerna. En annan konsekvens är att om du ändrar loggnivåerna i det här användargränssnittet ändras inte den information som loggas i de traditionella loggfilerna. Om du lägger till och tar bort loggare i det här användargränssnittet påverkas bara minnesloggaren. Dessutom återspeglas ändringen av loggningskonfigurationerna i framtiden för minnesloggaren. Poster som redan är loggade och inte längre är relevanta tas inte bort, men liknande poster loggas inte i framtiden.

Du kan konfigurera vad som loggas genom att tillhandahålla loggkonfigurationer från den övre vänstra kugghjulsknappen i användargränssnittet. Där kan du lägga till, ta bort eller uppdatera loggkonfigurationer. En loggningskonfiguration består av en **loggnivå** (VARNA / INFO / DEBUG) och **filternamn**. The **filternamn** har rollen som att filtrera källan för loggmeddelanden som loggas. Om en loggare däremot ska samla in alla loggmeddelanden för den angivna nivån ska filternamnet vara &quot;**root**&quot;. Om du anger nivån för en logger aktiveras inhämtning av alla meddelanden med en nivå som är lika med eller högre än den angivna.

Exempel:

* Om du planerar att hämta alla **FEL** meddelanden - ingen konfiguration krävs. Alla FELmeddelanden hämtas som standard.
* Om du planerar att hämta alla **FEL**, **VARNING** och **INFORMATION** meddelanden - loggningsnamnet ska anges till: &quot;**root**&quot;, och loggningsnivån till: **INFORMATION**.

* Om du planerar att hämta alla meddelanden som kommer från ett visst paket (till exempel com.adobe.granite) ska loggningsnamnet anges till: &quot;com.adobe.granite&quot;. Och loggningsnivån är inställd på: **FELSÖKNING** (gör det fångar alla **FEL**, **VARNING**, **INFORMATION** och **FELSÖKNING** som visas i bilden nedan.

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>Du kan inte ange ett loggningsnamn så att endast FELMEDDELANDEN hämtas via ett angivet filter. Som standard hämtas alla FELmeddelanden.

>[!NOTE]
>
>Användargränssnittet för loggmeddelanden återspeglar inte den faktiska felloggen. Såvida du inte konfigurerar andra typer av loggmeddelanden i användargränssnittet visas endast FELmeddelanden. Mer information om hur du visar specifika loggmeddelanden finns i instruktionerna ovan.

>[!NOTE]
>
>Inställningarna på diagnossidan påverkar inte loggfilerna och omvänt. Så även om felloggen kan fånga upp INFO-meddelanden kanske du inte ser dem i användargränssnittet för loggmeddelanden. Via gränssnittet går det också att fånga upp DEBUG-meddelanden från vissa paket utan att det påverkar felloggen. Mer information om hur du konfigurerar loggfilerna finns i [Loggning](/help/sites-deploying/configure-logging.md).

>[!NOTE]
>
>**Med AEM 6.4**, loggas underhållsaktiviteter ut ur kartongen i ett mer informationsformat på INFO-nivå. Det här arbetsflödet ger bättre synlighet för underhållsuppgifternas status.
>
>Om du använder verktyg från tredje part (till exempel Splunk) för att övervaka och reagera på underhållsaktiviteter kan du använda följande loggsatser:

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### Begär prestanda {#request-performance}

På sidan Prestandabegäran kan du analysera de långsammaste sidbegäranden som behandlas. Endast innehållsbegäranden registreras på den här sidan. Mer specifikt hämtas följande förfrågningar:

1. Begäranden om åtkomst till resurser under `/content`
1. Begäranden om åtkomst till resurser under `/etc/design`
1. Begäranden med `".html"` extension

![chlimage_1-122](assets/chlimage_1-122.png)

Sidan visar:

* Tiden då begäran gjordes
* URL:en och förfrågningsmetoden
* Längden i millisekunder

Som standard hämtas de långsammaste 20 sidbegäranden, men gränsen kan ändras i Configuration Manager.

### Frågeprestanda {#query-performance}

På sidan Frågeprestanda kan du analysera de långsammaste frågorna som har utförts av systemet. Denna information tillhandahålls av databasen i en JMX Mbean. I Jackrabbit `com.adobe.granite.QueryStat` JMX Mbean lämnar denna information, medan den i Oak-databasen erbjuds av `org.apache.jackrabbit.oak.QueryStats.`

Sidan visar:

* Tidpunkten då frågan gjordes
* Frågans språk
* Antal gånger frågan utfärdades
* Frågeinstruktionen
* Längden i millisekunder

![chlimage_1-123](assets/chlimage_1-123.png)

### Förklara fråga {#explain-query}

För varje given fråga försöker Oak hitta det bästa sättet att köra baserat på de Oak-index som definieras i databasen under **oak:index** nod. Oak kan välja olika index beroende på frågan. Att förstå hur Oak kör en fråga är det första steget till att optimera frågan.

Förklara frågan är ett verktyg som förklarar hur Oak kör en fråga. Den kan nås genom att **Verktyg - Åtgärder - diagnostik** på AEM välkomstskärm. Klicka sedan på **Frågeprestanda** och växla till **Förklara fråga** -fliken.

**Funktioner**

* Stöder frågespråken Xpath, JCR-SQL och JCR-SQL2
* Rapporterar den faktiska körningstiden för den angivna frågan
* Identifierar långsamma frågor och varningar om frågor som kan vara långsamma
* Rapporterar Oak-indexet som används för att köra frågan
* Visar den faktiska förklaringen till Oak Query-motorn
* Innehåller klickbar-för-inläsningslista med långsamma och populära frågor

När du är i användargränssnittet för enkla frågor anger du frågan och trycker på **Förklara** knapp:

![chlimage_1-124](assets/chlimage_1-124.png)

Den första posten i avsnittet Frågeförklaring är den faktiska förklaringen. Förklaringen visar vilken typ av index som användes för att köra frågan.

Den andra posten är körningsplanen.

Kickar **Inkludera körningstid** innan frågan körs visas även hur lång tid frågan kördes i. The **Inkludera nodantal** Alternativet rapporterar antalet noder. Rapporten innehåller mer information som kan användas för att optimera index för ditt program eller din distribution.

![chlimage_1-125](assets/chlimage_1-125.png)

### Index Manager {#the-index-manager}

Syftet med indexhanteraren är att underlätta indexhantering, t.ex. att underhålla index eller visa deras status.

Du kommer åt den genom att gå till **Verktyg - Åtgärder - Diagnos **från välkomstskärmen och sedan klicka på **Indexhanteraren** -knappen.

Den kan också nås direkt på den här URL:en: `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![index_manager](assets/index_manager.png)

Gränssnittet kan användas för att filtrera index i tabellen genom att skriva in filtervillkoren i sökrutan i skärmens övre vänstra hörn.

### Download Status ZIP {#download-status-zip}

Den här åtgärden aktiverar nedladdningen av en zip som innehåller användbar information om systemstatus och konfiguration. Arkivet innehåller instanskonfigurationer, en lista över paket, OSGI, Sling-statistik och statistik, som kan resultera i en stor fil. Du kan minska effekten av stora statusfiler genom att använda **Download Status ZIP**-fönstret. Du kommer åt fönstret från:**AEM > Verktyg > Åtgärder > Diagnostik > Download Status ZIP.**

I det här fönstret kan du välja vad som ska exporteras (loggfiler och/eller tråddumpar) och antalet dagar med loggar som ingår i hämtningen i förhållande till det aktuella datumet.

![download_status_zip](assets/download_status_zip.png)

### Ladda ned tråddump {#download-thread-dump}

Den här åtgärden aktiverar nedladdningen av en zip som innehåller information om trådarna i systemet. Information om varje tråd anges, t.ex. dess status, klassinläsaren och stackspårningen.

### Ladda ned Heap Dump {#download-heap-dump}

Du kan hämta en ögonblicksbild av heapen för att analysera den senare. Den här åtgärden aktiverar hämtning av en stor fil (hundratals megabyte).

## Automatiserade underhållsuppgifter {#automated-maintenance-tasks}

Sidan Automatiserade underhållsaktiviteter är en plats där du kan visa och spåra rekommenderade underhållsaktiviteter som schemalagts för periodisk körning. Uppgifterna integreras med systemet för hälsokontroll. Uppgifterna kan också utföras manuellt från gränssnittet.

Om du vill gå till sidan Underhåll på kontrollpanelen för drift går du AEM välkomstskärmen till **Verktyg - Drift - Kontrollpanel - Underhåll**, eller följ den här länken direkt:

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

Följande åtgärder är tillgängliga på kontrollpanelen för åtgärder:

1. The **Rensa version** uppgift, som finns under **Daglig underhållsperiod** -menyn.
1. The **Lucene Binaries Cleanup** uppgift, som finns under **Daglig underhållsperiod** -menyn.
1. The **Rensa arbetsflöde** uppgift, som finns under **Underhållsfönster varje vecka** -menyn.
1. The **Skräpinsamling för datalager** uppgift, som finns under **Underhållsfönster varje vecka** -menyn.
1. The **Underhåll av granskningslogg** uppgift, som finns under **Underhållsfönster varje vecka** -menyn.
1. The **Underhåll av versionsrensning** uppgift, som finns under **Underhållsfönster varje vecka** -menyn.

Standardtimingen för det dagliga underhållet är 2:00 till 5:00. De uppgifter som konfigurerats för att köras varje vecka i underhållsfönstret körs mellan 1:00 A.M och 2:00 A.M. på lördagar.

Du kan också konfigurera timinginställningarna genom att trycka på kugghjulsikonen på något av de två underhållskorten:

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>Sedan AEM 6.1 kan de befintliga underhållsfönstren även konfigureras att köras månadsvis.

### Rensa version {#revision-clean-up}

Mer information om Revision Clean Up finns här: [se den här dedikerade artikeln](/help/sites-deploying/revision-cleanup.md).

### Lucene Binaries Cleanup {#lucene-binaries-cleanup}

Genom att använda rensningsaktiviteten för Lucene-binärfiler kan du rensa bort lucene-binärfiler och minska storlekskraven för det datalager som körs. Lucene&#39;s binary churn regenereras dagligen i stället för det tidigare beroendet av en lyckad [skräpinsamling för datalager](/help/sites-administering/data-store-garbage-collection.md) kör.

Även om underhållsarbetet utvecklades för att minska Lucene-relaterat revisionsskräp, finns det allmänna effektivitetsvinster när uppgiften körs:

* Den veckovisa körningen av skräpinsamlingen för datalagret kan slutföras snabbare.
* Den kan också förbättra den övergripande AEM något.

Du kan komma åt aktiviteten Rensa Lucene-binärfiler från: **AEM > Verktyg > Åtgärder > Underhåll > Dagligt underhåll > Lucene Binaries Cleanup**.

### Skräpinsamling för datalager {#data-store-garbage-collection}

Mer information om skräpinsamlingen i datalagret finns i den dedikerade [dokumentsida](/help/sites-administering/data-store-garbage-collection.md).

### Rensa arbetsflöde {#workflow-purge}

Arbetsflöden kan också rensas från kontrollpanelen för underhåll. Så här kör du tömningsaktiviteten för arbetsflöde:

1. Klicka på **Underhållsfönster varje vecka** sida.
1. Klicka på **Spela upp** i **Rensa arbetsflöde** kort.

>[!NOTE]
>
>Mer information om underhåll av arbetsflöden finns i [den här sidan](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances).

### Underhåll av granskningslogg {#audit-log-maintenance}

Mer information om underhåll av granskningslogg finns i [separat dokumentationssida.](/help/sites-administering/operations-audit-log.md)

### Rensa version {#version-purge}

Du kan schemalägga underhållsaktiviteten Rensa version så att tidigare versioner tas bort automatiskt. Den här åtgärden minimerar behovet av att manuellt använda [Verktyg för versionsrensning](/help/sites-deploying/version-purging.md). Du kan schemalägga och konfigurera aktiviteten Rensa version genom att gå till **Verktyg > Åtgärder > Underhåll > Fönster för veckounderhåll** och följande steg:

1. Klicka **Lägg till**.
1. Välj **Rensa version** i listrutan.

   ![version_purge_MaintenanceMetask](assets/version_purge_maintenancetask.png)

1. Konfigurera aktiviteten Rensa version genom att klicka på **växlar** ikonen på det nya underhållskortet Version Renge.

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**Med AEM 6.4** kan du stoppa underhållsaktiviteten Rensa version enligt följande:

* Automatiskt - Om det schemalagda underhållsfönstret stängs innan aktiviteten kan slutföras stoppas aktiviteten automatiskt. Den återupptas när nästa underhållsfönster öppnas.
* Manuellt - Om du vill stoppa aktiviteten manuellt går du till underhållskortet för versionsrensning och klickar på **Stoppa** -ikon. Nästa körning innebär att uppgiften återupptas utan problem.

>[!NOTE]
>
>Om du stoppar underhållsaktiviteten innebär det att körningen avbryts utan att det pågående jobbet går förlorat.

>[!CAUTION]
>
>För att optimera databasstorleken bör du köra versionsrensningen ofta. Uppgiften bör schemaläggas utanför kontorstid när trafiken är begränsad.

## Anpassade underhållsaktiviteter {#custom-maintenance-tasks}

Anpassade underhållsåtgärder kan implementeras som OSGi-tjänster. Eftersom infrastrukturen för underhållsaktiviteter baseras på Apache Slings jobbhantering måste en underhållsåtgärd implementera Java™-gränssnittet ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`. Dessutom måste den deklarera flera egenskaper för serviceregistrering som ska identifieras som en underhållsuppgift enligt nedan:

<table>
 <tbody>
  <tr>
   <td><strong>Tjänstegenskapsnamn</strong><br /> </td>
   <td><strong>Beskrivning</strong></td>
   <td><strong>Exempel</strong><br /> </td>
   <td><strong>Typ</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>Booleskt attribut som definierar om aktiviteten kan stoppas av användaren. Om en aktivitet deklarerar att den kan avbrytas måste den under körningen kontrollera om den har stoppats och sedan agera därefter. Standardvärdet är false.</td>
   <td>true</td>
   <td>Valfritt</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>Booleskt attribut som definierar om en uppgift är obligatorisk och måste köras regelbundet. Om en uppgift är obligatorisk men inte finns i något aktivt schemafönster rapporterar en hälsokontroll det här felet. Standardvärdet är false.</td>
   <td>true</td>
   <td>Valfritt</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>Ett unikt namn för aktiviteten - namnet används för att referera till uppgiften och är bara ett enkelt namn.</td>
   <td>MyMaintenanceTask</td>
   <td>Obligatoriskt</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>En titel som visas för den här uppgiften</td>
   <td>Min speciella underhållsuppgift</td>
   <td>Obligatoriskt</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>Ett unikt ämne i underhållsaktiviteten.<br /> Jobbhanteringen i Apache Sling startar ett jobb med exakt det här avsnittet för att köra underhållsaktiviteten. När aktiviteten registreras för det här avsnittet körs den.<br /> Ämnet måste börja med <i>com/adobe/granite/Maintenance/job/</i></td>
   <td>com/adobe/granite/Maintenance/job/MyMaintenanceTask</td>
   <td>Obligatoriskt</td>
  </tr>
 </tbody>
</table>

Förutom de ovanstående tjänstegenskaperna finns följande `process()` metod för `JobConsumer` -gränssnittet måste implementeras genom att lägga till koden som ska köras för underhållsaktiviteten. Angiven `JobExecutionContext` kan användas för att visa statusinformation, kontrollera om jobbet har stoppats av användaren och skapa ett resultat (om det lyckades eller misslyckades).

I situationer där en underhållsuppgift inte ska köras på alla installationer (till exempel bara på publiceringsinstansen), kan du få tjänsten att kräva att en konfiguration är aktiv genom att lägga till `@Component(policy=ConfigurationPolicy.REQUIRE)`. Du kan sedan markera konfigurationen som körningsläge beroende i databasen. Mer information finns i [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository).

Nedan visas ett exempel på en anpassad underhållsåtgärd som tar bort filer från en konfigurerbar tillfällig katalog som har ändrats under de senaste 24 timmarna:

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experience-anager-java-MaintenanceMetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

När tjänsten har distribuerats visas den i gränssnittet för kontrollpanelen för åtgärder. Du kan lägga till den i något av de tillgängliga underhållsschemana:

![chlimage_1-127](assets/chlimage_1-127.png)

Den här åtgärden lägger till en motsvarande resurs på /apps/granite/operations/config/intenance/`schedule`/`taskname`. Om aktiviteten är beroende av körningsläge måste egenskapen granite.operations.conditions.runmode anges på den noden med värdena för de körningslägen som måste vara aktiva för den här underhållsaktiviteten.

## Systemöversikt {#system-overview}

The **Kontrollpanel för systemöversikt** visar en översikt på hög nivå över konfiguration, maskinvara och hälsa för AEM. Systemets hälsostatus är transparent och all information samlas på en enda kontrollpanel.

>[!NOTE]
>
>Du kan också [se videon](https://video.tv.adobe.com/v/21340) om du vill få en introduktion till kontrollpanelen för systemöversikt.

### Så här får du åtkomst {#how-to-access}

Om du vill komma åt kontrollpanelen för systemöversikt går du till **Verktyg > Åtgärder > Systemöversikt**.

![system_overview_dashboard](assets/system_overview_dashboard.png)

### Kontrollpanelen för systemöversikt förklaras {#system-overview-dashboard-explained}

Tabellen nedan beskriver all information som visas i kontrollpanelen för systemöversikt. Om det inte finns någon relevant information att visa (t.ex. om säkerhetskopiering inte pågår finns det inga hälsokontroller som är kritiska) visas meddelandet&quot;Inga poster&quot; i respektive avsnitt.

Du kan även hämta en `JSON` fil som sammanfattar instrumentpanelsinformationen genom att klicka på **Ladda ned** i kontrollpanelens övre högra hörn. The `JSON` slutpunkten är `/libs/granite/operations/content/systemoverview/export.json` och kan användas i en `curl` för extern övervakning.

<table>
 <tbody>
  <tr>
   <td><strong>Avsnitt</strong></td>
   <td><strong>Vilken information som visas</strong></td>
   <td><strong>När är det viktigt?</strong></td>
   <td><strong>Länkar till</strong></td>
  </tr>
  <tr>
   <td>Hälsokontroller</td>
   <td>
    <ul>
     <li>en lista över kontroller som har statusen Kritisk</li>
     <li>en lista över kontroller som har statusen Varna</li>
    </ul> </td>
   <td>Visuellt:<br />
    <ul>
     <li>en röd tagg för kritiska kontroller</li>
     <li>en orange tagg för Warn-kontroller</li>
    </ul> </td>
   <td>
    <ul>
     <li>Sidan Hälsorapporter</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Underhållsåtgärder</td>
   <td>
    <ul>
     <li>en lista över misslyckade uppgifter</li>
     <li>en lista över aktiviteter som körs</li>
     <li>en lista över åtgärder som har slutförts i den senaste körningen</li>
     <li>en lista över uppgifter som aldrig har körts</li>
     <li>en lista över aktiviteter som inte är schemalagda</li>
    </ul> </td>
   <td><p>Visuellt:</p>
    <ul>
     <li>en röd tagg för misslyckade uppgifter</li>
     <li>en orange tagg för att köra uppgifter (eftersom de kan påverka prestandan)</li>
     <li>grå taggar för varannan status</li>
    </ul> </td>
   <td>
    <ul>
     <li>Underhållsaktiviteter</li>
    </ul> </td>
  </tr>
  <tr>
   <td>System</td>
   <td>
    <ul>
     <li>operativsystem och OS-version (till exempel macOS X)</li>
     <li>systemets genomsnittliga belastning, som hämtats från <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeusable</a></li>
     <li>diskutrymme (på partitionen där arbetskatalogen finns)</li>
     <li>maximal heap, som returneras av <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a></li>
    </ul> </td>
   <td>Ej tillämpligt</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Instans</td>
   <td>
    <ul>
     <li>AEM</li>
     <li>lista över körningslägen</li>
     <li>det datum då instansen startades</li>
    </ul> </td>
   <td>Ej tillämpligt</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Databas</td>
   <td>
    <ul>
     <li>Oak-versionen</li>
     <li>typ av nodarkiv (Segmentmål eller dokument)
      <ul>
       <li>om typen är dokument, visas typen av dokumentarkiv (RDB eller Mongo)</li>
      </ul> </li>
     <li>om det finns ett anpassat datalager:
      <ul>
       <li>för ett fildatalager visas sökvägen</li>
       <li>för ett S3-datalager visas namnet på S3-bucket</li>
       <li>för ett delat S3-datalager visas namnet på S3-bucket</li>
       <li>för ett Azure Data Store visas behållaren</li>
      </ul> </li>
     <li>om det inte finns något anpassat externt datalager visas ett meddelande som anger detta</li>
    </ul> </td>
   <td>Ej tillämpligt</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Distributionsagenter</td>
   <td>
    <ul>
     <li>en lista över agenter med blockerade köer</li>
     <li>en lista över felkonfigurerade agenter ("Konfigurationsfel")</li>
     <li>en lista över agenter med köbearbetning pausad</li>
     <li>en lista över inaktiva agenter</li>
     <li>en lista över agenter som körs (som för närvarande bearbetar poster)</li>
    </ul> </td>
   <td><p>Visuellt:</p>
    <ul>
     <li>en röd tagg för blockerade agenter eller konfigurationsfel</li>
     <li>en orange tagg för pausade agenter</li>
     <li>en grå tagg för pausade, inaktiva eller aktiva agenter<br /> </li>
    </ul> </td>
   <td>Distributionssida<br /> </td>
  </tr>
  <tr>
   <td>Replikeringsagenter</td>
   <td>
    <ul>
     <li>en lista över agenter med blockerade köer</li>
     <li>en lista över inaktiva agenter</li>
     <li>en lista över agenter som körs (som för närvarande bearbetar poster)</li>
    </ul> </td>
   <td><p>Visuellt:<br /> </p>
    <ul>
     <li>en röd tagg för blockerade agenter</li>
     <li>en grå tagg för pausade agenter</li>
    </ul> </td>
   <td>Replikeringssida</td>
  </tr>
  <tr>
   <td>Arbetsflöden</td>
   <td>
    <ul>
     <li>Arbetsflödesjobb:
      <ul>
       <li>antal misslyckade arbetsflödesjobb (om sådana finns)</li>
       <li>antal avbrutna arbetsflödesjobb (om sådana finns)</li>
      </ul> </li>
    </ul>
    <ul>
     <li>Antal arbetsflöden - antal arbetsflöden i en viss status (om sådana finns):
      <ul>
       <li>körs</li>
       <li>misslyckades</li>
       <li>pausad</li>
       <li>avbruten</li>
      </ul> </li>
    </ul> <p>För vart och ett av de statusvärden som anges ovan utförs en fråga, med en gräns på 400 millisekunder. Vid 400 millisekunder visas antalet poster fram till den punkten.</p> </td>
   <td><p>Ej tolkad:</p>
    <ul>
     <li>användaren bör undersöka när det finns arbetsflöden och jobb i oväntade statusvärden.</li>
    </ul> </td>
   <td>Sidan med arbetsflödesfel</td>
  </tr>
  <tr>
   <td>Försäljningsjobb</td>
   <td><p>Antal jobb vid körning - antal jobb med en given status (om sådana finns):</p>
    <ul>
     <li>misslyckades</li>
     <li>köad</li>
     <li>avbruten</li>
     <li>aktiv</li>
    </ul> </td>
   <td><p>Ej tolkad:</p>
    <ul>
     <li>användaren bör undersöka när det finns jobb i oväntade statusvärden eller med höga räkningar.</li>
    </ul> </td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Beräknat nodantal</td>
   <td><p>Beräknat antal:</p>
    <ul>
     <li>sidor</li>
     <li>resurser</li>
     <li>taggar</li>
     <li>auktoriszables</li>
     <li>totalt antal noder<br /> </li>
    </ul> <p>Det totala antalet noder hämtas från nodeCounterMBean, medan resten av statistiken hämtas från IndexInfoService.</p> </td>
   <td>Ej tillämpligt</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Säkerhetskopiering</td>
   <td>Visar i så fall "Onlinesäkerhetskopiering pågår".</td>
   <td>Ej tillämpligt</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>Indexering</td>
   <td><p>Skärmar:</p>
    <ul>
     <li>"Indexering pågår"</li>
     <li>"Fråga pågår"</li>
    </ul> <p>Om det finns en indexerings- eller frågetråd i tråddumpen.</p> </td>
   <td>Ej tillämpligt</td>
   <td>Ej tillämpligt</td>
  </tr>
 </tbody>
</table>
