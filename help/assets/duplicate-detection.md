---
title: Aktivera identifiering av dubblettresurser
description: Lär dig hur du aktiverar identifiering av duplicerade resurser i Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Aktivera identifiering av dubblettresurser {#enable-detection-of-duplicate-assets}

Om du försöker överföra en resurs som finns i Adobe Experience Manager Assets identifieras den som duplicerad av dubblettidentifieringsfunktionen. Dubblettidentifiering är inaktiverat som standard. Så här aktiverar du funktionen:

1. Öppna konfigurationssidan för Experience Manager Web Console genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Redigera konfigurationen för serverutrymmet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Markera **[!UICONTROL detect duplicate]** alternativet och klicka på **[!UICONTROL Save]**.

   ![Välj alternativet Identifiera dubblett i serverleten](assets/chlimage_1-377.png)

   *Bild: Välj alternativet Identifiera dubblett i serverleten*

Funktionen för att identifiera dubbletter är nu aktiverad i Assets. När en användare försöker ladda upp en resurs som finns i Experience Manager söker systemet efter en konflikt och anger den. Resurserna identifieras med SHA-1-hash som lagras på `jcr:content/metadata/dam:sha1`, vilket innebär att duplicerade resurser identifieras oavsett filnamn.

>[!MORELIKETHIS]
>
>* [Duplicera resurser i befintlig databas (en självstudiekurs från en community-medlem)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

