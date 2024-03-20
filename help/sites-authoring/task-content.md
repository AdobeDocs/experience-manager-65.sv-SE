---
title: Arbeta med uppgifter
description: Uppgifter representerar arbetsuppgifter som ska utföras på innehåll och används i projekt för att fastställa slutförandenivån för aktuella uppgifter
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 2%

---


# Arbeta med uppgifter {#working-with-tasks}

Uppgifter representerar arbetsuppgifter som ska utföras med avseende på innehåll. När du tilldelas en uppgift visas den i Inkorgen för arbetsflöde. Uppgiftsobjekt kan särskiljas från arbetsflödesobjekt med värdet för **Typ** kolumn.

Uppgifter används också i projekt för att fastställa projektets fullständighetsnivå.

## Spåra projektförlopp {#tracking-project-progress}

Du kan spåra projektförloppet genom att titta på aktiva/slutförda uppgifter i ett projekt som representeras av **Uppgifter** platta. Projektets förlopp kan avgöras av:

* **Åtgärdsfönster:** Ett övergripande förlopp för projektet visas i aktivitetspanelen, som finns på sidan med projektinformation.

* **Uppgiftslista:** När du klickar på aktivitetspanelen visas en lista med uppgifter. Den här listan innehåller detaljerad information om alla uppgifter som rör projektet.

Båda alternativen listar arbetsflödesuppgifter och uppgifter som du skapar direkt i aktivitetspanelen.

### Åtgärdsfönster {#task-tile}

Om ett projekt innehåller några relaterade uppgifter visas en aktivitetspanel i projektet. Aktivitetsrutan visar projektets aktuella status. Detta baseras på befintliga uppgifter i arbetsflödet och inkluderar inga uppgifter som kommer att genereras i framtiden allt eftersom arbetsflödet fortsätter. Följande information visas i åtgärdsrutan:

* Procent slutförda uppgifter
* Procent av aktiva uppgifter
* Procent av försenade uppgifter

![Aktivitetspanelen](assets/project-tile-tasks.png)

### Visa eller ändra uppgifter i ett projekt {#viewing-or-modifying-the-tasks-in-a-project}

Förutom att följa upp förloppet kanske du också vill visa mer information om projektet eller ändra det.

#### Uppgiftslista {#task-list}

Klicka på ellipsknappen längst ned till höger i aktivitetspanelen för att visa din inkorg filtrerad på aktiviteter relaterade till projektet. Uppgiftsinformationen visas tillsammans med metadata som förfallodatum, tilldelad, prioritet och status.

![Inkorg för projektuppgift](assets/project-tasks.png)

#### Uppgiftsinformation {#task-details}

Om du vill ha mer information om en viss uppgift klickar du i inkorgen på uppgiften för att markera den och sedan på **Öppna** i verktygsfältet.

![Uppgiftsinformation](assets/project-task-detail.png)

Du kan visa, redigera och lägga till information i en uppgift via olika flikar.

* **Uppgift** - Allmän uppgiftsinformation
* **Projektinformation** - Sammanfattning av projektet som aktiviteten är kopplad till
* **Arbetsflöde in** - Sammanfattning av arbetsflödet som aktiviteten är kopplad till (om tillämpligt)
* **Kommentar** - Allmänna kommentarer om själva uppgiften

### Lägga till uppgifter {#adding-tasks}

Du kan lägga till nya uppgifter i projekt. Dessa uppgifter visas sedan i aktivitetspanelen och är tillgängliga i inkorgen för meddelanden så att du är medveten om dina utestående uppgifter.

Så här lägger du till en uppgift:

1. Leta reda på **Uppgifter** panel
1. Klicka på nedåtvinklingen längst upp till höger på plattan och välj **Skapa uppgift**.
1. I **Lägg till uppgift** -fönstret, ange uppgiftsinformation som prioritet, tilldelad och förfallodatum.

   ![Lägga till en uppgift](assets/project-add-task.png)

1. Klicka **Skicka**.

## Arbeta med uppgifter i Inkorgen {#working-with-tasks-in-the-inbox}

I stället för att komma åt dina projektuppgifter från själva projektet kan du komma åt dem direkt från din inkorg. Inkorgen ger dig en översikt över dina uppgifter i olika projekt så att du kan förstå hela arbetsflödet.

I inkorgen kan du öppna uppgifterna och ange aktivitetsstatus. Uppgifter visas också i inkorgen när de tilldelas till en användargrupp som du tillhör. I det här fallet kan alla medlemmar i gruppen utföra arbetet och slutföra uppgiften.

![Inkorg](assets/project-inbox.png)

Om du vill slutföra en uppgift markerar du uppgiften och klickar på **Complete** i verktygsfältet. Lägg till information till uppgiften och klicka sedan på **Klar**. Se [Din inkorg](/help/sites-authoring/inbox.md) för mer information.
