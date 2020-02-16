---
title: Ändra gränssnittets färgschema
seo-title: Ändra gränssnittets färgschema
description: Hur man selektivt ändrar färgschemat i användargränssnittet i AEM Forms-arbetsytan.
seo-description: Hur man selektivt ändrar färgschemat i användargränssnittet i AEM Forms-arbetsytan.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ändra gränssnittets färgschema {#changing-the-color-scheme-of-the-interface}

Du kan ändra färgschemat för användargränssnittets delar i AEM Forms-arbetsytan så att de passar dina behov. Nedan följer några exempel på representativa färgschemaanpassningar. Förutom de steg som beskrivs i den här artikeln finns mer information i [Allmänna steg för anpassning](/help/forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms.

## Övre navigeringsfältet {#top-navigation-bar}

### Använda bakgrundsbild {#using-background-image}

Uppdatera navigeringsfältet högst upp på arbetsytan i AEM Forms.

1. Skapa en bakgrundsbild för att uppdatera färgen. Ge filen namnet newBackground.jpg.
1. Överför bakgrundsbildfilen i mappen /apps/ws/images med en WebDAV-klient.

   >[!NOTE]
   >
   >Mer information om WebDAV-åtkomst finns på [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Referera till den nya bakgrundsbilden i /apps/ws/css/newStyle.css genom att lägga till följande format.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Använda egenskapen color i CSS {#using-color-property-in-css}

1. Lägg till följande format i newStyle.css på /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Kategorikomponent {#category-component}

Kategorikomponenten visar de olika kategorierna för dina uppgifter i den vänstra panelen. Om du vill ändra färgen definierar du bakgrundsfärgen i CSS-filens `.category` element.

## Aktivitetskomponent {#task-component}

Uppgifter visas på den mittersta panelen som kallas TaskList-komponent. Om du vill ändra färgen ändrar du formatet som är associerat med aktivitetsväljaren i formatmallen.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
