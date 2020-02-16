---
title: Bädda in ett anpassningsbart formulär eller interaktiv kommunikation i AEM Sites Single Page Application
seo-title: Bädda in adaptiva formulär eller interaktiv kommunikation på AEM Sites-sidor
description: Bädda in adaptiva formulär eller interaktiv kommunikation på AEM Sites-sidor. Användare kan fylla i och skicka formulär utan att lämna sidan Webbplatser.
seo-description: Du kan bädda in adaptiva formulär eller interaktiv kommunikation på AEM Sites-sidor. Användare kan fylla i och skicka formulär utan att lämna sidan Webbplatser.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# Bädda in ett anpassningsbart formulär eller interaktiv kommunikation i AEM Sites Single Page Application{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Översikt {#overview}

Med AEM Forms kan formulärutvecklare smidigt bädda in adaptiva formulär och interaktiv kommunikation i ett AEM Sites Single Page Application (SPA). Det inbäddade adaptiva formuläret och den interaktiva kommunikationen fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt kontext för andra element på webbsidan och interagera samtidigt med det adaptiva formuläret eller den interaktiva kommunikationen.

I AEM Sites Single Page Application kan du lägga till ett adaptivt formulär eller interaktiv kommunikation med komponenten [](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[AEM Forms SPA Container.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Det är en AEM Forms-komponent för AEM Sites SPA som du kan lägga till på din Sites-sida.

Mer information om hur du bäddar in ett anpassat formulär i en icke-SPA AEM Sites finns i [Bädda in ett anpassat formulär eller interaktiv kommunikation på sidan](/help/forms/using/embed-adaptive-form-aem-sites.md)AEM Sites.

## Förutsättningar {#prerequisites}

Om du vill bädda in ett adaptivt formulär eller interaktiv kommunikation på en AEM-webbplats SPA med komponenten AEM Forms SPA Container kontrollerar du att du har installerat:

* Java SE Development Kit 8 eller senare
* Apache Maven 3.3.1 eller senare
* AEM-författarinstans
* [AEM Forms 6.4.2-tilläggspaket](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) på författarinstans

## Installera komponenten för AEM Forms SPA-behållare {#install-aem-forms-spa-container-component}

Så här installerar du komponenten AEM Forms SPA Container:

1. [Klona eller hämta AEM Forms-komponenten för SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installera AEM Forms-komponenten för SPA. Instruktionerna för att installera komponenten finns i filen [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) .

   Komponenten innehåller en [exempelReact-komponent](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) som kan användas för att integrera SPA-behållarkomponenten med ett React-baserat SPA-projekt.

1. [Klona eller ladda ned ett React-baserat SPA-projekt](https://github.com/adobe/aem-sample-we-retail-journal).
1. Integrera SPA-behållarkomponenten med ett React-baserat SPA-projekt enligt instruktionerna i [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) -filen.

   När du har installerat komponenten AEM Forms SPA Container och integrerat komponenten med ett React-baserat SPA-projekt kan du bädda in adaptiva formulär och interaktiv kommunikation på sidan AEM Sites.

## Bädda in ett anpassningsbart formulär eller interaktiv kommunikation {#af-component}

Så här bäddar du in ett adaptivt formulär eller interaktiv kommunikation med hjälp av AEM Forms för komponenten SPA Container:

1. Öppna sidan AEM-webbplatser, i redigeringsläge, där du vill bädda in ett adaptivt formulär eller interaktiv kommunikation.
1. Infoga **AEM-formuläret för SPA** -komponenten på sidan med något av följande alternativ:

   * Tryck på layoutbehållaren på sidan Platser, tryck **+** och välj komponenten **AEM Form for SPA** .

   * Dra och släpp **AEM-formuläret för SPA** -komponenten på sidan från panelen Komponentwebbläsaren.
   * Sök efter ett adaptivt formulär eller interaktiv kommunikation i Assets-webbläsaren och dra och släpp det på Sites-sidan. Formuläret bäddas in i en AEM Forms for SPA-komponentbehållare.
   >[!NOTE]
   >
   >Återgivning av flera AEM Forms SPA-behållarkomponenter på en sida stöds inte. Du kan ha flera AEM Forms SPA-behållare på en sida, men bara en komponent i taget återges. Se till att endast en komponent är synlig på en sida för att undvika avvikelser.

1. Tryck på den inbäddade AEM Forms SPA Container-komponenten på webbplatssidan och tryck sedan på ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. Dialogrutan **Redigera AEM Forms SPA-behållare** öppnas.
1. Ange följande i dialogrutan **Redigera AEM Forms Container** :

   * **** Resurstyp: Välj vilken typ av resurs som ska bäddas in. Alternativen är **Adaptiv form** och **Interaktiv kommunikation**

   * **Resurssökväg**: Bläddra och välj det adaptiva formulär eller den interaktiva kommunikation som ska bäddas in. Fältet fylls i automatiskt om ett anpassningsbart formulär eller interaktiv kommunikation infogas med hjälp av Resursläsaren.
   * **Kanal** (endast interaktiv kommunikation): Välj vilken typ av interaktiv kanal som ska bäddas in. Alternativen är **Webbkanal** och **Utskriftskanal**.

   * **Tema**: Välj ett tema som definierar formatering för komponenter i ditt adaptiva formulär eller Interaktiv kommunikation. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering.

1. Tryck ![](assets/done_icon.png) för att spara inställningarna. Det adaptiva formuläret eller den interaktiva kommunikationen är nu inbäddat på sidan.

## Publicera inbäddade adaptiva formulär och interaktiv kommunikation {#publish-embedded-adaptive-form-and-interactive-communication}

Tänk på följande scenarier för publicering av en inbäddad resurs (adaptiv form eller interaktiv kommunikation) på sidan AEM Sites:

* Om du publicerar sidan AEM Sites för första gången och den innehåller ett inbäddat adaptivt formulär eller interaktiv kommunikation publicerar du sidan Sites och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret eller den interaktiva kommunikationen på en publicerad webbplats publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Sidan Publicerade platser innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du ändrade sidan Webbplatser och det inbäddade adaptiva formuläret eller Interaktiv kommunikation publicerar du om sidan Webbplatser och den inbäddade resursen.

## Ändra inbäddat adaptivt formulär och interaktiv kommunikation {#modify-embedded-adaptive-form-and-interactive-communication}

Sidan AEM-webbplatser innehåller en referens till det adaptiva formuläret och den interaktiva kommunikationen i AEM Forms Container. Därför behålls alla konfigurationer och egenskaper, som tema, format och överföringsåtgärd, som konfigurerats i det ursprungliga adaptiva formuläret och interaktiv kommunikation i det inbäddade adaptiva formuläret och interaktiv kommunikation.

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret och interaktiv kommunikation gör du något av följande.

* Öppna originalformuläret i adaptiva formulär eller interaktiv kommunikation i respektive redigerare och ändra dem.
* Tryck på det adaptiva formuläret eller den interaktiva kommunikationen från sidan Webbplatser i redigeringsläget och tryck sedan på **Redigera i ett nytt fönster**. Det ursprungliga formuläret öppnas i redigeringsläge.

## Överväganden och bästa praxis {#considerations-and-best-practices}

Tänk på följande när du bäddar in adaptiva formulär på AEM-webbplatssidor:

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickade formulär på formulärportalen.
* Den skicka-åtgärd som är konfigurerad i det ursprungliga formuläret behålls i det inbäddade formuläret.
* Upplevelsemål och A/B-tester som konfigurerats på det ursprungliga formuläret fungerar inte i det inbäddade formuläret. Du kan dock använda målinriktning för upplevelser på sidan Webbplatser för att visa olika formulär baserade på användarprofiler.
* Om du har konfigurerat Adobe Analytics för det ursprungliga formuläret hämtas analysdata från det inbäddade formuläret i Adobe Analytics. Den är dock inte tillgänglig i rapporten för formuläranalys.

