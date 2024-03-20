---
title: Videoåtergivningar
description: Lär dig hur du använder Adobe Experience Manager Assets för att generera videoåtergivningar för videoresurser i olika format, som OGG, FLV och så vidare.
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
solution: Experience Manager, Experience Manager Assets
feature: Video
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# Videoåtergivningar {#video-renditions}

Adobe Experience Manager Assets genererar videoåtergivningar för videoresurser i olika format, bland annat OGG, FLV.

Experience Manager Assets har stöd för statiska och dynamiska återgivningar (DM-kodade återgivningar) för medieresurser.

Statiska återgivningar genereras internt med hjälp av FFMPEG (som är installerat och tillgängligt på systemsökvägen) och lagras i innehållsdatabasen.

DM-kodade återgivningar lagras på proxyservern och hanteras vid körning.

Experience Manager Assets har uppspelningsstöd för dessa återgivningar på klientsidan.

Om du vill visa återgivningarna för en viss videoresurs öppnar du resurssidan och väljer ikonen Global navigering. Välj sedan **[!UICONTROL Renditions]** från listan.

![chlimage_1-478](assets/chlimage_1-478.png)

Listan med videoåtergivningar visas i **[!UICONTROL Renditions]** -panelen.

![chlimage_1-479](assets/chlimage_1-479.png)

Om du vill konfigurera proxyservern för DM-kodade återgivningar [konfigurera Dynamic Media Cloud-tjänster](config-dynamic.md).

Om du vill generera videoåtergivningar med önskade parametrar [skapa en motsvarande videoprofil](video-profiles.md).

När du har konfigurerat proxyservern och skapat videoprofiler kan du ta med den här videoförinställningen i en bearbetningsprofil och använda bearbetningsprofilen i en mapp.

>[!NOTE]
>
>Ljuduppspelning fungerar inte för OGG- och WAV-filer i Microsoft® Internet Explorer 11. Ett fel `Invalid Source` visas på sidan med tillgångsinformation för resurser med filnamnstillägget OGG eller WAV.
>
>I MS® Edge och iPad spelas inte OGG-filer upp och ett formatfel som inte stöds genereras.
