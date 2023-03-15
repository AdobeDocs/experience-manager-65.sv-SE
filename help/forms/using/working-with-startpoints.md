---
title: Arbeta med startpunkter
seo-title: Working with Startpoints
description: Steg för att arbeta med en AEM Forms-process från din mobila enhet som definieras i Workbench.
seo-description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Arbeta med startpunkter{#working-with-startpoints}

En startpunkt anropar en process som skapats i Workbench. Den är kopplad till ett formulär som anropar processen när formuläret skickas.

>[!NOTE]
>
>Termerna startpunkter, startprocess och formulär används omväxlande när de refererar till det här konceptet.

Om du vill initiera en process från AEM Forms-appen måste du ha en startpunkt av typen **Arbetsyta** i processen. Du måste även välja **[!UICONTROL Visibile in Mobile Workspace]** för startpunkten.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Så här startar du en process som definieras i Workbench**

1. Om du vill visa startpunkterna i AEM Forms-appen går du till [Hemskärm](../../forms/using/home-screen.md).
1. På **[!UICONTROL Home]** som standard visas **[!UICONTROL All Forms]** visas.

   Startpunkten är kopplad till ett formulär. Tryck på det startpunktassocierade formuläret i listan för att öppna det.

   Formuläret som är kopplat till startpunkten öppnas.

1. Ange informationen i dialogrutan **[!UICONTROL Startpoint]** formulär.

   Du kan lägga till anteckningar i den här uppgiften med [bifogad](../../forms/using/add-attachments.md) -knappen.

1. När du har fyllt i formuläret trycker du på **[!UICONTROL Submit]** -knappen.

Om programmet är offline sparas formuläret och dess data i mappen Utkorgen.

Om appen är online synkroniseras uppgiften med AEM Forms-servern och tilldelas den användare som anges i processen.

Information om hur du arbetar med uppgiften i uppgiftslistan finns i [Öppna en uppgift](/help/forms/using/open-task.md).
