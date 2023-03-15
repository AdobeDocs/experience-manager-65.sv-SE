---
title: Clientlibs for Communities Components
seo-title: Clientlibs for Communities Components
description: Klientbibliotek för Communities
seo-description: Client-side libraries for Communities
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Clientlibs for Communities Components {#clientlibs-for-communities-components}

## Introduktion {#introduction}

I det här avsnittet av dokumentationen beskrivs hur du lägger till klientbibliotek (klientbibliotek) på en sida för webbgruppskomponenter.

Grundläggande information finns på

* [Använda bibliotek på klientsidan](/help/sites-developing/clientlibs.md) som innehåller användningsinformation och felsökningsverktyg
* [Clientlibs for SCF](/help/communities/client-customize.md#clientlibs) som ger användbar information när du anpassar SCF-komponenter


## Varför Clientlibs krävs {#why-clientlibs-are-required}

Clientlibs krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När det finns en [communityfunktion](/help/communities/functions.md) för en funktion kommer alla nödvändiga komponenter och konfigurationer, inklusive nödvändiga klienter, att finnas på communitywebbplatsen. Det är bara om ytterligare komponenter ska vara tillgängliga för författare som måste läggas till ytterligare klientlib.

När de nödvändiga klientlibs saknas, [lägga till en webbgruppskomponent på en sida](/help/communities/author-communities.md) kan resultera i javascript-fel och ett oväntat utseende.

### Exempel: Monterade granskningar utan Clientlibs {#example-placed-reviews-without-clientlibs}

![monterade granskningar](assets/placed-reviews.png)

### Exempel: Monterade granskningar med Clientlibs {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## Identifiera nödvändiga klienter {#identifying-required-clientlibs}

Den viktigaste funktionsinformationen för utvecklare identifierar de nödvändiga klientlibs.

Från en AEM förekomst bläddrar du dessutom till [Community Components Guide](/help/communities/components-guide.md) ger åtkomst till en lista över de klientlibkategorier som krävs för en komponent.

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
   * Välj `Value` för att komma åt dialogrutan String-array.

      * Bläddra nedåt om det behövs.
      * Välj + för att ange ett nytt klientbibliotek.

         * Upprepa om du vill lägga till fler klientbibliotek.

         * Välj **OK**.
   * Välj **Spara alla**.


>[!NOTE]
>
>Om webbplatsen inte är en communitywebbplats måste förekomsten eller platsen för klientbiblioteken som används för webbplatsen identifieras.

Använda [Komma igång med AEM Communities](/help/communities/getting-started.md) exempel, där `site-name` är *engagera*, är det så här klienten visas om du lägger till granskningskomponenten:

![review-component](assets/review-component.png)
