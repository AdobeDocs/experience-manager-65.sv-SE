---
title: Adobe Experience Manager (AEM) för AEM Forms
description: Adobe Experience Manager (AEM) för AEM Forms
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin,User
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Adobe Experience Manager (AEM) för AEM Forms {#aem-desktop-app-for-aem-forms}

Med AEM datorprogram kan du mappa Adobe Experience Manager (AEM) Assets-databasen och binära AEM Forms-filer till en nätverkskatalog på datorn. Du kan visa synkroniserade resurser och binära filer i en filutforskare och använda olika program för att redigera filerna efter behov. Förutom att visa filerna kan du även skapa, överföra och ta bort de binära filerna. Du kan också öppna, redigera och spara filer direkt från programmet. Du kan till exempel öppna och redigera en XDP-fil direkt från Designer. De ändringar du gör av resurserna lokalt återspeglas i AEM Assets-databasen och AEM Forms användargränssnitt.

Du kan hämta programmet från en AEM. Mer information om hur du hämtar appen finns i [AEM versionsinformation för skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

## AEM Forms-resurser som stöds AEM datorprogrammet {#aem-forms-assets-supported-in-aem-desktop-app}

Du kan använda appen för att synkronisera binära AEM Forms-filer av följande typ: Formulärmallar (.xdp), PDF-formulär (.pdf), Dokument (.pdf), Bilder, XML-schema (.xsd) och formatmallar (.xfs). I programmet visas alla andra filer (filer som inte stöds) som 0-byte-filer. Om du listar filer som inte stöds som 0-byte-filer ser du till att användaren är medveten om att det finns andra resurser som är tillgängliga på AEM Forms Server.

>[!NOTE]
>
>Ett filnamn får bara innehålla alfanumeriska tecken, bindestreck eller understreck.

## Aktivera AEM Forms för AEM {#enable-aem-forms-for-aem-desktop-app}

AEM använder WebDAV-protokoll i Microsoft® Windows och SMB1 i macOS X för att ansluta till en AEM Forms Server. AEM Forms Server är inte aktiverad för att synkronisera binära filer och andra resurser med en WebDAV- eller SMB-klient. Så här aktiverar du AEM Forms för AEM datorprogram:

1. Logga in på AEM Forms som administratör.
1. Klicka på ![adobeexperienceManager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Tools]** ![hammer](assets/hammer.png) **[!UICONTROL > Deployment > Operations > Web Console]** i författarinstansen. Webbkonsolen öppnas i ett nytt fönster.
1. Leta reda på och öppna alternativet **[!UICONTROL FormsManager AddOn Configuration]** i webbkonsolfönstret.
1. Avmarkera kryssrutan **[!UICONTROL Asynchronously Sync Resources]** i dialogrutan Lägg till i konfiguration för FormsManager och klicka på **[!UICONTROL Save]**.
1. Starta om AEM Forms Server. Efter omstarten är AEM Forms Server aktiverad för att acceptera och dela innehåll med AEM skrivbordsapp.
1. Öppna appen och anslut till AEM Forms Server.

   >[!NOTE]
   >
   > Du bör använda kommandot Ctrl + C för att starta om SDK:n. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java-processer, kan det leda till inkonsekvenser i den AEM utvecklingsmiljön.

   När anslutningen lyckades fyller programmet i mapparna `content/dam` och `content/dam/formsanddocuments`. Förutom att flytta filer från ovanstående mappar till lokala mappar kan du använda appen för att flytta innehåll mellan automatiskt ifyllda mappar.
