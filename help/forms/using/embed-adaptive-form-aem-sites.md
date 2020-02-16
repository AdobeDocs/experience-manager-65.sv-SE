---
title: Bädda in ett anpassningsbart formulär eller interaktiv kommunikation på AEM-webbplatssidan
seo-title: Bädda in ett anpassningsbart formulär eller interaktiv kommunikation på AEM-webbplatssidan
description: Du kan bädda in anpassningsbara formulär på AEM-webbplatssidor. Användarna kan fylla i och skicka formulär utan att lämna webbplatsens sidor.
seo-description: Du kan bädda in anpassningsbara formulär på AEM-webbplatssidor. Användarna kan fylla i och skicka formulär utan att lämna webbplatsens sidor.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Bädda in ett anpassningsbart formulär eller interaktiv kommunikation på AEM-webbplatssidan {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Översikt {#overview}

Med AEM Forms kan formulärutvecklare smidigt bädda in adaptiva formulär och interaktiv kommunikation på en AEM Sites-sida eller en webbsida som ligger utanför AEM. Det inbäddade adaptiva formuläret och den interaktiva kommunikationen fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret eller interaktiv kommunikation.

Mer information om hur du bäddar in adaptiva formulär på en extern webbsida finns i [Bädda in adaptiva formulär på en extern webbsida](/help/forms/using/embed-adaptive-form-external-web-page.md).

På sidan AEM Sites kan du lägga till ett anpassningsbart formulär eller interaktiv kommunikation med:

* **[AEM Forms Container-komponenten](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**AEM Forms innehåller en komponent som du kan lägga till på webbplatsens sidor. Med komponenten AEM Forms Container kan du bädda in ett anpassningsbart formulär och interaktiv kommunikation.

* **[Resursläsaren](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**Alla formulär och interaktiv kommunikation du skapar finns under Assets. Du kan dra och släppa formuläret som en resurs på sidan.

## Förutsättningar {#prerequisites}

Om du vill bädda in ett adaptivt formulär eller interaktiv kommunikation på en AEM-webbplatssida som använder en redigerbar mall kontrollerar du att AEM-formulärkomponenten är konfigurerad som en tillåten komponent i den associerade mallen. Mer information finns i avsnittet **Regler och egenskaper (layoutbehållare)** i [Skapa sidmallar](/help/sites-authoring/templates.md).

Om en platssida använder en statisk mall måste du konfigurera den i styckesystemet på webbplatssidan. Mer information finns i [Konfigurera komponenter i designläge](/help/sites-authoring/default-components-designmode.md) .

## Bädda in ett anpassningsbart formulär eller interaktiv kommunikation {#af-component}

Så här bäddar du in ett anpassningsbart formulär eller interaktiv kommunikation med komponenten AEM Forms Container:

1. Öppna sidan AEM-webbplatser, i redigeringsläge, där du vill bädda in ett anpassningsbart formulär eller interaktiv kommunikation.
1. Dra och släpp AEM Forms Container-komponenten på sidan från panelen Komponentwebbläsaren.

   Du kan också söka efter ett anpassningsbart formulär eller en interaktiv kommunikation i Assets-webbläsaren och dra och släppa det på sidan Platser. Formuläret bäddas in i en AEM Forms Container.

   >[!NOTE]
   >
   >Komponenter i flera AEM Forms Container på en sida stöds inte.

1. Tryck på den inbäddade AEM Forms Container-komponenten på webbplatssidan och tryck sedan på ![settings_icon](assets/settings_icon.png) i åtgärdsfältet. Dialogrutan **[!UICONTROL Redigera AEM Forms Container]** öppnas.
1. Ange följande i dialogrutan Redigera AEM Forms Container.

   * **** Resurstyp: Välj vilken typ av resurs som ska bäddas in. Alternativen är anpassningsbar form och interaktiv kommunikation
   * **Resurssökväg**: Bläddra och välj det adaptiva formulär eller den interaktiva kommunikation som ska bäddas in. Den fylls i automatiskt om du släppte den från Assets-webbläsaren.
   * (Endast anpassat formulär) **Skicka** in: Välj den åtgärd som ska utlösas när formulär skickas. Du kan välja att visa ett tackmeddelande eller en tacksida.

      * **Tack**! Skriv ett meddelande med RTF-redigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
      * **Tack**! Bläddra och välj den sida som ska visas när formuläret skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
      * **Uppdatera sidan vid överföring**: Aktivera det här alternativet om du vill uppdatera sidan som innehåller det inbäddade adaptiva formuläret så att du kan visa tack-sidan. I annat fall ersätter tack-sidan det anpassade formuläret i AEM Forms-behållaren, utan att sidan uppdateras. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Tema**: Välj ett tema som definierar format för komponenter i ditt adaptiva formulär eller interaktiva kommunikation. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering.
   * **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
   * **CSS-klientbibliotek**: Ange sökväg till ett CSS-klientbibliotek.


1. Spara inställningarna. Det anpassningsbara formuläret eller den interaktiva kommunikationen är nu inbäddad på sidan.

## Publicera inbäddad adaptiv form och interaktiv kommunikation {#publishing-embedded-adaptive-form-and-interactive-communication}

Vi ska titta på följande scenarier för publicering av en inbäddad resurs (adaptiv form eller interaktiv kommunikation) på sidan AEM-webbplatser:

* Om du publicerar AEM-webbplatssidan för första gången och den innehåller ett inbäddat adaptivt formulär eller interaktiv kommunikation publicerar du webbplatssidan och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret eller den interaktiva kommunikationen på en publicerad webbplatssida publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du ändrade webbplatssidan och det inbäddade adaptiva formuläret eller den interaktiva kommunikationen publicerar du webbplatssidan och den inbäddade resursen igen.

## Modifiera inbäddad adaptiv form och interaktiv kommunikation {#modifying-embedded-adaptive-form-and-interactive-communication}

Sidan AEM-webbplatser innehåller en referens till det adaptiva formuläret och den interaktiva kommunikationen i AEM Forms Container. Därför behålls alla konfigurationer och egenskaper, som tema, format och överföringsåtgärd, som konfigurerats i den ursprungliga adaptiva formen och interaktiv kommunikation i den inbäddade adaptiva formen och i den interaktiva kommunikationen.

Gör något av följande om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret och den interaktiva kommunikationen.

* Öppna originalformuläret i anpassningsbara formulär eller interaktiv kommunikation i respektive redigerare och ändra dem.
* Tryck på det adaptiva formuläret eller den interaktiva kommunikationen inifrån webbplatssidan i redigeringsläge och tryck sedan på **[!UICONTROL Redigera i ett nytt fönster]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

>[!NOTE]
>
>De ändringar som gjorts i det ursprungliga adaptiva formuläret eller den interaktiva kommunikationen återspeglas automatiskt i det inbäddade formuläret. Publicera om det adaptiva formuläret, den interaktiva kommunikationen eller webbplatssidan så att ändringarna på den publicerade sidan återspeglas.

## Överväganden och bästa praxis {#considerations-and-best-practices}

Tänk på följande när du bäddar in adaptiva formulär på AEM-webbplatssidor:

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickade formulär på formulärportalen.
* Den skicka-åtgärd som är konfigurerad i det ursprungliga formuläret behålls i det inbäddade formuläret.
* Upplevelsemål och A/B-tester som konfigurerats på det ursprungliga formuläret fungerar inte i det inbäddade formuläret. Du kan dock använda målinriktning för upplevelser på webbplatssidan för att presentera olika formulär baserat på användarprofiler.
* Om du har konfigurerat Adobe Analytics för det ursprungliga formuläret hämtas analysdata från det inbäddade formuläret i Adobe Analytics. Den är dock inte tillgänglig i rapporten för formuläranalys.

