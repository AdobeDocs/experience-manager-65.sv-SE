---
title: Förbered resurser för översättning
description: Skapa rotmappar för språk för att förbereda resurser för översättning för stöd av flerspråkiga resurser.
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Förbered resurser för översättning {#preparing-assets-for-translation}

Flerspråkiga resurser innebär resurser med binärfiler, metadata och taggar på flera språk. I allmänhet finns binära filer, metadata och taggar för resurser på ett språk, som sedan översätts till andra språk för användning i flerspråkiga projekt.

I [!DNL Adobe Experience Manager Assets], inkluderas flerspråkiga resurser i mappar där varje mapp innehåller resurserna på ett annat språk.

Varje språkmapp kallas för en språkkopia. Rotmappen för en språkkopia, som kallas språkrot, identifierar språket för innehållet i språkkopian. Till exempel: */content/dam/it* är den italienska språkroten för den italienska språkversionen. Språkkopior måste använda en [korrekt konfigurerad språkrot](preparing-assets-for-translation.md#creating-a-language-root) så att rätt språk anges som mål när översättningar av källresurser utförs.

Språkkopian som du ursprungligen lade till resurser för är det primära språket. Språkets primära språk är källan som översätts till andra språk. En exempelmapphierarki innehåller flera språkrötter:

```shell
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

1. Skapa språkroten för din primära språkversion. Språkroten för den engelska språkkopian i exempelmapphierarkin är till exempel `/content/dam/en`. Kontrollera att språkroten är korrekt konfigurerad enligt informationen i [Skapa en språkrot](preparing-assets-for-translation.md#creating-a-language-root).

1. Lägg till resurser i ditt primära språk.
1. Skapa språkroten för varje målspråk som du behöver en språkkopia för.

## Skapa en språkrot {#creating-a-language-root}

Om du vill skapa språkroten skapar du en mapp och använder en ISO-språkkod som värde för egenskapen Namn. När du har skapat språkroten kan du skapa en språkkopia på valfri nivå i språkroten.

Rotsidan för den italienska språkkopian av exempelhierarkin har till exempel `it` som egenskapen Name. Egenskapen Namn används som namn på objektnoden i databasen och avgör därför sökvägen till resurserna. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. Från [!DNL Assets] konsol, klicka **[!UICONTROL Create]** och välja **[!UICONTROL Folder]** på menyn.

   ![Skapa mapp](assets/Create-folder.png)

1. I **[!UICONTROL Name]** fälttyp landskoden i formatet `<language-code>`.

   ![Lägg till språkkod i mappen](assets/Add-language-code-in-folder.png)

1. Klicka på **[!UICONTROL Create]**. Språkroten skapas i [!DNL Assets] konsol.

## Visa språkrötter {#viewing-language-roots}

[!DNL Experience Manager] -gränssnittet har en **[!UICONTROL References]** som visar en lista med språkrötter som har skapats i [!DNL Assets].

1. I [!DNL Assets] väljer du det språk du vill skapa språkkopior för.
1. Välj **[!UICONTROL References]** för att öppna [!UICONTROL Reference] fönster.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Klicka på i rutan Referenser **[!UICONTROL Language Copies]**. The [!UICONTROL Language Copies] På panelen visas språkkopiorna för resurserna.

   ![språkversioner](assets/lang-copy2.png)
