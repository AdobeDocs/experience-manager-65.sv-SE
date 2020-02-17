---
title: Introduktion till att publicera formulär på en portal
seo-title: Introduktion till att publicera formulär på en portal
description: AEM Forms innehåller komponenter som du kan använda för att skapa din formulärportal. I den här artikeln beskrivs de tillgängliga komponenterna i formulärportalen.
seo-description: AEM Forms innehåller komponenter som du kan använda för att skapa din formulärportal. I den här artikeln beskrivs de tillgängliga komponenterna i formulärportalen.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Introduktion till att publicera formulär på en portal{#introduction-to-publishing-forms-on-a-portal}

## Översikt över komponenter i AEM Forms-portalen {#aem-forms-portal-components-overview}

I ett typiskt formulärcentrerat portalscenario är formulärutveckling och portalutveckling två osammanhängande aktiviteter. När formulärdesigners designar och lagrar formulär i en databas skapar webbutvecklare ett webbprogram som listar formulär och hanterar inskickandet av formulär. Formulär kopieras över till webbnivån eftersom det inte finns någon kommunikation mellan formulärdatabasen och webbprogrammet.

Sådana scenarier leder ofta till hanteringsproblem och produktionsförseningar. Om det till exempel finns en nyare version av ett formulär i databasen måste du ersätta formuläret på webbnivån, ändra webbprogrammet och distribuera om formuläret på den offentliga webbplatsen. Om du omdistribuerar webbprogrammet kan det orsaka serverdriftavbrott. Vanligtvis är serverns driftstopp en planerad aktivitet och därför kan ändringarna inte skickas direkt till den offentliga platsen.

AEM Forms innehåller portalkomponenter som minskar administrationskostnader och förseningar i produktionen. Komponenterna gör det möjligt för webbutvecklare att skapa och anpassa en formulärportal på webbplatser som skapats med Adobe Experience Manager (AEM).

![AEM Forms-portalen](assets/aem-forms-portal.png)

Med formulärportalkomponenterna kan du lägga till följande funktioner:

* Visa formulär i anpassade layouter. Layouter för listvyn, kortvyn och panelvyn medföljer. Du kan skapa egna layouter.
* Gör att du kan visa anpassade metadata och anpassade åtgärder när du listar dem.
* Visa en lista över formulär som publicerats av AEM Forms-användargränssnittet på den publiceringsinstans där Forms Portal-komponenter används.
* Tillåt slutanvändare att återge formulär i både HTML- och PDF-format.
* Använd anpassad HTML-profil för att återge formulär.
* Möjliggör sökning av formulär baserat på olika kriterier, t.ex. formuläregenskaper, metadata och taggar.
* Skicka formulärdata till en server.
* Använd anpassad CSS för att anpassa utseendet på portalen.
* Skapa länkar till formulär.
* Visar utkast och inskickat material som rör adaptiva formulär som skapats av slutanvändaren.

## Tillgängliga AEM Forms-portalkomponenter {#available-aem-forms-portal-components}

AEM Forms innehåller följande portalkomponenter som grupperats under komponentgrupperna **Document Services** och **Document Services Predicates** :

### Sök och visa {#search-amp-lister}

Med komponenten Sök och lista kan du lista formulär från formulärdatabasen på din portalsida, och du får konfigurationsalternativ för att lista formulär baserat på angivna villkor. Du kan också ange sökvillkor så att portalanvändarna kan söka i formulärlistan.

### Utkast och inskickat material {#drafts-amp-submissions}

Komponenten Sök och lista visar formulär som har publicerats av formulärförfattaren, medan komponenten Utkast och inskickningar visar formulär som har sparats som utkast för att senare kunna fylla i och skicka formulär. Den här komponenten ger en personaliserad upplevelse till alla inloggade användare.

### Link {#link}

Med länkkomponenten kan du skapa en länk till ett formulär var som helst på sidan. Tänk dig ett scenario där du erbjuder ett utbildningsprogram och du vill att dina användare ska skicka in ett formulär för registrering för kursen. På webbplatsen har du lagt ut programinformationen. Under informationen vill du skapa en länk till registreringsformuläret. Med länkkomponenten kan du skapa länken.

## Formulärportalens arbetsflöde {#forms-portal-workflow}

Med Forms Portal kan du lista formulär från formulärdatabasen på din portalsida. Du kan också ange sökvillkor så att portalanvändarna kan söka i formulärlistan. Du kan också använda komponenten Utkast och inskickningar för att visa formulär som har sparats som ett utkast för att fylla i senare och skickade formulär. Du måste utföra en viss uppsättning åtgärder innan de här funktionerna blir tillgängliga på en webbplatssida. Utför stegen i den listade sekvensen för att göra komponenterna och respektive funktioner tillgängliga på en webbplatssida:

1. **Aktivera komponenter** i Forms Portal:Komponenterna i formulärportalen är inte tillgängliga för användning. [Aktivera komponenterna från AEM-sidan](/help/forms/using/enabling-forms-portal-components.md) för en AEM Sites-sida.
1. **** Visa formulär på en sida (skapa formulärportalsida): Du kan lista formulär både på AEM Sites och på sidor som inte är från AEM Site. Listan innehåller formulär som är tillgängliga på publiceringsinstansen. Användaren kan öppna formulär och börja fylla i dem. När en användare öppnar ett formulär skapas en ny instans av formuläret:

   1. **Visa formulär på en AEM Sites-sida**: Lägg till **[Search &amp; Lister](../../forms/using/creating-form-portal-page.md)**-komponenten på sidan och konfigurera**[ listpanelen](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** i den för att lista formulär på en sida. Lägg till och konfigurera **sökfönsterkomponenten** i **sök- och listkomponenten** för att lägga till sökfunktioner på sidan. Sidan med formulärportalkomponenten kallas för [formulärportalsidan](../../forms/using/creating-form-portal-page.md).

   1. **** Visa formulär på en sida som inte är AEM Sites: Använd API:erna [för](/help/forms/using/listing-forms-webpage-using-apis.md) formulärportalsökning för att fråga efter, hämta och lista formulär på sidor som inte är AEM-webbplatser.

1. **Visa utkast och skickade formulär på en formulärportalsida**: Lägg till och konfigurera komponenten Utkast och inskickat material på formulärportalsidan. Komponenten visar alla formulär som är i utkastläge och de formulär som redan har skickats.

   Om du vill att ett skickat anpassat formulär ska visas på fliken Skicka anger du åtgärden **** Skicka till **[formulärportalåtgärden](configuring-submit-actions.md).**Du kan också aktivera alternativet Skicka i formulärportalen. När en användare skickar formuläret läggs formuläret till på fliken Skicka.

1. **** Konfigurera lagring för formulärdata som skickas och skickas: Som standard lagras utkast- och inskickningsdata i AEM-databasen. I en produktionsmiljö bör du inte lagra utkast eller inskickade formulärdata i AEM-databasen. [Konfigurera formulärportalkomponenten för att spara data på en säker plats](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **** (Valfritt) Anpassa komponenterna i formulärportalen: [Anpassa mallarna](../../forms/using/customizing-templates-forms-portal-components.md) för blankettportalsidor för att ge komponenterna ett distinkt utseende.
1. **** (Valfritt) Lägg till anpassade metadata i formulär: Lägg [in anpassade metadata i blanketter](../../forms/using/customizing-templates-forms-portal-components.md) för att förbättra listningen och sökupplevelsen.
1. **** Publicera formulärportalsidan: Din formulärportalsida är nu klar. Publicera sidan.

## Relaterade artiklar {#related-articles}

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](../../forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](../../forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Exempel för att integrera komponent för utkast och inlämning med databas](integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](../../forms/using/introduction-publishing-forms.md)

