---
title: Privata mappar för att dela resurser
description: Lär dig hur du skapar en privat mapp i  [!DNL Adobe Experience Manager Assets] och delar den med andra användare och tilldelar olika behörigheter till dem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Privat mapp i [!DNL Adobe Experience Manager Assets] {#private-folder}

Du kan skapa en privat mapp i [!DNL Adobe Experience Manager Assets]-användargränssnittet som är exklusivt tillgänglig för dig. Du kan dela den här privata mappen med andra användare och tilldela andra användare olika behörigheter. Beroende på vilken behörighetsnivå du tilldelar kan användare utföra olika åtgärder i mappen, till exempel visa resurser i mappen eller redigera resurserna.

>[!NOTE]
>
>Den privata mappen har minst en medlem med ägarrollen.

## Skapa och dela privata mappar {#create-share-private-folder}

Så här skapar och delar du en privat mapp:

1. Klicka på **[!UICONTROL Create]** i verktygsfältet i [!DNL Assets]-konsolen och välj sedan **[!UICONTROL Folder]** på menyn.

   ![Skapa resursmapp](assets/Create-folder.png)

1. I dialogrutan **[!UICONTROL Create Folder]** anger du en rubrik och ett namn (valfritt) för mappen och väljer alternativet **[!UICONTROL Private]**.

1. Klicka på **[!UICONTROL Create]**. En privat mapp skapas.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Om du vill dela mappen med andra användare och tilldela behörigheter till dem markerar du mappen och klickar på **[!UICONTROL Properties]** i verktygsfältet.

   ![infoalternativ](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >Mappen visas inte för andra användare förrän du delar den.

1. På sidan **[!UICONTROL Folder Properties]** väljer du en användare i listan **[!UICONTROL Add User]**, tilldelar en roll till användaren i din privata mapp och klickar på **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Du kan tilldela olika roller, till exempel `Editor`, `Owner` eller `Viewer` till användaren som du delar mappen med. Om du tilldelar användaren en `Owner`-roll har användaren `Editor`-behörighet för mappen. Dessutom kan användaren dela mappen med andra. Om du tilldelar en `Editor`-roll kan användaren redigera resurserna i din privata mapp. Om du tilldelar en visningsprogramroll kan användaren bara visa resurserna i din privata mapp.

   >[!NOTE]
   >
   >Den privata mappen har minst en medlem med rollen `Owner`. Administratören kan därför inte ta bort alla ägarmedlemmar från en privat mapp. Om du vill ta bort befintliga ägare (och själva administratören) från den privata mappen måste administratören lägga till en annan användare som ägare.

1. Klicka på **[!UICONTROL Save]**. Beroende på vilken roll du tilldelar tilldelas användaren en uppsättning behörigheter i din privata mapp när användaren loggar in på [!DNL Assets].
1. Klicka på **[!UICONTROL Ok]** för att stänga bekräftelsemeddelandet.
1. Användaren som du delar mappen med får ett delningsmeddelande. Logga in på [!DNL Assets] med inloggningsuppgifterna för användaren för att visa meddelandet.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Klicka på [!UICONTROL Notifications] för att öppna en lista med meddelanden.

   ![Förteckning över meddelanden](assets/Assets-Notification.png)

1. Klicka på posten för den privata mappen som delas av administratören för att öppna mappen.

>[!NOTE]
>
>Om du vill skapa en privat mapp måste du ha behörigheten Läs och Ändra [åtkomstkontroll](/help/sites-administering/security.md#permissions-in-aem) för den överordnade mapp som du vill skapa en privat mapp i. Om du inte är administratör aktiveras dessa behörigheter inte som standard för `/content/dam`. I så fall måste du först skaffa dessa behörigheter för ditt användar-ID/din grupp innan du försöker skapa privata mappar.

## Ta bort privat mapp {#delete-private-folder}

Du kan ta bort en mapp genom att markera mappen och välja [!UICONTROL Delete] på den översta menyn eller genom att använda Backsteg på tangentbordet.

![ta bort alternativ på den översta menyn](assets/delete-option.png)

>[!CAUTION]
>
>Om du tar bort en privat mapp från CRXDE Lite lämnas överflödiga användargrupper kvar i databasen.

>[!NOTE]
>
>Om du tar bort en mapp med metoden ovan från användargränssnittet tas även de associerade användargrupperna bort.
>
>Befintliga redundanta, oanvända och autogenererade användargrupper kan dock tas bort från databasen med metoden `clean` i JMX i författarinstansen (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
