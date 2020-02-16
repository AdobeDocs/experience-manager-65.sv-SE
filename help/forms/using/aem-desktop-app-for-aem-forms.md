---
title: AEM-datorprogram för AEM Forms
seo-title: AEM-datorprogram för AEM Forms
description: 'null'
seo-description: 'null'
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: 6fa293028332596bb93013119b4339c7721eb536

---


# AEM-datorprogram för AEM Forms {#aem-desktop-app-for-aem-forms}

Med AEM-skrivbordsappen kan du mappa Adobe Experience Manager-resurskatalogen (AEM) och binära AEM Forms-filer till en nätverkskatalog på datorn. Du kan visa synkroniserade resurser och binära filer i en filutforskare och använda olika program för att redigera filerna efter behov. Förutom att visa filerna kan du även skapa, överföra och ta bort de binära filerna. Du kan också öppna, redigera och spara filer direkt från programmet. Du kan till exempel öppna och redigera en XDP-fil direkt i Designer. De ändringar du gör i resurserna lokalt återspeglas i AEM Resurser-databasen och användargränssnittet för AEM Forms.

Du kan hämta programmet från en AEM-instans. Mer information om hur du hämtar programmet finns i Versionsinformation om [AEM-skrivbordsappen](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## AEM Forms-resurser som stöds i AEM-skrivbordsappen {#aem-forms-assets-supported-in-aem-desktop-app}

Du kan använda appen för att synkronisera binära AEM Forms-filer av följande typ: formulärmallar (.xdp), PDF-formulär (.pdf), dokument (.pdf), bilder, XML-schema (.xsd), formatmallar (.xfs). I programmet visas alla andra filer (filer som inte stöds) som 0-byte-filer. Om du listar filer som inte stöds som 0-byte-filer ser du till att användaren är medveten om att det finns andra resurser som är tillgängliga på AEM Forms-servern.

>[!NOTE]
>
>Ett filnamn får bara innehålla alfanumeriska tecken, bindestreck eller understreck.

## Aktivera AEM Forms för datorprogrammet AEM {#enable-aem-forms-for-aem-desktop-app}

AEM Desktop App använder WebDAV-protokoll i Microsoft Windows och SMB1 i Mac OS X för att ansluta till en AEM Forms-server. Som standard är AEM Forms-servern inte aktiverad för att synkronisera binära filer och andra resurser med en WebDAV- eller SMB-klient. Gör så här för att aktivera AEM Forms för AEM-skrivbordsappen:

1. Logga in på AEM Forms som administratör.
1. I författarinstansen klickar du på ![adobeexperienceManager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Tools **![hammer](assets/hammer.png)**> Distribution > Operations > Web Console]**. Webbkonsolen öppnas i ett nytt fönster.
1. I webbkonsolfönstret letar du upp och öppnar alternativet **[!UICONTROL FormsManager AddOn Configuration]** .
1. Avmarkera kryssrutan Synkronisera resurser **[!UICONTROL asynkront i dialogrutan Lägg till i konfiguration för FormsManager och klicka på]** Spara ****.
1. Starta om AEM Forms-servern. Efter omstarten är AEM Forms-servern aktiverad för att acceptera och dela innehåll med AEM-skrivbordsappen.
1. Öppna appen och anslut till AEM Forms-servern.

   När anslutningen lyckades fyller programmet i `content/dam` - och `content/dam/formsanddocuments` mapparna. Förutom att flytta filer från mapparna ovan till lokala mappar kan du använda appen för att flytta innehåll mellan automatiskt ifyllda mappar.

