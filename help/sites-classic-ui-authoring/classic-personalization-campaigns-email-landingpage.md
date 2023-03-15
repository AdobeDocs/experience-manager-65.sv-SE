---
title: Skapa en startsida för ett effektivt nyhetsbrev
seo-title: Creating an Effective Newsletter Landing Page
description: En effektiv startsida för nyhetsbrev hjälper er att få så många människor som möjligt att registrera sig för ert nyhetsbrev (eller andra e-postmarknadsföringskampanjer). Du kan använda den information du samlar in från nyhetsbrevet för att få leads.
seo-description: An effective newsletter landing page helps you get as many people as possible to sign up for your newsletter (or other email marketing campaign). You can use the information you gather from your newsletter sign ups to get leads.
uuid: 0799b954-076b-4e95-8724-3661ae8fddb6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b41de64a-7d27-4633-a8d5-ac91d47eb1bb
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# Skapa en startsida för ett effektivt nyhetsbrev{#creating-an-effective-newsletter-landing-page}

En effektiv startsida för nyhetsbrev hjälper er att få så många människor som möjligt att registrera sig för ert nyhetsbrev (eller andra e-postmarknadsföringskampanjer). Du kan använda den information du samlar in från nyhetsbrevet för att få leads.

Om du vill skapa en effektiv startsida för nyhetsbrevet måste du göra följande:

1. Skapa en lista för nyhetsbrevet så att andra kan prenumerera på det.
1. Skapa anmälningsformuläret. När du gör det lägger du till ett arbetsflödessteg som automatiskt lägger till personen som registrerar sig för nyhetsbrevet i din lista med leads.
1. Skapa en bekräftelsesida som tackar användarna för att de har anmält sig och eventuellt erbjuder dem en befordran.
1. Lägg på teasers.

>[!NOTE]
>
>Adobe planerar inte att ytterligare förbättra denna funktion (Hantera leads och listor).
>Rekommendationen är att [Adobe Campaign och integrationen med AEM](/help/sites-administering/campaign.md).

## Skapa en lista för nyhetsbrevet {#creating-a-list-for-the-newsletter}

Skapa en lista, till exempel **Geometrixx Newsletter**, i MCM för det nyhetsbrev som folk ska prenumerera på. Hur du skapar listor beskrivs i [Skapa listor](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

I följande exempel visas ett exempel på en lista:

![mcm_listcreate](assets/mcm_listcreate.png)

## Skapa ett anmälningsformulär {#create-a-sign-up-form}

Skapa ett registreringsformulär för nyhetsbrev där användarna kan prenumerera på taggar. Exempelwebbplatsen för Geometrixx innehåller en nyhetsbrevsida i verktygsfältet Geometrixx där du kan skapa ditt formulär.

Om du vill skapa ett eget nyhetsbrevformulär läser du i informationen om hur du skapar formulär i [Forms-dokumentation](/help/sites-authoring/default-components.md#form). Nyhetsbrevet använder taggarna från taggbiblioteket. Mer information om hur du lägger till ytterligare taggar finns i [Taggsadministration](/help/sites-authoring/tags.md#tagadministration).

De dolda fälten i följande exempel anger den minsta mängden information (e-post). Du kan dessutom lägga till fler fält senare, men detta påverkar konverteringsgraden.

Följande exempel är ett formulär som skapats på https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html.

1. Skapa formuläret.

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. Klicka **Redigera** i formulärkomponenten för att konfigurera formuläret så att det går till en Tack-sida (se [Skapa tacksidor](#creating-a-thank-you-page)).

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. Ange formuläråtgärden (d.v.s. vad som ska hända när du skickar formuläret) och konfigurera gruppen så att den tilldelar registrerade användare till listan som du skapade tidigare (t.ex. geometrixx-nyhetsbrev).

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### Skapa en tacksida {#creating-a-thank-you-page}

När användare klickar på **Prenumerera nu** vill du att sidan Tack ska öppnas automatiskt. Skapa sidan Tack på sidan Geometrixx Newsletter. När du har skapat nyhetsbrevformuläret redigerar du formulärelementet och lägger till sökvägen på tacksidan.

Om du skickar begäran tar det användaren till en **Tack** sida efter vilken de får ett e-postmeddelande. Denna tacksida skapades på /content/geometrixx/en/toolbar/newsletter/thanks_you.

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### Lägga till lärare {#adding-teasers}

Lägg till [teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) att inrikta sig på specifika målgrupper. Du kan till exempel lägga till lärare på sidan Tack och på registreringssidan för nyhetsbrev.

Så här lägger du till testare för att skapa en effektiv startsida för nyhetsbrevet:

1. Skapa en läcker paragraf för en gåva. Välj **Första** som strategi och innehåller text som informerar dem om vilken gåva de kommer att få.

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. Skapa ett underordnat stycke för sidan Tack. Välj **Första** som strategi och inkludera text som anger att presenten är på väg.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Skapa en kampanj med de två teasers - tagga en med företag och en utan taggar.

### Skicka innehåll till prenumeranter {#pushing-content-to-subscribers}

Gör ändringar i sidorna med funktionen för nyhetsbrev i MCM. Sedan skickar du uppdaterat innehåll till prenumeranterna.

Se [Skickar nyhetsbrev](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
