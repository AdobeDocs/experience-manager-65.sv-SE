---
title: Så här kör du AEM med StjärmMK Cold Standby
seo-title: Så här kör du AEM med StjärmMK Cold Standby
description: Lär dig hur du skapar, konfigurerar och underhåller en StjärtMK Cold Standby-konfiguration.
seo-description: Lär dig hur du skapar, konfigurerar och underhåller en StjärtMK Cold Standby-konfiguration.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
translation-type: tm+mt
source-git-commit: c5e6098b62ff7e3e787b5f0f3c3b32a35e3981c6

---


# Så här kör du AEM med StjärmMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Introduktion {#introduction}

Tack vare kapaciteten för vänteläge i kallt läge för Tjärmikrokärnan kan en eller flera AEM-instanser i vänteläge ansluta till en primär instans. Synkroniseringsprocessen är bara ett sätt, vilket innebär att den bara utförs från den primära instansen till standby-instansen.

Syftet med standby-instanserna är att garantera en live-datakopia av huvuddatabasen och se till att det går snabbt att växla utan dataförlust om mallsidan inte är tillgänglig av någon anledning.

Innehållet synkroniseras linjärt mellan den primära instansen och standby-instansen utan några integritetskontroller för att filer eller databaser är skadade. På grund av den här designen är standby-instanser exakta kopior av den primära instansen och kan inte bidra till att minska inkonsekvenser i primära instanser.

>[!NOTE]
>
>Funktionen Kall vänteläge är avsedd att skydda scenarier där hög tillgänglighet krävs för **författarinstanser** . I situationer där hög tillgänglighet krävs för att **publicera** instanser med hjälp av Tjärmikrokärnan rekommenderar Adobe att du använder en publiceringsgrupp.
>
>Mer information om fler tillgängliga distributioner finns på sidan [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md) .

## Så här fungerar det {#how-it-works}

På den primära AEM-instansen öppnas en TCP-port och lyssnar på inkommande meddelanden. För närvarande finns det två typer av meddelanden som slavarna skickar till huvudpersonen:

* ett meddelande som begär det aktuella huvudets segmend-ID
* ett meddelande som begär segmentdata med ett angivet ID

Vänteläge begär regelbundet segment-ID:t för den primära huvuddelen. Om segmentet är lokalt okänt hämtas det. Om den redan finns jämförs segmenten och om det behövs efterfrågas även refererade segment.

>[!NOTE]
>
>Standby-instanser tar inte emot någon typ av begäranden eftersom de körs i synkroniseringsläge. Det enda avsnittet som är tillgängligt på en standby-instans är webbkonsolen för att underlätta konfigureringen av paket och tjänster.

En typisk STAMK Cold Standby-driftsättning:

![chlimage_1](assets/chlimage_1.png)

## Andra egenskaper {#other-characteristics}

### Robusta {#robustness}

Dataflödet är utformat för att automatiskt upptäcka och hantera anslutnings- och nätverksrelaterade problem. Alla paket är paketerade med kontrollsummor och så snart problem med anslutningen eller skadade paket uppstår aktiveras återförsöksmekanismer.

#### Prestanda {#performance}

Om du aktiverar TonaMK Cold Standby på den primära instansen påverkas prestanda nästan inte. Den extra processorförbrukningen är mycket låg och den extra hårddisk- och nätverks-I/O-funktionen bör inte ge upphov till prestandaproblem.

I vänteläge kan du förvänta dig hög processorförbrukning under synkroniseringsprocessen. Eftersom proceduren inte är flertrådig går det inte att öka hastigheten genom att använda flera kärnor. Om inga data ändras eller överförs blir det ingen mätbar aktivitet. Anslutningshastigheten varierar beroende på maskinvara och nätverksmiljö, men beror inte på storleken på databasen eller SSL-användningen. Du bör tänka på detta när du beräknar den tid som krävs för en inledande synkronisering eller när mycket data har ändrats under tiden på den primära noden.

#### Dokumentskydd {#security}

Om man utgår ifrån att alla instanser körs i samma säkerhetszon för intranätet minskar risken för säkerhetsöverträdelse avsevärt. Du kan dock lägga till extra säkerhetslager genom att aktivera SSL-anslutningar mellan slavarna och mallsidan. På så sätt minskar risken för att data äventyras av en man-in-the-middle.

Du kan dessutom ange vilka standby-instanser som tillåts ansluta genom att begränsa IP-adressen för inkommande begäranden. Detta bör bidra till att garantera att ingen i intranätet kan kopiera databasen.

>[!NOTE]
>
>Vi rekommenderar att en belastningsutjämnare läggs till mellan Dispatcher och servrarna som ingår i konfigurationen för vänteläge i molnet. Belastningsutjämnaren bör konfigureras så att den dirigerar användartrafik endast till den **primära** instansen för att säkerställa konsekvens och förhindra att innehåll kopieras i standby-instansen på annat sätt än med mekanismen för vänteläge i kylläge.

## Skapa en AEM tarMK Cold Standby-inställning {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>PID:t för segmentnodbutiken och tjänsten Standby store har ändrats i AEM 6.3 jämfört med tidigare versioner enligt följande:
>
>* från org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService to org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* från org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService to org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>
 Se till att du gör de nödvändiga konfigurationsjusteringarna för att återspegla den här ändringen.

För att kunna skapa en kallig TjärMK-standby-inställning måste du först skapa standby-instanserna genom att utföra en kopia av hela installationsmappen för den primära till en ny plats. Du kan sedan starta varje instans med ett körningsläge som anger dess roll ( `primary` eller `standby`).

Nedan visas proceduren som måste följas för att skapa en konfiguration med en master- och en standby-instans:

1. Installera AEM.

1. Stäng instansen och kopiera installationsmappen till den plats där instansen av kallstart ska köras. Även om du kör från olika datorer måste du ge varje mapp ett beskrivande namn (som *aem-primär* eller *aem-standby*) för att kunna skilja på instanserna.
1. Gå till installationsmappen för den primära instansen och:

   1. Kontrollera och ta bort tidigare OSGi-konfigurationer som du har under `aem-primary/crx-quickstart/install`

   1. Skapa en mapp som anropas `install.primary` under `aem-primary/crx-quickstart/install`

   1. Skapa de konfigurationer som krävs för det önskade nodarkivet och datalagret under `aem-primary/crx-quickstart/install/install.primary`
   1. Skapa en fil som anropas `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` på samma plats och konfigurera den därefter. Mer information om konfigurationsalternativen finns i [Konfiguration](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Om du använder en AEM tarMK-instans med ett externt datalager skapar du en mapp med namnet `crx3` under `aem-primary/crx-quickstart/install``crx3`

   1. Placera konfigurationsfilen för datalagret i `crx3` mappen.
   Om du t.ex. kör en AEM-tjäraMK-instans med ett externt fildatalager behöver du följande konfigurationsfiler:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`
   Här nedan hittar du exempelkonfigurationer för den primära instansen:

   **Exempel på** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Exempel på org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Exempel på org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Starta det primära läget och kontrollera att du anger det primära körningsläget:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Skapa en ny Apache Sling Logging Logger för **paketet org.apache.jackrabbit.oak.segment** . Ställ in loggnivån på &quot;Felsök&quot; och peka loggutdata på en separat loggfil, som */logs/tarmk-coldstandby.log*. For more information, see [Logging](/help/sites-deploying/configure-logging.md).
1. Gå till platsen för **standby** -instansen och starta den genom att köra burken.
1. Skapa samma loggningskonfiguration som för den primära. Stoppa sedan instansen.
1. Förbered sedan standby-instansen. Du kan göra detta genom att utföra samma steg som för den primära instansen:

   1. Ta bort alla filer som du har under `aem-standby/crx-quickstart/install`.
   1. Skapa en ny mapp som anropas `install.standby` under `aem-standby/crx-quickstart/install`

   1. Skapa två konfigurationsfiler med namnet:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. Skapa en ny mapp som anropas `crx3` under `aem-standby/crx-quickstart/install`

   1. Skapa datalagerkonfigurationen och placera den under `aem-standby/crx-quickstart/install/crx3`. I det här exemplet måste du skapa följande fil:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. Redigera filerna och skapa de konfigurationer som behövs.
   Nedan visas exempel på konfigurationsfiler för en vanlig standby-instans:

   **Exempel på org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Exempel på org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Exempel på org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Starta **standby** -instansen med vänteläget:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

Tjänsten kan även konfigureras via webbkonsolen genom att:

1. Gå till webbkonsolen på: *https://serveraddress:serverport/system/console/configMgr*
1. Letar efter en tjänst som heter **Apache Jackrabbit Oak Segment tar Standby Service** och dubbelklickar på den för att redigera inställningarna.
1. Spara inställningarna och starta om instanserna så att de nya inställningarna kan börja gälla.

>[!NOTE]
>
>Du kan kontrollera rollen för en instans när som helst genom att kontrollera om det finns **primära** eller **väntelägen** i webbkonsolen för delningsinställningar.

>Du kan göra detta genom att gå till *https://localhost:4502/system/console/status-slingsettings* och kontrollera raden **&quot;Run Modes&quot;** .
>

## Första synkroniseringen {#first-time-synchronization}

När beredningen är klar och standby-läget startas för första gången kommer det att uppstå en kraftig nätverkstrafik mellan instanserna när standby-läget fångar upp till primärt läge. Du kan läsa loggarna för att se synkroniseringens status.

I standby *target-coldstandby.log* visas följande poster:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

I väntelägets *error.log* bör du se en post som den här:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

I ovanstående loggutdrag är *10.20.30.40* den primära IP-adressen.

I den **primära** *target-coldstandby.log* visas bl.a. följande:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

I det här fallet är &quot;klienten&quot; som nämns i loggen **standby** -instans.

När de här posterna inte längre visas i loggen kan du anta att synkroniseringsprocessen är slutförd.

Ovanstående poster visar att avsökningsfunktionen fungerar som den ska, men det är ofta bra att förstå om det finns data som synkroniseras när avsökningen sker. Om du vill göra det söker du efter poster som följande:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

När du kör med ett icke-delat meddelande `FileDataStore`kommer meddelanden som följande att bekräfta att de binära filerna överförs korrekt:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Konfiguration {#configuration}

Följande OSGi-inställningar är tillgängliga för tjänsten Cold Standby:

* **** Beständig konfiguration: om det är aktiverat lagras konfigurationen i databasen i stället för de traditionella OSGi-konfigurationsfilerna. Vi rekommenderar att den här inställningen är inaktiverad på produktionssystem så att den primära konfigurationen inte hämtas i vänteläge.

* **`mode`Läge (**): Då väljs instansens körningsläge.

* **** Port (port): den hamn som ska användas för kommunikation. The default is `8023`.

* **`primary.host`Primär värd (**): - den primära instansens värd. Den här inställningen gäller endast för vänteläge.
* **`interval`Synkroniseringsintervall (**): - den här inställningen avgör intervallet mellan synkroniseringsbegäranden och gäller endast för standby-instansen.

* **`primary.allowed-client-ip-ranges`Tillåtna IP-intervall (**): - IP-intervallen som den primära servern tillåter anslutningar från.
* **`secure`Säker (**): Aktivera SSL-kryptering. För att den här inställningen ska kunna användas måste den vara aktiverad i alla instanser.
* **`standby.readtimeout`Timeout för vänteläsning (**): Timeout för begäranden som utfärdas från standby-instansen i millisekunder. Den rekommenderade timeoutinställningen är 43200000. Normalt rekommenderas att du anger en tidsgräns på minst 12 timmar.

* **`standby.autoclean`Automatisk rensning i vänteläge (**): Anropa rensningsmetoden om storleken på butiken ökar under en synkroniseringscykel.

>[!NOTE]
Vi rekommenderar att primär data och vänteläge har olika databas-ID för att göra dem separat oidentifierbara för tjänster som Offloading.
Det bästa sättet att se till att detta täcks är att ta bort filen *sling.id* i vänteläge och starta om instansen.

## Redundansprocedurer {#failover-procedures}

Om den primära instansen av någon anledning inte fungerar kan du ställa in en av standby-instanserna så att den tar rollen som primär genom att ändra start-runmode enligt beskrivningen nedan:

>[!NOTE]
Konfigurationsfilerna måste också ändras så att de matchar inställningarna som används för den primära instansen.

1. Gå till den plats där standby-instansen är installerad och stoppa den.

1. Om du har konfigurerat en belastningsutjämnare med konfigurationen kan du ta bort den primära från belastningsutjämnarens konfiguration nu.
1. Säkerhetskopiera `crx-quickstart` mappen från en installationsmapp i vänteläge. Den kan användas som utgångspunkt när du skapar ett nytt vänteläge.

1. Starta om instansen med `primary` körningsläget:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Lägg till den nya primära till belastningsutjämnaren.
1. Skapa och starta en ny standby-instans. Mer information finns i proceduren ovan om hur du [skapar en AEM tarMK Cold Standby-inställning](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Använda snabbkorrigeringar i en konfiguration för vänteläge i kallt format {#applying-hotfixes-to-a-cold-standby-setup}

Det rekommenderade sättet att tillämpa snabbkorrigeringar på en kallstartsinstallation är att installera dem på den primära instansen och sedan klona den i en ny kallig standby-instans med snabbkorrigeringarna installerade.

Du kan göra detta genom att följa stegen nedan:

1. Stoppa synkroniseringsprocessen på den kalla standby-instansen genom att gå till JMX-konsolen och använda **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**bean. Mer information om hur du gör detta finns i avsnittet [Övervakning](#monitoring).
1. Stoppa kallstartsinstansen.
1. Installera snabbkorrigeringen på den primära instansen. Mer information om hur du installerar en snabbkorrigering finns i [Arbeta med paket](/help/sites-administering/package-manager.md).
1. Testa instansen efter problem efter installationen.
1. Ta bort instansen av det kalla vänteläget genom att ta bort installationsmappen.
1. Stoppa den primära instansen och klona den genom att utföra en kopia av hela installationsmappen i filsystemet till platsen för det kalla vänteläget.
1. Konfigurera om den nyligen skapade klonen så att den fungerar som en instans i kallt vänteläge. Mer information finns i [Skapa ett vänteläge för AEM tarMK Cold.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Starta både det primära och det kalla vänteläget.

## Övervakning {#monitoring}

Funktionen visar information med JMX eller MBeans. På så sätt kan du inspektera det aktuella läget för standby och master med [JMX-konsolen](/help/sites-administering/jmx-console.md). Informationen finns i MBean med `type org.apache.jackrabbit.oak:type="Standby"`namnet `Status`.

**Standby**

Om du observerar en standby-instans visas en nod. ID:t är vanligtvis ett generiskt UUID.

Den här noden har fem skrivskyddade attribut:

* `Running:` booleskt värde som anger om synkroniseringsprocessen körs eller inte.

* `Mode:` Klient: följt av det UUID som används för att identifiera instansen. Observera att detta UUID ändras varje gång konfigurationen uppdateras.

* `Status:` en textbeteckning för det aktuella läget (som `running` eller `stopped`).

* `FailedRequests:`antalet på varandra följande fel.
* `SecondsSinceLastSuccess:` antalet sekunder som gått sedan den senaste kommunikationen med servern. Det visas `-1` om ingen kommunikation har lyckats.

Det finns också tre anropbara metoder:

* `start():` startar synkroniseringsprocessen.
* `stop():` stoppar synkroniseringsprocessen.
* `cleanup():` kör rensningsåtgärden i vänteläge.

**Primär**

När du observerar det primära exponeras viss allmän information via ett MBean vars ID-värde är det portnummer som standbytjänsten tarMK använder (8023 som standard). De flesta metoder och attribut är desamma som i vänteläge, men vissa skiljer sig åt:

* `Mode:` visar alltid värdet `primary`.

Dessutom kan information för upp till 10 klienter (standby-instanser) som är anslutna till mallen hämtas. MBean-ID:t är instansens UUID. Det finns inga anropbara metoder för dessa MBeans, men några mycket användbara skrivskyddade attribut:

* `Name:` ID för klienten.
* `LastSeenTimestamp:` tidsstämpeln för den senaste begäran i en textbeteckning.
* `LastRequest:` klientens senaste begäran.
* `RemoteAddress:` klientens IP-adress.
* `RemotePort:` den port klienten använde för den senaste begäran.
* `TransferredSegments:` det totala antalet segment som överförts till den här klienten.
* `TransferredSegmentBytes:`det totala antalet byte som har överförts till klienten.

## Underhåll av vänteläge, kall {#cold-standby-repository-maintenance}

### Revision Cleanup {#revision-clean}

>[!NOTE]
Om du kör rensning [av](/help/sites-deploying/revision-cleanup.md) onlineändringar på den primära instansen behövs inte den manuella proceduren nedan. Om du använder onlinesortering för revision utförs dessutom åtgärden automatiskt på standby-instansen `cleanup ()` .

>[!NOTE]
Kör inte någon rensning av offlineversioner i vänteläge. Den behövs inte och minskar inte segmentlagerstorleken.

Adobe rekommenderar regelbundet underhåll för att förhindra alltför stor databastillväxt över tid. Följ stegen nedan om du vill utföra underhåll i vänteläge manuellt:

1. Stoppa standbyprocessen i standby-instansen genom att gå till JMX-konsolen och använda **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)** -böna. Mer information om hur du gör detta finns i avsnittet ovan om [övervakning](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Stoppa den primära AEM-instansen.
1. Kör ekkomprimeringsverktyget på den primära instansen. Mer information finns i [Underhålla databasen](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Starta den primära instansen.
1. Starta standby-processen i standby-instansen med samma JMX-böna som i det första steget.
1. Se loggarna och vänta tills synkroniseringen är klar. Det är möjligt att en avsevärd ökning av beredskapslagringsplatsen kommer att ses just nu.
1. Kör `cleanup()` åtgärden i standby-instansen med samma JMX-böna som i det första steget.

Det kan ta längre tid än vanligt för standby-instansen att slutföra synkroniseringen med den primära, eftersom offlinekomprimeringen effektivt skriver om databashistoriken, vilket gör att beräkning av ändringarna i databaserna tar längre tid. Det bör också noteras att när processen är slutförd kommer storleken på databasen i vänteläge att vara ungefär lika stor som databasen på den primära databasen.

Som ett alternativ kan den primära databasen kopieras till vänteläge manuellt efter att du har kört komprimering på den primära, vilket innebär att vänteläget återskapas varje gång komprimeringen körs.

### Skräpinsamling för datalager {#data-store-garbage-collection}

Det är viktigt att du kör skräpinsamlingen på fildatalagrets instanser då och då, annars finns borttagna binärfiler kvar i filsystemet och fyller i enheten. Så här kör du skräpinsamlingen:

1. Kör underhåll av kyla standby-databaser enligt beskrivningen i avsnittet [ovan](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. När underhållsprocessen har slutförts och instanserna har startats om:

   * Kör skräpinsamlingen i datalagret via den relevanta JMX-böna enligt beskrivningen i [den här artikeln](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * I vänteläge är skräpinsamlingen i datalagret endast tillgänglig via **BlobGarbageCollection** MBean - `startBlobGC()`. **RepositoryManagement **MBean är inte tillgängligt i vänteläge.
   >[!NOTE]
   Om du inte använder ett delat datalager måste skräpinsamlingen först köras på primär plats och sedan i vänteläge.

