---
title: Sidskillnader
seo-title: Page Diff
description: Med funktionen för sidskillnader kan du enkelt jämföra två sidor sida vid sida med skillnaderna markerade.
seo-description: The page diff feature allows for the convenient side-by-side comparison of two pages with their differences highlighted.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# Sidskillnader{#page-diff}

## Introduktion {#introduction}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill enkelt kunna jämföra den aktuella sidan sida vid sida med en annan version.

Med funktionen för sidskillnader kan du enkelt jämföra två sidor sida vid sida med skillnaderna markerade.

>[!TIP]
>
>Se [Developing and Page Diff](/help/sites-developing/pagediff.md#operation-details) för mer teknisk information om den här funktionen.

## Använd {#use}

Diff:en sida vid sida kan jämföra:

* [Versioner](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) - Tidigare version av en sida med det aktuella läget
* [Live-kopior](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy med utkast
* [Startar](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) - Starta med källan
* [Språkkopior](/help/sites-administering/tc-manage.md#comparing-language-copies) - En sida före och efter (re-)översättning

Läs respektive avsnitt om hur du påbörjar skillnaderna i dessa sammanhang.

### Presentation av skillnader {#presentation-of-differences}

Oberoende av vilket innehåll som jämförs, förblir presentationen av skillnaderna densamma.

* Det innehåll som valdes när du startade differensen visas till vänster (diff-startpunkten).
* Jämförelseinnehållet visas till höger (vad det markerade innehållet jämförs med).

Om du till exempel jämför versioner visas den aktuella versionen till vänster och den föregående versionen till höger.

Källan för båda sidorna visas tydligt i sidhuvudsfältet högst upp i webbläsarfönstret.

![Källa visas i rubriken](assets/chlimage_1-109.png)

Skillnaden identifierar ändringar på komponentnivå och HTML-nivå. Objekt som har ändrats markeras med olika färger.

**Komponentändringar**

* Ljusgrön - komponent tillagd
* Rosa - komponent borttagen

**Ändringar i HTML**

* Mörkgrön - tillagd HTML
* Röd - HTML har tagits bort

>[!NOTE]
>
>När du jämför språkkopior inaktiveras markering, eftersom i en översättning ändras allt och markering inte har någon fördel.

### Helskärm och avslutande {#fullscreen-and-exiting}

Om du vill fokusera på visst innehåll kan du klicka på helskärmsikonen för endera sidan av diff-ikonen och förstora den till hela webbläsarfönstret.

![Ikon för helskärmsläge](do-not-localize/chlimage_1-18.png)

Den markerade sidan fyller hela fönstret, men fältet förblir överst så att du kan växla mellan de två sidorna.

![Med fältet längst upp kan du växla mellan sidor](assets/chlimage_1-110.png)

Du kan också stänga helskärmsläget genom att klicka på ikonen för att avsluta helskärmsläget.

![Stäng helskärm](do-not-localize/chlimage_1-19.png)

Du kan när som helst stänga diff sida vid sida genom att klicka på stängningsknappen i sidhuvudet.

## Begränsningar {#limitations}

I vissa situationer kan det hända att sidskillnader inte identifierar någon skillnad som förväntat.

* När olika versioner och starter används inte dynamiska komponenter som vägbeskrivningar, menyer, produktlistor eller logotyper (komponenter som är beroende av webbplatsstrukturen för att återge sitt innehåll).
* För versioner återskapar inte diff åtkomstkontrollprincipen och Live copy-relationen.
* Om en sida flyttas kan du inte längre göra några skillnader med versioner som gjorts före flyttningen.

   * Om du får problem med en skillnad ska du kontrollera [Tidslinje](/help/sites-authoring/basic-handling.md#timeline) för att se om sidan har flyttats.

>[!NOTE]
>
>Versioner kan inte jämföras med varandra. Endast den aktuella versionen kan jämföras med andra versioner av sidan. Den aktuella versionen är alltid den version som markeras med ändringar.

>[!NOTE]
>
>Mer information om hur sidskillnader fungerar samt om begränsningar som kan påverka sidskillnader finns i [dokumentation för utvecklare](/help/sites-developing/pagediff.md) av den här funktionen.
