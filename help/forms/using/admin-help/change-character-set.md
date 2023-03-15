---
title: Ändra teckenuppsättningen
seo-title: Change the character set
description: Du kan ange den teckenuppsättning som används för att koda utdataströmmen. Lär dig hur du kan ändra teckenuppsättningen.
seo-description: You can specify the character set used to encode the output stream. Learn how you can change the character set.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# Ändra teckenuppsättningen {#change-the-character-set}

Du kan ange den teckenuppsättning som används för att koda utdataströmmen.

1. I administrationskonsolen klickar du på **[!UICONTROL Services > output]**.
1. Välj en teckenuppsättning i listan Teckenuppsättning under Internationalisering. Den här inställningen är beroende av `TransformationFormat` och `PrintFormat` som anges via API. Om du vill ange en annan teckenuppsättning än de som visas väljer du Anpassad och anger ett kodningsvärde i rutan som visas.

   If `TransformationFormat` är PDF och PDF/A eller `PrintFormat` är PCL, PostScript, Zebra-etikett, IPL, DPL, TPCL, GenericColorPCL eller GenericPSLevel3. Endast specifika teckenuppsättningar stöds.

   Teckenuppsättningen måste vara ett giltigt kanoniskt namn. Standardvärdet är ISO-8859-1.

1. Klicka på **[!UICONTROL Save]**.
