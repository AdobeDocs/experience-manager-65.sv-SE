---
title: Privata mappar för att dela resurser
description: Lär dig hur du skapar en privat mapp [!DNL Adobe Experience Manager Assets] och delar den med andra användare samt tilldelar olika behörigheter till dem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 63d08f932b09e375e1b0da92cde27a60ec6e7f56
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Privat mapp i [!DNL Adobe Experience Manager Assets] {#private-folder}

Du kan skapa en privat mapp i [!DNL Adobe Experience Manager Assets] användargränssnittet som är exklusivt tillgänglig för dig. Du kan dela den här privata mappen med andra användare och tilldela andra användare olika behörigheter. Beroende på vilken behörighetsnivå du tilldelar kan användare utföra olika åtgärder i mappen, till exempel visa resurser i mappen eller redigera resurserna.

>[!NOTE]
>
>Den privata mappen har minst en medlem med ägarrollen.

## Skapa och dela privata mappar {#create-share-private-folder}

Så här skapar och delar du en privat mapp:

1. Klicka på [!DNL Assets] verktygsfältet i **[!UICONTROL Create]** konsolen och välj sedan **[!UICONTROL Folder]** från menyn.

   ![Skapa resursmapp](assets/Create-folder.png)

1. I **[!UICONTROL Create Folder]** dialogrutan anger du en rubrik och ett namn (valfritt) för mappen och väljer **[!UICONTROL Private]** alternativ.

1. Klicka på **[!UICONTROL Create]**. En privat mapp skapas.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![infoalternativ](assets/do-not-localize/info-circle-icon.png)

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
   >Den privata mappen har minst en medlem med ägarrollen. Administratören kan därför inte ta bort alla ägarmedlemmar från en privat mapp. Om du vill ta bort befintliga ägare (och själva administratören) från den privata mappen måste administratören lägga till en annan användare som ägare.

1. Klicka på **[!UICONTROL Save]**. Beroende på vilken roll du tilldelar tilldelas användaren en uppsättning behörigheter i din privata mapp när användaren loggar in på [!DNL Assets].
1. Klicka **[!UICONTROL Ok]** för att stänga bekräftelsemeddelandet.
1. Användaren som du delar mappen med får ett delningsmeddelande. Logga in [!DNL Assets] med användarens autentiseringsuppgifter för att visa meddelandet.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Klicka på Notifications (Meddelanden) för att öppna listan med meddelanden.

   ![Förteckning över meddelanden](assets/Assets-Notification.png)

1. Klicka på posten för den privata mappen som delas av administratören för att öppna mappen.

>[!NOTE]
>
>Om du vill skapa en privat mapp måste du ha [behörigheten](/help/sites-administering/security.md#permissions-in-aem) Läs och Ändra för den överordnade mappen som du vill skapa en privat mapp i. Om du inte är administratör aktiveras dessa behörigheter inte som standard för dig `/content/dam`. I så fall måste du först skaffa dessa behörigheter för ditt användar-ID/din grupp innan du försöker skapa privata mappar.

## Borttagning av privata mappar {#delete-private-folder}

Du kan ta bort en mapp genom att markera mappen och välja [!UICONTROL Delete] alternativ på den översta menyn, eller genom att använda backstegstangenten på tangentbordet.

![ta bort alternativ på den översta menyn](assets/delete-option.png)

>[!CAUTION]
>
>Om du tar bort en privat mapp från CRXDE Lite lämnas överflödiga användargrupper kvar i databasen.

>[!NOTE]
>
>Om du tar bort en mapp med metoden ovan från användargränssnittet tas även de associerade användargrupperna bort.
Befintliga redundanta, oanvända och autogenererade användargrupper kan rensas bort från databasen med hjälp av `clean` metoden i JMX i författarinstansen (http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets).
