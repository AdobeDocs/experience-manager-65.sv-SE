---
title: Installation av programserver
description: Lär dig hur du installerar Adobe Experience Manager med en programserver.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Installation av programserver{#application-server-install}

>[!NOTE]
>
>`JAR` och `WAR` är filtyperna som Adobe Experience Manager (AEM) släpps i. Dessa format genomgår kvalitetssäkring för att passa de supportnivåer som Adobe har åtagit sig.
>

I det här avsnittet beskrivs hur du installerar Adobe Experience Manager (AEM) med en programserver. Läs [Plattformar som stöds](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) om du vill läsa om de specifika supportnivåerna för de enskilda programservrarna.

Installationsstegen för följande programservrar beskrivs:

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Mer information om hur du installerar webbprogram, serverkonfigurationer och hur du startar och stoppar servern finns i dokumentationen för respektive programserver.

>[!NOTE]
>
>Om du använder Dynamic Media i en WAR-distribution kan du läsa [Dynamic Media-dokumentation](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Allmän beskrivning {#general-description}

### Standardbeteende vid installation av AEM i en programserver {#default-behaviour-when-installing-aem-in-an-application-server}

AEM kommer som en enda krigsfil att distribuera.

Om den distribueras händer följande som standard:

* körningsläget är `author`
* instansen (Repository, Felix OSGI environment, bundles, osv.) installeras i `${user.dir}/crx-quickstart`där `${user.dir}` är den aktuella arbetskatalogen, den här sökvägen till crx-quickstart anropas `sling.home`

* kontextroten är exempelvis krigsfilens namn,  `aem-6`

#### Konfiguration {#configuration}

Du kan ändra standardbeteendet på följande sätt:

* körningsläge: konfigurera `sling.run.modes` -parametern i `WEB-INF/web.xml` fil för AEM krigsfil före distribution

* sling.home: konfigurera `sling.home` -parametern i `WEB-INF/web.xml`fil för AEM krigsfil före distribution

* kontextrot: ändra namn på AEM krigsfil

#### Publicera installation {#publish-installation}

Om du vill distribuera en publiceringsinstans måste du ange att körningsläget ska publiceras:

* Packa upp WEB-INF/web.xml från AEM krigsfil
* Ändra parametern sling.run.modes till publicering
* Repetera web.xml-filen i AEM
* Distribuera AEM

#### Installationskontroll {#installation-check}

Om du vill kontrollera om alla är installerade kan du:

* svansa `error.log`för att se att allt innehåll är installerat
* titta in `/system/console` att alla paket är installerade

#### Två instanser på samma programserver {#two-instances-on-the-same-application-server}

I demonstrationssyfte kan det vara lämpligt att installera författaren och publicera instansen i en programserver. Gör så här:

1. Ändra variablerna sling.home och sling.run.modes i publiceringsinstansen.
1. Packa upp WEB-INF/web.xml från AEM krigsfil.
1. Ändra parametern sling.home till en annan sökväg (absoluta och relativa sökvägar är möjliga).
1. Ändra sling.run.modes till publicering för publiceringsinstansen.
1. Upprepa filen web.xml.
1. Byt namn på krigsfilerna så att de har olika namn. Exempel: en byter namn till aemauthor.war och den andra till aempublish.war.
1. Använd högre minnesinställningar. Standardinstanser AEM till exempel `-Xmx3072m`
1. Distribuera de två webbprogrammen.
1. Stoppa de två webbprogrammen efter distributionen.
1. I både författare- och publiceringsinstanser ser du till att egenskapen felix.service.urlhandlers=false anges i filen sling.properties (standard är att den är true).
1. Starta de två webbprogrammen igen.

## Installationsprocedurer för programservrar {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

Före en distribution ska du läsa [Allmän beskrivning](#general-description) ovan.

**Serverförberedelse**

* Låt Basic Auth Headers gå igenom:

   * Ett sätt för AEM att autentisera en användare är att inaktivera den globala administrativa säkerheten för WebSphere®-servern: gå till Säkerhet > Global säkerhet och avmarkera kryssrutan Aktivera administrativ säkerhet, spara och starta om servern.

* set `"JAVA_OPTS= -Xmx2048m"`
* Om du vill installera AEM med kontextroten = /, ändrar du kontextroten för det befintliga standardwebbprogrammet.

**Distribuera AEM webbprogram**

* Ladda ned AEM
* Gör dina konfigurationer i web.xml vid behov (se ovan i den allmänna beskrivningen)

   * Packa upp WEB-INF/web.xml
   * ändra sling.run.modes-parameter för publicering
   * avkommentera slinga.initial startparameter och ange den här sökvägen efter behov
   * Replikera filen web.xml

* Distribuera AEM

   * Välj en kontextrot (om du vill ange de körningslägen för sling som du behöver för att välja detaljerade steg i distributionsguiden, anger du dem sedan i steg 6 i guiden)

* Starta AEM

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

Före en distribution ska du läsa [Allmän beskrivning](#general-description) ovan.

**Förbered JBoss®-server**

Ange minnesargument i din conf-fil (till exempel `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

Om du använder distributionsskannern för att installera AEM kan det vara bra att öka `deployment-timeout,` för den uppsättningen `deployment-timeout` i xml-filen för instansen (till exempel `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Distribuera AEM webbprogram**

* Ladda upp det AEM webbprogrammet i JBoss® Administration Console.

* Aktivera det AEM webbprogrammet.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Före en distribution ska du läsa [Allmän beskrivning](#general-description) ovan.

Detta använder en enkel serverlayout med endast en Admin Server.

**Förberedelse av WebLogic-server**

* I `${myDomain}/config/config.xml`lägg till i avsnittet för säkerhetskonfiguration:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` se [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) för rätt position (standardinställningen är att placera den i slutet av avsnittet är OK)

* Öka inställningarna för virtuellt minne:

   * open `${myDomain}/bin/setDomainEnv.cmd` (Svara .sh) sök efter WLS_MEM_ARGS, ange till exempel set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * starta om WebLogic-server

* Skapa i `${myDomain}` en paketmapp och i en cq-mapp och i den en Plan-mapp

**Distribuera AEM webbprogram**

* Ladda ned AEM
* Lägg AEM krigsfil i ${myDomain}/packages/cq mapp
* Gör dina konfigurationer till `WEB-INF/web.xml` vid behov (se ovan i den allmänna beskrivningen)

   * Packa upp `WEB-INF/web.xml`fil
   * ändra sling.run.modes-parameter för publicering
   * avkommentera sling.home initial parameter och ange den här sökvägen efter behov (se General Description)
   * Replikera filen web.xml

* Distribuera AEM krigsfil som ett program (använd standardinställningarna för de andra inställningarna)
* Installationen kan ta tid..
* Kontrollera att installationen har slutförts enligt beskrivningen ovan i den allmänna beskrivningen (t.ex. för att anpassa error.log)
* Du kan ändra kontextroten på fliken Konfiguration i webbprogrammet i WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Före en distribution ska du läsa [Allmän beskrivning](#general-description) ovan.

* **Förbered Tomcat Server**

   * Öka inställningarna för virtuellt minne:

      * I `bin/catalina.bat` (rep `catalina.sh` på UNIX®) lägger du till följande inställning:
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat ger inte administratörs- eller hanteraråtkomst vid installationen. Därför måste du redigera manuellt `tomcat-users.xml` för att ge åtkomst till dessa konton:

      * Redigera `tomcat-users.xml` för att ge åtkomst till administratörer och chefer. Konfigurationen bör se ut ungefär som i följande exempel:

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
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

   * Om du installerar AEM webbprogram med hanteraren-gui måste du öka den maximala storleken för en överförd fil, eftersom standardvärdet endast tillåter 50 MB uppladdningsstorlek. För att göra det öppnar web.xml för webbprogrammet manager,

     `webapps/manager/WEB-INF/web.xml`

     och öka max-file-size och max-request-size till minst 500 MB, se följande `multipart-config` exempel på en sådan `web.xml` -fil.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Distribuera AEM webbprogram**

   * Ladda ned AEM.
   * Gör dina konfigurationer i web.xml om det behövs (se ovan i den allmänna beskrivningen).

      * Packa upp WEB-INF/web.xml.
      * Ändra parametern sling.run.modes till publish.
      * Avkommentera sling.home initial parameter och ange den här sökvägen efter behov.
      * Repackera filen web.xml.

   * Byt namn AEM krigsfilen till ROOT.war om du vill distribuera den som en rotwebbapp. Byt namn på den till aemauthor.war om du vill ha en aemauthor som kontextrot.
   * Kopiera den till Tomcat&#39;s webbapps folder.
   * Vänta tills AEM har installerats.

## Felsökning {#troubleshooting}

Information om hur du hanterar problem som kan uppstå under installationen finns i:

* [Felsökning](/help/sites-deploying/troubleshooting.md)
