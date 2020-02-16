---
title: Installation av programserver
seo-title: Installation av programserver
description: Lär dig hur du installerar AEM med en programserver.
seo-description: Lär dig hur du installerar AEM med en programserver.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Installation av programserver{#application-server-install}

>[!NOTE]
>
>`JAR` och `WAR` är filtyperna som AEM släpps i. Dessa format genomgår kvalitetssäkring som motsvarar de supportnivåer som Adobe har åtagit sig.


I det här avsnittet beskrivs hur du installerar Adobe Experience Manager (AEM) med en programserver. Gå till avsnittet [Plattformar](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) som stöds för att se de specifika supportnivåerna för de enskilda programservrarna.

Installationsstegen för följande programservrar beskrivs:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Mer information om hur du installerar webbprogram, serverkonfigurationer och hur du startar och stoppar servern finns i dokumentationen för respektive programserver.

>[!NOTE]
>
>Om du använder Dynamic Media i en WAR-distribution kan du läsa dokumentationen [för](/help/assets/config-dynamic.md#enabling-dynamic-media)dynamiska media.

## Allmän beskrivning {#general-description}

### Standardbeteende vid installation av AEM i en programserver {#default-behaviour-when-installing-aem-in-an-application-server}

AEM levereras som en enda krigsfil att distribuera.

Om distribueras kommer följande att ske som standard:

* körningsläget är `author`
* instansen (Repository, Felix OSGI environment, bundles etc.) är installerat i `${user.dir}/crx-quickstart`den aktuella arbetskatalogen `${user.dir}` och den här sökvägen till crx-quickstart anropas `sling.home`

* kontextroten är krigsfilens namn, t.ex.: `aem-6`

#### Konfiguration {#configuration}

Du kan ändra standardbeteendet på följande sätt:

* körningsläge: konfigurera `sling.run.modes` parametern i AEM- `WEB-INF/web.xml` krigsfilen före distributionen

* sling.home: konfigurera `sling.home` parametern i AEM- `WEB-INF/web.xml`krigsfilen före distributionen

* kontextrot: byta namn på AEM-krigsfilen

#### Publicera installation {#publish-installation}

För att få en publiceringsinstans distribuerad måste du ange att körningsläget ska publiceras:

* Packa upp WEB-INF/web.xml från AEM-krigsfilen
* Ändra parametern sling.run.modes till publicering
* Repetera web.xml-filen i AEM war-filen
* Distribuera AEM-krigsfil

#### Installationskontroll {#installation-check}

Om du vill kontrollera om alla är installerade kan du:

* svepa `error.log`filen för att se att allt innehåll är installerat
* se i `/system/console` att alla paket är installerade

#### Två instanser på samma programserver {#two-instances-on-the-same-application-server}

I demonstrationssyfte kan det vara lämpligt att installera författaren och publicera instansen i en programserver. Gör så här:

1. Ändra variablerna sling.home och sling.run.modes i publiceringsinstansen.
1. Packa upp WEB-INF/web.xml från AEM war-filen.
1. Ändra parametern sling.home till en annan sökväg (absoluta och relativa sökvägar är möjliga).
1. Ändra sling.run.modes till publicering för publiceringsinstansen.
1. Upprepa filen web.xml.
1. Byt namn på krigsfilerna så att de har olika namn: t.ex. en byter namn till aemauthor.war och den andra till aempublish.war.
1. Använd högre minnesinställningar, t.ex. för standardinstanser av AEM använder du t.ex.: -Xmx3072m
1. Distribuera de två webbprogrammen.
1. Stoppa de två webbprogrammen efter distributionen.
1. I både författare- och publiceringsinstanser ser du till att egenskapen felix.service.urlhandlers=false anges i filen sling.properties (standard är att den är true).
1. Starta de två webbprogrammen igen.

## Installationsprocedurer för programservrar {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Läs [Allmän beskrivning](#general-description) ovan före en distribution.

**Serverförberedelse**

* Låt Basic Auth Headers gå igenom:

   * Ett sätt att låta AEM autentisera en användare är att inaktivera WebSphere-serverns globala administrativa säkerhet: Gå till Säkerhet -> Global säkerhet och avmarkera kryssrutan Aktivera administrativ säkerhet, spara och starta om servern.

* uppsättning `"JAVA_OPTS= -Xmx2048m"`
* Om du vill installera AEM med kontextroten = / måste du först ändra kontextroten för det befintliga standardwebbprogrammet

**Distribuera AEM-webbprogram**

* Ladda ned AEM war-fil
* Gör dina konfigurationer i web.xml vid behov (se ovan i den allmänna beskrivningen)

   * Packa upp WEB-INF/web.xml
   * ändra sling.run.modes-parameter för publicering
   * avkommentera slinga.initial startparameter och ange den här sökvägen efter behov
   * Replikera filen web.xml

* Distribuera AEM-krigsfil

   * Välj en kontextrot (om du vill ange de körningslägen för sling som du behöver för att välja detaljerade steg i distributionsguiden, anger du dem sedan i steg 6 i guiden)

* Starta AEM-webbprogram

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Läs [Allmän beskrivning](#general-description) ovan före en distribution.

**Förbered JBoss-server**

Ange minnesargument i din conf-fil (t.ex. `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

Om du använder distributionsskannern för att installera AEM-webbprogrammet kan det vara bra att öka värdet `deployment-timeout,` för det angivna `deployment-tiimeout` attributet i xml-filen för instansen (t.ex. `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Distribuera AEM-webbprogram**

* Överför AEM-webbprogrammet till JBoss-administrationskonsolen.

* Aktivera AEM-webbprogrammet.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Läs [Allmän beskrivning](#general-description) ovan före en distribution.

Detta använder en enkel serverlayout med endast en Admin Server.

**Förberedelse av WebLogic-server**

* I `${myDomain}/config/config.xml`tillägg till avsnittet Säkerhetskonfiguration:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` se [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) för rätt position (som standard är det OK att placera den i slutet av avsnittet)

* Öka inställningarna för virtuellt minne:

   * öppna `${myDomain}/bin/setDomainEnv.cmd` (Sesp .sh) sökning efter WLS_MEM_ARGS, ange t.ex. set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * starta om WebLogic-server

* Skapa i `${myDomain}` en paketmapp och i en cq-mapp och i den en Plan-mapp

**Distribuera AEM-webbprogram**

* Ladda ned AEM war-fil
* Placera AEM war-filen i mappen ${myDomain}/packages/cq
* Gör dina konfigurationer tillgängliga i vid `WEB-INF/web.xml` behov (se ovan i den allmänna beskrivningen)

   * Packa upp `WEB-INF/web.xml`fil
   * ändra sling.run.modes-parameter för publicering
   * avkommentera sling.home initial parameter och ange den här sökvägen efter behov (se General Description)
   * Replikera filen web.xml

* Distribuera AEM war-filen som ett program (för de andra inställningarna använder du standardinställningarna)
* Installationen kan ta tid..
* Kontrollera att installationen har slutförts enligt beskrivningen ovan i den allmänna beskrivningen (t.ex. finjustera error.log)
* Du kan ändra kontextroten på fliken Konfiguration i webbprogrammet i WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Läs [Allmän beskrivning](#general-description) ovan före en distribution.

* **Förbered Tomcat Server**

   * Öka inställningarna för virtuellt minne:

      * Lägg till följande inställning i `bin/catalina.bat` (svara `catalina.sh` vid unix):
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat ger varken administratörs- eller hanteraråtkomst vid installationen. Därför måste du redigera manuellt `tomcat-users.xml` för att tillåta åtkomst för dessa konton:

      * Redigera `tomcat-users.xml` för att inkludera åtkomst för admin och chef. Konfigurationen bör se ut ungefär som i följande exempel:
      * 
         ```
         <?xml version='1.0' encoding='utf-8'?>
          <tomcat-users>
          <role rolename="manager"/>
          <role rolename="tomcat"/>
          <role rolename="admin"/>
          <role rolename="role1"/>
          <role rolename="manager-gui"/>
          <user username="both" password="tomcat" roles="tomcat,role1"/>
          <user username="tomcat" password="tomcat" roles="tomcat"/>
          <user username="admin" password="admin" roles="admin,manager-gui"/>
          <user username="role1" password="tomcat" roles="role1"/>
          </tomcat-users>
         ```
   * Om du vill distribuera AEM med kontextroten &quot;/&quot; måste du ändra kontextroten för den befintliga ROOT-webbappen:

      * Stoppa och avdistribuera ROOT-webbprogram
      * Byt namn på mappen ROOT.war i Tomcat-webbappen
      * Starta webbprogrammet igen
   * Om du installerar AEM-webbprogrammet med hanteraren-gui måste du öka den maximala storleken för en överförd fil, eftersom standardinställningen endast tillåter 50 MB uppladdningsstorlek. Då öppnas web.xml för hanterarens webbprogram,

      `webapps/manager/WEB-INF/web.xml`

      och öka maxfilstorleken och max-request-size till minst 500 MB, se följande `multipart-config` exempel på en sådan `web.xml` fil:

      ```
        <multipart-config>
         <!-- 500MB max -->
         <max-file-size>524288000</max-file-size>
         <max-request-size>524288000</max-request-size>
         <file-size-threshold>0</file-size-threshold>
         </multipart-config>
      ```




* **Distribuera AEM-webbprogram**

   * Ladda ned AEM war-fil
   * Gör dina konfigurationer i web.xml vid behov (se ovan i den allmänna beskrivningen)

      * Packa upp WEB-INF/web.xml
      * ändra sling.run.modes-parameter för publicering
      * avkommentera slinga.initial startparameter och ange den här sökvägen efter behov
      * Replikera filen web.xml
   * Byt namn på AEM war-filen till ROOT.war om du vill distribuera den som en rotwebbapp, byt namn på den till t.ex. aemauthor.war om du vill ha en författare som kontextrot
   * kopiera det till Tomcat-webbappen
   * vänta tills AEM är installerat


## Felsökning {#troubleshooting}

Information om hur du hanterar problem som kan uppstå under installationen finns i:

* [Felsökning](/help/sites-deploying/troubleshooting.md)

