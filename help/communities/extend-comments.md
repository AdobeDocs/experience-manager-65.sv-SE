---
title: Komponenten Utöka kommentarer
description: Utöka komponenten Kommentarer för att ändra dess utseende eller beteende för specifika användningsområden
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Komponenten Utöka kommentarer  {#extend-comments-component}

Avsikten med att [utöka](client-customize.md#extensions) en standardkomponent är att ändra utseendet eller beteendet för en komponent för specifika användningsområden.

Sökvägen till komponenten är unik och refererar standardkomponenten som en överordnad resurstyp. Risken är mindre eftersom omfattningen är begränsad jämfört med den globala omfattningen för en komponentövertäckning.

>[!NOTE]
>
>Det går inte att utöka en [överlagrad](client-customize.md#overlays)-komponent.

## Exempel {#example}

Anta att rubriken för kommentarkomponenten måste visas med ett alternativt utseende på en plats i AEM, samtidigt som den visas med standardvisningen på en annan plats. I stället för att åsidosätta standardkommentaren, som ändrar kommentarkomponenten för alla instanser, är det bättre att se till att det finns flera kommentarskomponenter tillgängliga för användning på olika platser.

Om du vill implementera den här lösningen skapar du en komponent som utökar (åsidosätter) den befintliga och ändrar Handlebars-skriptet. Det område på webbplatsen som använder de nya kommentarerna kan använda det utökade området, medan de webbplatser som använder standardutseendet inte påverkas.

Kommentarskomponenten är i själva verket en av två komponenter som utgör kommentarssystemet. Det finns alltså två komponenter att utöka: *kommentarer* och *kommentar*. Skriptet som ska redigeras finns i *comment* -komponentens `header.hbs` -fil, medan den överordnade *comments* -komponenten (kommentarsystemet) är det som en författare faktiskt lägger till på sidan.

Om du vill utöka kommentarerna måste du:

1. [Skapa komponenterna](extend-create-components.md)
1. [Lägg till kommentar på exempelsida](extend-sample-page.md)
1. [Ändra utseendet](extend-alter-appearance.md)
