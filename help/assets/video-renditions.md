---
title: Videoåtergivningar
description: Videoåtergivningar
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Videoåtergivningar {#video-renditions}

Adobe Experience Manager Assets genererar videoåtergivningar för videoresurser i olika format, bland annat OGG, FLV.

Experience Manager Assets stöder statiska och dynamiska renderingar (DM-kodade renderingar) för medieresurser.

Statiska återgivningar genereras internt med hjälp av FFMPEG (som är installerat och tillgängligt på systemsökvägen) och lagras i innehållsdatabasen.

DM-kodade återgivningar lagras på proxyservern och hanteras vid körning.

Experience Manager Assets har uppspelningsstöd för dessa återgivningar på klientsidan.

Om du vill visa återgivningarna för en viss videoresurs öppnar du resurssidan och väljer ikonen Global navigering. Välj sedan **[!UICONTROL Renditions]** i listan.

![chlimage_1-478](assets/chlimage_1-478.png)

Listan med videoåtergivningar visas på panelen **[!UICONTROL Renditions]**.

![chlimage_1-479](assets/chlimage_1-479.png)

[Konfigurera Dynamic Media Cloud-tjänster](config-dynamic.md) om du vill konfigurera proxyservern för DM-kodade återgivningar.

Om du vill generera videoåtergivningar med önskade parametrar [skapar du en motsvarande videoprofil](video-profiles.md).

När du har konfigurerat proxyservern och skapat videoprofiler kan du ta med den här videoförinställningen i en bearbetningsprofil och använda bearbetningsprofilen i en mapp.

>[!NOTE]
>
>Ljuduppspelning fungerar inte för OGG- och WAV-filer i Microsoft® Internet Explorer 11. Ett fel `Invalid Source` visas på sidan med resursinformation för resurser med filnamnstillägget OGG eller WAV.
>
>På MS® Edge och iPad spelas inte OGG-filer upp och ett formatfel som inte stöds uppstår.
