---
title: Lägga till teckensnitt för grafikåtergivning
description: Med AEM kan du skapa grafik som innehåller text dynamiskt från ditt innehåll
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Lägga till teckensnitt för grafikåtergivning{#adding-fonts-for-graphic-rendering}

Med AEM kan du skapa grafik som innehåller text dynamiskt från ditt innehåll.

Om du vill göra det kan du även läsa in och använda dina egna teckensnitt.

För närvarande stöder alla implementeringar av Java Platform [TrueType](https://en.wikipedia.org/wiki/Truetype) teckensnitt.

1. Öppna CRXDE Lite och navigera till projektprogrammappen:

   `/apps/<your-project>/`

1. Under `/apps/<your-project>/` skapa en nod:

   * **Namn**: `fonts`
   * **Typ**: `sling:Folder`

   Spara alla ändringar.

1. Kopiera teckensnittsfilerna till den här mappen, till exempel med WebDAV.

   >[!NOTE]
   >
   >Teckensnittsfiler i databasen måste ha suffixet `*.ttf` eller `*.TTF`.

1. Uppdatera [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md) av [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Lägg till sökvägen till teckensnittsmappen, det vill säga `/apps/<your-project>/fonts`.

1. Återvänd till CRXDE Lite. Nu bör du se en `.fontlist` i mappen som innehåller namnet på de importerade teckensnitten.

   Dessa teckensnitt kan nu användas i Java API.

Mer information om hur du använder teckensnitten med Java API finns i [dokumentation för klassen Font i Java API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
