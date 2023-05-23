---
title: AEM Forms JEE 6.5.15.0 Service Pack - installationsproblem i JBoss® Linux®-miljö
description: AEM Forms JEE 6.5.15.0 Service Pack är inte korrekt installerat i JBoss® Linux®-miljön. Eventuella korrigeringsändringar tillämpas inte på programservern. Lägg till filen RUP_BOM.xml i XML-katalogen.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
source-git-commit: b8c9e5cd3192b51954091b677d700c51617c9460
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# AEM Forms 6.5.15.0 JEE Service Pack - installationsproblem i JBoss®-miljö {#aem-forms-installation-issue-environment}

## Problem {#issue}

AEM Forms JEE 6.5.15.0 Service Pack är inte korrekt installerat i JBoss® Linux®-miljön. I `PatchInstallerProcessing[1-9*].log` arkivera loggposten, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`, loggas. Detta anger att installationen av Service Pack för AEM Forms JEE 6.5.15.0 inte lyckas.

## Gäller för {#applies-to}

Denna lösning gäller
* JBoss® Linux® Environment

>[!NOTE]
>
> Kontrollera att AEM Forms JEE 6.5.15.0 Service Pack är installerat på programservern minst en gång innan du utför stegen i [lägga till filen RUP_BOM.xml i XML-katalogen](#solution-solution).

## Lösning {#solution}

För att åtgärda installationsproblemet med Service Pack för AEM Forms JEE 6.5.15.0 lägger du till `RUP_BOM.xml` till XML-katalogen:
1. Navigera till mappen där du extraherade korrigeringen `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Navigera till `/CDROM_Installers/Linux/Disk1/InstData` plats och leta upp `Resource1.zip` -fil.
1. Kopiera `Resource1.zip` på en annan plats utanför den extraherade mappen och packa upp `Resource1.zip` -fil.
1. Navigera till `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` och kopiera `RUP_BOM.xml` -fil.
1. Klistra in filen RUP_BOM.xml på `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Installera om [AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
