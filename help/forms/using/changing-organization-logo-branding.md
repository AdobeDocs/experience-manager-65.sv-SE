---
title: Ändra organisationslogotyp för varumärken
seo-title: Ändra organisationslogotyp för varumärken
description: Om du vill märka ut AEM Forms arbetsyta anger du din organisations logotyp genom att anpassa standardlogotypen.
seo-description: Om du vill märka ut AEM Forms arbetsyta anger du din organisations logotyp genom att anpassa standardlogotypen.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Ändra organisationslogotypen för varumärket {#changing-the-organization-logo-for-branding}

Organisationslogotypen visas i det övre vänstra hörnet på arbetsytan i AEM Forms. Om du vill uppdatera logotypen följer du de allmänna stegen i anpassning av arbetsytan i AEM Forms[ och följande steg.](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)

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
