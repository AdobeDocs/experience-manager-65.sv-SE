---
title: Grunderna för att konfigurera formulär
seo-title: Grunderna för att konfigurera formulär
description: Lär dig mer om de olika formulärtjänsterna som hjälper dig att skapa interaktiva program för datainhämtning.
seo-description: Lär dig mer om de olika formulärtjänsterna som hjälper dig att skapa interaktiva program för datainhämtning.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Grunderna för att konfigurera formulär {#basics-of-configuring-forms}

Med tjänsten Forms kan du skapa interaktiva klientapplikationer för datainhämtning som validerar, bearbetar, omvandlar och levererar blanketter som vanligtvis skapas i Designer. Formulärförfattare utvecklar en enda formulärdesign som Forms-tjänsten återger i olika format:

* som PDF i Adobe Reader eller i en webbläsare
* som HTML i olika webbläsarmiljöer, inklusive kompatibel XHTML 1.0-återgivning
* som formulärguider i olika webbläsarmiljöer som stöder Adobe Flash Player.

Mer information om tjänsten Forms finns i [Tjänstreferens](https://www.adobe.com/go/learn_aemforms_services_63).

Med hjälp av Forms-sidan i administrationskonsolen kan du konfigurera beteendet för Forms-tjänsten. De här inställningarna gäller för alla anrop av tjänsten. Alla parametrar som skickas via AEM formulär SDK åsidosätter de inställningar som angetts i administrationskonsolen. De påverkar dock bara det specifika anropet.

När du har ändrat Forms-inställningarna i administrationskonsolen klickar du på Spara. Du behöver inte starta om servern för att ändringarna ska börja gälla. Du kan dock behöva stoppa och starta om tjänsten Forms när du konfigurerar inställningar för cacheläge. (Se [Starta och stoppa tjänster](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
