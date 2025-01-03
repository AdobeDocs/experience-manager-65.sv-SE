---
title: Aktivera och inaktivera säkert säkerhetskopieringsläge
description: På sidan Säkerhetskopieringsinställningar kan du använda AEM formulär i säkert säkerhetskopieringsläge så att du kan säkerhetskopiera databasen och GDS-katalogen (Global Document Storage). Lär dig hur du aktiverar och inaktiverar läget för säker säkerhetskopiering.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Aktivera och inaktivera säkert säkerhetskopieringsläge {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

På sidan Säkerhetskopieringsinställningar kan du använda AEM formulär i säkert säkerhetskopieringsläge så att du kan säkerhetskopiera databasen och GDS-katalogen (Global Document Storage).

AEM formulär är i säkert säkerhetskopieringsläge, men fungerar normalt, förutom att det inte aktivt tar bort filer från GDS-katalogen.

>[!NOTE]
>
>Om du anger det här alternativet säkerhetskopieras inte systemet. Systemet förbereds för säkerhetskopiering.

## Aktivera säkert säkerhetskopieringsläge {#enable-safe-backup-mode}

1. I administrationskonsolen klickar du på Inställningar > Core Systems Settings > Backup Settings.
1. På sidan Inställningar för säkerhetskopiering väljer du Använd i säkert säkerhetskopieringsläge och klickar på OK.

>[!NOTE]
>
>Om systemet redan körs i säkert säkerhetskopieringsläge skapas ingen ny reservation när du klickar på OK.

## Inaktivera säkert säkerhetskopieringsläge {#disable-safe-backup-mode}

1. I administrationskonsolen klickar du på Inställningar > Core Systems Settings > Backup Settings.
1. Avmarkera Använd i säkert säkerhetskopieringsläge på sidan Inställningar för säkerhetskopiering och klicka på OK.
