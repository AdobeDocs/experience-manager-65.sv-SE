---
title: Aktivitetsström för digitala resurser i tidslinjevyn
description: I den här artikeln beskrivs hur du visar aktivitetsloggar för resurser på tidslinjen.
contentOwner: AG
feature: Resurshantering
role: Affärsledare, administratör
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 18%

---


# Aktivitetsström på tidslinjen {#activity-stream-in-timeline}

Den här funktionen visar aktivitetsloggar för resurser på tidslinjen. Om du utför någon av följande resursrelaterade åtgärder i [!DNL Adobe Experience Manager Assets] uppdaterar aktivitetsströmfunktionen tidslinjen så att den återspeglar aktiviteten.

Följande åtgärder är loggade i aktivitetsströmmen:

* Skapa
* Ta bort
* Ladda ned (inklusive återgivningar)
* Publicera
* Avpublicera
* Godkänn
* Avvisa
* Flytta

Aktivitetsloggarna som ska visas på tidslinjen hämtas från platsen `/var/audit/com.day.cq.dam/content/dam` i CRX, där loggfiler lagras. Dessutom loggas tidslinjeaktiviteten när nya resurser överförs eller befintliga resurser ändras och checkas in i [!DNL Experience Manager] via [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) eller [Experience Manager-datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>Övergående arbetsflöden visas inte på tidslinjen eftersom ingen historikinformation sparas för dessa arbetsflöden.

Om du vill visa aktivitetsströmmen utför du en eller flera av åtgärderna för resursen, markerar resursen och väljer sedan **[!UICONTROL Timeline]** i listan GlobalNav.

![tidslinje-2](assets/timeline-2.png)

Tidslinjen visar aktivitetsströmmen för de åtgärder du utför på resurserna.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>Standardplatsen för logglagring för uppgifterna **[!UICONTROL Publish]** och **[!UICONTROL Unpublish]** är `/var/audit/com.day.cq.replication/content`. För **[!UICONTROL Move]**-uppgifter är standardplatsen `/var/audit/com.day.cq.wcm.core.page`.
