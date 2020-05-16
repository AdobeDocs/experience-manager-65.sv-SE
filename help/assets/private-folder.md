---
title: Skapa och dela en privat mapp i AEM
description: Lär dig hur du skapar en privat mapp i Adobe Experience Manager-resurserna (AEM) och delar den med andra användare och tilldelar olika behörigheter till dem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 979d5074fcf94ca999fd941c77038ab6305cc67d
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---


# Delning av privata mappar {#private-folder-sharing}

Du kan skapa en privat mapp i användargränssnittet för Adobe Experience Manager (AEM) Assets som är tillgängligt enbart för dig. Du kan dela den här privata mappen med andra användare och tilldela andra användare olika behörigheter. Beroende på vilken behörighetsnivå du tilldelar kan användare utföra olika åtgärder i mappen, till exempel visa resurser i mappen eller redigera resurserna.

>[!NOTE]
>
> Privat mapp har alltid minst en medlem med ägarroll.


1. I resurskonsolen: tryck/klicka **[!UICONTROL Create]** i verktygsfältet och välj sedan **[!UICONTROL Folder]** från menyn.

   ![Skapa resursmapp](assets/Create-folder.png)

1. I **[!UICONTROL Create Folder]** dialogrutan anger du en rubrik och ett namn (valfritt) för mappen och väljer **[!UICONTROL Private]**.

   ![Markera kryssrutan Privat om du vill göra mappen privat](assets/private-folder.png)

1. Tryck/klicka på **[!UICONTROL Create]**. En privat mapp skapas i användargränssnittet.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Om du vill dela mappen med andra användare och tilldela behörigheter till dem markerar du mappen och klickar/trycker på ikonen **[!UICONTROL Properties]** i verktygsfältet.

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >Mappen visas inte för andra användare förrän du delar den.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Du kan tilldela olika roller, till exempel redigeraren, ägaren eller visningsprogrammet, till användaren som du delar mappen med. Om du tilldelar användaren en ägarroll har användaren redigeringsbehörighet för mappen. Dessutom kan användaren dela mappen med andra. Om du tilldelar en redigeringsroll kan användaren redigera resurserna i din privata mapp. Om du tilldelar en visningsprogramroll kan användaren bara visa resurserna i din privata mapp.

   >[!NOTE]
   >
   > Privat mapp har alltid minst en medlem med ägarroll. Administratören kan därför inte ta bort alla ägarmedlemmar från en privat mapp. Om du vill ta bort befintliga ägare från den privata mappadministratören måste du lägga till andra användare som ägare.

1. Klicka på **[!UICONTROL Save]**. Beroende på vilken roll du tilldelar tilldelas användaren en uppsättning behörigheter i din privata mapp när användaren loggar in på AEM Resurser.
1. Klicka **[!UICONTROL Ok]** för att stänga bekräftelsemeddelandet.
1. Användaren som du delar mappen med får ett delningsmeddelande. Logga in på AEM Assets med användarens inloggningsuppgifter för att visa meddelandet.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Tryck/klicka på meddelandeikonen för att öppna listan med meddelanden.

   ![Förteckning över meddelanden](assets/Assets-Notification.png)

1. Klicka på/tryck på posten för den privata mappen som delas av administratören för att öppna mappen.

>[!NOTE]
>
>Om du vill kunna skapa en privat mapp måste du ha behörigheten Läs och Redigera åtkomstkontrollista för den överordnade mappen som du vill skapa en privat mapp i. Om du inte är administratör aktiveras dessa behörigheter inte som standard för dig `/content/dam`. I så fall måste du först skaffa dessa behörigheter för ditt användar-ID/din grupp innan du försöker skapa privata mappar eller visa mappinställningar.
