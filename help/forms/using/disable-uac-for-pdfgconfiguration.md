---
title: Inaktivera UAC för PDFG-konfiguration för både JEE och OSGI
description: Lär dig hur du kan inaktivera UAC för PDFG-konfiguration för att korrigera konvertering från Word till PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Det går inte att konvertera Word- eller Excel-filen till PDF på Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problem {#issue}

När en användare försöker konvertera Word- eller Excel-filer till PDF på Microsoft® Windows Server, uppstår följande fel:

*Felmeddelande från den primära konverteraren:*
*ALC-PDG-015-003-Systemet kan inte öppna indatafilen. Skicka filen igen eller kontakta systemadministratören.*


## Lösning {#solution}

Gör följande:

1. Gå till **[!UICONTROL Start > Run]** och ange **[!UICONTROL MSCONFIG]** om du vill komma åt systemkonfigurationsverktyget.
1. Klicka på fliken **[!UICONTROL Tools]**, rulla nedåt och välj **[!UICONTROL Change UAC Settings]**. Klicka på **[!UICONTROL Launch]** så att du kan köra kommandot i ett nytt fönster.
1. Justera skjutreglaget till nivån för Aldrig meddelande. När du är klar stänger du kommandofönstret och stänger fönstret Systemkonfiguration.
1. Kontrollera att registerinställningen för UAC är inställd på 0 (noll). Verifiera genom att utföra följande steg:

   1. Microsoft® rekommenderar att du säkerhetskopierar registret innan du ändrar det. Detaljerade steg finns i [Säkerhetskopiera och återställa registret i Windows](https://support.microsoft.com/en-us/help/322756).
   1. Öppna Registereditorn i Microsoft® Windows. Öppna Registereditorn genom att gå till Start > Kör, skriva regedit och klicka på OK.
   1. Navigera till `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Kontrollera att värdet för EnableLUA är 0 (noll).
   1. Kontrollera att värdet för **EnableLUA** är 0 (noll). Om värdet inte är 0 ändrar du värdet till 0. Stäng Registereditorn.

1. Starta om datorn.

## Gäller för {#appliesto}

Den här lösningen gäller för AEM Forms på JEE Server och AEM Forms på OSGi Server.
