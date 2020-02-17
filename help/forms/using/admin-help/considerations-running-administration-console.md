---
title: Att tänka på vid körning av AdministrationConsole
seo-title: Att tänka på vid körning av AdministrationConsole
description: I det här dokumentet visas några punkter som du bör tänka på när du kör administrationskonsolen.
seo-description: I det här dokumentet visas några punkter som du bör tänka på när du kör administrationskonsolen.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Att tänka på när du kör administrationskonsolen {#considerations-when-running-administrationconsole}

Detta är några saker att tänka på när du kör administrationskonsolen:

* Om du öppnar administrationskonsolen via URL:en `https://[hostname]:[port]/adminui`får det angivna värdnamnet inte innehålla understreck. I annat fall kanske länkar till vissa delar av administrationskonsolen inte fungerar som de ska.
* Om du kör administrationskonsolen i Utforskaren i Windows på ett japanskt operativsystem kan du få följande problem:

   * När du klickar på en länk återgår du till inloggningssidan i stället för till den förväntade länken.
   * Om du klickar på en länk visas ett behörighetsfel.
   Det bästa sättet är att köra administrationskonsolen från en annan webbläsare, till exempel Mozilla Firefox, för att säkerställa att inga länkar fungerar.

* Använd inte omvända snedstreck () vid sökningar i administrationskonsolen.

