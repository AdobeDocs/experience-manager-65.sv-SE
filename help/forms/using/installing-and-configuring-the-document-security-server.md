---
title: Installera och konfigurera dokumentsäkerhetsservern
seo-title: Installera och konfigurera dokumentsäkerhetsservern
description: 'Använd dokumentskydd för att på ett säkert sätt distribuera information som du har sparat i ett format som stöds. Endast behöriga användare har åtkomst till skyddade dokument. '
seo-description: 'Använd dokumentskydd för att på ett säkert sätt distribuera information som du har sparat i ett format som stöds. Endast behöriga användare har åtkomst till skyddade dokument. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# Installera och konfigurera dokumentsäkerhetsservern {#installing-and-configuring-the-document-security-server}

Använd dokumentskydd för att på ett säkert sätt distribuera information som du har sparat i ett format som stöds. Endast behöriga användare har åtkomst till skyddade dokument.

Adobe Experience Manager Forms dokumentsäkerhet säkerställer att endast behöriga användare kan använda dina dokument. Med dokumentsäkerhet kan du distribuera all information som du har sparat i ett format som stöds. Filformat som stöds är Adobe PDF (Portable Document Format) samt Microsoft Word-, Excel- och PowerPoint-filer.

Du kan skydda dokument med hjälp av profiler. De sekretessinställningar du anger i en profil avgör hur en mottagare kan använda ett dokument som du tillämpar profilen på. Du kan till exempel ange om mottagarna ska kunna skriva ut eller kopiera text, redigera text eller lägga till signaturer och kommentarer i skyddade dokument.

Profilerna lagras på dokumentsäkerhetsservern. du tillämpar profilerna på dokument via ditt klientprogram. När du tillämpar en profil på ett dokument skyddar sekretessinställningarna som anges i profilen den information som dokumentet innehåller. Du kan distribuera det profilskyddade dokumentet till mottagare som har behörighet enligt profilen.

Dokumentsäkerhet ger även klienter, tittare och indexerare möjlighet att skydda dokument, visa skyddade dokument och indexera skyddade dokument. Mer information om dokumentsäkerhet finns i [om dokumentsäkerhet](/help/forms/using/admin-help/document-security.md).

## Distributionstopologi {#deployment-topology}

Dokumentsäkerhetsfunktionerna är bara tillgängliga i AEM Forms på JEE. Du behöver en instans av AEM Forms på JEE. Du kan också skapa ett kluster eller en grupp med AEM Forms-servrar om det behövs. Följande topologi är en indikativ topologi för att köra dokumentsäkerhetsfunktionen. Mer information om topologin finns i [Arkitektur och distributionstopologier för AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

Bilden nedan visar den typiska arkitekturen för AEM Forms Document Security:

![](do-not-localize/document-security-typical-environment.png)

## Installera AEM Forms på JEE {#installing-aem-forms-on-jee}

Så här installerar och konfigurerar du AEM Forms på JEE:

1. Ladda ned installationsprogrammet för AEM 6.5 Forms på JEE från [Adobe Licensing Website (LWS)](https://licensing.adobe.com/). Du behöver ett giltigt Maintenance &amp; Support-avtal för att ladda ned installationsprogrammet.
1. Läs [AEM Forms på JEE-plattformar som stöds](/help/forms/using/aem-forms-jee-supported-platforms.md) och kontrollera att du har programvaran, maskinvaran, operativsystemen, programservern, databaserna, JDK:n och annan infrastruktur redo att installera AEM Forms på JEE.
1. (Endast icke-nyckelinstallation) Läs [Förbereder installation av AEM Forms single server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) eller [Förbereder installation av AEM Forms serverkluster](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) och klar för installation och konfigurering av AEM Forms på JEE.
1. Beroende på din miljö och programserver väljer du något av följande dokument och följer instruktionerna för att slutföra installationen

   * [Installera och distribuera AEM Forms på JEE med nyckelkörning i JBoss](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installera och distribuera AEM Forms på JEE för JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installera och distribuera AEM Forms på JEE för WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installera och distribuera AEM Forms på JEE för WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Konfigurera AEM Forms på JEE i JBoss-kluster](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Konfigurera AEM Forms på JEE i WebLogic-kluster](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Konfigurera AEM Forms på JEE i WebSphere-kluster](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >Välj alternativet Dokumentsäkerhet på skärmen Modulval i AEM Forms i konfigurationshanteraren för JEE. Alternativet Dokumentskydd kräver inte att någon annan modul är markerad.

## Nästa steg {#next-steps}

* [Konfigurera klient- och serveralternativ](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Skapa och hantera policyer](/help/forms/using/admin-help/creating-policies.md)
* [Skapa och hantera principuppsättningar](/help/forms/using/admin-help/creating-policy-sets.md)
