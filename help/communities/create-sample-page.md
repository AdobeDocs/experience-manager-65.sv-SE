---
title: Skapa en exempelsida
seo-title: Skapa en exempelsida
description: Skapa en exempelwebbplats
seo-description: Skapa en exempelwebbplats
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: 824ddd48e4680eed1d4612c6ad450a8f1bc68e7c
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---


# Skapa en exempelsida {#create-a-sample-page}

Från och med AEM 6.1 Communities är det enklaste sättet att skapa en exempelsida att skapa en enkel communitywebbplats som består av en sidfunktion.

Detta inkluderar en parsys-komponent så att du kan [aktivera komponenter för redigering](basics.md#accessing-communities-components).

Ett annat alternativ för att undersöka exempelkomponenter är att använda funktionerna i [Community Components Guide](components-guide.md).

## Skapa en communitywebbplats {#create-a-community-site}

Det här liknar mycket att skapa en ny webbplats som beskrivs i [Komma igång med AEM Communities](getting-started.md).

Den största skillnaden är att den här självstudiekursen kommer att skapa en ny mall för communitysajter som endast innehåller funktionen [Sida](functions.md#page-function) för att skapa en enkel communitysajt som är fri från andra funktioner (förutom de förkabelade funktionerna som är grundläggande för alla communitysajter).

### Skapa ny platsmall {#create-new-site-template}

Skapa en enkel [mall för communitywebbplats](sites.md) för att komma igång.

Från global navigering på en författarinstans väljer du **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Site Templates]**.

![create-site-template](assets/create-site-template1.png)

* Välj `Create button`
* GRUNDLÄGGANDE INFORMATION

   * `Name`: Enkelsidig mall
   * `Description`: En mall som består av en enda sidfunktion.
   * Välj `Enabled`

![site-template-editor](assets/site-template-editor.png)

* STRUKTUR

   * Dra en `Page`-funktion till mallverktyget
   * Ange information om konfigurationsfunktionen

      * `Title`: En sida
      * `URL`: page

![site-template-editor-structure](assets/site-template-editor1.png)

* Välj **`Save`** för konfigurationen
* Välj **`Save`** för webbplatsmallen

### Skapa ny communitywebbplats {#create-new-community-site}

Skapa nu en ny communitywebbplats som bygger på den enkla webbplatsmallen.

När du har skapat webbplatsmallen väljer du **[!UICONTROL Communities > Sites]** från global navigering.

![create-community-site](assets/create-community-site1.png)

* Välj ikonen **`Create`**

* Steg `1 - Site Template`

   * `Title`: Enkel communitywebbplats
   * `Description`: En communitywebbplats som består av en enda sida för experiment.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: exempel

      * url = http://localhost:4502/content/sites/sample

      * `Template`: välj  `Single Page Template`

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

I [community-webbplatskonsolen](sites-console.md) väljer du publiceringsikonen för att publicera webbplatsen, som standard http://localhost:4503.

## Öppna webbplatsen på författaren i redigeringsläge {#open-the-site-on-author-in-edit-mode}

![öppen webbplats](assets/open-site.png)

Välj ikonen Öppna plats om du vill visa webbplatsen i redigeringsläge.

URL:en är [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![författarwebbplats](assets/author-site.png)

På den enkla startsidan är det möjligt att se vad som är förkopplat via communityfunktionerna och -mallarna, och att leka med att lägga till och konfigurera communitykomponenter.

## Visa webbplatsen vid publicering {#view-site-on-publish}

När du har publicerat sidan öppnar du sidan på [publiceringsinstansen](http://localhost:4503/content/sites/sample/en.html) för att experimentera med funktionerna som anonym besökare, inloggad medlem eller administratör. Administrationslänken som visas i författarmiljön visas inte i publiceringsmiljön om inte en administratör loggar in.
