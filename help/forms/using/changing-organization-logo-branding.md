---
title: Ändra organisationslogotyp för varumärken
seo-title: Changing the organization logo for branding
description: Om du vill märka ut AEM Forms arbetsyta anger du din organisations logotyp genom att anpassa standardlogotypen.
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Ändra organisationslogotyp för varumärken {#changing-the-organization-logo-for-branding}

Organisationslogotypen visas i det övre vänstra hörnet på arbetsytan i AEM Forms. Uppdatera logotypen genom att följa [Allmänna steg för anpassning av AEM Forms arbetsyta](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) och därefter följande steg.

1. Skapa en logotyp och ge filen namnet `NewWorkspace.png`. Placera bildfilen i mappen /apps/ws/images med en WebDAV-klient.

   >[!NOTE]
   >
   >Den rekommenderade storleken på logotypbilden är 218 px × 20 px.

   >[!NOTE]
   >
   >Mer information om WebDAV-åtkomst finns i [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Referera till den nya logotypbilden i formatmallen på /apps/ws/css/newStyle.css genom att lägga till följande format.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
