---
title: Köra AEM-formulär i underhållsläge
seo-title: Köra AEM-formulär i underhållsläge
description: Underhållsläget är användbart när du utför uppgifter som att åtgärda en DSC-fil, uppgradera AEM-formulär eller använda ett Service Pack-paket. Läs mer om hur du kör AEM-formulär i underhållsläge.
seo-description: Underhållsläget är användbart när du utför uppgifter som att åtgärda en DSC-fil, uppgradera AEM-formulär eller använda ett Service Pack-paket. Läs mer om hur du kör AEM-formulär i underhållsläge.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Köra AEM-formulär i underhållsläge {#running-aem-forms-in-maintenance-mode}

Underhållsläget är användbart när du utför uppgifter som att åtgärda en DSC-fil, uppgradera AEM-formulär eller använda ett Service Pack-paket.

Undvik att anropa processer när servern är i underhållsläge. Detta är vad som händer om en process anropas medan servern är i underhållsläge:

* Om processen är långvarig läggs den till i jobbdatabasen, men startas inte. När du avslutar underhållsläget bearbetar AEM-formulären de långvariga jobben i kön, även om servern startades om i underhållsläge.
* Om processen är kort, behandlas den direkt.

**Placera AEM-formulär i underhållsläge**

1. I en webbläsare anger du:

   `https://`*[värdnamnsportens ]*`:`*[]* `/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[administratörsanvändarnamn ]*`&password=`*[lösenord]*

   Ett&quot;nu pausat&quot;-meddelande visas i webbläsarfönstret.

   >[!NOTE]
   >
   >Om du stänger av servern medan den är i underhållsläge är den fortfarande i underhållsläge när den startas om. Du måste stänga av underhållsläget när du är klar med underhållsåtgärderna.

**Kontrollera om AEM-formulär körs i underhållsläge**

1. I en webbläsare anger du:

   `https://`*[värdnamn]:[portadministratörens ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[användarnamn]* `&password=`*[lösenord ]*

   Statusen visas i webbläsarfönstret. Statusen &quot;true&quot; anger att servern körs i underhållsläge och &quot;false&quot; anger att servern inte är i underhållsläge.

**Inaktivera underhållsläge**

1. I en webbläsare anger du:

   `https://`*[värdnamn]:[portadministratörens ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[användarnamn]* `&password=`*[lösenord ]*

   Ett meddelande som&quot;nu körs&quot; visas i webbläsarfönstret.

