---
title: Göra teckensnitt tillgängliga
seo-title: Göra teckensnitt tillgängliga
description: Kontrollera att teckensnitten som används i ett formulär är tillgängliga för användning på J2EE-programservern som är värd för AEM-formulär.
seo-description: Kontrollera att teckensnitten som används i ett formulär är tillgängliga för användning på J2EE-programservern som är värd för AEM-formulär.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Göra teckensnitt tillgängliga {#make-fonts-available}

Kontrollera att teckensnitten som används i ett formulär är tillgängliga för användning på J2EE-programservern som är värd för AEM-formulär. Ta till exempel följande scenario. En formulärdesigner lägger till ett teckensnitt i teckensnittskatalogen som Designer använder och skapar ett formulär som använder teckensnittet på en separat dator. För att Output-tjänsten ska kunna använda teckensnittet placerar du det i kundens teckensnittskatalog. Om kundens teckensnittskatalog inte finns skapar du en katalog på J2EE-programservern som är värd för AEM-formulär.

Mer information om ytterligare teckensnittsinställningar finns i [Konfigurera allmänna AEM-formulärsinställningar](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Ange platsen för kundens teckensnittskatalog**

1. I administrationskonsolen klickar du på Inställningar > Core Systems Settings > Configurations.
1. Ange sökvägen till kundens teckensnittskatalog i rutan Plats för systemteckensnittskatalogen. Flera kataloger kan läggas till, åtskilda med semikolon **;**
1. Klicka på OK.
1. Starta om systemet där AEM-formulär är installerade.

>[!NOTE]
>
> Teckensnitt hämtas från Windows-systemets teckensnittscache och en systemomstart krävs för att uppdatera cachen. När du har angett kundens teckensnittskatalog måste du starta om datorn där AEM-formulär är installerade.

