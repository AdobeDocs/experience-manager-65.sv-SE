---
cloud: experience-cloud
product: adobe experience manager
audience: end-user
user-guide-title: AEM 6.5 Deployment Guide
breadcrumb-title: Deploying Guide
user-guide-description: Learn more about installing, deploying, and the architecture of Adobe Experience Manager 6.5, including our Adobe Managed Services cloud deployment.
translation-type: tm+mt
source-git-commit: cb07e24b01084f57ad46615cb463ad5a0329c181
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---


# Användarhandbok för distribution av AEM 6.5 {#deploying}

+ [Distribuera användarhandbok](home.md)
+ Introduktion till AEM {#introduction}
   + [Introduktion till AEM](platform.md)
   + [Tekniska krav](technical-requirements.md)
   + [Lagringselement i AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM med MongoDB](aem-with-mongodb.md)
+ Distribuera AEM {#deploying}
   + [Driftsättning och underhåll](deploy.md)
   + [Rekommenderade distributioner](recommended-deploys.md)
   + [Installation av programserver](application-server-install.md)
   + [Anpassad fristående installation](custom-standalone-install.md)
   + [Kommandoradens start och stopp](command-line-start-and-stop.md)
   + [Konfigurera nodarkiv och datalager i AEM 6](data-store-config.md)
   + [Revision Cleanup](revision-cleanup.md)
   + [Fråga och indexering](queries-and-indexing.md)
   + [Så här kör du AEM med TARMK Cold Standby](tarmk-cold-standby.md)
   + [Stöd för RDBMS i AEM 6.5](rdbms-support-in-aem.md)
   + [Indexering via Oak-run Jar](indexing-via-the-oak-run-jar.md)
   + [Exempel på indexeringsanvändning för Oak-run.jar](oak-run-indexing-usecases.md)
   + [Felsöka ekindex](troubleshooting-oak-indexes.md)
   + [Insamling av aggregerad användningsstatistik](opt-in-aggregated-usage-statistics.md)
   + [Felsökning](troubleshooting.md)
+ Konfigurera AEM {#configuring}
   + [Grundläggande konfigurationskoncept](configuring.md)
   + [Loggning](configure-logging.md)
   + [Konfigurerar OSGi](configuring-osgi.md)
   + [Konfigurationsinställningar för OSGi](osgi-configuration-settings.md)
   + [Körningslägen](configure-runmodes.md)
   + [Webbkonsol](web-console.md)
   + [Replikering](replication.md)
   + [Replikering med ömsesidig SSL](mssl-replication.md)
   + [Felsökning av replikering](troubleshoot-rep.md)
   + [Förfallotid för statiska objekt](expiration-static-objects.md)
   + [Rensning av version](version-purging.md)
   + [Övervaka och underhålla AEM](monitoring-and-maintaining.md)
   + [Avlastar jobb](offloading.md)
   + [Enkel inloggning](single-sign-on.md)
   + [Resursmappning](resource-mapping.md)
   + [Aktivera HTTP över SSL](/help/sites-administering/ssl-by-default.md)
   + [Konsekvenskontroll och genomgående kontroll](consistency-check.md)
   + [Riktlinjer för prestanda](performance-guidelines.md)
   + [Prestandaoptimering](configuring-performance.md)
   + [Prestandahandbok för resurser](assets-performance-sizing.md)
   + [Instruktionsartiklar för konfiguration](ht-deploy.md)
   + [Konfigurerar webbkonsolen](configuring-web-console.md)
+ Uppgradera till AEM 6.5 {#upgrading}
   + [Uppgradera till AEM 6.5](upgrade.md)
   + [Planera din uppgradering](upgrade-planning.md)
   + [Utvärdera uppgraderingskomplexiteten med mönsteravkännaren](pattern-detector.md)
   + [Bakåtkompatibilitet i AEM 6.5](backward-compatibility.md)
   + [Uppgraderingsprocedur](upgrade-procedure.md)
   + [Utföra en uppgradering på plats](in-place-upgrade.md)
   + [Använda omindexering offline för att minska driftstoppen under en uppgradering](upgrade-offline-reindexing.md)
   + [Lazy Content Migration](lazy-content-migration.md)
   + [Använda CRX2Oak Migration Tool](using-crx2oak.md)
   + [Underhållsaktiviteter före uppgraderingen](pre-upgrade-maintenance-tasks.md)
   + [Kontrollera och felsök efter uppgradering](post-upgrade-checks-and-troubleshooting.md)
   + [Uppgraderar Forms för anpassad sökning](upgrading-custom-search-forms.md)
   + [Hållbara uppgraderingar](sustainable-upgrades.md)
   + [Uppgradera kod och anpassningar](upgrading-code-and-customizations.md)
   + [Uppgradera steg för programserverinstallationer](app-server-upgrade.md)
   + [Lista över föråldrade paket som avinstallerats efter uppgraderingen](obsolete-bundles.md)
+ Omstrukturering av lager {#restructuring}
   + [Omstrukturering av lager i AEM 6.5](repository-restructuring.md)
   + [Omstrukturering av de gemensamma tillgångarna i AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Omstrukturering av anläggningar Repository i AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Omstrukturering av tillgångar Repository i AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Omstrukturering av Dynamic Media Repository i AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Omstrukturering av Forms-lager i AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Omstrukturering av e-handelslager i AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Repositionsomstrukturering för AEM Communities i 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [e-handel - översikt](ecommerce.md)
   + [SAP Commerce Cloud](sap-commerce-cloud.md)
   + [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ Bästa praxis {#practices}
   + [Distribuera bästa praxis](best-practices.md)
   + [Prestandaträd](performance-tree.md)
   + [Bästa metoder för prestandatestning](best-practices-for-performance-testing.md)
   + [Metodtips för frågor och indexering](best-practices-for-queries-and-indexing.md)
   + [Användargränssnitt Recommendations för kunder](ui-recommendations.md)
   + [Prestanda och skalbarhet](performance.md)
