---
title: Introduktion till att publicera formulär på en portal
seo-title: Introduction to publishing forms on a portal
description: AEM Forms innehåller komponenter som du kan använda för att skapa din formulärportal. I den här artikeln beskrivs de tillgängliga komponenterna i formulärportalen.
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# Introduktion till att publicera formulär på en portal{#introduction-to-publishing-forms-on-a-portal}

## Översikt över komponenter i AEM Forms portal {#aem-forms-portal-components-overview}

I ett typiskt formulärcentrerat portalscenario är formulärutveckling och portalutveckling två osammanhängande aktiviteter. När formulärdesigners designar och lagrar formulär i en databas skapar webbutvecklare ett webbprogram som listar formulär och hanterar inskickandet av formulär. Forms kopieras till webbnivån eftersom det inte finns någon kommunikation mellan formulärdatabasen och webbprogrammet.

Sådana scenarier leder ofta till hanteringsproblem och produktionsförseningar. Om det till exempel finns en nyare version av ett formulär i databasen måste du ersätta formuläret på webbnivån, ändra webbprogrammet och distribuera om formuläret på den offentliga webbplatsen. Om du omdistribuerar webbprogrammet kan det orsaka serverdriftavbrott. Vanligtvis är serverns driftstopp en planerad aktivitet och därför kan ändringarna inte skickas direkt till den offentliga platsen.

AEM Forms tillhandahåller portalkomponenter som minskar administrationskostnaderna och förseningarna i produktionen. Komponenterna gör det möjligt för webbutvecklare att skapa och anpassa en formulärportal på webbplatser som skapats med Adobe Experience Manager (AEM).

![AEM Forms portal](assets/aem-forms-portal.png)

Med formulärportalkomponenterna kan du lägga till följande funktioner:

* Visa formulär i anpassade layouter. Layouter för listvyn, kortvyn och panelvyn medföljer. Du kan skapa egna layouter.
* Gör att du kan visa anpassade metadata och anpassade åtgärder när du listar dem.
* Visa en lista över formulär som publicerats av AEM Forms-gränssnittet på den publiceringsinstans där Forms Portal-komponenter används.
* Tillåt slutanvändare att återge formulär i både HTML och PDF.
* Använd den anpassade HTML-profilen för att återge formulär.
* Möjliggör sökning av formulär baserat på olika kriterier, t.ex. formuläregenskaper, metadata och taggar.
* Skicka formulärdata till en server.
* Använd anpassad CSS för att anpassa utseendet på portalen.
* Skapa länkar till formulär.
* Visar utkast och inskickat material som rör adaptiva formulär som skapats av slutanvändaren.

## Tillgängliga AEM Forms portalkomponenter {#available-aem-forms-portal-components}

AEM Forms tillhandahåller följande portalkomponenter som grupperats under **Dokumenttjänster** och **Document Services Predicates** komponentgrupper:

### Sök och visa {#search-amp-lister}

Med komponenten Sök och lista kan du lista formulär från formulärdatabasen på din portalsida, och du får konfigurationsalternativ för att lista formulär baserat på angivna villkor. Du kan också ange sökvillkor så att portalanvändarna kan söka i formulärlistan.

### Utkast och inskickat material {#drafts-amp-submissions}

Medan komponenten Sök och Lister visar formulär som har publicerats av Forms författare, visar komponenten Utkast och inskickningar formulär som har sparats som utkast för att fylla i senare och skickade formulär. Den här komponenten ger en personaliserad upplevelse till alla inloggade användare.

### Länk {#link}

Med länkkomponenten kan du skapa en länk till ett formulär var som helst på sidan. Tänk dig ett scenario där du erbjuder ett utbildningsprogram och du vill att dina användare ska skicka in ett formulär för registrering för kursen. På webbplatsen har du lagt ut programinformationen. Under informationen vill du skapa en länk till registreringsformuläret. Med länkkomponenten kan du skapa länken.

## Forms Portal Workflow {#forms-portal-workflow}

På Forms Portal kan du lägga in blanketter från blankettdatabasen på portalsidan. Du kan också ange sökvillkor så att portalanvändarna kan söka i formulärlistan. Du kan också använda komponenten Utkast och inskickningar för att visa formulär som har sparats som ett utkast för att fylla i senare och skickade formulär. Du måste utföra en viss uppsättning åtgärder innan de här funktionerna blir tillgängliga på en webbplatssida. Utför stegen i den listade sekvensen för att göra komponenterna och respektive funktioner tillgängliga på en webbplatssida:

1. **Aktivera Forms Portal-komponenter**: Komponenterna i formulärportalen är inte tillgängliga för användning. [Aktivera komponenterna från AEM](/help/forms/using/enabling-forms-portal-components.md) för en AEM Sites-sida.
1. **Visa formulär på en sida (skapa formulärportalsida):** Du kan lista formulär både på AEM Sites-sidor och på andra AEM webbplatssidor. Listan innehåller formulär som är tillgängliga på publiceringsinstansen. Användaren kan öppna formulär och börja fylla i dem. När en användare öppnar ett formulär skapas en ny instans av formuläret:

   1. **Visa formulär på en AEM Sites-sida**: Lägg till **[Sök och visa](../../forms/using/creating-form-portal-page.md)** till sidan och konfigurera **[Listruta](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** i den för att lista formulär på en sida. Lägg till och konfigurera **Sökruta** till **Sök och visa** -komponenten för att lägga till sökfunktioner på sidan. Sidan med formulärportalkomponenten kallas [formulärportalsida](../../forms/using/creating-form-portal-page.md).

   1. **Visa formulär på en sida som inte är AEM Sites:** Använd [API:er för formulärportalsökning](/help/forms/using/listing-forms-webpage-using-apis.md) att söka, hämta och lista formulär på icke-AEM Sites-sidor.

1. **Visa utkast och skickade formulär på en formulärportalsida**: Lägg till och konfigurera komponenten Utkast och inskickat material på formulärportalsidan. Komponenten visar alla formulär som är i utkastläge och de formulär som redan har skickats.

   Om du vill att ett skickat anpassat formulär ska visas på fliken Skicka anger du **Skicka åtgärd** till **[Forms Portal Submit Action](configuring-submit-actions.md).** Du kan också aktivera alternativet Skicka i Forms Portal. När en användare skickar formuläret läggs formuläret till på fliken Skicka.

1. **Konfigurera lagring för formulärdata som ska skickas och skickas:** Som standard lagras utkast- och inskickningsdata i AEM. I en produktionsmiljö bör du inte lagra utkast eller skickade formulärdata i AEM. [Konfigurera formulärportalkomponenten för att spara data på en säker plats](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(Valfritt) Anpassa komponenterna i formulärportalen:** [Anpassa mallarna för formulärportalsidor](../../forms/using/customizing-templates-forms-portal-components.md) för att ge komponenterna ett distinkt utseende.
1. **(Valfritt) Lägg till anpassade metadata i formulär:** [Lägga till anpassade metadata i formulär](../../forms/using/customizing-templates-forms-portal-components.md) för att förbättra listnings- och sökupplevelsen.
1. **Publicera formulärportalsidan:** Din formulärportalsida är nu klar. Publicera sidan.

## Relaterade artiklar {#related-articles}

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](../../forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](../../forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Exempel för att integrera komponent för utkast och inlämning med databas](integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](../../forms/using/introduction-publishing-forms.md)
