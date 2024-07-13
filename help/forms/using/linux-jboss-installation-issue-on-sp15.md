---
title: AEM Forms JEE 6.5.15.0 Service Pack - installationsproblem i JBoss® Linux®-miljö
description: AEM Forms JEE 6.5.15.0 Service Pack är inte korrekt installerat i JBoss® Linux®-miljön. Eventuella korrigeringsändringar tillämpas inte på programservern. Lägg till filen RUP_BOM.xml i XML-katalogen.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# AEM Forms 6.5.15.0 JEE Service Pack - installationsproblem i JBoss®-miljö {#aem-forms-installation-issue-environment}

## Problem {#issue}

AEM Forms JEE 6.5.15.0 Service Pack är inte korrekt installerat i JBoss® Linux®-miljön. Loggposten `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing` loggas i filen `PatchInstallerProcessing[1-9*].log`. Detta anger att installationen av Service Pack för AEM Forms JEE 6.5.15.0 inte lyckas.

## Gäller för {#applies-to}

Denna lösning gäller
* JBoss® Linux® Environment

>[!NOTE]
>
> Kontrollera att AEM Forms JEE 6.5.15.0-Service Pack är installerat på programservern minst en gång innan du utför stegen i [lägger till filen RUP_BOM.xml i XML-katalogen](#solution-solution).

## Lösning {#solution}

För att åtgärda installationsproblemet med Service Pack för AEM Forms JEE 6.5.15.0 lägger du till filen `RUP_BOM.xml` i XML-katalogen:
1. Navigera till mappen där du extraherade korrigeringen `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Navigera till platsen `/CDROM_Installers/Linux/Disk1/InstData` och leta upp filen `Resource1.zip`.
1. Kopiera filen `Resource1.zip` på en annan plats utanför den extraherade mappen och packa upp filen `Resource1.zip`.
1. Navigera till `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` och kopiera filen `RUP_BOM.xml`.
1. Klistra in filen RUP_BOM.xml på `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Installera om [AEM Forms JEE 6.5.15.0 Service Pack ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
