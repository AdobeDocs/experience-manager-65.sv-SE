---
title: Temaanpassning
seo-title: Temaanpassning
description: Så här anpassar du temat i din AEM Forms-app.
seo-description: Så här anpassar du temat i din AEM Forms-app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Temaanpassning {#theme-customization}

Du kan anpassa HTML-koden och CSS-filen för att ge AEM Forms-appen ett distinkt organisationsspecifikt utseende. Du kan till exempel ändra bakgrundsfärgen och höjden på uppgifter eller startpunkter. I följande exempel finns instruktioner för hur du ändrar:

* visningsanvisningar i stället för beskrivningen
* antal visningsrutter
* bakgrundsövertoningsfärg

## Steg {#steps}

1. Öppna projektet.

   * Öppna `Capture.xcodeproj` i Xcode för iOS
   * För Android öppnar du Android-projektet i Eclipse.
   * För Windows öppnar du `MWSWindows.sln` i Visual Studio.

1. Navigera till mappen Mallar.

   * I Xcode navigerar du till mappen **Capture > www > wsmoble > js > runtime > templates**.
   * I Eclipse navigerar du till mappen **assets > www > wsmoble > js > runtime > templates**.
   * I Visual Studio går du till mappen **MWSWindows > www > wsmoble > js > runtime > templates**.

1. Öppna `template.html`-filen för redigering.
1. Leta reda på följande sträng:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Ersätt den med `<%`.

1. Leta reda på följande kod i `template.html`-filen:

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

   * I Xcode går du till **Capture > www > wsmoble > css**.
   * I Eclipse går du till **assets > www > wsmoble > css**.
   * I Visual Studio går du till **MWSWindows > www > wsmoble > css**.

1. Öppna `_style.css`-filen för redigering.
1. För bakgrundsbild ändrar du `#323232` till `#fff`.
1. Spara ändringarna och stäng `_style.css`-filen.
1. Öppna appen AEM Forms.

   Nu visas instruktioner i stället för beskrivningar i AEM Forms-appen.
