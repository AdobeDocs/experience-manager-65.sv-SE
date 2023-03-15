---
title: Underhållsaktiviteter före uppgraderingen
seo-title: Pre-Upgrade Maintenance Tasks
description: Läs mer om föruppgraderingsuppgifterna i AEM.
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2148'
ht-degree: 0%

---

# Underhållsaktiviteter före uppgraderingen{#pre-upgrade-maintenance-tasks}

Innan du påbörjar uppgraderingen är det viktigt att du följer dessa underhållsåtgärder för att vara säker på att systemet är klart och kan återställas om det skulle uppstå problem:

* [Se till att det finns tillräckligt med diskutrymme](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Helt AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Säkerhetskopiera ändringar i /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Generera filen quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Konfigurera rensning av arbetsflöde och granskningslogg](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Installera, konfigurera och köra uppgifter före uppgradering](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Inaktivera anpassade inloggningsmoduler](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Ta bort uppdateringar från katalogen /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Stoppa alla väntelägesförekomster i kallt läge](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Inaktivera anpassade schemalagda jobb](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Kör rensning av offlineredigering](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Kör skräpinsamling för datastore](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Uppgradera databasschemat om det behövs](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Ta bort användare som kan tyda på en uppgradering](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Rotera loggfiler](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Se till att det finns tillräckligt med diskutrymme {#ensure-sufficient-disk-space}

När du utför uppgraderingen måste du utföra en databasmigrering, förutom innehålls- och koduppgraderingsaktiviteterna. Migreringen skapar en kopia av databasen i det nya segmenttjärformatet. Därför behöver du tillräckligt med diskutrymme för att behålla en andra, eventuellt större, version av databasen.

## Helt AEM {#fully-back-up-aem}

AEM bör säkerhetskopieras fullständigt innan uppgraderingen påbörjas. Säkerhetskopiera databasen, programinstallationen, datalagret och Mongo-instanserna om tillämpligt. Mer information om säkerhetskopiering och återställning av en AEM finns i [Säkerhetskopiering och återställning](/help/sites-administering/backup-and-restore.md).

## Säkerhetskopiera ändringar i /etc {#backup-changes-etc}

Uppgraderingsprocessen gör det möjligt att underhålla och sammanfoga befintligt innehåll och befintliga konfigurationer från `/apps` och `/libs` sökvägar i databasen. För ändringar i `/etc` sökväg, inklusive Context Hub-konfigurationer, är det ofta nödvändigt att tillämpa dessa ändringar igen efter uppgraderingen. Under uppgraderingen görs en säkerhetskopia av alla ändringar som inte kan sammanfogas under `/var`rekommenderar vi att du säkerhetskopierar dessa ändringar manuellt innan du påbörjar uppgraderingen.

## Generera filen quickstart.properties {#generate-quickstart-properties}

När du börjar AEM från filen jar `quickstart.properties` filen skapas under `crx-quickstart/conf`. Om AEM bara har startats med det tidigare startskriptet kommer den här filen inte att finnas och uppgraderingen misslyckas. Kontrollera om filen finns och starta om AEM från filen jar om den inte finns.

## Konfigurera rensning av arbetsflöde och granskningslogg {#configure-wf-audit-purging}

The `WorkflowPurgeTask` och `com.day.cq.audit.impl.AuditLogMaintenanceTask` uppgifter kräver separata OSGi-konfigurationer och fungerar inte utan dem. Om de inte fungerar när en uppgift körs före uppgraderingen är det mest troligt att konfigurationer saknas. Se därför till att du lägger till OSGi-konfigurationer för dessa uppgifter eller tar bort dem helt och hållet från listan över uppgifter som ska optimeras före uppgraderingen om du inte vill köra dem. Dokumentation om hur du konfigurerar rensningsåtgärder för arbetsflöden finns på [Administrera arbetsflödesinstanser](/help/sites-administering/workflows-administering.md) och konfigurationen av underhållsaktiviteten för granskningsloggen finns på [Granskningslogghantering i AEM 6](/help/sites-administering/operations-audit-log.md).

Information om rensning av arbetsflödes- och granskningslogg på CQ 5.6 samt rensning av granskningslogg på AEM 6.0 finns i [Rensa arbetsflödes- och granskningsnoder](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Installera, konfigurera och köra uppgifter före uppgradering {#install-configure-run-pre-upgrade-tasks}

På grund av den nivå av anpassning som AEM tillåter, följer miljöer vanligtvis inte ett enhetligt sätt att utföra uppgraderingar. Detta gör det svårt att skapa en standardiserad uppgraderingsprocedur.

I tidigare versioner var det också svårt för AEM uppgraderingar som stoppats eller som inte återställts på ett säkert sätt. Detta ledde till situationer där det var nödvändigt att starta om hela uppgraderingsförfarandet eller där felaktiga uppgraderingar utfördes utan att några varningar utlöstes.

För att åtgärda dessa problem har Adobe lagt till flera förbättringar i uppgraderingsprocessen, vilket gör den mer flexibel och användarvänlig. Underhållsuppgifter före uppgradering som tidigare skulle utföras manuellt optimeras och automatiseras. Rapporter efter uppgraderingen har lagts till så att processen kan granskas i sin helhet i hopp om att problemen blir enklare.

Underhållsuppgifter före uppgradering sprids för närvarande över olika gränssnitt som delvis eller helt utförs manuellt. Den underhållsoptimering före uppgradering som introducerades i AEM 6.3 möjliggör ett enhetligt sätt att utlösa dessa uppgifter och kunna inspektera deras resultat vid behov.

Alla uppgifter som ingår i det föruppgraderade optimeringssteget är kompatibla med alla versioner från och med AEM 6.0.

### Så här konfigurerar du {#how-to-set-it-up}

I AEM 6.3 och senare finns underhållsoptimeringen i snabbstartsbehållaren. Om du uppgraderar från en äldre version av AEM 6 görs de tillgängliga via separata paket som du kan hämta från pakethanteraren.

Paketen finns på följande platser:

* [För uppgradering från AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [För uppgradering från AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [För uppgradering från AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### Så här använder du den {#how-to-use-it}

The `PreUpgradeTasksMBean` OSGI-komponenten levereras förkonfigurerad med en lista över föruppgraderade underhållsåtgärder som kan köras alla samtidigt. Du kan konfigurera uppgifterna genom att följa proceduren nedan:

1. Gå till webbkonsolen genom att bläddra till *https://serveraddress:serverport/system/console/configMgr*

1. Sök efter &quot;**föruppgraderingsuppgifter**&quot; och klicka sedan på den första matchande komponenten. Komponentens fullständiga namn är `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Ändra listan över underhållsaktiviteter som behöver köras enligt nedan:

   ![1487758925984](assets/1487758925984.png)

Uppgiftslistan varierar beroende på vilket körningsläge som används för att starta instansen. Nedan visas en beskrivning av det körläge som varje underhållsåtgärd är avsedd för.

<table>
 <tbody>
  <tr>
   <td><strong>Uppgift</strong></td>
   <td><strong>Körningsläge</strong></td>
   <td><strong>Anteckningar</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>Jag kommer att springa mark och svepa. Ta bort det här steget och kör för delade datalager<br /> förbered instanser manuellt eller korrekt före körning.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>Du måste konfigurera OSGi för rensningskonfiguration för arbetsflöde för Adobe Granite innan du kör.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Om du använder TjäraMK-instanser AEM 6.0 till 6.2 ska du manuellt köra Revision Cleanup offline i stället.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>Du måste konfigurera OSGi-konfigurationen för rensning av granskningslogg innan du kör.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` anropar en DataStore-skräpinsamlingsåtgärd med markerings- och svepfasen om en sådan används. För distributioner som använder ett delat datalager måste du antingen konfigurera om det eller konfigurera om det eller förbereda instansen för att undvika att objekt som refereras av en annan instans tas bort. Detta kan kräva att markeringsfasen körs manuellt på alla instanser innan den här föruppgraderingsaktiviteten aktiveras.

### Standardkonfiguration för hälsokontroller före uppgradering {#default-configuration-of-the-pre-upgrade-health-checks}

The `PreUpgradeTasksMBeanImpl` OSGI-komponenten levereras förkonfigurerad med en lista med föruppgraderingstaggar för hälsokontroll som ska köras när `runAllPreUpgradeHealthChecks` metoden anropas:

* **system** - den tagg som används av hälsokontrollerna för granitunderhåll

* **föruppgradering** - det här är en anpassad tagg som kan läggas till i alla hälsokontroller som du kan ställa in att köra före en uppgradering

Listan kan redigeras. Du kan använda plustecknet **(+)** och minus **(-)** förutom taggarna för att lägga till fler anpassade taggar eller ta bort standardtaggar.

**MBean-metoder**

Den hanterade böldfunktionen är tillgänglig med [JMX Console](/help/sites-administering/jmx-console.md).

Du kan komma åt MBeans genom att:

1. Gå till JMX-konsolen på *https://serveraddress:serverport/system/console/jmx*
1. Sök efter **PreUpgradeTasks** och klicka på resultatet

1. Välj en metod i **Operationer** avsnitt och markera **Anropa** i följande fönster.

Nedan visas en lista med alla tillgängliga metoder som `PreUpgradeTasksMBeanImpl` exponeras:

<table>
 <tbody>
  <tr>
   <td><strong>Metodnamn</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>INFO</td>
   <td>Visar en lista med tillgängliga namn på underhållsaktiviteter före uppgradering.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFO</td>
   <td>Visar en lista med taggar för hälsokontroller som är före uppgraderingen.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>ÅTGÄRD</td>
   <td>Kör alla underhållsaktiviteter som är före uppgraderingen i listan.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>ÅTGÄRD</td>
   <td>Kör underhållsaktiviteten före uppgradering med det namn som anges som parameter.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Kontrollerar om <code>runAllPreUpgradeTasksmaintenance</code> aktiviteten körs.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Kontrollerar om någon underhållsuppgift som körs före uppgraderingen körs och<br /> returnerar en array som innehåller namnen på de uppgifter som körs.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>ÅTGÄRD</td>
   <td>Visar den exakta körningstiden för underhållsaktiviteten före uppgradering med det namn som anges som parameter.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>ÅTGÄRD</td>
   <td>Visar det senaste körningstillståndet för underhållsaktiviteten före uppgradering med det namn som anges som parameter.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>ÅTGÄRD</td>
   <td><p>Kör alla föruppgraderingskontroller och sparar statusen i en fil med namnet <code>preUpgradeHCStatus.properties</code> som finns i slingstartsökvägen. Om <code>shutDownOnSuccess</code> parametern är inställd på <code>true</code>AEM kommer att stängas av, men endast om alla hälsokontroller före uppgraderingen har statusen OK.</p> <p>Egenskapsfilen kommer att användas som en förutsättning för framtida uppgraderingar<br /> och uppgraderingsprocessen avbryts om hälsokontrollen före uppgraderingen görs<br /> körningen misslyckades. Om du vill ignorera resultatet av föruppgraderingen<br /> hälsokontroller och starta uppgraderingen ändå kan du ta bort filen.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>ÅTGÄRD</td>
   <td>Visar alla importerade paket som inte längre kommer att uppfyllas när<br /> uppgradera till den angivna AEM. AEM måste vara<br /> anges som parameter.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>MBean-metoderna kan anropas via:
>
>* JMX-konsolen
>* Alla externa program som ansluter till JMX
>* cURL
>


## Inaktivera anpassade inloggningsmoduler {#disable-custom-login-modules}

>[!NOTE]
>
>Det här steget krävs bara om du uppgraderar från en version av AEM 5. Den kan hoppas över helt och hållet för uppgraderingar från äldre AEM 6-versioner.

Skräddarsytt sätt `LoginModules` har konfigurerats för autentisering på databasnivå och har ändrats i Apache Oak.

I AEM versioner som använde CRX2-konfiguration placerades i `repository.xml` filen, medan den från och med AEM 6 görs i Apache Felix JAAS Configuration Factory-tjänsten via webbkonsolen.

Alla befintliga konfigurationer måste därför inaktiveras och återskapas för Apache Oak efter uppgraderingen.

Inaktivera anpassade moduler som definierats i JAAS-konfigurationen för `repository.xml`måste du ändra konfigurationen för att kunna använda standardinställningarna `LoginModule`, som i det här exemplet:

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>Mer information finns i [Autentisering med modulen för extern inloggning](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Ett exempel på `LoginModule` konfiguration i AEM 6, se [Konfigurera LDAP med AEM 6](/help/sites-administering/ldap-config.md).

## Ta bort uppdateringar från katalogen /install {#remove-updates-install-directory}

>[!NOTE]
>
>Ta endast bort paket från katalogen crx-quickstart/install när AEM stängts. Detta är ett av de sista stegen innan du startar uppgraderingsproceduren.

Ta bort alla servicepaket, funktionspaket eller snabbkorrigeringar som har distribuerats via `crx-quickstart/install` på det lokala filsystemet. Detta förhindrar oavsiktlig installation av gamla snabbkorrigeringar och servicepaket ovanpå den nya AEM när uppdateringen har slutförts.

## Stoppa alla väntelägesförekomster i kallt läge {#stop-tarmk-coldstandby-instance}

Om du använder kallstart för TjäraMK ska du stoppa alla kalliga standby-instanser. Detta garanterar ett effektivt sätt att komma tillbaka online om det uppstår problem i uppgraderingen. När uppgraderingen har slutförts måste alla instanser av kallstart återskapas från de uppgraderade primära instanserna.

## Inaktivera anpassade schemalagda jobb {#disable-custom-scheduled-jobs}

Inaktivera alla schemalagda OSGi-jobb som ingår i programkoden.

## Kör rensning av offlineredigering {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Detta steg är endast nödvändigt för TjärMK-installationer

Om du använder tarMK bör du köra Revision Cleanup offline innan du uppgraderar. Detta gör att migreringen av databasen och efterföljande uppgraderingsuppgifter går mycket snabbare och säkerställer att rensning av onlineändringar kan utföras korrekt när uppgraderingen har slutförts. Mer information om hur du kör funktionen för borttagning av offlinerevision finns i [Utför rensning av offlineredigering](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Kör skräpinsamling för datastore {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Det här steget är bara nödvändigt för instanser som kör crx3

När du har kört revisionsrensning på CRX3-instanser bör du köra Datastore-skräpinsamlingen för att ta bort alla blobbar som inte refereras i datalagret. Instruktioner finns i dokumentationen om [Skräpinsamling för datalager](/help/sites-administering/data-store-garbage-collection.md).

## Uppgradera databasschemat om det behövs {#upgrade-the-database-schema-if-needed}

Vanligtvis tar den underliggande Apache Oak-stacken AEM använder för beständighet hand om att uppgradera databasschemat vid behov.

Det kan dock inträffa när schemat inte kan uppgraderas automatiskt. Detta är oftast miljöer med hög säkerhet där databasen körs under en användare med mycket begränsade behörigheter. Om detta händer kommer AEM att fortsätta använda det gamla schemat.

För att förhindra att detta händer måste du uppgradera schemat genom att följa nedanstående procedur:

1. Stäng den AEM som behöver uppgraderas.
1. Uppgradera databasschemat. Läs dokumentationen om din databastyp för att se vilka verktyg du behöver för att uppnå detta.

   Mer information om hur Oak hanterar schemauppgraderingar finns i [den här sidan på Apache-webbplatsen](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Fortsätt med att uppgradera AEM.

## Ta bort användare som kan tyda på en uppgradering {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Underhållsuppgifterna är bara nödvändiga om:
>
>* Du uppgraderar från AEM versioner som är äldre än AEM 6.3
>* Du stöter på något av de fel som nämns nedan under uppgraderingen.
>


Det finns exceptionella fall när tjänstanvändare kan få äldre AEM som felaktigt taggade som vanliga användare.

Om detta inträffar kommer uppgraderingen att misslyckas med ett meddelande som detta:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Se till att du gör följande för att lösa problemet:

1. Frigör instansen från produktionstrafiken
1. Skapa en säkerhetskopia av de användare som orsakar problemet. Det kan du göra via Package Manager. Mer information finns i [Så här arbetar du med paket.](/help/sites-administering/package-manager.md)
1. Ta bort de användare som orsakar problemet. Nedan finns en lista över användare som kan ingå i den här kategorin:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Rotera loggfiler {#rotate-log-files}

Vi rekommenderar att du arkiverar dina aktuella loggfiler innan du påbörjar uppgraderingen. Detta gör det enklare att övervaka och söka igenom loggfilerna under och efter uppgraderingen för att identifiera och lösa eventuella problem som kan uppstå.
