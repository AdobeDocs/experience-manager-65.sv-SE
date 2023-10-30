---
title: Inaktivera UAC för PDFG-konfiguration för både JEE och OSGI
description: Steg för att inaktivera UAC för PDFG-konfiguration för att korrigera konvertering från Word till PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Det går inte att konvertera Word- eller Excel-filen till PDF på Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problem {#issue}

När en användare försöker konvertera Word- eller Excel-filer till PDF på Microsoft Windows Server, uppstår följande fel:

*Felmeddelande från den primära konverteraren: ALC-PDG-015-003-Systemet kan inte öppna indatafilen. Skicka filen igen eller kontakta systemadministratören.*


## Lösning {#solution}

Utför följande steg för att lösa problemet:
1. Gå till verktyget Systemkonfiguration **[!UICONTROL Start > Run]** och sedan ange **[!UICONTROL MSCONFIG]**.
1. Klicka på **[!UICONTROL Tools]** och rulla nedåt och markera **[!UICONTROL Change UAC Settings]**. Klicka **[!UICONTROL Launch]** för att köra kommandot i ett nytt fönster.
1. Justera skjutreglaget till nivån för Aldrig meddelande. När du är klar stänger du kommandofönstret och stänger fönstret Systemkonfiguration.
1. Kontrollera att registerinställningen för UAC är inställd på 0 (noll). Verifiera genom att utföra följande steg:

   1. Microsoft® rekommenderar att du säkerhetskopierar registret innan du ändrar det. Detaljerade anvisningar finns i [Säkerhetskopiera och återställa registret i Windows](https://support.microsoft.com/en-us/help/322756).
   1. Öppna Registereditorn i Microsoft® Windows. Öppna Registereditorn genom att gå till Start > Kör, skriva regedit och klicka på OK.
   1. Navigera till `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Kontrollera att värdet för EnableLUA är 0 (noll).
   1. Ange värdet för **EnableLUA** är inställt på 0 (noll). Om värdet inte är 0 ändrar du värdet till 0. Stäng Registereditorn.

1. Starta om datorn.

## Gäller för {#appliesto}

Denna lösning gäller följande:
* AEM Forms på JEE Server
* AEM Forms on OSGi Server
