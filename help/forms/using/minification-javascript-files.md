---
title: Miniatyrbilder av JavaScript-filer
seo-title: Minification of the JavaScript files
description: Instruktioner för att generera minierad kod efter AEM Forms-arbetsyteanpassningar för att optimera JS-filerna för webben.
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# Miniatyrbilder av JavaScript-filer {#minification-of-the-javascript-files}

Med miniatyr tas de redundanta tecknen bort från källkoden, till exempel blanksteg, ny rad och kommentarer. Detta förbättrar prestandan genom att minska storleken på koden. Miniatyrfunktionen påverkar inte funktionen, men den minskar kodens läsbarhet.

Följ de här stegen för att generera miniatyrkod för semantiska ändringar.

1. Kopiera `client-html/src/main/webapp/js` från src-package i filsystemet.

   >[!NOTE]
   >
   >Se [Introduktion till anpassning av arbetsytan i AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) för mer information om paketen.

1. Uppdatera banor i `main.js` finns under client-html/src/main/webapp/js, för tillagda/uppdaterade modeller/vyer.

   Om du till exempel lägger till en ny Sharequeue-modell, till exempel mySharequeue, ändrar du:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   Till

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Uppdatera `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` om det finns en ändring/tillägg av alias i `main.js`.

   Om du till exempel lägger till en ny Sharequeue-modell, till exempel mySharequeue, ändrar du:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   Till

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. Kör kommando på client-html/src/main/webapp/js/minifier:

   ```shell
   mvn clean install
   ```

   Den genererar en mapp med minifierade filer, under client-html/src/main/webapp/js med minifierade main.js och register.js.

>[!NOTE]
>
>Miniatyrbilder fungerar bara på 64-bitars JVM.

>[!NOTE]
>
>Uppgraderingen påverkas om du minimerar.
