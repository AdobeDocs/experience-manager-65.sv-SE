---
title: Miniatyrbilder av JavaScript-filer
seo-title: Miniatyrbilder av JavaScript-filer
description: Instruktioner för att generera minierad kod efter anpassning av arbetsytan i AEM Forms för att optimera JS-filerna för webben.
seo-description: Instruktioner för att generera minierad kod efter anpassning av arbetsytan i AEM Forms för att optimera JS-filerna för webben.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Miniatyrbilder av JavaScript-filer {#minification-of-the-javascript-files}

Med miniatyr tas de redundanta tecknen bort från källkoden, till exempel blanksteg, ny rad och kommentarer. Detta förbättrar prestandan genom att minska storleken på koden. Miniatyrfunktionen påverkar inte funktionen, men den minskar kodens läsbarhet.

Följ de här stegen för att generera miniatyrkod för semantiska ändringar.

1. Kopiera `client-html/src/main/webapp/js` från src-paket i filsystemet.

   >[!NOTE]
   >
   >Mer information om paketen finns i [Introduktion till att anpassa arbetsytan](/help/forms/using/introduction-customizing-html-workspace.md) AEM Forms.

1. Uppdatera sökvägar i `main.js` som finns under client-html/src/main/webapp/js, för tillagda/uppdaterade modeller/vyer.

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
