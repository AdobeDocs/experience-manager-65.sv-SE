---
title: Ändra organisationslogotyp för varumärken
description: Om du vill märka ut AEM Forms arbetsyta anger du din organisations logotyp genom att anpassa standardlogotypen.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Ändra organisationslogotyp för varumärken {#changing-the-organization-logo-for-branding}

Organisationslogotypen visas i det övre vänstra hörnet på arbetsytan i AEM Forms. Om du vill uppdatera logotypen följer du de [allmänna stegen för anpassning av arbetsytan i AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) och följande steg.

1. Skapa en logotyp och ge filen namnet `NewWorkspace.png`. Placera bildfilen i mappen /apps/ws/images med en WebDAV-klient.

   >[!NOTE]
   >
   >Den rekommenderade storleken på logotypbilden är 218 px × 20 px.

   >[!NOTE]
   >
   >Mer information finns i [WebDAV-åtkomst](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=sv-SE).

   [WebDAV-åtkomst](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=sv-SE)

1. Referera till den nya logotypbilden i formatmallen på /apps/ws/css/newStyle.css genom att lägga till följande format.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
