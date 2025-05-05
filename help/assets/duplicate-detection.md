---
title: Aktivera identifiering av dubblettresurser
description: Lär dig hur du aktiverar identifiering av duplicerade resurser i Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Aktivera identifiering av dubblettresurser {#enable-detection-of-duplicate-assets}

Om du försöker överföra en resurs som finns i [!DNL Adobe Experience Manager Assets] identifieras den som duplicerad av dubblettidentifieringsfunktionen. Dubblettidentifiering är inaktiverat som standard. Så här aktiverar du funktionen:

1. Öppna webbkonsolens konfigurationssida [!DNL Experience Manager] genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Redigera konfigurationen för servern **[!UICONTROL Day CQ DAM Create Asset]**.
1. Välj alternativet **[!UICONTROL detect duplicate]** och klicka på **[!UICONTROL Save]**.

   ![Välj alternativet Identifiera dubblett i serverleten](assets/chlimage_1-377.png)

   *Bild: Välj alternativet Identifiera dubblett i serverleten.*

Funktionen för att identifiera dubbletter har nu aktiverats i [!DNL Assets]. När en användare försöker överföra en resurs som finns i [!DNL Experience Manager] söker systemet efter en konflikt och anger den. Resurserna identifieras med SHA-1-hash som lagras på `jcr:content/metadata/dam:sha1`, vilket innebär att duplicerade resurser identifieras oavsett filnamn.

>[!MORELIKETHIS]
>
>* [Duplicera resurser i befintlig databas (en självstudiekurs från en community-medlem)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Identifiera duplicerade resurser i AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html?lang=sv-SE)
