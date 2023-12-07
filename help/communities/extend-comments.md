---
title: Komponenten Utöka kommentarer
description: Utöka komponenten Kommentarer för att ändra dess utseende eller beteende för specifika användningsområden
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Komponenten Utöka kommentarer  {#extend-comments-component}

Avsikten med [utöka](client-customize.md#extensions) en standardkomponent är att ändra en komponents utseende eller beteende för specifika användningsområden.

Sökvägen till komponenten är unik och refererar standardkomponenten som en överordnad resurstyp. Risken är mindre eftersom omfattningen är begränsad jämfört med den globala omfattningen för en komponentövertäckning.

>[!NOTE]
>
>Utöka en [överlagrad](client-customize.md#overlays) stöds inte.

## Exempel {#example}

Anta att rubriken för kommentarkomponenten måste visas med ett alternativt utseende på en plats i AEM, samtidigt som den visas med standardvisningen på en annan plats. I stället för att åsidosätta standardkommentaren, som ändrar kommentarkomponenten för alla instanser, är det bättre att se till att det finns flera kommentarskomponenter tillgängliga för användning på olika platser.

Om du vill implementera den här lösningen skapar du en komponent som utökar (åsidosätter) den befintliga och ändrar Handlebars-skriptet. Det område på webbplatsen som använder de nya kommentarerna kan använda det utökade området, medan de webbplatser som använder standardutseendet inte påverkas.

Kommentarskomponenten är i själva verket en av två komponenter som utgör kommentarssystemet. Det finns alltså två komponenter att utöka: *kommentarer* och *kommentar*. Skriptet som ska redigeras finns i *kommentar* -komponenten `header.hbs` -filen, medan den överordnade *kommentarer* -komponenten (kommentarsystemet) är det som en författare lägger till på sidan.

Om du vill utöka kommentarerna måste du:

1. [Skapa komponenterna](extend-create-components.md)
1. [Lägg till kommentar på exempelsida](extend-sample-page.md)
1. [Ändra utseendet](extend-alter-appearance.md)
