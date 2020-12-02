---
title: Översätta innehåll för flerspråkiga webbplatser
seo-title: Översätta innehåll för flerspråkiga webbplatser
description: Lär dig hur du översätter innehåll för flerspråkiga webbplatser.
seo-description: Lär dig hur du översätter innehåll för flerspråkiga webbplatser.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Översätter innehåll för flerspråkiga webbplatser {#translating-content-for-multilingual-sites}

Automatisera översättning av sidinnehåll, resurser och användargenererat innehåll för att skapa och underhålla flerspråkiga webbplatser. Om du vill automatisera arbetsflöden för översättning integrerar du översättare med AEM och skapar projekt för översättning av innehåll till flera språk. AEM har stöd för arbetsflöden för översättning mellan människor och datorer.

* Översättning: Innehållet skickas till översättningsleverantören och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.
* Maskinöversättning: Maskinöversättningstjänsten översätter ditt innehåll omedelbart.

Översättning av innehåll omfattar följande steg:

1. [Koppla AEM med översättningstjänsten ](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) och  [skapa konfigurationer](/help/sites-administering/tc-tic.md) för översättningsintegrering.
1. [Koppla sidorna i ditt språk till ](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) översättningstjänsten och ramverkskonfigurationerna.
1. [Identifiera vilken typ av ](/help/sites-administering/tc-rules.md) innehåll som ska översättas.
1. [Förbered innehållet för ](/help/sites-administering/tc-prep.md) översättning genom att skapa språket överordnad och skapa rotsidorna för språkkopior.
1. [Skapa översättningsprojekt ](/help/sites-administering/tc-manage.md) för att samla in det innehåll som ska översättas och förbereda översättningsprocessen.
1. Använd översättningsprojekten för att [hantera innehållsöversättningsprocessen](/help/sites-administering/tc-manage.md).

Om översättningstjänsten inte har någon koppling till AEM stöder AEM manuell extrahering och återinfogning av översättningsinnehåll i XML-format.

>[!NOTE]
>
>Användaren måste vara medlem i projektadministratörsgruppen för att kunna använda funktionerna för språkkopiering.

## Bästa praxis {#best-practices}

Sidan [Bästa praxis för översättning](/help/sites-administering/tc-bp.md) innehåller viktig information om implementeringen.
