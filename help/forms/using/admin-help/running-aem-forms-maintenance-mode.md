---
title: Köra AEM formulär i underhållsläge
seo-title: Running AEM forms in maintenance mode
description: Underhållsläget är användbart när du utför uppgifter som att korrigera en DSC-fil, uppgradera AEM formulär eller använda ett Service Pack-paket. Läs mer om hur du kör AEM formulär i underhållsläge.
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Köra AEM formulär i underhållsläge {#running-aem-forms-in-maintenance-mode}

Underhållsläget är användbart när du utför uppgifter som att korrigera en DSC-fil, uppgradera AEM formulär eller använda ett Service Pack-paket.

Undvik att anropa processer när servern är i underhållsläge. Detta är vad som händer om en process anropas medan servern är i underhållsläge:

* Om processen är långvarig läggs den till i jobbdatabasen, men startas inte. När du avslutar underhållsläget bearbetar AEM de långvariga jobben i kön, även om servern startades om i underhållsläge.
* Om processen är kort, behandlas den direkt.

**AEM formulär i underhållsläge**

1. I en webbläsare anger du:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Ett&quot;nu pausat&quot;-meddelande visas i webbläsarfönstret.

   >[!NOTE]
   >
   >Om du stänger av servern medan den är i underhållsläge är den fortfarande i underhållsläge när den startas om. Du måste stänga av underhållsläget när du är klar med underhållsåtgärderna.

**Kontrollera om AEM körs i underhållsläge**

1. I en webbläsare anger du:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   Statusen visas i webbläsarfönstret. Statusen &quot;true&quot; anger att servern körs i underhållsläge och &quot;false&quot; anger att servern inte är i underhållsläge.

**Inaktivera underhållsläge**

1. I en webbläsare anger du:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Ett meddelande som&quot;nu körs&quot; visas i webbläsarfönstret.
