---
title: Översikt över utdatatjänsten
description: Med Output kan du sammanfoga XML-formulärdata med en formulärdesign som skapats i Designer för att skapa ett dokumentutdataflöde i olika format.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Översikt över utdatatjänsten {#overview-of-output-service}

Med Output kan du sammanfoga XML-formulärdata med en formulärdesign som skapats i Designer för att skapa ett dokumentutdataflöde i olika format. Utdataströmmen kan skickas till en nätverksskrivare, en lokal skrivare eller en diskfil

Du kan använda utdatasidan i administrationskonsolen för att administrera utdatatjänsten. De inställningar du konfigurerar används vid körning när motsvarande inställningar inte har angetts via AEM-API:t för formulär. Konfigurationen som görs via AEM formulär SDK åsidosätter inställningarna som konfigurerats med administrationskonsolen.

Mer information om Output-tjänsten finns i [Tjänstreferens](https://www.adobe.com/go/learn_aemforms_services_61).

På utdatasidorna i administrationskonsolen kan du utföra flera åtgärder:

* Ange teckenuppsättningar för internationalisering. (Se [Ändra teckenuppsättningen](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Ange absoluta och relativa sökvägar för URL:er, URI:er, XCI:er och filplatser. (Se [Ange filplatser för utdata](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Konfigurera cachestorlekar och principer. (Se [Ange cacheläge](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) och [Konfigurerar cacheinställningar](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Gör teckensnitt tillgängliga på programservern. (Se [Göra teckensnitt tillgängliga](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Ange teckensnitt som ska bäddas in. (Se [Ange teckensnitt som ska bäddas in](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Ange XCI-konfigurationsalternativ. (Se [Ange XCI-konfigurationsalternativ](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Ange säkerhetsinställningar. (Se [Ange säkerhetsinställningar](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

När du har ändrat inställningarna klickar du på Spara för att använda dem på Utdata. Du behöver inte starta om servern för att ändringarna ska börja gälla, men du kan behöva starta om utdatatjänsten när du konfigurerar cacheinställningarna.
