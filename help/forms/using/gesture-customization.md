---
title: Gestanpassning
description: Lär dig hur du anpassar gesterna i AEM Forms-appen. Du kan anpassa gesterna för att få en tydlig metod för interaktion med programmet.
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Gestanpassning {#gesture-customization}

Du kan anpassa gesterna i AEM Forms-appen för att skapa en distinkt metod för interaktion med appen. Du kan till exempel lägga till nya gester för att öppna eller stänga en uppgift eller startpunkt.

## Anpassa gester i AEM Forms {#to-customize-gestures-in-aem-forms-app}

I AEM Forms-appen öppnas en ny åtgärd med den vänstra svepningen eller startpunkten medan den högra svepningen inte gör något. Följande exempel innehåller steg för att öppna en ny uppgift eller Startpunkt för att utföra högersvepningsgester i AEM Forms-appen.

1. Öppna projektet.

   * För iOS, öppna `Capture.xcodeproj` i Xcode
   * För Android öppnar du Android-projektet i Eclipse.
   * För Windows: öppna `MWSWindows.sln` i Visual Studio.

1. Navigera till vymappen och öppna `task.js` fil för redigering.

   * I Xcode navigerar du till **Capture > www > wsmoble > js > runtime > views** mapp.
   * I Eclipse navigerar du till **assets > www > wsmoble > js > runtime > views** mapp.
   * I Visual Studio går du till **MWSWindows > www > wsmoble > js > runtime > views** mapp.

   >[!NOTE]
   >
   >Filen task.js innehåller den stamnätsvy som är associerad med varje uppgift eller startpunkt som listas i uppgifts- eller startpunktslistorna.

1. I `task.js` söker du efter egenskapen events för vyn.

   Egenskapen events är en karta med varje post i formatet:

   `"EventName Selector": "Function"`

   När du utlöser en JavaScript-händelse med namnet `EventName`på ett HTML-element som anges av `Selector`, `Function`anropas.

1. Sök

   * &quot;tap.taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;tap.taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;tap.task-content&quot; : &quot;onTaskClick&quot;,

     &quot;tap.last_empty_div&quot; : &quot;onTaskClick&quot;,

   och ersätt med

   * &quot;swipe.taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe.taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Spara och stäng `task.js` -fil.
1. Bygg och kör appen AEM Forms. Nu kan du öppna en med hjälp av vänstersvepning och högersvepning.

På samma sätt kan du göra ändringar i andra vyer för olika kombinationer av gester, HTML-element och funktioner.
