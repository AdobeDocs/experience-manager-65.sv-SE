---
title: Översikt över hälsoövervakning
seo-title: Översikt över hälsoövervakning
description: Det här dokumentet innehåller en översikt över hälsoövervakaren och information om hur du kan komma åt den.
seo-description: Det här dokumentet innehåller en översikt över hälsoövervakaren och information om hur du kan komma åt den.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Översikt över hälsoövervakning {#overview-of-health-monitor}

Health Monitor ger viktig information om AEM-formulärsystemet, t.ex. serverinformation, minnesanvändning och processoranvändning. Det finns också tillgänglig statistik för Work Manager, t.ex. antalet arbetsobjekt eller jobb i kön och deras status. Du kan utföra följande uppgifter med Hälsoövervakning:

* Kontrollera att systemet körs som det ska
* Visa information för att hjälpa till att diagnostisera systemproblem när de uppstår
* Utför åtgärder på arbetsuppgifter eller jobb som visar problem
* Rensa inaktuella poster från Job Manager-databasen

Hälsoövervakarsidan i administrationskonsolen har tre flikar:

* På fliken System visas resursövervakningsdiagram och information om formulärservern (eller noden i en klustermiljö). (Se [Visa systeminformation](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* Fliken Arbetshanteraren visar data som är relaterade till Arbetshanteraren, t.ex. antalet arbetsobjekt i arbetshanterarkön. Du kan filtrera informationen genom att använda olika villkor eller hantera enskilda arbetsobjekt med åtgärdsverktygen. (Se [Visa statistik för Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* På fliken Schemaläggaren för jobbtömning kan du rensa bort inaktuella poster från jobbhanterardatabasen. (Se [Rensa poster från jobbhanterardatabasen](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

Webbsidan för Hälsoövervakning är ifylld med statistik som samlats in via ett Gemfire-API. Denna API identifierar automatiskt alla noder i ett kluster. Det löser också säkerhetsproblem som uppstår vid insamling av statistik från proxyservrar eller belastningsutjämnare. Det finns Java-alternativ för att finjustera hälsoövervakaren och därmed minska prestandan i AEM-formulärmiljön. (Se [Finjustera prestanda](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)för hälsoövervakning.)

**Hälsoövervakning för åtkomst**

1. Klicka på Hälsoövervakning i det övre högra hörnet på sidan i administrationskonsolen.

