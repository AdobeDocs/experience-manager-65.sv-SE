---
title: Rensningsprocessdata
seo-title: Purging process data
description: Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Se hur du kan tömma processdata.
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Rensningsprocessdata {#purging-process-data}

Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Det är god praxis att rensa processdata när det inte längre behövs några poster. AEM innehåller flera sätt att rensa processdata:

* Du kan använda administrationskonsolen för att utföra en engångsåtervinning av föråldrade poster som rör långvariga processer eller för att schemalägga regelbundna automatiska rensningar. (Se [Rensa poster från Job Manager-databasen](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Du kan använda AEM Java API och webbtjänstAPI för att programmässigt rensa processdata som rör långvariga processer. (Se&quot;Rensa processdata&quot; i [Programmera med AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Använd processrensningsverktyget för att rensa processer baserat på processnamn och andra parametrar. Mer information finns i Viktigt-filen för processrensningsverktyget i *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
