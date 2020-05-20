---
title: Förbered resurser för översättning
description: Skapa rotmappar för språk för att förbereda resurser för översättning för stöd av flerspråkiga resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Förbered resurser för översättning {#preparing-assets-for-translation}

Flerspråkiga resurser innebär resurser med binärfiler, metadata och taggar på flera språk. I allmänhet finns binära filer, metadata och taggar för resurser på ett språk, som sedan översätts till andra språk för användning i flerspråkiga projekt.

I Adobe Experience Manager (AEM) Assets inkluderas flerspråkiga resurser i mappar, där varje mapp innehåller resurserna på ett annat språk.

Varje språkmapp kallas för en språkkopia. Rotmappen för en språkkopia, som kallas språkrot, identifierar språket för innehållet i språkkopian. Till exempel är */content/dam/it* den italienska språkroten för den italienska språkkopian. För språkkopior måste en [korrekt konfigurerad språkrot](preparing-assets-for-translation.md#creating-a-language-root) användas, så att rätt språk används när översättningar av källresurser utförs.

Språkkopian som du ursprungligen lade till resurser för är språkinställningen. Språkmallsidan är källan som översätts till andra språk. En exempelmapphierarki innehåller flera språkrötter:

```
 /content
  /- dam
   |- en
   |- fr
   |- de
   |- es
   |- it
   |- ja
   |- zh
```

Utför följande steg för att förbereda dina resurser för översättning:

1. Skapa språkroten för din språkinställning. Språkroten för den engelska språkkopian i exempelmapphierarkin är till exempel `/content/dam/en`. Kontrollera att språkroten är korrekt konfigurerad enligt informationen i [Skapa en språkrot](preparing-assets-for-translation.md#creating-a-language-root).

1. Lägg till resurser i din språkinställning.
1. Skapa språkroten för varje målspråk som du behöver en språkkopia för.

## Skapa en språkrot {#creating-a-language-root}

Om du vill skapa språkroten skapar du en mapp och använder en ISO-språkkod som värde för egenskapen Namn. När du har skapat språkroten kan du skapa en språkkopia på valfri nivå i språkroten.

Rotsidan för den italienska språkkopian av exempelhierarkin har till exempel `it` egenskapen Namn. Egenskapen Namn används som namn på objektnoden i databasen och avgör därför sökvägen till resurserna. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. From the Assets console, click **[!UICONTROL Create]** and choose **[!UICONTROL Folder]** from the menu.

   ![Skapa mapp](assets/Create-folder.png)

1. I fältet skriver du landskoden i formatet **[!UICONTROL Name]** `<language-code>`.

   ![Lägg till språkkod i mappen](assets/Add-language-code-in-folder.png)

1. Klicka på **[!UICONTROL Create]**. Språkroten skapas i resurskonsolen.

## Visa språkrötter {#viewing-language-roots}

I AEM-gränssnittet finns en **[!UICONTROL References]** panel med en lista över språkrötter som har skapats i AEM Resurser.

1. I resurskonsolen väljer du den språkinställning som du vill skapa språkkopior för.
1. Klicka på ikonen GlobalNav och välj **[!UICONTROL References]** att öppna [!UICONTROL Reference] rutan.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Klicka på i rutan Referenser **[!UICONTROL Language Copies]**. På [!UICONTROL Language Copies] panelen visas språkkopiorna för resurserna.

   ![chlimage_1-123](assets/chlimage_1-123.png)
