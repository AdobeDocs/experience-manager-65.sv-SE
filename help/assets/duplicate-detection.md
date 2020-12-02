---
title: Aktivera identifiering av dubblettresurser
description: Lär dig hur du aktiverar identifiering av duplicerade resurser i Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Aktivera identifiering av dubblettresurser {#enable-detection-of-duplicate-assets}

Om du försöker överföra en resurs som finns i [!DNL Adobe Experience Manager Assets] identifierar funktionen för dubblettidentifiering den som dubblett. Dubblettidentifiering är inaktiverat som standard. Så här aktiverar du funktionen:

1. Öppna konfigurationssidan för [!DNL Experience Manager]-webbkonsolen genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Redigera konfigurationen för servleten **[!UICONTROL Day CQ DAM Create Asset]**.
1. Välj alternativet **[!UICONTROL detect duplicate]** och klicka på **[!UICONTROL Save]**.

   ![Välj alternativet Identifiera dubblett i serverleten](assets/chlimage_1-377.png)

   *Bild: Välj alternativet Identifiera dubbletter i serverleten.*

Funktionen för att identifiera dubbletter är nu aktiverad i [!DNL Assets]. När en användare försöker överföra en resurs som finns i [!DNL Experience Manager], söker systemet efter en konflikt och anger den. Resurserna identifieras med SHA-1-hash som lagras på `jcr:content/metadata/dam:sha1`, vilket innebär att duplicerade resurser identifieras oavsett filnamn.

>[!MORELIKETHIS]
>
>* [Duplicera resurser i befintlig databas (en självstudiekurs från en community-medlem)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

