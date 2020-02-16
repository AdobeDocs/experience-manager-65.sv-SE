---
title: Ändra teckenuppsättningen
seo-title: Ändra teckenuppsättningen
description: Du kan ange den teckenuppsättning som används för att koda utdataströmmen. Lär dig hur du kan ändra teckenuppsättningen.
seo-description: Du kan ange den teckenuppsättning som används för att koda utdataströmmen. Lär dig hur du kan ändra teckenuppsättningen.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ändra teckenuppsättningen {#change-the-character-set}

Du kan ange den teckenuppsättning som används för att koda utdataströmmen.

1. I administrationskonsolen klickar du på **[!UICONTROL Tjänster > Utdata]**.
1. Välj en teckenuppsättning i listan Teckenuppsättning under Internationalisering. Den här inställningen beror på `TransformationFormat` och `PrintFormat` anges via API:t. Om du vill ange en annan teckenuppsättning än de som visas väljer du Anpassad och anger ett kodningsvärde i rutan som visas.

   Om `TransformationFormat` är PDF och PDF/A eller `PrintFormat` är PCL, PostScript, Zebra-etikett, IPL, DPL, TPCL, GenericColorPCL eller GenericPSLevel3 stöds endast specifika teckenuppsättningar.

   Teckenuppsättningen måste vara ett giltigt kanoniskt namn. Standardvärdet är ISO-8859-1.

1. Click **[!UICONTROL Save]**.

