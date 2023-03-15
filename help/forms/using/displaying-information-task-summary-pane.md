---
title: Visa information i åtgärdssammanfattningsrutan
seo-title: Displaying information in the Task Summary pane
description: I AEM Forms-arbetsytan kan en åtgärdssammanfattningsruta konfigureras för att sammanfatta uppgiften eller visa en annan webbsida.
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Visa information i åtgärdssammanfattningsrutan {#displaying-information-in-the-task-summary-pane}

När du öppnar en uppgift på arbetsytan i AEM Forms kan en åtgärdssammanfattning visa en sammanfattning av uppgiften. Denna ytterligare och relevanta information för en uppgift ger mer värde för slutanvändaren av AEM Forms arbetsyta.

På arbetsytan i AEM Forms kan du visa en webbsida som du väljer i rutan Sammanfattning av uppgifter. En process kan skapas för att visa en åtgärdssammanfattningsruta med Workbench.

1. Skapa en process för tilldelning av uppgift i Workbench. Mer information om åtgärden Tilldela uppgift finns i avsnittet om tjänstreferens i [Workbench - hjälp](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >Om det finns en URL för en TaskSummary öppnas vyn Sammanfattning som standard i stället för formulärvyn. I det här fallet öppnas inte formuläret i maximerat läge, även om användaren aktiverar alternativet&quot;Öppna formuläret i maximerat läge&quot; i Tilldela uppgift.

1. Konfigurera URL-fältet för uppgiftssammanfattning. Du kan ange ett literalt värde, en mall, en variabel eller ett XPath-uttryck.
1. Ett exempel på hur informationen på sidan Uppgiftssammanfattning visas nedan.

   * Logga in i CRXDE Lite-miljön på `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:ostrukturerad`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** under `/apps`. I åtkomstkontrollistan för `/apps/SampleSummary`, lägga till en post för `PERM_WORKSPACE_USER` tillåta `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Ange värdet för uppgiftssammanfattnings-URL som `/lc/content/SampleSummary.html` i steget Tilldela uppgift.
   * När den uppgift som är associerad med det här steget Tilldela uppgift öppnas i AEM Forms arbetsyta, `html.esp` på `/apps/SampleSummary` återges i åtgärdssammanfattningsfönstret.
