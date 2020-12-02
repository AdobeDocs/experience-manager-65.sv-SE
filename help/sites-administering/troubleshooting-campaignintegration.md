---
title: Felsöka Adobe Campaign-integreringen
seo-title: Felsöka Adobe Campaign-integreringen
description: Lär dig hur du felsöker problem med Adobe Campaign Integration.
seo-description: Lär dig hur du felsöker problem med Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---


# Felsöka din Adobe Campaign-integrering{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Den här sidan gäller Campaign Classic.

Följande felsökningstips hjälper dig att lösa de vanligaste problemen du kan stöta på när du integrerar AEM med Adobe Campaign:

## Allmänna felsökningstips {#general-troubleshooting-tips}

För båda integreringarna kan du kontrollera om HTTP-anrop skickas (AEM > Adobe Campaign, Adobe Campaign > AEM):

* När integreringar misslyckas kontrollerar du att dessa samtal kommer till den andra änden (för att undvika brandväggs-/SSL-problem).
* För AEM funktionalitet ser du att json-anrop begärs från AEM författargränssnitt. dessa bör inte resultera i ett HTTP-500-fel. Om du ser HTTP-500-fel bör du kontrollera `error.log` för mer information om detta.
* Genom att höja felsökningsnivån för kampanjklasser i AEM kan du även felsöka problem.

## Om anslutningen misslyckas {#if-the-connection-fails}

Kontrollera att du har konfigurerat **aemserver**-operatorn i Adobe Campaign.

## Om bilder inte visas i Adobe Campaign-konsolen {#if-images-do-not-appear-in-the-adobe-campaign-console}

Kontrollera HTML-källan och validera att du kan öppna URL:en från klientdatorn. Om URL:en innehåller localhost:4503 ändrar du konfigurationen för Day CQ Link Externalizer på författarinstansen så att den pekar på en publiceringsinstans som kan nås från Adobe Campaign konsoldator.

Se [Konfigurera externalisering.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Om du inte kan ansluta från AEM till Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Leta efter följande felmeddelande i Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Åtgärda problemet genom att ändra följande i **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Om inga data visas i Adobe Campaign-dialogrutan {#if-no-data-displays-in-the-adobe-campaign-dialog}

Kontrollera att du inte har några avslutande snedstreck (/) efter portnumret i Adobe Campaign.

![chlimage_1-149](assets/chlimage_1-149.png)

## Om du får en varning om ditt språkområde {#if-you-get-a-warning-about-your-setlocale}

Om du startar Apache HTTPD-tjänsten och ser felet `"Warning: setlocale: LC_CTYPE cannot change locale"` kontrollerar du att du har installerat språket **en_CA.ISO-8859-15** på datorn.

Du kan kontrollera om den är installerad med `local -a`. Om den inte är installerad kan du korrigera **/usr/local/neolane/nl6/env.sh**-skriptet och ändra språkinställningen till en installerad.

## Om du får ett fel när skriptet &#39;get_nms_amcGetSeedMetaData_jssp&#39; kompileras {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Om följande felmeddelande visas i AEM loggfil:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Använd följande lösning:

1. Öppna filen **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Ändra rad 467 i metoden amcGetSeedMetaData
1. Ändra `label : [inclView.@label](mailto:inclView.@label)` till `label : String([inclView.@label](mailto:inclView.@label))`

1. Spara.
1. Starta om servern.

## Om ett fel visas i Adobe Campaign när du klickar på knappen Synkronisera {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Följande fel visas om du klickar på knappen **Synkronisera** i Adobe Campaign Classic:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Kontrollera att den AEM anslutnings-URL som är konfigurerad i det externa kontot kan nås från datorn för att åtgärda problemet.

Ett byte från **localhost** till en IP-adress löste problemet.

## Om du får felet &#39;Det går inte att tolka XTK Date+Time &#39;undefined&#39; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

När du har klickat på Synkronisera visas ett felmeddelande om att ett skript på sidorna har inträffat: Det går inte att parsa XTK-datum+tid &#39;undefined&#39;: inte ett giltigt XTK-värde.

Det här inträffar om det fortfarande finns inaktuell Adobe Campaign-information för AEM. Lös problemet genom att ta bort alla kampanjintegreringskonfigurationer som finns AEM och återskapa dem. Skapa sedan en ny mall.

## Om en anslutning till SSL visar ett fel när molntjänsten {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service} konfigureras

I error.log för AEM, om följande visas:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Ring upp en biljett till Adobe Campaign supportteam.

## Om du ser http i stället för förväntade https-länkar i synkroniseringsdialogrutan {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Med följande inställningar:

* Värdbaserad Adobe Campaign med https för kommunikation med AEM Author
* Återför proxy som avslutar SSL
* Lokal AEM Author-instans

När du försöker synkronisera innehåll i Adobe Campaign returnerar AEM en lista med nyhetsbrev. URL:erna till nyhetsbreven i listan är http-adresser. När du väljer ett av objekten i listan inträffar ett fel.

Så här löser du problemet:

* Avsändaren eller den omvända proxyn måste konfigureras för att skicka det ursprungliga protokollet som en rubrik.
* *Apache Felix Http Service SSL-filtret* i OSGi-konfigurationen ([https://&lt;värd>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) måste konfigureras till respektive rubrikinställningar. Se [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Om den anpassade mall som jag skapade inte kan väljas i Sidegenskaper {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

När du skapar en e-postmall för Adobe Campaign måste du ta med egenskapen **acMapping** med värdet **mapRecipient** i **jcr:content**-noden för mallen, annars kan du inte välja Adobe Campaign-mallen i **Sidegenskaper** för AEM (fältet är inaktiverat).

## Om du får felmeddelandet&quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; i dina loggar {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

När du använder din anpassade mall visas felmeddelandet&quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; i loggarna. I så fall måste du installera Featurepack 6576 från [Paketresurs](/help/sites-administering/package-manager.md#package-share). Det här är ett problem där ett tomt värde skapas på Adobe Campaign Manager-sidan om egenskapen acMapping har ett annat värde än receive.firstName.
