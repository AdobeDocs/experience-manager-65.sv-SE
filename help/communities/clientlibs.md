---
title: Clientlibs for Communities Components
description: Lär dig hur du lägger till klientbibliotek (klientbibliotek) på en sida så att du kan samla in användningsinformation och använda felsökningsverktyg för communitykomponenter.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Clientlibs for Communities Components {#clientlibs-for-communities-components}

## Introduktion {#introduction}

I det här avsnittet av dokumentationen beskrivs hur du lägger till klientbibliotek (klientbibliotek) på en sida för webbgruppskomponenter.

Grundläggande information finns i följande:

* [Använda bibliotek på klientsidan](/help/sites-developing/clientlibs.md) som innehåller användningsinformation och felsökningsverktyg
* [Clientlibs for SCF](/help/communities/client-customize.md#clientlibs) som ger användbar information när du anpassar SCF-komponenter


## Varför Clientlibs krävs {#why-clientlibs-are-required}

Clientlibs krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När det finns en [communityfunktion](/help/communities/functions.md) för en funktion finns alla nödvändiga komponenter och konfigurationer, inklusive de nödvändiga klientlibs, på communitywebbplatsen. Bara om ytterligare komponenter ska vara tillgängliga för författare måste ytterligare klientlib läggas till.

När de nödvändiga klientlibs saknas, [lägga till en webbgruppskomponent på en sida](/help/communities/author-communities.md) kan resultera i JavaScript-fel och ett oväntat utseende.

### Exempel: Monterade granskningar utan Clientlibs {#example-placed-reviews-without-clientlibs}

![monterade granskningar](assets/placed-reviews.png)

### Exempel: Monterade granskningar med Clientlibs {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## Identifiera nödvändiga klienter {#identifying-required-clientlibs}

Den viktigaste funktionsinformationen för utvecklare identifierar de nödvändiga klientlibs.

Från en AEM förekomst bläddrar du dessutom till [Guide för communitykomponenter](/help/communities/components-guide.md) ger åtkomst till en lista över de klientlibkategorier som krävs för en komponent.

Till exempel längst upp på [Granskningssida](https://localhost:4502/content/community-components/en/reviews.html) de nödvändiga listorna är

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## Lägga till nödvändiga klienter {#adding-required-clientlibs}

När du vill lägga till en webbgruppskomponent på en sida måste du lägga till de nödvändiga klientlibs för komponenten om det inte redan finns.

Använd [CRXDE|Lite](#using-crxde-lite) om du vill ändra en befintlig klientlistorlista för en communitywebbplats.

Så här lägger du till en klientlib för en community-webbplats med [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Bläddra till [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Leta reda på `clientlibslist` nod för den sida där du vill lägga till komponenten:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Med `clientlibslist` markerad nod:

   * Leta reda på strängen[] property `scg:requiredClientLibs`.
   * Välj `Value` så att du kan komma åt dialogrutan String-array.

      * Bläddra nedåt om det behövs.
      * Välj + för att ange ett nytt klientbibliotek.

         * Upprepa om du vill lägga till fler klientbibliotek.

         * Välj **OK**.

   * Välj **Spara alla**.

>[!NOTE]
>
>Om webbplatsen inte är en communitywebbplats måste förekomsten eller platsen för klientbiblioteken som används för webbplatsen upptäckas.

Använda [Komma igång med AEM Communities](/help/communities/getting-started.md) exempel, där `site-name` är *engagera*, är det så här klienten visas om du lägger till granskningskomponenten:

![review-component](assets/review-component.png)
