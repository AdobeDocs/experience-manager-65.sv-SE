---
title: Lägga till teckensnitt för grafikåtergivning
seo-title: Lägga till teckensnitt för grafikåtergivning
description: Med AEM kan du skapa grafik som innehåller text dynamiskt från ditt innehåll
seo-description: Med AEM kan du skapa grafik som innehåller text dynamiskt från ditt innehåll
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Lägga till teckensnitt för grafikåtergivning{#adding-fonts-for-graphic-rendering}

Med AEM kan du skapa grafik som innehåller text dynamiskt från ditt innehåll.

Om du vill göra det kan du även läsa in och använda dina egna teckensnitt.

För närvarande stöder alla implementeringar av Java Platform [TrueType](https://en.wikipedia.org/wiki/Truetype) -teckensnitt.

1. Öppna CRXDE Lite och navigera till projektprogrammappen:

   `/apps/<your-project>/`

1. Under `/apps/<your-project>/` Skapa en ny nod:

   * **Namn**: `fonts`
   * **Typ**: `sling:Folder`
   Spara alla ändringar.

1. Kopiera teckensnittsfilerna till denna mapp; till exempel med WebDAV.

   >[!NOTE]
   >
   >Teckensnittsfiler i databasen måste ha suffixet `*.ttf` eller `*.TTF`.

1. Uppdatera [OSGi-konfigurationen](/help/sites-deploying/configuring-osgi.md) för [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Lägg till sökvägen till teckensnittsmappen; dvs. `/apps/<your-project>/fonts`.

1. Återgå till CRXDE Lite. Nu bör du se en `.fontlist` nod i mappen som innehåller namnet på de importerade teckensnitten.

   Dessa teckensnitt kan nu användas i Java API.

Mer information om hur du använder teckensnitten med Java API finns i [dokumentationen för klassen Font i Java API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).

