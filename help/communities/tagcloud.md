---
title: Använda molnet för sociala taggar
seo-title: Använda molnet för sociala taggar
description: Lägga till en komponent i molnet för sociala taggar på en sida
seo-description: Lägga till en komponent i molnet för sociala taggar på en sida
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Använda molnet för sociala taggar {#using-social-tag-cloud}

## Introduktion {#introduction}

Komponenten `Social Tag Cloud` markerar taggar som används av communitymedlemmar när innehåll publiceras. Det är ett sätt att identifiera trendämnen och göra det möjligt för webbplatsbesökare att snabbt hitta taggat innehåll.

Ytterligare sätt att identifiera aktuella trender finns på [Aktivitetstrender](trends.md).

Den här sidan dokumenterar inställningarna i `Social Tag Cloud`-komponentdialogrutan och beskriver användarupplevelsen.

Mer information om utvecklare finns i [Tagga viktiga](tag.md).

Se [Administrera taggar](../../help/sites-administering/tags.md) om du vill ha information om hur du skapar och hanterar taggar, samt om vilka innehållstaggar som har tillämpats.

## Lägga till ett moln för sociala taggar {#adding-a-social-tag-cloud}

Om du vill lägga till en `Social Tag Cloud`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på `Communities / Social Tag Cloud` och dra komponenten till en plats på en sida där taggmolnet ska visas.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](tag.md#essentials-for-client-side) inkluderas visas `Social Tag Cloud`-komponenten så här:

![social-tag](assets/social-tag.png)

## Konfigurerar molnet för social tagg {#configuring-social-tag-cloud}

Markera den monterade `Social Tag Cloud`-komponenten som ska öppnas och välj ikonen `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under fliken **[!UICONTROL Social Tag Cloud]** anger du vilka taggar som ska visas och, om taggarna är aktiva länkar, platsen för sidan för sökresultat:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Social Tags to Display]**
Identifiera vilka UGC-taggar som ska visas. De nedrullningsbara alternativen är:

   * `From page and child pages`
   * `All tags`

   Standardvärdet är `From page and child pages`, där &quot;page&quot; refererar till inställningen **Sida** nedan.

* **[!UICONTROL Page]**

   (Obligatoriskt om inte `All tags)` Sökvägen till UGC för en sida. Standard är den aktuella sidan om den lämnas tom.

* **[!UICONTROL No links on tags]**

   Om du markerar det här alternativet visas taggarna i taggmolnet som oformaterad text. Om du inte markerar det här alternativet visas taggarna som aktiva länkar som söker efter allt innehåll som taggen tillämpas på. Standardvärdet är avmarkerat och kräver att **[!UICONTROL Search Result Path]** har angetts.

* **[!UICONTROL Search Result Path]**

   Sökvägen till en sida där en `Search Result`-komponent har placerats, konfigurerad att referera till UGC som innehåller den UGC-sökväg som anges av inställningen **Sida**.

## Ändra visning av molnet för sociala taggar {#change-display-of-social-tag-cloud}

Om du vill redigera visningen av **molnet för sociala taggar** anger du [designläge](../../help/sites-authoring/default-components-designmode.md) och dubbelklickar på den monterade `Social Tag Cloud`-komponenten för att öppna en dialogruta med en extra flik.

Ange hur taggar ska visas på fliken **[!UICONTROL Social Tag Cloud (Design)]**. En tagg kan vara en enkel tagg, ett enstaka ord i standardnamnutrymmet eller en hierarkisk taxonomi:

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

   `Geometrixx Media (the namespace)`,  `Gadgets`och  `Cars`

   * Markerad: Endast `Cars` visas om det används.
   * Avmarkerad: `Geometrixx Media` och `Gadgets`samt `Cars` visas om de används.

   En enkel tagg är en lövtagg.

   Standard är avmarkerat.

* **[!UICONTROL Link Template]**

   En annan mall än en standardmall som används för att visa länkarna i ett taggmoln när länkarna aktiveras via redigeringsdialogrutan för komponenten.

* **[!UICONTROL Same size for all tags]**

   Om det här alternativet är markerat formateras alla ord i taggmolnet på samma sätt. Om alternativet inte är markerat formateras ord på olika sätt beroende på hur de används. Standard är avmarkerat.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Taggar Essentials](tag.md) för utvecklare.

Mer information om hur du skapar och hanterar taggar finns i [Tagga användargenererat innehåll](tag-ugc.md) (UGC).
