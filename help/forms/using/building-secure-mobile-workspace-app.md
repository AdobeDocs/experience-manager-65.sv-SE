---
title: Bygga en säker AEM Forms-app för iOS
seo-title: Bygga en säker AEM Forms-app för iOS
description: Steg för att skapa en säker AEM Forms-app.
seo-description: Steg för att skapa en säker AEM Forms-app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Skapa en säker AEM Forms-app för iOS {#building-a-secure-aem-forms-app-for-ios}

Du måste arkivera Xcode-projektet för AEM Forms-programmet för att kunna skapa installationsprogrammet (en IPA-fil) och en egenskapslista (en PLIST-fil). Egenskapslistfilen innehåller konfigurationsinformation för det värdbaserade interna programmet, till exempel namnet och appens värdplats. Mer information om egenskapslistfilen finns i [Om informationsegenskapslistefiler](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Logga in på följande webbplats:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Skapa ett program-ID. Mer information om hur du skapar ett program-ID finns i [Skapa och konfigurera program-ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Klicka på **[!UICONTROL Configure App ID]** om du vill konfigurera paketidentifieraren för iOS-programmet för din app.
1. Välj **[!UICONTROL Enable for Data Protection]** längst ned på webbsidan. Ange alternativ för dataskydd.

   Klicka på **[!UICONTROL Done]**.

1. Navigera till Provisioning->Distribution och skapa en ny profil med det program-ID som konfigurerats i steg 3.
1. Hämta och lägg till provisioneringsprofilen i Xcode och iPad.
1. Logga in på en Mac-dator som har Xcode och iOS SDK installerat och konfigurerat.
1. Öppna `AEM Forms.xcodeproj`-projektet i Xcode.
1. Klicka på **[!UICONTROL AEM Forms]**, under **[!UICONTROL TARGETS]**, välj **[!UICONTROL AEM Forms]**. Välj fliken **[!UICONTROL Build Settings]**, leta upp avsnittet **[!UICONTROL Code Signing Entitlement]** och välj alternativet **[!UICONTROL LC Enterprise]** i listrutan Entitlements.
1. Leta reda på och öppna `LC Enterprise.entitlements`-filen i Xcode för redigering. Under **XCode-berättiganden** lägger du till samma nyckelvärdepar som i provisioneringsprofilen.
1. Klicka på **[!UICONTROL All]** på fliken **[!UICONTROL Build Settings]** och sedan på **[!UICONTROL Combined]**.
1. Expandera **[!UICONTROL Code Signing]** från listan **[!UICONTROL Settings]**.
1. Välj lämplig signatur för **[!UICONTROL Code Signing Identity]**. Se till att samma signatur är markerad för **[!UICONTROL Debug]**, **[!UICONTROL Release]** och **[!UICONTROL Any iOS SDK]**.
1. Under **[!UICONTROL PROJECT]** väljer du **[!UICONTROL AEM Forms]** och kontrollerar att rätt signatur är markerad för **[!UICONTROL Code Signing Identity]**, **[!UICONTROL Debug]**, **[!UICONTROL Release]** och **[!UICONTROL Any iOS SDK]**.
1. Bygg och distribuera appen AEM Forms. Detaljerade anvisningar om hur du skapar och distribuerar AEM Forms-program finns i [Bygg installationsprogrammet för AEM Forms-programmet](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
