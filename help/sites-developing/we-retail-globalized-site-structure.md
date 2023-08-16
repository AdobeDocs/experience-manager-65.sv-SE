---
title: Prova den globala webbplatsstrukturen i webb.butik
description: Prova den globala webbplatsstrukturen i webb.butik
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---

# Prova den globala webbplatsstrukturen i webb.butik{#trying-out-the-globalized-site-structure-in-we-retail}

Vi. Detaljhandeln har byggts med en global webbplatsstruktur som erbjuder en språkinställning som kan kopieras live till landsspecifika webbplatser. Allt är klart att användas för att experimentera med den här strukturen och de inbyggda översättningsfunktionerna.

## Prova {#trying-it-out}

1. Öppna webbplatskonsolen från **Global navigering -> Webbplatser**.
1. Växla till kolumnvyn (om den inte redan är aktiv) och välj We.Retail. Lägg märke till landstrukturen med Schweiz, USA, Frankrike och så vidare, tillsammans med Language Master.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Välj Schweiz och se språkrötterna för det landets språk. Det finns ännu inget innehåll under dessa rötter.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Växla till listvyn och se att språkkopiorna för länderna är live-kopior.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Återgå till kolumnvyn och klicka på Language Master och se språkinställningens rötter med innehåll. Det är bara engelska som har innehåll.

   Vi.Retail innehåller inget översatt innehåll, men strukturen och konfigurationen finns på plats så att du kan demonstrera översättningstjänsterna.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. När den engelska språkmallen är markerad öppnar du **Referenser** i webbplatskonsolen och välj **Språkkopior**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Markera kryssrutan bredvid **Språkkopior** etikett för att välja alla språkkopior. I **Uppdatera språkkopior** markerar du alternativet **Skapa ett nytt översättningsprojekt**. Ange ett namn för projektet och klicka på **Uppdatera**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Ett projekt skapas för varje språköversättning. Visa dem under **Navigering -> Projekt**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Klicka på tyska för att se information om översättningsprojektet. Statusen är **Utkast**. Om du vill starta översättningen med Microsoft® översättningstjänst klickar du på markören bredvid **Översättningsjobb** rubrik och markera **Starta**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Översättningsprojektet startar. Klicka på ellipsen längst ned på kortet Översättningsjobb för att se mer information. Sidor med läget **Klar för granskning** har redan översatts av översättningstjänsten.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Markera en av sidorna i listan och sedan **Förhandsgranska på platser** i verktygsfältet öppnar den översatta sidan i sidredigeraren.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Den här proceduren demonstrerade den inbyggda integrationen med maskinöversättning från Microsoft®. Använda [AEM Translation Integration Framework](/help/sites-administering/translation.md)kan ni integrera med många standardöversättningstjänster för att samordna översättningen av AEM.

## Ytterligare information {#further-information}

Mer information finns i redigeringsdokumentet [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md) för fullständig teknisk information.
