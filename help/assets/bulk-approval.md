---
title: Granska resurser i mappar och samlingar
description: Ställ in granskningsarbetsflöden för material i en mapp eller en samling och dela dem med granskare eller kreativa partners för att få feedback.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 5%

---

# Granska resurser i mappar och samlingar {#review-folder-assets-and-collections}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/bulk-approval.html?lang=en) |

Ställ in granskningsarbetsflöden för material i en mapp eller en samling och dela dem med granskare eller kreativa partners för att få feedback.

[!DNL Adobe Experience Manager Assets] Med kan du skapa ett ad hoc-arbetsflöde för granskning av resurser i en mapp eller samling och dela det med granskare eller kreativa partner för att få feedback.

Du kan antingen associera granskningsarbetsflödet med ett projekt eller skapa en oberoende granskningsåtgärd.

När du har delat resurserna kan granskarna godkänna eller avvisa dem. Meddelanden skickas i olika faser av arbetsflödet för att meddela avsedda mottagare om att olika uppgifter har slutförts. När du till exempel delar en mapp eller samling får granskaren ett meddelande om att en mapp/samling har delats för granskning.

När granskaren har slutfört granskningen (godkänner eller avvisar resurser) får du ett meddelande om slutförd granskning.

## Skapa en granskningsuppgift för mappar {#creating-a-review-task-for-folders}

1. Från [!DNL Assets] i väljer du den mapp som du vill skapa en granskningsuppgift för.
1. I verktygsfältet klickar du på **[!UICONTROL Create Review Task]** ![skapa granskningsuppgift](assets/do-not-localize/create-review-task.png) för att öppna **[!UICONTROL Review Task]** sida. Om du inte kan se alternativet i verktygsfältet klickar du på **[!UICONTROL More]** och välj sedan alternativet.

1. (Valfritt) Från **[!UICONTROL Project]** väljer du det projekt som du vill associera granskningsuppgiften med. Som standard är **[!UICONTROL None]** är markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigeringsbehörighet för (eller högre) visas i **[!UICONTROL Projects]** lista.

1. Ange ett namn för granskningsaktiviteten och välj en godkännare på menyn **[!UICONTROL Assign To]** lista.

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i **[!UICONTROL Assign To]** lista.

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details](assets/task_details.png)

1. På fliken Avancerat anger du en etikett som ska användas för att skapa URI:n.

   ![review_name](assets/review_name.png)

1. Klicka **[!UICONTROL Submit]** och klicka sedan på **[!UICONTROL Done]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på [!DNL Assets] som godkännare och navigera till [!DNL Assets] Gränssnitt. Om du vill godkänna resurser klickar du på **[!UICONTROL Notifications]** och välj sedan granskningsaktiviteten i listan.

   ![Resursmeddelande](assets/aemAssetsNotification.png)

1. I **[!UICONTROL Review Task]** Granska informationen om granskningen och klicka sedan på **[!UICONTROL Review]**.
1. I **[!UICONTROL Review Task]** sida, markera resurser och klicka på **[!UICONTROL Approve/Reject]** godkänna eller avvisa, beroende på vad som är lämpligt.

   ![review_task](assets/review_task.png)

1. Klicka på **[!UICONTROL Complete]** i verktygsfältet. Skriv en kommentar i dialogrutan och klicka på  **[!UICONTROL Complete]** för att bekräfta.
1. Navigera till [!DNL Assets] -användargränssnittet och öppna mappen. Ikonerna för godkännandestatus för resurserna visas i kortvyn och listvyn.

   **Kortvy**

   ![Granska status som den visas i kortvyn](assets/chlimage_1-404.png)

   **Listvy**

   ![Granska status som den visas i listvyn](assets/review_status_listview.png)

## Skapa en granskningsuppgift för samlingar {#creating-a-review-task-for-collections}

1. På sidan Samlingar väljer du den samling som du vill skapa en granskningsuppgift för.
1. I verktygsfältet klickar du på **[!UICONTROL Create Review Task]** ![skapa granskningsuppgift](assets/do-not-localize/create-review-task.png) för att öppna **[!UICONTROL Review Task]** sida. Om du inte ser alternativet i verktygsfältet klickar du på **[!UICONTROL More]** och välj sedan alternativet.

1. (Valfritt) Från **[!UICONTROL Project]** väljer du det projekt som du vill associera granskningsuppgiften med. Som standard är **[!UICONTROL None]** är markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigeringsbehörighet för (eller högre) visas i **[!UICONTROL Projects]** lista.

1. Ange ett namn för granskningsaktiviteten och välj en godkännare på menyn **[!UICONTROL Assign To]** lista.

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i **[!UICONTROL Assign To]** lista.

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details-collection](assets/task_details-collection.png)

1. Klicka **[!UICONTROL Submit]** och klicka sedan på **[!UICONTROL Done]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på [!DNL Assets] som godkännare och navigera till [!DNL Assets] konsol. Om du vill godkänna resurser klickar du på **[!UICONTROL Notifications]** och välj sedan granskningsaktiviteten i listan.
1. I **[!UICONTROL Review Task]** Granska informationen om granskningen och klicka sedan på **[!UICONTROL Review]**.
1. Alla resurser i samlingen visas på granskningssidan. Markera resurserna och klicka på **[!UICONTROL Approve/Reject]** godkänna eller avvisa resurser, beroende på vad som är lämpligt.

   ![review_task_collection](assets/review_task_collection.png)

1. Klicka på **[!UICONTROL Complete]** i verktygsfältet. Skriv en kommentar i dialogrutan och klicka på **[!UICONTROL Complete]** för att bekräfta.
1. Navigera till samlingskonsolen och öppna samlingen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Bild: Kortvy.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Bild: Listvy.*
