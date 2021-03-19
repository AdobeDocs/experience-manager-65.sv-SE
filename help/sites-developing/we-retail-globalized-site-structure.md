---
title: Prova den globala webbplatsstrukturen i webb.butik
seo-title: Prova den globala webbplatsstrukturen i webb.butik
description: Prova den globala webbplatsstrukturen i webb.butik
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 2%

---


# Prova den globala platsstrukturen i We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

Vi.Retail har byggts med en global webbplatsstruktur som erbjuder språkmallar som kan kopieras live till landsspecifika webbplatser. Allt är klart att användas för att experimentera med den här strukturen och de inbyggda översättningsfunktionerna.

## Prova {#trying-it-out}

1. Öppna webbplatskonsolen från **Global navigering -> Platser**.
1. Växla till kolumnvyn (om den inte redan är aktiv) och välj We.Retail. Anteckna landstrukturen med Schweiz, USA, Frankrike osv., tillsammans med språkmallarna.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Välj Schweiz och se språkrötterna för det landets språk. Observera att det ännu inte finns något innehåll under dessa rötter.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Växla till listvyn och se att språkkopiorna för länderna är live-kopior.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Gå tillbaka till kolumnvyn och klicka på Överordnad Språk och se det språk som är överordnad med innehåll. Observera att endast engelska har innehåll.

   Vi.Retail innehåller inget översatt innehåll, men strukturen och konfigurationen finns på plats så att du kan demonstrera översättningstjänsterna.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. När Överordnad för engelska är markerad öppnar du **Referenser** i webbplatskonsolen och väljer **Språkkopior**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Markera kryssrutan bredvid etiketten **Språkkopior** om du vill markera alla språkkopior. I avsnittet **Uppdatera språkkopior** på listen väljer du alternativet **Skapa ett nytt översättningsprojekt**. Ange ett namn för projektet och klicka på **Uppdatera**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Ett projekt skapas för varje språköversättning. Visa dem under **Navigering -> Projekt**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Klicka på tyska för att se information om översättningsprojektet. Observera att statusen är i **Utkast**. Om du vill starta översättningen med Microsofts översättningstjänst klickar du på markören bredvid rubriken **Översättningsjobb** och väljer **Start**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Översättningsprojektet startar. Klicka på ellipsen längst ned på kortet Översättningsjobb för att se mer information. Sidor med tillståndet **Klart för granskning** har redan översatts av översättningstjänsten.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Om du väljer en av sidorna i listan och sedan **Förhandsgranska i platser** i verktygsfältet öppnas den översatta sidan i sidredigeraren.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Den här proceduren demonstrerade den inbyggda integrationen med Microsoft maskinöversättning. Med [AEM Translation Integration Framework](/help/sites-administering/translation.md) kan du integrera med många standardöversättningstjänster för att samordna översättning av AEM.

## Ytterligare information {#further-information}

Mer information finns i redigeringsdokumentet [Translating Content for Multilingual Sites](/help/sites-administering/translation.md) för fullständig teknisk information.
