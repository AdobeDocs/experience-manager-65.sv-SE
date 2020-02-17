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
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# Bygga en säker AEM Forms-app för iOS {#building-a-secure-aem-forms-app-for-ios}

Du måste arkivera Xcode-projektet för AEM Forms-appen för att skapa installationsprogrammet (en IPA-fil) och en egenskapslista (en .plist-fil). Egenskapslistfilen innehåller konfigurationsinformation för det värdbaserade interna programmet, till exempel namnet och appens värdplats. Mer information om egenskapslistfiler finns i [Om egenskapslistefiler](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Logga in på följande webbplats:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Skapa ett program-ID. Mer information om hur du skapar ett program-ID finns i [Skapa och konfigurera program-ID:n](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Om du vill konfigurera källidentifieraren för iOS-programmet för din app klickar du på **[!UICONTROL Konfigurera program-ID]**.
1. Längst ned på webbsidan väljer du **[!UICONTROL Aktivera för dataskydd]**. Ange alternativ för dataskydd.

   Klicka på **[!UICONTROL Klar]**.

1. Navigera till Provisioning->Distribution och skapa en ny profil med det program-ID som konfigurerats i steg 3.
1. Hämta och lägg till provisioneringsprofilen i Xcode och iPad.
1. Logga in på en Mac-dator som har Xcode och iOS SDK installerat och konfigurerat.
1. Öppna `AEM Forms.xcodeproj` projektet i Xcode.
1. Klicka på **[!UICONTROL AEM Forms]** och välj **[!UICONTROL AEM Forms]** under **[!UICONTROL MÅL]**. Välj fliken **[!UICONTROL Bygginställningar]** , gå till avsnittet **[!UICONTROL Kodsigneringsberättigande]** och välj alternativet **[!UICONTROL LC Enterprise]** i listrutan Entitlements.
1. Leta reda på och öppna `LC Enterprise.entitlements` filen i Xcode för redigering. Under **XCode-berättiganden** lägger du till samma nyckel/värde-par som i provisioneringsprofilen.
1. Klicka på **[!UICONTROL Alla]** på fliken **[!UICONTROL Bygginställningar]** och sedan på **[!UICONTROL Kombinerad]**.
1. Expandera **[!UICONTROL Kodsignering i listan]** Inställningar ****.
1. Välj lämplig signatur för **[!UICONTROL Kodsigneringsidentitet]**. Se till att samma signatur är markerad för **[!UICONTROL Felsök]**, **[!UICONTROL Frigör]** och **[!UICONTROL Valfri iOS SDK]**.
1. Under **[!UICONTROL PROJEKT]** väljer du **[!UICONTROL AEM Forms]** och ser till att rätt signatur är markerat för **[!UICONTROL kodsigneringsidentitet]**, **[!UICONTROL felsökning]**, **[!UICONTROL release]** **** och¥Any iOS SDK.
1. Bygg och distribuera appen AEM Forms. Detaljerade anvisningar om hur du skapar och distribuerar appen AEM Forms finns i [Skapa installationsprogrammet för appen](/help/forms/using/setup-xcode-project-build-installer.md#main-pars-text-12)AEM Forms.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
