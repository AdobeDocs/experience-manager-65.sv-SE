---
title: Bädda in ett anpassningsbart formulär eller interaktiv kommunikation i AEM Sites Single Page Application
description: Bädda in adaptiva formulär eller interaktiv kommunikation på AEM Sites sidor. Användare kan fylla i och skicka formulär utan att lämna sidan Webbplatser.
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 0%

---

# Bädda in ett anpassningsbart formulär eller interaktiv kommunikation i AEM Sites Single Page Application{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

<span class="preview"> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE) för [att skapa nya adaptiva Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [att lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

## Ökning {#overview}

Med AEM Forms kan formulärutvecklare smidigt bädda in adaptiva formulär och interaktiv kommunikation i ett AEM Sites Single Page Application (SPA). Det inbäddade adaptiva formuläret och den interaktiva kommunikationen fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt kontext för andra element på webbsidan och interagera samtidigt med det adaptiva formuläret eller den interaktiva kommunikationen.

I AEM Sites Single Page Application kan du lägga till ett adaptivt formulär eller interaktiv kommunikation med komponenten [AEM Forms SPA Container](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) [.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Det är en AEM Forms-komponent för AEM Sites SPA som du kan lägga till på din webbplatssida.

Mer information om hur du bäddar in ett anpassat formulär i ett icke-SPA AEM Sites finns i [Bädda in ett anpassat formulär eller interaktiv kommunikation på AEM Sites sida](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Förutsättningar {#prerequisites}

Om du vill bädda in ett adaptivt formulär eller interaktiv kommunikation på en AEM webbplatser SPA med komponenten AEM Forms SPA Container kontrollerar du att du har installerat:

* Java SE Development Kit 8 eller senare
* Apache Maven 3.3.1 eller senare
* AEM författarinstans
* [AEM Forms 6.4.2-tilläggspaket](https://helpx.adobe.com/se/aem-forms/kb/aem-forms-releases.html) på författarinstans

## Installera AEM Forms SPA Container-komponenten {#install-aem-forms-spa-container-component}

Så här installerar du AEM Forms SPA Container-komponenten:

1. [Klona eller hämta AEM Forms-komponenten för SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installera AEM Forms-komponenten för SPA. Instruktionerna för att installera komponenten finns i filen [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   Komponenten innehåller en [exempelreaktionskomponent](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) som kan användas för att integrera SPA behållarkomponent med ett React-baserat SPA.

1. [Klona eller hämta ett React-baserat SPA](https://github.com/adobe/aem-sample-we-retail-journal).
1. Integrera SPA behållarkomponent med ett React-baserat SPA-projekt enligt instruktionerna i filen [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   När du har installerat komponenten AEM Forms SPA Container och integrerat komponenten med ett React-baserat SPA-projekt kan du bädda in adaptiva formulär och interaktiv kommunikation på AEM Sites-sidan.

## Bädda in ett anpassningsbart formulär eller interaktiv kommunikation {#af-component}

Så här bäddar du in ett adaptivt formulär eller interaktiv kommunikation med AEM Forms för SPA Container-komponenten:

1. Öppna sidan AEM webbplatser i redigeringsläge där du vill bädda in ett adaptivt formulär eller interaktiv kommunikation.
1. Infoga formuläret **AEM för SPA** på sidan med något av följande alternativ:

   * Markera layoutbehållaren på sidan Platser, markera **+** och välj komponenten **AEM Formulär för SPA**.

   * Dra och släpp **AEM-formuläret för komponenten SPA** på sidan från panelen Komponentwebbläsaren.
   * Sök efter ett anpassningsbart formulär eller en interaktiv kommunikation i webbläsaren Assets och dra och släpp det på sidan Webbplatser. Formuläret bäddas in i en AEM Forms för SPA.

   >[!NOTE]
   >
   >Återgivning av flera AEM Forms SPA Container-komponenter på en sida stöds inte. Du kan ha flera AEM Forms SPA Container på en sida, men bara en komponent i taget återges. Se till att endast en komponent är synlig på en sida för att undvika avvikelser.

1. Markera den inbäddade AEM Forms SPA Container-komponenten på webbplatssidan och välj sedan ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. Dialogrutan **Redigera AEM Forms SPA Container** öppnas.
1. Ange följande i dialogrutan **Redigera AEM Forms-behållare**:

   * **Resurstyp:** Välj den typ av resurs som ska bäddas in. Alternativen är **Adaptiv form** och **Interaktiv kommunikation**

   * **Resurssökväg**: Bläddra och välj det adaptiva formulär eller den interaktiva kommunikation som ska bäddas in. Fältet fylls i automatiskt om ett anpassningsbart formulär eller interaktiv kommunikation infogas med Assets webbläsare.
   * **Kanal** (endast interaktiv kommunikation): Välj vilken typ av interaktiv kanal som ska bäddas in. Alternativen är **Webbkanal** och **Utskriftskanal**.

   * **Tema**: Välj ett tema som definierar format för komponenter i ditt adaptiva formulär eller interaktiva kommunikation. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering.

1. Välj ![done_icon](assets/done_icon.png) om du vill spara inställningarna. Det adaptiva formuläret eller den interaktiva kommunikationen är nu inbäddat på sidan.

## Publish inbyggda adaptiva blanketter och interaktiv kommunikation {#publish-embedded-adaptive-form-and-interactive-communication}

Tänk på följande scenarier för publicering av inbäddade resurser (adaptiv form eller interaktiv kommunikation) på AEM Sites-sidan:

* Om du publicerar AEM Sites-sidan för första gången och den innehåller ett inbäddat adaptivt formulär eller interaktiv kommunikation publicerar du webbplatssidan och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret eller den interaktiva kommunikationen på en publicerad webbplats publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Sidan Publicerade platser innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du ändrade sidan Webbplatser och det inbäddade adaptiva formuläret eller Interaktiv kommunikation publicerar du om sidan Webbplatser och den inbäddade resursen.

## Ändra inbäddat adaptivt formulär och interaktiv kommunikation {#modify-embedded-adaptive-form-and-interactive-communication}

AEM webbplatssida innehåller en referens till det adaptiva formuläret och interaktiv kommunikation i AEM Forms Container. Därför behålls alla konfigurationer och egenskaper, som tema, format och överföringsåtgärd, som konfigurerats i det ursprungliga adaptiva formuläret och interaktiv kommunikation i det inbäddade adaptiva formuläret och interaktiv kommunikation.

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret och interaktiv kommunikation gör du något av följande.

* Öppna originalformuläret i adaptiva formulär eller interaktiv kommunikation i respektive redigerare och ändra dem.
* Markera det adaptiva formuläret eller den interaktiva kommunikationen på sidan Webbplatser i redigeringsläge och välj sedan **Redigera i ett nytt fönster**. Det ursprungliga formuläret öppnas i redigeringsläge.

## Överväganden och bästa praxis {#considerations-and-best-practices}

Tänk på följande när du bäddar in anpassningsbara formulär på AEM sidor:

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickat Forms på formulärportalen.
* Den skicka-åtgärd som är konfigurerad i det ursprungliga formuläret behålls i det inbäddade formuläret.
* Upplevelsemål och A/B-tester som konfigurerats på det ursprungliga formuläret fungerar inte i det inbäddade formuläret. Du kan dock använda målinriktning för upplevelser på sidan Webbplatser för att visa olika formulär baserade på användarprofiler.
* Om du har konfigurerat Adobe Analytics för det ursprungliga formuläret hämtas analysdata från det inbäddade formuläret i Adobe Analytics. Den är dock inte tillgänglig i rapporten för formuläranalys.
