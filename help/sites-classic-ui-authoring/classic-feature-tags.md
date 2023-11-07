---
title: Använda taggar
description: Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats. Taggar kan ses som nyckelord eller etiketter som kan bifogas till en sida, en resurs eller annat innehåll för att göra det möjligt att söka efter innehållet och relaterat innehåll.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 4b6c273c-560e-4330-b886-a02825d5aaa1
source-git-commit: 27e5c7fea4e90873bf80f976e179b5af0088f550
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Använda taggar{#using-tags}

Taggar är ett snabbt och enkelt sätt att klassificera innehåll på en webbplats. Taggar kan ses som nyckelord eller etiketter som kan bifogas till en sida, en resurs eller annat innehåll för att göra det möjligt att söka efter innehållet och relaterat innehåll.

* Se [Administrera taggar](/help/sites-administering/tags.md) om du vill ha information om hur du skapar och hanterar taggar och till vilka innehållstaggar har tillämpats.
* Se [Tagga för utvecklare](/help/sites-developing/tags.md) om du vill ha information om taggningsramverket och inkludera och utöka taggar i anpassade program.

## Tio skäl att använda märkord {#ten-reasons-to-use-tagging}

1. Ordna innehåll: taggning gör livet enklare för författare eftersom de snabbt kan ordna innehåll utan ansträngning.
1. Ordna taggar: när taggar organiserar innehåll organiserar hierarkiska taxonomier/namnutrymmen taggar.
1. Djupt organiserade taggar: med möjlighet att skapa taggar och undertaggar blir det möjligt att uttrycka hela taxonomiska system som omfattar termer, undertermer och deras relationer. Detta gör att en andra (eller tredje) innehållshierarki kan skapas parallellt med den officiella.
1. Kontrollerad taggning: taggning kan styras genom att behörigheter tillämpas på taggar och/eller namnutrymmen för att styra hur taggar skapas och används.
1. Flexibel taggning: Taggar har många namn och ansikten: taggar, taxonomitermer, kategorier, etiketter och mycket annat. De är flexibla i sin innehållsmodell och i hur de kan användas, t.ex. när måldemografi kontureras, kategoriseras och klassificeras innehåll eller när en sekundär innehållshierarki skapas.
1. Förbättrad sökning: Standardsökkomponenten i AEM innehåller i stort sett skapade taggar och använda taggar som du kan använda filter på för att begränsa resultaten till de som är relevanta.
1. SEO-aktivering: taggar som används som sidegenskaper visas automatiskt i de metataggar på sidan som gör den synlig för sökmotorer.
1. Enkel sofistikering: taggar kan skapas från ett ord och med en knapptryckning. Därefter kan en titel, beskrivning och ett obegränsat antal etiketter läggas till för att ge taggen mer semantik.
1. Core Consistency : taggningssystemet är en viktig komponent i AEM och används av alla AEM för att kategorisera innehåll. Programmeringsgränssnittet för taggning är även tillgängligt för utvecklare som skapar taggningsaktiverade program med tillgång till samma taxonomier.
1. Kombinerar struktur och flexibilitet: AEM är idealiskt för att arbeta med strukturerad information på grund av inkapsling av sidor och banor. Det är lika kraftfullt när du arbetar med ostrukturerad information på grund av den inbyggda textsökningen. Taggning kombinerar styrkan hos både strukturen och flexibiliteten.

När du utformar innehållsstrukturen för en plats och metadatarammet för resurser bör du tänka på att taggningen är enkel och tillgänglig.

## Tillämpar taggar {#applying-tags}

I redigeringsmiljön kan författare lägga till taggar genom att gå till sidegenskaperna och ange en eller flera taggar i **Taggar/nyckelord** fält.

Tillämpa [fördefinierade taggar](/help/sites-administering/tags.md), i **Sidegenskaper** fönstret använder `Tags/Keywords` nedrullningsbar meny där du kan välja taggar i listan över taggar som är tillåtna för sidan. Tthe **Standardtaggar** är standardnamnutrymmet, vilket betyder att det inte finns något `namespace-string:` som är förfixerade till taxonomin.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Publiceringstaggar {#publishing-tags}

Precis som med sidor kan du göra följande med taggar och namnutrymmen:

**Aktivera**

* Aktivera enskilda taggar.

  Precis som för sidor måste nyligen skapade taggar aktiveras innan de blir tillgängliga i publiceringsmiljön.

>[!NOTE]
>
>När du aktiverar en sida öppnas en dialogruta automatiskt där du kan aktivera oaktiverade taggar som hör till sidan.

**Inaktivera**

* Inaktivera de markerade taggarna.

## Tagga moln {#tag-clouds}

Taggmoln visar ett moln med taggar, antingen för den aktuella sidan, för hela webbplatsen eller för de mest använda. Tagga moln är ett sätt att markera problem som är (har varit) av intresse för användaren. Storleken på texten som används för att visa taggen varierar beroende på hur den används.

The [Tag Cloud](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) används för att lägga till ett taggmoln på en sida.

## Söka på taggar {#searching-on-tags}

Du kan söka efter taggar både i författarmiljön och i publiceringsmiljön.

### Använda sökkomponenten {#using-search-component}

Lägga till en [Sökkomponent](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) till en sida har en sökfunktion som innehåller taggar och kan användas både i författarmiljön och publiceringsmiljön.

![chlimage_1-3](assets/chlimage_1-3a.png)
