---
title: Uppdaterar länken till dokumentationen
description: Så här uppdaterar du målet för hjälplänken för arbetsytan i AEM Forms så att den pekar på den anpassade dokumentationslänken.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Uppdaterar länken till dokumentationen {#updating-the-link-to-the-documentation}

Du kommer åt standardhjälpinnehållet för AEM Forms genom att välja **Hjälp > Hjälp för arbetsytan**. Den hänvisar till onlinedokumentationen på Adobe webbplats. Du kan dock uppdatera den så att den pekar på en annan URL.

Här följer några exempel på hur du kan ändra standardhjälpens URL: n:

* För att få hjälp på valfritt språk.
* Skräddarsy hjälpinnehåll för din anpassade arbetsyta.

Följ webbadressen för onlinedokumentationen för att uppdatera webbadressen [Allmänna anpassningssteg](/help/forms/using/generic-steps-html-workspace-customization.md) och därefter följande steg.

1. Kopiera `userinfo.html` fil från `/libs/ws/js/runtime/templates` till `/apps/ws/js/runtime/templates`.
1. Ändra:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   till

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Gör följande:

   1. Öppna /apps/ws/js/registry.js för redigering.
   1. Söka och ersätta `text!/lc/libs/ws/js/runtime/templates/userinfo.html` med `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
