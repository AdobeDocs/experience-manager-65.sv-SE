---
title: Bygga en säker AEM Forms-app för iOS
seo-title: Building a secure AEM Forms app for iOS
description: Steg för att skapa en säker AEM Forms-app.
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '320'
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

1. Navigera till Provisioning->Distribution och skapa en ny profil med det program-ID som konfigurerats i steg 3.
1. Hämta och lägg till provisioneringsprofilen i Xcode och iPad.
1. Logga in på en Mac-dator som har Xcode och iOS SDK installerat och konfigurerat.
1. Öppna `AEM Forms.xcodeproj` projekt i Xcode.
1. Klicka **[!UICONTROL AEM Forms]**, under **[!UICONTROL TARGETS]**, markera **[!UICONTROL AEM Forms]**. Välj **[!UICONTROL Build Settings]** -fliken, leta upp **[!UICONTROL Code Signing Entitlement]** och i listrutan Entitlements väljer du **[!UICONTROL LC Enterprise]** alternativ.
1. Leta reda på och öppna `LC Enterprise.entitlements` i Xcode för redigering. Under **XCode-berättiganden** lägger du till samma nyckelvärdepar som i din provisioneringsprofil.
1. I **[!UICONTROL Build Settings]** flik, klicka **[!UICONTROL All]** och sedan klicka **[!UICONTROL Combined]**.
1. Från **[!UICONTROL Settings]** lista, expandera **[!UICONTROL Code Signing]**.
1. För **[!UICONTROL Code Signing Identity]** väljer du lämplig signatur. Se till att samma signatur är vald för **[!UICONTROL Debug]**, **[!UICONTROL Release]** och **[!UICONTROL Any iOS SDK]**.
1. Under **[!UICONTROL PROJECT]**, markera **[!UICONTROL AEM Forms]** och se till att rätt signatur väljs för **[!UICONTROL Code Signing Identity]**, **[!UICONTROL Debug]**, **[!UICONTROL Release]** och **[!UICONTROL Any iOS SDK]**.
1. Bygg och distribuera appen AEM Forms. Detaljerade anvisningar om hur du bygger och distribuerar AEM Forms-program finns i [Bygg installationsprogrammet för AEM Forms-appen](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
