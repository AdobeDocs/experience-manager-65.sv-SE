---
title: Arbeta med startpunkter
description: Steg för att arbeta med en Adobe Experience Manager Forms-process från din mobila enhet som definieras i Workbench.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Arbeta med startpunkter{#working-with-startpoints}

En startpunkt anropar en process som skapats i Workbench. Den är kopplad till ett formulär som anropar processen när formuläret skickas in.

>[!NOTE]
>
>Termerna startpunkter, startprocess och formulär används omväxlande när de hänvisar till det här konceptet.

Om du vill initiera en process från appen Adobe Experience Manager (AEM) Forms måste du ha en startpunkt av typen **Arbetsyta** i processen. Du måste även välja **[!UICONTROL Visible in Mobile Workspace]** för startpunkten.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Så här startar du en process som definieras i Workbench**

1. Om du vill visa startpunkterna i AEM Forms-appen går du till [Hemskärm](../../forms/using/home-screen.md).
1. På **[!UICONTROL Home]** som standard visas **[!UICONTROL All Forms]** visas.

   Startpunkten är kopplad till ett formulär. Markera startpunkten som är associerad med formuläret i listan för att öppna det.

   Formuläret som är kopplat till startpunkten öppnas.

1. Ange informationen i dialogrutan **[!UICONTROL Startpoint]** formulär.

   Du kan lägga till anteckningar i den här uppgiften med [bifogad](../../forms/using/add-attachments.md) -knappen.

1. När du har fyllt i formuläret väljer du **[!UICONTROL Submit]** -knappen.

Om programmet är offline sparas formuläret och dess data i mappen Utkorgen.

Om appen är online synkroniseras uppgiften med AEM Forms Server och tilldelas den användare som anges i processen.

Information om hur du arbetar med uppgiften i uppgiftslistan finns i [Öppna en uppgift](/help/forms/using/open-task.md).
