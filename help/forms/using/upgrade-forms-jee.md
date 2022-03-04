---
title: Uppgradera till AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: Du kan uppgradera direkt från AEM 6.1 Forms, AEM 6.2 Forms och LiveCycle ES4 SP1 till AEM 6.3 Forms.
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: 96ba82e984d061d41bb55814d9e573326f9eaf67
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Uppgradera till AEM 6.5 Forms på JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms on JEE innehåller två typer av installationsprogram: Fullständigt installationsprogram och korrigeringsprogram.

**Fullständig installationsfil**: Du kan använda det fullständiga installationsprogrammet för att uppgradera från AEM 6.3 Forms på JEE eller AEM 6.4 på JEE till AEM 6.5.12.0 Forms på JEE. Det är också till för kunder som skapar nya AEM Forms-instanser och utför uppgraderingar som inte är på plats.

**Installationsprogram för korrigeringsfiler**: Patch installer är avsett för kunder som redan använder AEM 6.5.x.x. Du kan använda installationsprogrammet för korrigeringsfilen för att uppgradera till den senaste versionen av AEM Forms.

I följande tabell visas avsändare som använder fullständig installation och korrigeringsinstallation.

![](assets/full-and-patch-installer.png)

Utför följande procedur för att använda det fullständiga installationsprogrammet för att uppgradera befintliga AEM 6.3 Forms på JEE eller AEM 6.4 Forms på JEE till AEM 6.5.12.0 Forms på JEE:

1. Ladda ned installationsprogrammet för AEM 6.5 Forms on JEE från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Du behöver ett giltigt Maintenance &amp; Support-avtal för att kunna använda installationsprogrammet.
1. Se [Upgrade checklist and planning](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) om du vill veta mer om vilka kontroller som ska utföras för att säkerställa en lyckad uppgradering.
1. Se [Förbered uppgradering till AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) för att lära sig mer och utföra de uppgifter som säkerställer att uppgraderingen körs korrekt med minimal drifttid på servern.
1. Beroende på din befintliga miljö och programserver väljer du något av följande dokument och följer instruktionerna.

   * [Uppgradera från AEM 6.3 eller AEM 6.4 Forms till AEM 6.5 Forms for JBoss](http://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [Uppgradera från AEM 6.3 eller AEM 6.4 Forms till AEM 6.5 Forms för WebSphere](http://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [Uppgradera från AEM 6.3 eller AEM 6.4 Forms till AEM 6.5 Forms for JBoss Turnkey](http://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

Direktuppgradering från LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms till AEM 6.5 Forms är inte tillgängligt. Du kan uppgradera till en eller flera versioner av LiveCycle eller AEM Forms och sedan uppgradera från AEM 6.5 Forms. En lista över mellanversioner och motsvarande uppgraderingsinstruktioner finns i [Välj en uppgraderingssökväg](upgrade.md).
