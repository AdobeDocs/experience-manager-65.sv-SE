---
title: Lägg till versioner, kommentarer och anteckningar i AEM 6.5 adaptive form.
description: Använd AEM 6.5 adaptiva formulärkärnkomponenter för att lägga till kommentarer, anteckningar och versionshantering i ett adaptivt formulär.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
source-git-commit: a4e155de8a4f60d3746cecea110466b1d5d44dbb
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Versionshantering, granskning och kommentering i ett adaptivt formulär

<!--
<span class="preview"> This feature is under the Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>
-->

<span class="preview"> Den här funktionen är under det tidiga adopterprogrammet. Om du är intresserad av att delta i vårt program för tidig åtkomst för den här funktionen kan du skicka ett e-postmeddelande från din officiella adress till aem-forms-ea@adobe.com och begära åtkomst till </span>

Med de adaptiva kärnkomponenterna kan formulärförfattare lägga till versionshantering, kommentarer och anteckningar i formulär. Dessa funktioner förenklar formulärutvecklingen genom att man kan skapa och hantera flera versioner, samarbeta genom kommentarer och lägga in kommentarer i specifika formuläravsnitt, vilket förbättrar formulärbyggandet.

## Förutsättning {#prerequisite-versioning}

Om du vill använda versionshantering, kommentarer och anteckningsfunktioner i ett adaptivt formulär kontrollerar du att [kärnkomponenterna för det adaptiva formuläret](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components) är aktiverade i din AEM 6.5 Forms-miljö.

## Versionshantering av anpassningsbara formulär {#adaptive-form-versioning}

Med anpassad formulärversionshantering kan du lägga till versioner i ett formulär. Formulärförfattare kan enkelt skapa flera versioner av ett formulär och till slut använda den som passar affärsmålen. Dessutom kan formuläranvändare även återställa formuläret till tidigare versioner. Man kan också jämföra två versioner av ett formulär genom att förhandsgranska dem så att de kan analysera dem bättre ur gränssnittsperspektiv. Låt oss gå in i detalj på varje funktion för anpassad versionshantering av formulär:

### Skapa en formulärversion {#create-a-form-version}

Följ stegen nedan när du vill skapa en version av ett formulär:

1. I din AEM Forms-miljö går du till **[!UICONTROL Form]**>>**[!UICONTROL Forms & Documents]** och väljer ditt **formulär**.
1. Välj **[!UICONTROL Versions]** i listrutan över den vänstra panelen.
   ![Välj ett formulär](assets/select-a-form.png)
1. Klicka på de **tre punkterna** som finns på den nedre panelen till vänster och klicka på **[!UICONTROL Save as Version]**.
1. Ange en etikett för formulärversionen, du kan också lägga till information om formuläret via en kommentar.
   ![Skapa en formulärversion](assets/create-a-form-version.png)

### Uppdatera en formulärversion {#update-a-form-version}

När du har redigerat och uppdaterat formuläret lägger du till en ny version i formuläret. Följ stegen i det sista avsnittet för att namnge en ny version av formuläret så som det visas i bilden:

![Uppdatera en formulärversion](assets/update-a-form-version.png)

### Återställa en formulärversion {#revert-a-form-version}

Om du vill återställa en formulärversion till föregående väljer du en formulärversion och klickar på **[!UICONTROL Revert to this Version]**.

![Återställ formulärversion](assets/revert-form-version.png)

### Jämför formulärversioner {#compare-form-versions}

Formulärförfattare kan jämföra två olika versioner av ett formulär för förhandsgranskning. Om du vill jämföra versioner väljer du en formulärversion och klickar på **[!UICONTROL Compare to Current]**. Den visar två olika formulärversioner i förhandsgranskningsläge.

![Jämför formulärversioner](assets/compare-form-versions.png)

## Lägg till kommentarer {#add-comments}

En granskning är en mekanism som gör att en eller flera granskare kan kommentera i formulär. Alla formuläranvändare kan kommentera i ett formulär eller granska ett formulär med hjälp av kommentarer. Om du vill kommentera ett formulär markerar du **[!UICONTROL Form]** och lägger till en **[!UICONTROL Comment]** i formuläret.

>[!NOTE]
> När du använder kommentarer i adaptiva formulärkärnkomponenter enligt beskrivningen ovan, inaktiveras formulärfunktionen [att lägga till granskare i formulär](/help/forms/using/create-reviews-forms.md).


![Lägg till kommentarer i ett formulär](assets/form-comments.png)

## Lägg till anteckningar {#adaptive-form-annotations}

I många fall måste formulärgruppsanvändare lägga till kommentarer i ett formulär för granskning, t.ex. på en viss flik eller komponenter i ett formulär. I sådana fall kan författare använda anteckningar.
Gör så här om du vill lägga till anteckningar i ett formulär:

1. Öppna ett formulär i läget **[!UICONTROL Edit]**.

1. Klicka på ikonen **lägg till** som finns i bildens övre högra hörn.
   ![Anteckning](assets/annotation.png)

1. Klicka nu på ikonen **lägg till** i det övre vänstra fältet enligt bilden för att lägga till anteckningen.
   ![Lägg till anteckning](assets/add-annotation.png)

1. Nu kan du lägga till kommentarer, rita skisser med flera färger i formulärkomponenterna.

1. Om du vill se alla dina tillagda anteckningar i ett formulär markerar du formuläret och ser att de tillagda anteckningarna på den vänstra panelen, som visas i bilden.

   ![Se tillagda anteckningar](assets/see-annotations.png)

## Se även

* [Jämför adaptiva Forms Core-komponenter](/help/forms/using/compare-forms-core-components.md)
