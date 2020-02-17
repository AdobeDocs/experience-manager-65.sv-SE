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
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Arbeta med startpunkter{#working-with-startpoints}

En startpunkt anropar en process som skapats i Workbench. Den är kopplad till ett formulär som anropar processen när formuläret skickas. Gå igenom genomgången av [Geometrixx Finance Reference Site](../../forms/using/finance-reference-site-walkthrough.md) för att få information om processerna.

>[!NOTE]
>
>Termerna startpunkter, startprocess och formulär används omväxlande när de refererar till det här konceptet.

Om du vill initiera en process från appen AEM Forms måste du ha en startpunkt av typen **Workspace **i processen. Du måste också markera alternativet **[!UICONTROL Visio i mobil arbetsyta]** för startpunkten.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Så här startar du en process som definieras i Workbench**

1. Om du vill visa startpunkterna som är tillgängliga i appen AEM Forms går du till [startsidan](../../forms/using/home-screen.md).
1. Som standard visas listan **[!UICONTROL Alla formulär]**som standard på skärmen **[!UICONTROL Hem]**.

   Startpunkten är kopplad till ett formulär. Tryck på det startpunktassocierade formuläret i listan för att öppna det.

   Formuläret som är kopplat till startpunkten öppnas.

1. Ange informationen i formuläret **[!UICONTROL StartPoint]**.

   Du kan lägga till anteckningar i den här uppgiften med knappen [Bifogad](../../forms/using/add-attachments.md) fil.

1. När du har fyllt i formuläret trycker du på knappen **Skicka** .

Om programmet är offline sparas formuläret och dess data i mappen Utkorgen.

Om appen är online synkroniseras uppgiften med AEM Forms-servern och tilldelas den användare som anges i processen.

Information om hur du arbetar med uppgiften i uppgiftslistan finns i [Öppna en uppgift](/help/forms/using/open-task.md).

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
