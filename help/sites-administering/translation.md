---
title: Översätta innehåll för flerspråkiga webbplatser
seo-title: Translating Content for Multilingual Sites
description: Lär dig hur du översätter innehåll för flerspråkiga webbplatser.
seo-description: Learn how to translate content for multilingual sites.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Översätta innehåll för flerspråkiga webbplatser {#translating-content-for-multilingual-sites}

Automatisera översättning av sidinnehåll, resurser och användargenererat innehåll för att skapa och underhålla flerspråkiga webbplatser. Om du vill automatisera arbetsflöden för översättning integrerar du översättare med AEM och skapar projekt för översättning av innehåll till flera språk. AEM har stöd för arbetsflöden för översättning mellan människor och datorer.

* Översättning: Innehållet skickas till översättningsleverantören och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.
* Maskinöversättning: Maskinöversättningstjänsten översätter ditt innehåll omedelbart.

Översättning av innehåll omfattar följande steg:

1. [Anslut AEM till översättningstjänstleverantören](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) och [skapa konfigurationer för översättningsintegreringsramverk](/help/sites-administering/tc-tic.md).
1. [Koppla samman sidorna på din språkinställning](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) med översättningstjänsten och ramverkskonfigurationerna.
1. [Identifiera innehållstypen](/help/sites-administering/tc-rules.md) att översätta.
1. [Förbered innehållet för översättning](/help/sites-administering/tc-prep.md) genom att skapa det överordnad språket och skapa rotsidorna för språkkopior.
1. [Skapa översättningsprojekt](/help/sites-administering/tc-manage.md) för att samla det innehåll som ska översättas och förbereda översättningsprocessen.
1. Använd översättningsprojekt för att [hantera innehållsöversättningsprocessen](/help/sites-administering/tc-manage.md).

Om översättningstjänsten inte har någon koppling till AEM stöder AEM manuell extrahering och återinfogning av översättningsinnehåll i XML-format.

>[!NOTE]
>
>Användaren måste vara medlem i projektadministratörsgruppen för att kunna använda funktionerna för språkkopiering.

## Bästa praxis {#best-practices}

The [Bästa praxis för översättning](/help/sites-administering/tc-bp.md) sidan innehåller viktig information om implementeringen.
