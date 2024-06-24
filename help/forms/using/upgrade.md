---
title: Uppgradera till AEM 6.5 Forms
description: Du kan uppgradera direkt från AEM 6.3 Forms och AEM 6.4 Forms till AEM 6.5 Forms.
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%

---

# Uppgradera till AEM 6.5 Forms {#upgrade-to-aem-forms}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html) |
| AEM 6.5 | Den här artikeln |


AEM 6.5 Forms innehåller flera nya funktioner och förbättringar som effektiviserar framtagning, hantering och användarupplevelser med formulär och korrespondenser. Mer information om alla nya funktioner och förbättringar i AEM 6.5 Forms finns i [Översikt över nya funktioner](../../forms/using/whats-new.md).

Du kan uppgradera din befintliga LiveCycle- eller AEM Forms-installation för att få tillgång till nya funktioner och förbättringar som finns i AEM 6.5 Forms samtidigt som befintliga data, processer och resurser bevaras intakta. Vid uppgradering bevaras också metadata och processernas status. Du kan välja ett uppgraderingsalternativ för att komma igång med uppgraderingen.

I följande diagram visas de tillgängliga uppgraderingsmöjligheterna för AEM Forms på OSGi:

![Uppgraderingsflöde för OSGi](do-not-localize/osgi-upgrade-path.png)

Du kan uppgradera direkt från:

* AEM 6.3 Forms on OSGi
* AEM 6.4 Forms on OSGi

Du kan också utföra en uppgradering från

* AEM 6.0 Forms on OSGi
* AEM 6.1 Forms on OSGi
* AEM 6.2 Forms on OSGi

I följande diagram visas de tillgängliga uppgraderingsmöjligheterna för AEM Forms på JEE:

![JEE upgrade 6.5](do-not-localize/jee-upgrade-6-5.png)


Du kan uppgradera direkt från:

* AEM 6.3 Forms on JEE
* AEM 6.4 Forms on JEE
* AEM 6.5.x.x Forms på JEE

Du kan också utföra en uppgradering från

* LiveCycle ES4 SP1
* AEM 6.0 Forms on JEE
* AEM 6.1 Forms on JEE
* AEM 6.2 Forms on JEE

AEM 6.5.18.0 Forms på JEE innehåller två typer av installationsprogram: [Fullständig installationsfil](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) och [Installationsprogram för korrigering](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

**Fullständig installationsfil**: Du kan använda det fullständiga installationsprogrammet för att ställa in nya AEM Forms-instanser eller utföra uppgraderingar från AEM 6.5.x.x Forms på JEE till AEM 6.5.18.0 Forms på JEE.

**Installationsprogram för korrigering**: Patch installer är avsett för kunder som redan använder AEM 6.5.x.x. Du kan använda installationsprogrammet för korrigeringsfilen för att uppgradera till den senaste versionen av AEM Forms.

I följande bild visas avsändare som använder det fullständiga installationsprogrammet och korrigeringsprogrammet.

![Installationsprogram för fullständig installation och korrigering](/help/forms/using/assets/full-and-patch-installer.png)

Se [Installationsanvisningar för AEM 6.5 Forms Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html) artikel för att installera den senaste Service Pack-versionen för JEE-miljön.

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->


