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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Använda molnet för sociala taggar {#using-social-tag-cloud}

## Introduktion {#introduction}

Komponenten `Social Tag Cloud` markerar taggar som används av communitymedlemmar när innehåll publiceras. Det är ett sätt att identifiera trendämnen och göra det möjligt för webbplatsbesökare att snabbt hitta taggat innehåll.

Ytterligare sätt att identifiera aktuella trender finns på [Aktivitetstrender](trends.md).

Den här sidan dokumenterar inställningarna i `Social Tag Cloud` komponentens dialogruta och beskriver användarupplevelsen.

Mer information för utvecklare finns i [Tagga viktiga](tag.md).

Se [Administrera taggar](../../help/sites-administering/tags.md) för information om hur du skapar och hanterar taggar samt om vilka innehållstaggar som har tillämpats.

## Lägga till ett moln för sociala taggar {#adding-a-social-tag-cloud}

Om du vill lägga till en `Social Tag Cloud` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på `Communities / Social Tag Cloud` och dra komponenten till en plats på en sida där taggmolnet ska visas.

Mer information finns i Grunderna för [communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](tag.md#essentials-for-client-side) inkluderas visas `Social Tag Cloud` komponenten så här:

![chlimage_1-303](assets/chlimage_1-303.png)

## Konfigurerar molnet för sociala taggar {#configuring-social-tag-cloud}

Markera den monterade `Social Tag Cloud` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-304](assets/chlimage_1-304.png)

Under fliken **[!UICONTROL Social Tag Cloud]** anger du vilka taggar som ska visas och, om taggarna är aktiva länkar, platsen för sidan för sökresultat:

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL Sociala taggar som visas]** för att identifiera vilka UGC-taggar som ska visas. De nedrullningsbara alternativen är

   * `From page and child pages`
   * `All tags`
   Standardvärdet är `From page and child pages`, där &quot;sida&quot; refererar till inställningen för **sida** nedan.

* **[!UICONTROL Sida]**(krävs om inte `All tags)` Sökvägen till UGC för en sida. Standard är den aktuella sidan om den lämnas tom.

* **[!UICONTROL Inga länkar på taggar]** Om det här alternativet är markerat visas taggarna i taggmolnet som oformaterad text. Om du inte markerar det här alternativet visas taggarna som aktiva länkar som söker efter allt innehåll som taggen tillämpas på. Standardvärdet är avmarkerat och kräver att **[!UICONTROL sökresultatsökvägen]** anges.

* **[!UICONTROL Sökresultatsökväg]** Sökvägen till en sida där en `Search Result` komponent har placerats, konfigurerad att referera till UGC som innehåller den UGC-sökväg som anges av inställningen **Sida** .

## Ändra visning av molnet för sociala taggar {#change-display-of-social-tag-cloud}

Om du vill redigera visningen av **Social Tag Cloud** anger du [designläge](../../help/sites-authoring/default-components-designmode.md) och dubbelklickar på den monterade `Social Tag Cloud` komponenten för att öppna en dialogruta med en extra flik.

Använd fliken **[!UICONTROL Social Tag Cloud (Design)]** för att ange hur taggar ska visas. En tagg kan vara en enkel tagg, ett enstaka ord i standardnamnutrymmet eller en hierarkisk taxonomi:

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL Visa fullständiga titelsökvägar]** Om det här alternativet är markerat visas rubrikerna för de överordnade taggarna och namnutrymmet för varje tillämpad tagg.

   Exempel:

   * Markerad: `Geometrixx Media: Gadgets / Cars`
   * Avmarkerad: `Cars`
   Det är ingen skillnad för en enkel tagg.

   Standard är avmarkerat.

* **[!UICONTROL Visa endast lövtaggar]** Om det här alternativet är markerat visas endast tillämpade taggar som inte innehåller några andra taggar.

   Med taggID för

   `Geometrixx Media: Gadgets / Cars`

   Det finns tre taggar som kan användas: `Geometrixx Media (the namespace)`, `Gadgets`och `Cars`

   * Markerad: visas bara `Cars` om det används
   * Avmarkerad: `Geometrixx Media` och `Gadgets`även `Cars` kommer att visas, om det används
   En enkel tagg är en lövtagg.

   Standard är avmarkerat.

* **[!UICONTROL Länkmall]** En annan mall än en standardmall som används för att visa länkarna i ett taggmoln när länkar aktiveras via redigeringsdialogrutan för komponenten.

* **[!UICONTROL Samma storlek för alla taggar]** Om det här alternativet är markerat formateras alla ord i taggmolnet på samma sätt. Om alternativet inte är markerat formateras ord på olika sätt beroende på hur de används. Standard är avmarkerat.

## Additional Information {#additional-information}

Mer information finns på sidan [Taggar Essentials](tag.md) för utvecklare.

Mer information om hur du skapar och hanterar taggar finns i [Tagga användargenererat innehåll](tag-ugc.md) (UGC).
