---
title: Bygga en säker AEM Forms-app för iOS
description: Lär dig hur du skapar en säker AEM Forms-app för iOS genom att arkivera Xcode-projektet. Detta skapar en installationsfil (en .ipa-fil) och en egenskapslista (en .plist-fil).
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Bygga en säker AEM Forms-app för iOS {#building-a-secure-aem-forms-app-for-ios}

Du måste arkivera Xcode-projektet för AEM Forms-programmet för att kunna skapa installationsprogrammet (en IPA-fil) och en egenskapslista (en PLIST-fil). Egenskapslistfilen innehåller konfigurationsinformation för det värdbaserade interna programmet, till exempel namnet och appens värdplats. Mer information om egenskapslistfilen finns i [Om egenskapslistfiler för information](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Logga in på följande webbplats:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Skapa ett program-ID. Detaljerade anvisningar om hur du skapar ett program-ID finns i [Skapa och konfigurera program-ID:n](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Om du vill konfigurera källidentifieraren för iOS-programmet för din app klickar du på **[!UICONTROL Configure App ID]**.
1. Längst ned på webbsidan väljer du **[!UICONTROL Enable for Data Protection]**. Ange alternativ för dataskydd.

   Klicka på **[!UICONTROL Done]**.

1. Navigera till Provisioning>Distribution och skapa en ny profil med det program-ID som konfigurerats i steg 3.
1. Hämta och lägg till provisioneringsprofilen i Xcode och iPad.
1. Logga in på en Mac-dator som har Xcode och iOS SDK installerat och konfigurerat.
1. Öppna `AEM Forms.xcodeproj` projekt i Xcode.
1. Klicka **[!UICONTROL AEM Forms]**, under **[!UICONTROL TARGETS]**, markera **[!UICONTROL AEM Forms]**. Välj **[!UICONTROL Build Settings]** -fliken, leta upp **[!UICONTROL Code Signing Entitlement]** och i listrutan Tillstånd väljer du **[!UICONTROL LC Enterprise]** alternativ.
1. Leta reda på och öppna `LC Enterprise.entitlements` i Xcode för redigering. Under **XCode-berättiganden** lägger du till samma nyckelvärdepar som i din provisioneringsprofil.
1. I **[!UICONTROL Build Settings]** flik, klicka **[!UICONTROL All]** och sedan klicka **[!UICONTROL Combined]**.
1. Från **[!UICONTROL Settings]** lista, expandera **[!UICONTROL Code Signing]**.
1. För **[!UICONTROL Code Signing Identity]** väljer du lämplig signatur. Se till att samma signatur är vald för **[!UICONTROL Debug]**, **[!UICONTROL Release]** och **[!UICONTROL Any iOS SDK]**.
1. Under **[!UICONTROL PROJECT]**, markera **[!UICONTROL AEM Forms]** och se till att rätt signatur väljs för **[!UICONTROL Code Signing Identity]**, **[!UICONTROL Debug]**, **[!UICONTROL Release]** och **[!UICONTROL Any iOS SDK]**.
1. Bygg och distribuera appen AEM Forms. Detaljerade anvisningar om hur du bygger och distribuerar AEM Forms-program finns i [Skapa installationsprogrammet för AEM Forms-appen](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
