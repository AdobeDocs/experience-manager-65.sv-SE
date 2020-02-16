---
title: Gestanpassning
seo-title: Gestanpassning
description: Anpassa gesterna i appen AEM Forms
seo-description: Anpassa gesterna i appen AEM Forms
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gestanpassning {#gesture-customization}

Du kan anpassa gesterna i AEM Forms-appen för att skapa en distinkt metod för interaktion med appen. Du kan till exempel lägga till nya gester för att öppna eller stänga en uppgift eller startpunkt.

## Anpassa gester i appen AEM Forms {#to-customize-gestures-in-aem-forms-app}

I appen AEM Forms öppnar den vänstra svepningen en ny uppgift eller startpunkten medan den högra svepningen inte gör något. Följande exempel innehåller steg för att öppna en ny uppgift eller startpunkt för att utföra högersvepningsgester i appen AEM Forms.

1. Öppna projektet.

   * Öppna `Capture.xcodeproj` i Xcode för iOS
   * För Android öppnar du Android-projektet i Eclipse.
   * För Windows öppnar du `MWSWindows.sln` i Visual Studio.

1. Navigera till vymappen och öppna filen för redigering. `task.js`

   * I Xcode navigerar du till mappen **Capture > www > wsmoble > js > runtime > views** .
   * I Eclipse navigerar du till mappen **assets > www > wsmoble > js > runtime > views** .
   * I Visual Studio går du till **MWSWindows > www > wsmoble > js > runtime > views** folder.
   >[!NOTE]
   >
   >Filen task.js innehåller den stamnätsvy som är associerad med varje uppgift eller startpunkt som listas i uppgifts- eller startpunktslistorna.

1. I `task.js` filen söker du efter egenskapen events för vyn.

   Egenskapen events är en karta med varje post i formatet:

   `"EventName Selector": "Function"`

   När du utlöser en Javascript-händelse med namnet `EventName`på ett HTML-element som anges av `Selector`anropas `Function`händelsen.

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


1. Spara och stäng `task.js` filen.
1. Bygg och kör appen AEM Forms. Nu kan du öppna en med hjälp av vänstersvepning och högersvepning.

På samma sätt kan du göra ändringar i andra vyer för olika kombinationer av gester, HTML-element och funktioner.

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
