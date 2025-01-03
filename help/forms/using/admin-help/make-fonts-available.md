---
title: Göra teckensnitt tillgängliga
description: Kontrollera att teckensnitten som används i ett formulär är tillgängliga för användning på J2EE-programservern som är värd AEM formulär.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Göra teckensnitt tillgängliga {#make-fonts-available}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

Kontrollera att teckensnitten som används i ett formulär är tillgängliga för användning på J2EE-programservern som är värd AEM formulär. Ta till exempel följande scenario. En formulärdesigner lägger till ett teckensnitt i teckensnittskatalogen som Designer använder och skapar ett formulär som använder teckensnittet på en separat dator. För att Output-tjänsten ska kunna använda teckensnittet placerar du det i kundens teckensnittskatalog. Om kundens teckensnittskatalog inte finns skapar du en katalog på J2EE-programservern som AEM formulär.

Mer information om ytterligare teckensnittsinställningar finns i [Konfigurera allmänna inställningar AEM formulär](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Ange platsen för kundens teckensnittskatalog**

1. I administrationskonsolen klickar du på Inställningar > Core Systems Settings > Configurations.
1. Ange sökvägen till kundens teckensnittskatalog i rutan Plats för systemteckensnittskatalogen. Flera kataloger kan läggas till, avgränsade med semikolon **;**
1. Klicka på OK.
1. Starta om datorn där AEM har installerats.

>[!NOTE]
>
>Teckensnitt hämtas från Windows-systemets teckensnittscache och en systemomstart krävs för att uppdatera cachen. När du har angett kundens teckensnittskatalog måste du starta om systemet där AEM är installerat.
