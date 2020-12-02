---
title: Arbeta med startpunkter
seo-title: Arbeta med startpunkter
description: Steg för att arbeta med en AEM Forms-process från din mobila enhet som definieras i Workbench.
seo-description: Steg för att arbeta med en AEM Forms-process från din mobila enhet som definieras i Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Arbeta med startpunkter{#working-with-startpoints}

En startpunkt anropar en process som skapats i Workbench. Den är kopplad till ett formulär som anropar processen när formuläret skickas.

>[!NOTE]
>
>Termerna startpunkter, startprocess och formulär används omväxlande när de refererar till det här konceptet.

Om du vill initiera en process från AEM Forms-appen måste du ha en startpunkt av typen **Workspace** i processen. Du måste även välja alternativet **[!UICONTROL Visibile in Mobile Workspace]** för startpunkten.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Så här startar du en process som definieras i Workbench**

1. Gå till [Startskärmen](../../forms/using/home-screen.md) för att visa startpunkterna i AEM Forms-appen.
1. Listan **[!UICONTROL All Forms]** visas som standard på skärmen **[!UICONTROL Home]**.

   Startpunkten är kopplad till ett formulär. Tryck på det startpunktassocierade formuläret i listan för att öppna det.

   Formuläret som är kopplat till startpunkten öppnas.

1. Ange informationen i **[!UICONTROL Startpoint]**-formuläret.

   Du kan lägga till anteckningar i den här aktiviteten med knappen [attachment](../../forms/using/add-attachments.md).

1. När du har fyllt i formuläret trycker du på **[!UICONTROL Submit]**.

Om programmet är offline sparas formuläret och dess data i mappen Utkorgen.

Om appen är online synkroniseras uppgiften med AEM Forms-servern och tilldelas den användare som anges i processen.

Information om hur du arbetar med uppgiften i uppgiftslistan finns i [Öppna en uppgift](/help/forms/using/open-task.md).
