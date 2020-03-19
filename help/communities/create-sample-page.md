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
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# Skapa en exempelsida {#create-a-sample-page}

Från och med AEM 6.1 Communities är det enklaste sättet att skapa en exempelsida att skapa en enkel communitywebbplats som består av en sidfunktion.

Detta inkluderar en parsys-komponent så att du kan [aktivera komponenter för redigering](basics.md#accessing-communities-components).

Ett annat alternativ för att utforska exempelkomponenter är att använda funktionerna i [Community Components Guide](components-guide.md).

## Skapa en communitywebbplats {#create-a-community-site}

Det här liknar mycket att skapa en ny webbplats som beskrivs i [Komma igång med AEM Communities](getting-started.md).

Den största skillnaden är att den här självstudiekursen kommer att skapa en ny mall för communitysajter som bara innehåller funktionen [](functions.md#page-function) Sida för att skapa en enkel communitysajt som är fri från andra funktioner (andra än de förkabelade funktioner som är grundläggande för alla communitysajter).

### Skapa ny platsmall {#create-new-site-template}

Börja med att skapa en enkel mall [för en](sites.md)community-webbplats.

Från global navigering på en författarinstans väljer du **[!UICONTROL Verktyg > Communities > Site Templates]**.

![chlimage_1-82](assets/chlimage_1-82.png)

* Välj `Create button`
* GRUNDLÄGGANDE INFORMATION

   * `Name`: Enkelsidig mall
   * `Description`: En mall som består av en enda sidfunktion.
   * Välj `Enabled`

![chlimage_1-83](assets/chlimage_1-83.png)

* STRUKTUR

   * Dra en `Page` funktion till mallverktyget
   * Ange information om konfigurationsfunktionen

      * `Title`: En sida
      * `URL`: page

![chlimage_1-84](assets/chlimage_1-84.png)

* Välj **`Save`** konfiguration
* Välj **`Save`** för platsmallen

### Skapa ny community-webbplats {#create-new-community-site}

Skapa nu en ny communitywebbplats som bygger på den enkla webbplatsmallen.

När du har skapat platsmallen väljer du **[!UICONTROL Communities > Sites]** från global navigering.

![chlimage_1-85](assets/chlimage_1-85.png)

* Välj **`Create`** ikon

* Step `1 - Site Template`

   * `Title`: Enkel communitywebbplats
   * `Description`: En communitywebbplats som består av en enda sida för experiment.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: exempel

      * url = http://localhost:4502/content/sites/sample
   * `Template`: välj `Single Page Template`


![chlimage_1-86](assets/chlimage_1-86.png)

* Välj `Next`
* Step `2 - Design`

   * Välj en design

* Välj `Next`
* Välj `Next`

   (Acceptera alla standardinställningar)

* Välj `Create`

![chlimage_1-87](assets/chlimage_1-87.png)

## Publicera webbplatsen {#publish-the-site}

![chlimage_1-88](assets/chlimage_1-88.png)

På [community-webbplatskonsolen](sites-console.md)väljer du publiceringsikonen för att publicera webbplatsen, som standard http://localhost:4503.

## Öppna webbplatsen på författaren i redigeringsläge {#open-the-site-on-author-in-edit-mode}

![chlimage_1-89](assets/chlimage_1-89.png)

Välj ikonen Öppna plats om du vill visa webbplatsen i redigeringsläge.

URL:en kommer att vara [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![chlimage_1-90](assets/chlimage_1-90.png)

På den enkla startsidan är det möjligt att se vad som är förkopplat via communityfunktionerna och -mallarna, och att leka med att lägga till och konfigurera communitykomponenter.

## Visa webbplats vid publicering {#view-site-on-publish}

När du har publicerat sidan öppnar du sidan i [publiceringsinstansen](http://localhost:4503/content/sites/sample/en.html) för att experimentera med funktionerna som anonym besökare, inloggad medlem eller administratör. Administrationslänken som visas i författarmiljön visas inte i publiceringsmiljön om inte en administratör loggar in.
