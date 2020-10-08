---
title: Clientlibs for Communities Components
seo-title: Clientlibs for Communities Components
description: Klientbibliotek för Communities
seo-description: Klientbibliotek för Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Clientlibs for Communities Components {#clientlibs-for-communities-components}

## Introduktion {#introduction}

I det här avsnittet av dokumentationen beskrivs hur du lägger till klientbibliotek (klientbibliotek) på en sida för webbgruppskomponenter.

Grundläggande information finns på

* [Använda bibliotek](/help/sites-developing/clientlibs.md) på klientsidan som innehåller användarinformation och felsökningsverktyg
* [Clientlibs for SCF](/help/communities/client-customize.md#clientlibs) som ger användbar information när du anpassar SCF-komponenter
* [Blogg: AEM Client Libraries förklaras av exempel](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Varför Clientlibs krävs {#why-clientlibs-are-required}

Clientlibs krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När det finns en [communityfunktion](/help/communities/functions.md) för en funktion kommer alla nödvändiga komponenter och konfigurationer, inklusive de nödvändiga klientlibs, att finnas på communitywebbplatsen. Det är bara om ytterligare komponenter ska vara tillgängliga för författare som måste läggas till ytterligare klientlib.

När de nödvändiga klientlibs saknas kan det leda till javascript-fel och ett oväntat utseende om du [lägger till en webbgruppskomponent på en sida](/help/communities/author-communities.md) .

### Exempel: Monterade granskningar utan Clientlibs {#example-placed-reviews-without-clientlibs}

![monterade granskningar](assets/placed-reviews.png)

### Exempel: Monterade granskningar med Clientlibs {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## Identifiera nödvändiga klienter {#identifying-required-clientlibs}

Den viktigaste funktionsinformationen för utvecklare identifierar de nödvändiga klientlibs.

Om du AEM till [Community Components Guide](/help/communities/components-guide.md) får du dessutom tillgång till en lista med de clientlib-kategorier som krävs för en komponent.

Till exempel, högst upp på sidan [](https://localhost:4502/content/community-components/en/reviews.html) Recensioner, visas de klickbara listerna

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## Lägga till nödvändiga klienter {#adding-required-clientlibs}

När du vill lägga till en webbgruppskomponent på en sida måste du lägga till de nödvändiga klientlibs för komponenten om det inte redan finns.

Använd [CRXDE|Lite](#using-crxde-lite) för att ändra en befintlig klientlibslista för en communitywebbplatssida.

Så här lägger du till en klientlib för en community-webbplats med [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Gå till [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Leta reda på `clientlibslist` noden för sidan där du vill lägga till komponenten:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Med `clientlibslist` nod markerad:

   * Leta reda på egenskapen String[] `scg:requiredClientLibs`.
   * Välj dess `Value` för att öppna dialogrutan String-array.

      * Bläddra nedåt om det behövs.
      * Välj + för att ange ett nytt klientbibliotek.

         * Upprepa om du vill lägga till fler klientbibliotek.

         * Välj **OK**.
   * Välj **Spara alla**.


>[!NOTE]
>
>Om webbplatsen inte är en communitywebbplats måste förekomsten eller platsen för klientbiblioteken som används för webbplatsen identifieras.

I exemplet [Komma igång med AEM Communities](/help/communities/getting-started.md) , där `site-name` är *engagerande*, visas klienten så här om du lägger till granskningskomponenten:

![review-component](assets/review-component.png)

