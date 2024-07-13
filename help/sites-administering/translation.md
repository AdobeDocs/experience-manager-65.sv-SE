---
title: Översätta innehåll för flerspråkiga webbplatser
description: Lär dig hur du översätter innehåll för flerspråkiga webbplatser.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Översätta innehåll för flerspråkiga webbplatser {#translating-content-for-multilingual-sites}

Automatisera översättning av sidinnehåll, resurser och användargenererat innehåll för att skapa och underhålla flerspråkiga webbplatser. Om du vill automatisera arbetsflöden för översättning integrerar du översättare med AEM och skapar projekt för översättning av innehåll till flera språk. AEM har stöd för arbetsflöden för översättning mellan människor och datorer.

* Översättning till människor: Innehållet skickas till din översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.
* Maskinöversättning: Maskinöversättningstjänsten översätter ditt innehåll omedelbart.

Översättning av innehåll omfattar följande steg:

1. [Anslut AEM med översättningstjänstleverantören](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) och [skapa konfigurationer för översättningsintegreringsramverk](/help/sites-administering/tc-tic.md).
1. [Koppla sidorna på din språkinställning](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) till översättningstjänsten och ramverkskonfigurationerna.
1. [Identifiera den typ av innehåll ](/help/sites-administering/tc-rules.md) som ska översättas.
1. [Förbered innehållet för översättning](/help/sites-administering/tc-prep.md) genom att skapa språkinställningen och skapa rotsidorna för språkkopior.
1. [Skapa översättningsprojekt](/help/sites-administering/tc-manage.md) för att samla in innehållet som ska översättas och förbereda översättningsprocessen.
1. Använd översättningsprojekten för att [hantera innehållsöversättningsprocessen](/help/sites-administering/tc-manage.md).

Om översättningstjänsten inte har någon koppling till AEM stöder AEM manuell extrahering och återinfogning av översättningsinnehåll i XML-format.

>[!NOTE]
>
>Användaren måste vara medlem i gruppen projekt-administratörer för att kunna använda funktionerna för språkkopiering.

## Bästa praxis {#best-practices}

Sidan [Bästa praxis för översättning](/help/sites-administering/tc-bp.md) innehåller viktig information om din implementering.
