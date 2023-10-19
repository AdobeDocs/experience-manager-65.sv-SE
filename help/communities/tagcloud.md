---
title: Använda molnet för sociala taggar
description: Lär dig hur du lägger till en komponent i Social Tag Cloud på en sida där inloggade communitymedlemmar snabbt kan identifiera trendämnen och hitta taggat innehåll.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Använda molnet för sociala taggar {#using-social-tag-cloud}

## Introduktion {#introduction}

The `Social Tag Cloud` markerar taggar som används av communitymedlemmar när innehåll publiceras. Det är ett sätt att identifiera trendämnen och göra det möjligt för webbplatsbesökare att snabbt hitta taggat innehåll.

Ytterligare sätt att identifiera aktuella trender finns på [Aktivitetstrender](trends.md).

Den här sidan dokumenterar `Social Tag Cloud` i dialogrutan och beskriver användarupplevelsen.

Mer information om utvecklare finns i [Tagg Essentials](tag.md).

Se [Administrera taggar](../../help/sites-administering/tags.md) om du vill ha information om hur du skapar och hanterar taggar och till vilka innehållstaggar har tillämpats.

## Lägga till ett socialt taggmoln {#adding-a-social-tag-cloud}

Lägga till en `Social Tag Cloud` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp `Communities / Social Tag Cloud` och dra den till en plats på en sida där taggmolnet ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](tag.md#essentials-for-client-side) ingår så här `Social Tag Cloud` visas:

![social-tag](assets/social-tag.png)

## Konfigurerar molnet för sociala taggar {#configuring-social-tag-cloud}

Markera den monterade `Social Tag Cloud` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under **[!UICONTROL Social Tag Cloud]** anger du vilka taggar som ska visas och, om taggarna är aktiva länkar, platsen för sidan där sökresultaten ska visas:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Social Tags to Display]**
Identifiera vilka UGC-taggar som ska visas. De nedrullningsbara alternativen är:

   * `From page and child pages`
   * `All tags`

  Standardvärdet är `From page and child pages`, där&quot;sida&quot; avser **Sida** nedan.

* **[!UICONTROL Page]**

  (Obligatoriskt om inte `All tags)` Sökvägen till användargränssnittets användargränssnitt för en sida. Standard är den aktuella sidan om den lämnas tom.

* **[!UICONTROL No links on tags]**

  Om du markerar det här alternativet visas taggarna i taggmolnet som oformaterad text. Om du inte markerar det här alternativet visas taggarna som aktiva länkar som söker efter allt innehåll som taggen tillämpas på. Standard är avmarkerat och kräver **[!UICONTROL Search Result Path]** som ska anges.

* **[!UICONTROL Search Result Path]**

  Sökvägen till en sida där `Search Result` -komponenten har placerats ut, konfigurerats för att referera till UGC som innehåller UGC-sökvägen som anges av **Sida** inställning.

## Ändra visning av molnet för sociala taggar {#change-display-of-social-tag-cloud}

Redigera visningen av **Social Tag Cloud**, ange [Designläge](../../help/sites-authoring/default-components-designmode.md) och dubbelklicka på den monterade `Social Tag Cloud` om du vill öppna en dialogruta med en extra flik.

Använda **[!UICONTROL Social Tag Cloud (Design)]** anger du hur -taggar ska visas. En tagg kan vara en enkel tagg, ett enstaka ord i standardnamnutrymmet eller en hierarkisk taxonomi:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Show full title paths]**

  Om du markerar det här alternativet visas rubrikerna för de överordnade taggarna och namnutrymmet för varje tillämpad tagg.

  Till exempel:

   * Markerad: `Geometrixx Media: Gadgets / Cars`
   * Avmarkerad: `Cars`

  Det är ingen skillnad för en enkel tagg.

  Standard är avmarkerat.

* **[!UICONTROL Show only leaf tags]**

  Om det här alternativet är markerat visas endast tillämpade taggar som inte innehåller några andra taggar.

  Med taggID för:

  `Geometrixx Media: Gadgets / Cars`

  Det finns tre taggar som kan användas:

  `Geometrixx Media (the namespace)`, `Gadgets`och `Cars`

   * Markerad: Endast `Cars` visas om de används.
   * Avmarkerad: `Geometrixx Media`, `Gadgets`och `Cars` visas, om det används.

  En enkel tagg är en lövtagg.

  Standard är avmarkerat.

* **[!UICONTROL Link Template]**

  En annan mall än en standardmall som används för att visa länkarna i ett taggmoln när länkarna aktiveras via redigeringsdialogrutan för komponenten.

* **[!UICONTROL Same size for all tags]**

  Om det här alternativet är markerat formateras alla ord i taggmolnet på samma sätt. Om alternativet inte är markerat formateras ord på olika sätt beroende på hur de används. Standard är avmarkerat.

## Ytterligare information {#additional-information}

Mer information finns på [Tagg Essentials](tag.md) för utvecklare.

Se [Tagga användargenererat innehåll](tag-ugc.md) (UGC) om du vill ha information om hur du skapar och hanterar taggar.
