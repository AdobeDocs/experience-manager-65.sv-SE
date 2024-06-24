---
title: Uppgradera till AEM 6.5 Forms på JEE
description: Du kan uppgradera direkt från AEM 6.1 Forms, AEM 6.2 Forms och LiveCycle ES4 SP1 till AEM 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Uppgradera till AEM 6.5 Forms på JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.18.0 Forms för JEE har två typer av installationsprogram: ett fullständigt installationsprogram och ett korrigeringsprogram.

**Fullständig installationsfil**: Du kan använda [AEM 6.5.18.0 i JEE, fullständigt installationsprogram](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) för att skapa nya AEM Forms-instanser eller utföra uppgraderingar från AEM 6.5.x.x Forms på JEE till AEM 6.5.18.0 Forms på JEE.

**Installationsprogram för korrigering**: [AEM 6.5.18.0 i JEE patch installer](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) är till för kunder som redan använder AEM 6.5.x.x. Du kan använda installationsprogrammet för korrigeringsfilen för att uppgradera till den senaste versionen av AEM Forms.

I följande tabell visas avsändare som använder fullständig installation och korrigeringsinstallation.

![Installationsscenario för fullständig installation och korrigering](assets/full-and-patch-installer.png)

Utför följande procedur för att använda det fullständiga installationsprogrammet för att uppgradera befintliga AEM Forms 6.5.x.x i JEE till AEM 6.5.18.0 Forms i JEE:

1. Ladda ned installationsprogrammet för AEM 6.5 Forms on JEE från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Du behöver ett giltigt Maintenance &amp; Support-avtal för att kunna använda installationsprogrammet.
1. Se [Upgrade checklist and planning](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) om du vill veta mer om vilka kontroller som ska utföras för att säkerställa en lyckad uppgradering.
1. Se [Förbered uppgradering till AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) för att lära sig mer och utföra de uppgifter som säkerställer att uppgraderingen körs korrekt med minimal drifttid på servern.
1. Beroende på din befintliga miljö och programserver väljer du något av följande dokument och följer instruktionerna.

   * [Uppgradera från AEM 6.3 eller AEM 6.4 Forms till AEM 6.5 Forms for JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [Uppgradera från AEM 6.3 eller AEM 6.4 Forms till AEM 6.5 Forms för WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [Uppgradera från AEM 6.3 eller AEM 6.4 Forms till AEM 6.5 Forms for JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

Direktuppgradering från LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms till AEM 6.5 Forms är inte tillgängligt. Du kan uppgradera till en eller flera versioner av LiveCycle eller AEM Forms och sedan uppgradera till AEM 6.5 Forms. En lista över mellanversioner och motsvarande uppgraderingsinstruktioner finns i [Välj en uppgraderingssökväg](upgrade.md).
