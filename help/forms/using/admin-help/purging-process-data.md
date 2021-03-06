---
title: Rensningsprocessdata
seo-title: Rensningsprocessdata
description: Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Se hur du kan tömma processdata.
seo-description: Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Se hur du kan tömma processdata.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Rensar processdata {#purging-process-data}

Processdata som genereras när en långvarig process anropas kan bli för stora, vilket kan ge sämre prestanda för AEM och kräver onödigt diskutrymme. Det är god praxis att rensa processdata när det inte längre behövs några poster. AEM innehåller flera sätt att rensa processdata:

* Du kan använda administrationskonsolen för att utföra en engångsåtervinning av föråldrade poster som rör långvariga processer eller för att schemalägga regelbundna automatiska rensningar. (Se [Rensa poster från jobbhanterardatabasen](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Du kan använda AEM Java API och webbtjänstAPI för att programmässigt rensa processdata som rör långvariga processer. (Se&quot;Rensa processdata&quot; i [Programmering med AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Använd processrensningsverktyget för att rensa processer baserat på processnamn och andra parametrar. Mer information finns i Viktigt-filen för processrensningsverktyget, som finns i *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.

