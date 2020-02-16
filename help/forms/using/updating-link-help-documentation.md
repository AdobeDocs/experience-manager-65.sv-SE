---
title: Uppdaterar länken till dokumentationen
seo-title: Uppdaterar länken till dokumentationen
description: Så här uppdaterar du målet för hjälplänken för arbetsytan i AEM Forms-arbetsytan så att den pekar på den anpassade dokumentationslänken.
seo-description: Så här uppdaterar du målet för hjälplänken för arbetsytan i AEM Forms-arbetsytan så att den pekar på den anpassade dokumentationslänken.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uppdaterar länken till dokumentationen {#updating-the-link-to-the-documentation}

Du kommer åt standardhjälpinnehållet för AEM Forms-arbetsytan genom att välja **Hjälp > Hjälp** om arbetsyta. Det hänvisar till onlinedokumentationen på Adobes webbplats. Du kan dock uppdatera den så att den pekar på en annan URL.

Här följer några exempel på hur du kan ändra standardhjälpens URL:

* För att få hjälp på valfritt språk.
* Skräddarsy hjälpmaterial för en skräddarsydd arbetsyta.

Om du vill uppdatera webbadressen för onlinedokumentationen följer du de [allmänna anpassningsstegen](/help/forms/using/generic-steps-html-workspace-customization.md) och sedan följande steg.

1. Kopiera `userinfo.html` filen från `/libs/ws/js/runtime/templates` till `/apps/ws/js/runtime/templates`.
1. Ändra:

   ```
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   till

   ```
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Gör följande:

   1. Öppna /apps/ws/js/registry.js för redigering.
   1. Sök och ersätt `text!/lc/libs/ws/js/runtime/templates/userinfo.html` med `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
