---
title: Övervaka användning av AEM-formulär
seo-title: Övervaka användning av AEM-formulär
description: Du kan övervaka AEM-formulärdistributioner både på systemnivå och på intern nivå. Läs mer om hur du övervakar AEM-formulärdistributioner i det här dokumentet.
seo-description: Du kan övervaka AEM-formulärdistributioner både på systemnivå och på intern nivå. Läs mer om hur du övervakar AEM-formulärdistributioner i det här dokumentet.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
translation-type: tm+mt
source-git-commit: 215ba1cb3e98954418b844849c812c9ba6cf572b

---


# Övervaka användning av AEM-formulär {#monitoring-aem-forms-deployments}

Du kan övervaka AEM-formulärdistributioner både på systemnivå och på intern nivå. Du kan använda specialhanteringsverktyg som HP OpenView, IBM Tivoli och CA UniCenter samt en JMX-bildskärm från tredje part som kallas *JConsole* för att specifikt övervaka Java-aktivitet. Implementeringen av en övervakningsstrategi förbättrar tillgängligheten, tillförlitligheten och prestandan för era AEM-blanketter.

Mer information om hur du övervakar AEM-formulärdistributioner finns i [En teknisk guide för övervakning av AEM-formulärdistributioner](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf).

## Övervaka med MBeans {#monitoring-using-mbeans}

AEM-formulär innehåller två registrerade MBeans som tillhandahåller navigering och statistisk information. Detta är de enda MBeans som stöds för integrering och inspektion:

* **** ServiceStatistic: Denna MBean ger information om tjänstens namn och version.
* **** OperationStatistic: Denna MBean ger statistik för alla formulärservertjänster. Här kan administratörer få information om en viss tjänst, t.ex. starttid, antal fel osv.

### ServiceStatisticMbean public interfaces {#servicestatisticmbean-public-interfaces}

Dessa publika gränssnitt för ServiceStatistic MBean kan användas i testsyfte:

```as3
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean-offentliga gränssnitt {#operationstatisticmbean-public-interfaces}

Dessa publika gränssnitt för OperationStatistic MBean kan användas i testsyfte:

```as3
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean-träd- och åtgärdsstatistik {#mbean-tree-operation-statistics}

Med en JMX-konsol (JConsole) finns statistik från OperationStatistic MBean tillgänglig. Statistiken är MBean-attribut och kan navigeras under följande hierarkiträd:

**MBean-träd**

**** Adobe-domännamn: Beroende på programserver. Om programservern inte definierar domänen är adobe.com som standard.

**** ServiceType: AdobeService är det namn som används för att lista alla tjänster.

**** AdobeServiceName: Tjänstnamn eller tjänst-ID.

**** Version: Tjänstens version.

**Åtgärdsstatistik**

**** Anropstid: Tidsåtgång för körning av metoden. Detta inkluderar inte den tidpunkt då begäran serialiseras, överförs från klient till server och avserialiseras.

**** Antal anrop: Antalet gånger som tjänsten anropas.

**** Genomsnittlig anropstid: Genomsnittlig tid för alla anrop som har körts sedan servern startades.

**** Maximal starttid: Varaktigheten för det längsta anropet som har körts sedan servern startades.

**** Minsta anropstid: Varaktigheten för det kortaste anropet som har körts sedan servern startades.

**** Antal undantag: Antal anrop som har resulterat i fel.

**** Undantagsmeddelande: Felmeddelandet för det senaste undantaget som inträffade.

**** Datum och tid för senaste provtagning: Datum för det senaste anropet.

**** Tidsenhet: Standardvärdet är millisekunder.

För att JMX-övervakning ska kunna aktiveras behöver programservrarna vanligtvis någon konfiguration. Mer information finns i programserverdokumentationen.

### Exempel på hur du konfigurerar öppen JMX-åtkomst {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - konfigurera JVM-start**

Om du vill visa MBeans från JConsole konfigurerar du JBoss-programserverns JVM-startparametrar. Kontrollera att JBoss har startats från filen run.bat/sh.

1. Redigera filen run.bat som finns under InstallJBoss/bin.
1. Hitta raden JAVA_OPTS och lägg till följande:

   ```as3
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2/10 - konfigurera JVM-start**

1. Redigera filen startWebLogic.bat som finns under `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Hitta raden JAVA_OPTS och lägg till följande:

   ```as3
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Starta om WebLogic.

>[!NOTE]
>
>För WebLogic kan du komma åt MBean via fjärr- eller IIOP-funktionen.

**Fjärråtkomst till MBean**

1. Starta JConsole för en ny anslutning och klicka på fjärrfliken.
1. Ange värdnamnet och porten (9088, det värde du anger under JVM-startalternativen).

**Websphere 6.1 - konfigurera JVM-start**

1. Lägg till följande rad i fältet för allmänt JVM-argument i Admin Console (Programserver > server1 > Processdefinition > JVM):

   ```as3
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Lägg till eller ta bort kommentarer för följande tre rader i /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (eller &lt;Your Websphere JRE>/ lib/management/management.properties):

   ```as3
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Starta om WebSphere.

