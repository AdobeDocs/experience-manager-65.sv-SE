---
title: Översikt över hälsoövervakning
description: Det här dokumentet innehåller en översikt över hälsoövervakaren och information om hur du kan komma åt den.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Översikt över hälsoövervakning {#overview-of-health-monitor}

Health Monitor ger viktig information om AEM som serverinformation, minnesanvändning och processoranvändning. Det finns också tillgänglig statistik för Work Manager, t.ex. antalet arbetsobjekt eller jobb i kön och deras status. Du kan utföra följande uppgifter med Hälsoövervakning:

* Kontrollera att systemet körs som det ska
* Visa information för att hjälpa till att diagnostisera systemproblem när de uppstår
* Utför åtgärder på arbetsuppgifter eller jobb som visar problem
* Rensa inaktuella poster från Job Manager-databasen

Hälsoövervakarsidan i administrationskonsolen har tre flikar:

* På fliken System visas resursövervakningsdiagram och information om Forms Server (eller noden i en klustrad miljö). (Se [Visa systeminformation](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* Fliken Arbetshanteraren visar data som är relaterade till Arbetshanteraren, t.ex. antalet arbetsobjekt i arbetshanterarkön. Du kan filtrera informationen genom att använda olika villkor eller hantera enskilda arbetsobjekt med åtgärdsverktygen. (Se [Visa statistik för Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* På fliken Schemaläggaren för jobbtömning kan du rensa bort inaktuella poster från jobbhanterardatabasen. (Se [Rensa poster från jobbhanterardatabasen](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

Webbsidan för Hälsoövervakaren innehåller statistik som samlats in via ett Gemfire-API. Denna API identifierar automatiskt alla noder i ett kluster. Det löser också säkerhetsproblem som uppstår vid insamling av statistik från proxyservrar eller belastningsutjämnare. Det finns Java-alternativ för att finjustera hälsoövervakaren och minska påverkan på prestanda i AEM formulärmiljö. (Se [Finjustera prestanda för hälsoövervakning](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Åtkomsthälsoövervakaren**

1. Klicka på Hälsoövervakning i det övre högra hörnet på sidan i administrationskonsolen.
