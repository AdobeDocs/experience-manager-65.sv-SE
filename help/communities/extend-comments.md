---
title: Komponenten Utöka kommentarer
seo-title: Komponenten Utöka kommentarer
description: Utöka komponenten Kommentarer för att ändra dess utseende eller beteende för specifika användningsområden
seo-description: Utöka komponenten Kommentarer för att ändra dess utseende eller beteende för specifika användningsområden
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Komponenten Utöka kommentarer {#extend-comments-component}

Avsikten med att [utöka](client-customize.md#extensions) en standardkomponent är att ändra en komponents utseende eller beteende för specifika användningsområden.

Sökvägen till komponenten är unik och refererar standardkomponenten som en överordnad resurstyp. Risken är mindre eftersom omfattningen är begränsad jämfört med den globala omfattningen för en komponentövertäckning.

>[!NOTE]
>
>Det går inte att utöka en [överlagrad](client-customize.md#overlays) komponent.

## Exempel {#example}

Anta att rubriken för kommentarkomponenten måste visas med ett alternativt utseende på en webbplats i AEM-instansen, samtidigt som den visas med standardvisningen på en annan webbplats. I stället för att åsidosätta standardkommentaren, som ändrar kommentarkomponenten för alla instanser, är det bättre att se till att det finns flera kommentarskomponenter tillgängliga för användning på olika platser.

Om du vill implementera den här lösningen skapar du en ny komponent som utökar (åsidosätter) den befintliga och ändrar Handlebars-skriptet. Det område på webbplatsen som använder de nya kommentarerna kan använda det utökade området, medan de webbplatser som använder standardutseendet inte påverkas.

Kommentarskomponenten är i själva verket en av två komponenter som utgör kommentarssystemet. Det finns alltså två komponenter att utöka: *kommentarer* och *kommentarer*. Skriptet som ska redigeras finns i *comment *-komponentens `header.hbs` fil, medan den överordnade *kommentarkomponenten* (kommentarsystemet) är det som en författare faktiskt lägger till på sidan.

Om du vill lägga in kommentarer måste du

1. [Skapa komponenterna](extend-create-components.md)
1. [Lägg till kommentar på exempelsida](extend-sample-page.md)
1. [Ändra utseendet](extend-alter-appearance.md)

