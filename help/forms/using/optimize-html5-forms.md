---
title: Optimera HTML5-formulär
seo-title: Optimizing HTML5 forms
description: Du kan optimera utdatastorleken för HTML5-formulär.
seo-description: You can optimize the output size of the HTML5 forms.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Optimera HTML5-formulär {#optimizing-html-forms}

HTML5-formulär återger formulär i HTML5-format. Resultatet kan bli stort beroende på faktorer som formulärstorleken och bilderna i formuläret. För att optimera dataöverföringen rekommenderar vi att du komprimerar HTML-svaret med webbservern som begäran skickas från. Detta minskar svarsstorleken, nätverkstrafiken och den tid som krävs för att strömma data mellan servern och klientdatorerna.

I den här artikeln beskrivs stegen som krävs för att aktivera komprimering för 32-bitars Apache Web Server 2.0 med JBoss.

>[!NOTE]
>
>Följande instruktioner gäller inte för andra servrar än Apache Web Server 2.0 32 bitar.

Skaffa webbserverprogrammet Apache som kan användas i ditt operativsystem:

* För Windows hämtar du Apache-webbservern från Apache HTTP Server Project-webbplatsen.
* För Solaris 64-bitars hämtar du Apache-webbservern från Sunfreeware for Solaris-webbplatsen.
* För Linux är Apache-webbservern förinstallerad på ett Linux-system.

Apache kan kommunicera med JBoss med HTTP eller AJP-protokollet.

1. Avkommentera följande modulkonfigurationer i *APACHE_HOME/conf/httpd.conf* -fil.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >För Linux är standardkatalogen APACHE_HOME /etc/httpd/.

1. Konfigurera proxyn på port 8080 för JBoss.

   Lägg till följande konfiguration i *APACHE_HOME/conf/httpd.conf* konfigurationsfil.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >När du använder en proxy krävs följande konfigurationsändringar:
   >
   >* Åtkomst: *https://&lt;server>:&lt;port>/system/console/configMgr*
   * Redigera konfigurationen för referensfiltret för Apache Sling
   * Lägg till posten för proxyservern i Tillåt värdar


1. Aktivera komprimering.

   Lägg till följande konfiguration i *APACHE_HOME/conf/httpd.conf* konfigurationsfil.

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. Använd https:// för att få åtkomst till AEM server[Apache_server]:80.
