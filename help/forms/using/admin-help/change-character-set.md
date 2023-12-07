---
title: Ändra teckenuppsättningen
description: Du kan ange den teckenuppsättning som används för att koda utdataströmmen. Lär dig hur du kan ändra teckenuppsättningen.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Ändra teckenuppsättningen {#change-the-character-set}

Du kan ange den teckenuppsättning som används för att koda utdataströmmen.

1. I administrationskonsolen klickar du på **[!UICONTROL Services > output]**.
1. Välj en teckenuppsättning i listan Teckenuppsättning under Internationalisering. Den här inställningen är beroende av `TransformationFormat` och `PrintFormat` som anges via API:t. Om du vill ange en annan teckenuppsättning än de som visas väljer du Anpassad och anger ett kodningsvärde i rutan som visas.

   If `TransformationFormat` är PDF och PDF/A eller `PrintFormat` är PCL, PostScript, Zebra-etikett, IPL, DPL, TPCL, GenericColorPCL eller GenericPSLevel3. Endast specifika teckenuppsättningar stöds.

   Teckenuppsättningen måste vara ett giltigt kanoniskt namn. Standardvärdet är ISO-8859-1.

1. Klicka på **[!UICONTROL Save]**.
