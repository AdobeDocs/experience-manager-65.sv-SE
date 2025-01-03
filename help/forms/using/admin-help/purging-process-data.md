---
title: Rensningsprocessdata
description: Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Se hur du kan tömma processdata.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Rensningsprocessdata {#purging-process-data}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Det är god praxis att rensa processdata när det inte längre behövs några poster. AEM innehåller flera sätt att rensa processdata:

* Du kan använda administrationskonsolen för att utföra en engångsåtervinning av föråldrade poster som rör långvariga processer eller för att schemalägga regelbundna automatiska rensningar. (Se [Rensa poster från jobbhanterardatabasen](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Du kan använda AEM Java API och webbtjänstAPI för att programmässigt rensa processdata som rör långvariga processer. (Se&quot;Tömma processdata&quot; i [Programmering med AEM formulär](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Använd processrensningsverktyget för att rensa processer baserat på processnamn och andra parametrar. Mer information finns i Viktigt-filen för processrensningsverktyget i *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
