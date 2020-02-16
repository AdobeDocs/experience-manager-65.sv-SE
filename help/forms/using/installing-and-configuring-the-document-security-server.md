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

---


# Installera och konfigurera dokumentsäkerhetsservern {#installing-and-configuring-the-document-security-server}

Använd dokumentskydd för att på ett säkert sätt distribuera information som du har sparat i ett format som stöds. Endast behöriga användare har åtkomst till skyddade dokument.

Dokumentskyddet i Adobe Experience Manager Forms säkerställer att endast behöriga användare kan använda dina dokument. Med dokumentsäkerhet kan du distribuera all information som du har sparat i ett format som stöds. Filformat som stöds är Adobe PDF (Portable Document Format) samt Microsoft Word-, Excel- och PowerPoint-filer.

Du kan skydda dokument med hjälp av profiler. De sekretessinställningar du anger i en profil avgör hur en mottagare kan använda ett dokument som du tillämpar profilen på. Du kan till exempel ange om mottagarna ska kunna skriva ut eller kopiera text, redigera text eller lägga till signaturer och kommentarer i skyddade dokument.

Profilerna lagras på dokumentsäkerhetsservern. du tillämpar profilerna på dokument via ditt klientprogram. När du tillämpar en profil på ett dokument skyddar sekretessinställningarna som anges i profilen den information som dokumentet innehåller. Du kan distribuera det profilskyddade dokumentet till mottagare som har behörighet enligt profilen.

Dokumentsäkerhet ger även klienter, tittare och indexerare möjlighet att skydda dokument, visa skyddade dokument och indexera skyddade dokument. Mer information om dokumentsäkerhet finns [i Dokumentsäkerhet](/help/forms/using/admin-help/document-security.md).

## Distributionstopologi {#deployment-topology}

Funktionen för dokumentsäkerhet är bara tillgänglig i AEM Forms på JEE. Du behöver en instans av AEM Forms på JEE. Du kan också skapa ett kluster eller en grupp med AEM Forms-servrar om det behövs. Följande topologi är en indikativ topologi för att köra dokumentsäkerhetsfunktionen. Mer information om topologin finns i [Arkitektur och distributionstopologier för AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

I följande diagram visas den typiska arkitekturen för AEM Forms Document Security:

![](do-not-localize/document-security-typical-environment.png)

## Installera AEM-formulär på JEE {#installing-aem-forms-on-jee}

Så här installerar och konfigurerar du AEM Forms på JEE:

1. Ladda ned AEM 6.5 Forms on JEE installer från [Adobes licenswebbplats (LWS)](https://licensing.adobe.com/). Du behöver ett giltigt Maintenance &amp; Support-avtal för att ladda ned installationsprogrammet.
1. Läs dokumentet [](/help/forms/using/aem-forms-jee-supported-platforms.md) AEM Forms on JEE Supported Platforms (AEM-formulär på JEE-plattformar som stöds) och kontrollera att du har programvaran, maskinvaran, operativsystemen, programservern, databaserna, JDK:er och annan infrastruktur redo att installera AEM Forms på JEE.
1. (Endast icke-nyckelinstallationer) Läs [Förberedelsen för att installera AEM Forms på en enda server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) eller [Förbereda för att installera AEM Forms-serverklustret](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) och förbered miljön för att installera och konfigurera AEM Forms på JEE.
1. Beroende på din miljö och programserver väljer du något av följande dokument och följer instruktionerna för att slutföra installationen

   * [Installera och distribuera AEM Forms på JEE med nyckelord för JBoss](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installera och distribuera AEM-formulär på JEE för JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installera och distribuera AEM-formulär på JEE för WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installera och distribuera AEM-formulär på JEE för WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Konfigurera AEM-formulär på JEE i JBoss-kluster](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Konfigurera AEM-formulär på JEE i WebLogic-kluster](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Konfigurera AEM Forms på JEE i WebSphere-kluster](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)
   >[!NOTE]
   >
   >Välj alternativet Dokumentsäkerhet på skärmen Modulval i AEM Forms on JEE configuration manager. Alternativet Dokumentskydd kräver inte att någon annan modul är markerad.

## Nästa steg {#next-steps}

* [Konfigurera klient- och serveralternativ](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Skapa och hantera policyer](/help/forms/using/admin-help/creating-policies.md)
* [Skapa och hantera principuppsättningar](/help/forms/using/admin-help/creating-policy-sets.md)
