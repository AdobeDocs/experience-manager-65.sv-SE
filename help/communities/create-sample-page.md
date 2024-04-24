---
title: Skapa en exempelsida
description: Lär dig hur du skapar en mall för en community-webbplats som bara innehåller funktionen Sida som kan hjälpa dig att skapa en enkel community-webbplats.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Skapa en exempelsida {#create-a-sample-page}

Från och med AEM 6.1 Communities är det enklaste sättet att skapa en exempelsida att skapa en enkel communitywebbplats som består av en sidfunktion.

Detta inkluderar en parsykomponent så att du kan [aktivera komponenter för utveckling](basics.md#accessing-communities-components).

Ett annat alternativ för att utforska exempelkomponenter är att använda funktionerna i [Guide för communitykomponenter](components-guide.md).

## Skapa en communitywebbplats {#create-a-community-site}

Det här liknar att skapa en plats som beskrivs i [Komma igång med AEM Communities](getting-started.md).

Den största skillnaden är att den här självstudiekursen skapar en mall för en community-webbplats som bara innehåller [Sidfunktion](functions.md#page-function) för att skapa en enkel communitywebbplats. Den gör detta utan andra funktioner (andra än de funktioner som är grundläggande för alla communitysajter).

### Skapa ny platsmall {#create-new-site-template}

Skapa en enkel [mall för communitywebbplats](sites.md).

Från global navigering på en författarinstans väljer du **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Site Templates]**.

![create-site-template](assets/create-site-template1.png)

* Välj `Create button`
* GRUNDLÄGGANDE INFORMATION

   * `Name`: Enkelsidig mall
   * `Description`: En mall som består av en enda sidfunktion.
   * Välj `Enabled`

![site-template-editor](assets/site-template-editor.png)

* STRUKTUR

   * Dra en `Page` funktionen till Template Builder
   * Ange information om konfigurationsfunktionen

      * `Title`: En sida
      * `URL`: sida

![site-template-editor-structure](assets/site-template-editor1.png)

* Välj **`Save`** för konfigurationen
* Välj **`Save`** för webbplatsmallen

### Skapa ny community-webbplats {#create-new-community-site}

Skapa nu en communitywebbplats baserad på den enkla webbplatsmallen.

När du har skapat webbplatsmallen väljer du från global navigering **[!UICONTROL Communities > Sites]**.

![create-community-site](assets/create-community-site1.png)

* Välj **`Create`** icon

* Steg `1 - Site Template`

   * `Title`: Enkel communitywebbplats
   * `Description`: En communitywebbplats som består av en enda sida för experiment.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: sample

      * url = http://localhost:4502/content/sites/sample

      * `Template`: välj `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* Välj `Next`
* Steg `2 - Design`

   * Välj en design

* Välj `Next`
* Välj `Next`

  (Acceptera alla standardinställningar)

* Välj `Create`

  ![create-community-site](assets/create-community-site.png)

## Publicera webbplatsen {#publish-the-site}

![publicera-webbplats](assets/publish-site.png)

Från [community sites console](sites-console.md), väljer du publiceringsikonen för att publicera webbplatsen, som standard http://localhost:4503.

## Öppna webbplatsen på författaren i redigeringsläge {#open-the-site-on-author-in-edit-mode}

![öppen webbplats](assets/open-site.png)

Markera ikonen Öppna plats så att du kan visa webbplatsen i redigeringsläge.

URL:en är [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![författarwebbplats](assets/author-site.png)

På den enkla startsidan är det möjligt att se vad som är förkopplat via communityfunktionerna och -mallarna, och att leka med att lägga till och konfigurera communitykomponenter.

## Visa webbplats vid publicering {#view-site-on-publish}

Öppna sidan på sidan när du har publicerat sidan [publish instance](http://localhost:4503/content/sites/sample/en.html) för att experimentera med funktionerna som anonym besökare, inloggad medlem eller administratör. Administrationslänken som visas i redigeringsmiljön visas inte i publiceringsmiljön om inte en administratör loggar in.
