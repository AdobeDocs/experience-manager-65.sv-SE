---
title: I den här artikeln finns anvisningar om hur du avinstallerar Forms-tilläggspaketet med CRX Package Manager.
description: Lär dig hur du avinstallerar Forms tilläggspaket med CRX Package Manager.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Avinstallera AEM Forms Add-on Package från AEM Instance

I den här artikeln beskrivs de steg som krävs för att avinstallera AEM Forms-tilläggspaketet från en AEM Forms SDK-instans. Följ de här stegen för att se till att Forms-tilläggspaketet tas bort och för att förhindra eventuella problem med AEM.

## Förutsättning

Se till att säkerhetskopiera för att undvika dataförlust.

## Avinstallera AEM Forms Add-on Package

Så här avinstallerar du AEM Forms Add-on Package:

1. **Avinstallera AEM Forms-tilläggspaketet:**
   1. Navigera till `http://[host]:[port]/crx/de/index.jsp`.
   1. Leta upp och avinstallera `AEM Forms add-on package`.

   ![Avinstallera paket](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **Ta bort den ursprungliga mappen från CRXDE:**
   1. Navigera till `http://[host]:[port]/crx/de/index.jsp`.
   1. Gå till `/libs/fd/native/install` och ta bort mappen `native` i CRXDE.

      ![Ta bort intern nod från CRX/de](/help/forms/using/assets/native-install-folder-crxde.png)
   1. Spara ändringarna.

1. **Stoppa AEM Forms SDK:**
   1. Stoppa AEM Forms SDK-instansen med kommandot Ctrl + C.

1. **Kontrollera om det finns mappar i grunden och installera dem i mappen crx-quickstart**
   1. Navigera till mappen `..author\crx-quickstart` i AEM Forms SDK-instansen.
   1. Sök efter mappar med namnen `bedrock` och `install`.
Om de hittas kontrollerar du att de tas bort från mappen `crx-quickstart` i AEM Forms SDK-instansen.

   >[!NOTE]
   >
   > Mappen `bedrock` skapas automatiskt igen när du startar om AEM Forms SDK-instansen.

1. **Starta om AEM:**
   1. När alla föregående steg har slutförts [startar du om AEM Forms SDK-instansen](/help/forms/using/restart-aem-sdk.md).




