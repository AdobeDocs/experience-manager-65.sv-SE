---
title: Översätta innehåll för flerspråkiga webbplatser
description: Lär dig hur du översätter innehåll för flerspråkiga webbplatser.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
source-git-commit: 3f5173c0c2b17e8cf560753088451f78c6529f5c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Översätta innehåll för flerspråkiga webbplatser {#translating-content-for-multilingual-sites}

Automatisera översättning av sidinnehåll, resurser och användargenererat innehåll för att skapa och underhålla flerspråkiga webbplatser. Om du vill automatisera arbetsflöden för översättning integrerar du översättare med AEM och skapar projekt för översättning av innehåll till flera språk. AEM har stöd för arbetsflöden för översättning mellan människor och datorer.

* Översättning till människor: Innehållet skickas till din översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.
* Maskinöversättning: Maskinöversättningstjänsten översätter ditt innehåll omedelbart.

Översättning av innehåll omfattar följande steg:

1. [Anslut AEM till översättningstjänstleverantören](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) och [skapa konfigurationer för översättningsintegreringsramverk](/help/sites-administering/tc-tic.md).
1. [Associera sidorna i din språkinställning](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) med översättningstjänsten och ramverkskonfigurationerna.
1. [Identifiera innehållstypen](/help/sites-administering/tc-rules.md) att översätta.
1. [Förbered innehållet för översättning](/help/sites-administering/tc-prep.md) genom att skapa språkinställningarna och skapa rotsidorna för språkkopior.
1. [Skapa översättningsprojekt](/help/sites-administering/tc-manage.md) för att samla det innehåll som ska översättas och förbereda översättningsprocessen.
1. Använd översättningsprojekt för att [hantera innehållsöversättningsprocessen](/help/sites-administering/tc-manage.md).

Om översättningstjänsten inte har någon koppling till AEM stöder AEM manuell extrahering och återinfogning av översättningsinnehåll i XML-format.

>[!NOTE]
>
>Användaren måste vara medlem i gruppen projekt-administratörer för att kunna använda funktionerna för språkkopiering.

## Bästa praxis {#best-practices}

The [Bästa praxis för översättning](/help/sites-administering/tc-bp.md) sidan innehåller viktig information om implementeringen.
