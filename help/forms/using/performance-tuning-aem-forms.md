---
title: Prestandajustering av AEM Forms-server
seo-title: Prestandajustering av AEM Forms-server
description: For AEM Forms to perform optimally, you can fine-tune the cache settings and JVM parameters. Om du använder en webbserver kan du dessutom förbättra AEM Forms prestanda.
seo-description: För att AEM Forms ska fungera optimalt kan du finjustera cacheinställningarna och JVM-parametrarna. Om du använder en webbserver kan du dessutom förbättra AEM Forms prestanda.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# Prestandajustering av AEM Forms-server{#performance-tuning-of-aem-forms-server}

I den här artikeln beskrivs strategier och bästa metoder som du kan implementera för att minska flaskhalsar och optimera prestandan för driftsättningen av AEM Forms.

## Cacheinställningar {#cache-settings}

Du kan konfigurera och styra cachningsstrategin för AEM Forms med komponenten **Mobile Forms Configurations** i AEM Web Configuration Console på:

* (AEM Forms on OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms på JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

De tillgängliga alternativen för cachelagring är följande:

* **None**: Enforces not to cache any artifact. Detta saktar i praktiken ned prestanda och kräver hög minnestillgänglighet på grund av att cache saknas.
* **Konservativ**: Dicates to cache only the intermediära artefacts that are generated before rendering the form, such as a template containing inline fragments and images.
* **Aggressiv**: Framtvingar cache-lagring av nästan allt som kan cachas, inklusive återgivet HTML-innehåll förutom alla artefakter från den konservativa cachenivån. Det ger bästa prestanda men kräver också mer minne för att lagra cachelagrade artefakter. Aggressiv cachningsstrategi innebär att du får konstant tidsprestanda när du återger ett formulär när det återgivna innehållet cachas.

Standardinställningarna för cacheminnet för AEM Forms kanske inte är tillräckligt bra för att få optimala prestanda. Därför rekommenderar vi att du använder följande inställningar:

* **Cachestrategi**: Aggressiv
* **Cachestorlek** (i antal formulär): Som krävs
* **Maximal objektstorlek**: Som krävs

![Konfigurationer av mobilformulär](assets/snap.png)

>[!NOTE]
>
>Om du använder AEM Dispatcher för att cachelagra adaptiva formulär cache-lagras även adaptiva formulär som innehåller formulär med förfyllda data. Om sådana formulär hanteras från AEM Dispatcher-cache kan det leda till att förfyllda eller inaktuella data skickas till användarna. Använd därför AEM Dispatcher för att cachelagra adaptiva formulär som inte använder förifyllda data. Dessutom gör inte en dispatchercache cachelagrade cachelagrade fragment automatiskt ogiltiga. Använd den alltså inte för att cachelagra formulärfragment. Använd cache för [adaptiva formulär för sådana formulär och fragment](../../forms/using/configure-adaptive-forms-cache.md).

## JVM-parametrar {#jvm-parameters}

För optimala prestanda bör du använda följande JVM- `init` argument för att konfigurera `Java heap` och `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>De rekommenderade inställningarna är för Windows 2008 R2 8 Core och Oracle HotSpot 1.7 (64-bitars) JDK och bör skalas upp eller ned enligt din systemkonfiguration.

## Använda en webbserver {#using-a-web-server}

Adaptive forms and HTML5 forms render in HTML5 format. Resultatet kan bli stort beroende på faktorer som formulärstorleken och bilderna i formuläret. För att optimera dataöverföringen rekommenderar vi att du komprimerar HTML-svaret med webbservern som begäran skickas från. Detta minskar svarsstorleken, nätverkstrafiken och den tid som krävs för att strömma data mellan server- och klientdatorer.

For example, perform the following steps to enable compression on Apache Web Server 2.0 32-bit with JBoss:

>[!NOTE]
>
>Följande instruktioner gäller inte för andra servrar än 32-bitars Apache Web Server 2.0. Om du vill ha mer information om vilka steg som gäller för andra servrar läser du i motsvarande produktdokumentation.

I följande steg visas de ändringar som krävs för att aktivera komprimering med Apache Web Server

**Skaffa webbserverprogrammet Apache som kan användas i ditt operativsystem**

* Windows: download the Apache web server from the Apache HTTP Server Project site.
* Solaris 64-bitars: ladda ned Apache-webbservern från Sunfreeware för Solaris webbplats.
* Linux: webbservern Apache är förinstallerad på ett Linux-system.

Apache kan kommunicera med CRX med HTTP-protokollet. Konfigurationerna är avsedda för optimering med HTTP.

1. Avkommentera följande modulkonfigurationer i `APACHE_HOME/conf/httpd.conf` filen.

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >För Linux `APACHE_HOME` är standardvärdet `/etc/httpd/`.

1. Konfigurera proxyn på port 4502 för crx.
Lägg till följande konfiguration i `APACHE_HOME/conf/httpd.conf` konfigurationsfilen.

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Aktivera komprimering. Lägg till följande konfiguration i `APACHE_HOME/conf/httpd.conf` konfigurationsfilen.

   **För HTML5-formulär**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **För anpassningsbara formulär**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   Om du vill få åtkomst till crx-servern använder du `https://'server':80`, där `server` är namnet på den server där Apache-servern körs.

## Använda ett antivirus på en server som kör AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

Du kan uppleva långsam prestanda på servrar som kör ett antivirusprogram. Ett program som alltid använder antivirusprogram (sökningsprogram vid åtkomst) söker igenom alla filer i ett system. Det kan göra servern långsammare och AEM Forms prestanda påverkas.

För att förbättra prestandan kan du instruera antivirusprogrammet att utesluta följande AEM Forms-filer och -mappar från sökningen (vid åtkomst):

* AEM-installationskatalog. Om det inte går att exkludera hela katalogen ska du utelämna följande:

   * [AEM-installationskatalog]\crx-repository\temp
   * [AEM-installationskatalog]\crx-repository\repository
   * [AEM-installationskatalog]\crx-repository\launchpad

* Programserverns tillfälliga katalog. Standardplatsen är:

   * (Jboss) [AEM-installationskatalog]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(Endast AEM Forms på JEE)** GDS-katalog (Global Document Storage). Standardplatsen är:

   * (JBoss) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(Endast AEM Forms på JEE)** AEM Forms serverloggar och temporär katalog. Standardplatsen är:

   * Serverloggar - installationskatalogen [för]AEM Forms \Adobe\AEM forms\[app-server]\server\all\logs
   * Temp directory - [AEM Forms installationskatalog]\temp

>[!NOTE]
>
>* Om du använder en annan plats för GDS och en tillfällig katalog öppnar du AdminUI på `https://'[server]:[port]'/adminui`och går till **Hem > Inställningar > Core System Settings > Core Configurations** för att bekräfta platsen som används.

* Om AEM Forms-servern fungerar långsamt även efter att de föreslagna katalogerna har utelämnats ska du även utelämna den körbara Java-filen (java.exe).



