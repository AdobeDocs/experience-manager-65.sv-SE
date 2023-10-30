---
title: Temaanpassning
description: Lär dig hur du anpassar temat för AEM Forms-program. Du kan anpassa HTML-koden och CSS-filen för att ge organisationsspecifik stil och känsla.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Temaanpassning {#theme-customization}

Du kan anpassa HTML-koden och CSS-filen för att ge AEM Forms-appen ett distinkt organisationsspecifikt utseende. Du kan till exempel ändra bakgrundsfärgen och höjden på uppgifter eller startpunkter. I följande exempel finns instruktioner för hur du ändrar:

* visningsanvisningar i stället för beskrivningen
* antal visningsrutter
* bakgrundsövertoningsfärg

## Steg {#steps}

1. Öppna projektet.

   * För iOS, öppna `Capture.xcodeproj` i Xcode
   * För Android öppnar du Android-projektet i Eclipse.
   * För Windows: öppna `MWSWindows.sln` i Visual Studio.

1. Navigera till mappen Mallar.

   * I Xcode navigerar du till **Capture > www > wsmoble > js > runtime > templates** mapp.
   * I Eclipse navigerar du till **assets > www > wsmoble > js > runtime > templates** mapp.
   * I Visual Studio går du till **MWSWindows > www > wsmoble > js > runtime > templates** mapp.

1. Öppna `template.html` fil för redigering.
1. Leta reda på följande sträng:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Ersätt den med `<%`.

1. Leta reda på följande kod i `template.html` fil:

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Kommentera följande rad och spara filen.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Navigera till css-mappen.

   * I Xcode navigerar du till **Capture > www > wsmoble > css**.
   * I Eclipse navigerar du till **assets > www > wsmoble > css**.
   * I Visual Studio går du till **MWSWindows > www > wsmoble > css**.

1. Öppna `_style.css` fil för redigering.
1. För bakgrundsbild ändrar du `#323232` till `#fff`.
1. Spara ändringarna och stäng `_style.css` -fil.
1. Öppna appen AEM Forms.

   Nu visas instruktioner i stället för beskrivningar i AEM Forms-appen.
