---
title: Initiera en ny process med befintliga processdata på arbetsytan i AEM Forms
seo-title: Initiating a new process with existing process data in AEM Forms workspace
description: Se hur du kan initiera en ny process med befintliga processdata i AEM Forms arbetsyta.
seo-description: See how you can initiate a new process with existing process data in AEM Forms workspace.
uuid: 4cb96d7f-483b-4db4-bea1-57948931423d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: cbc5af90-5d51-4fdb-ac72-eea91137975d
docset: aem65
exl-id: 6fa97c06-9238-4444-b67f-983ef3b6fdc8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Initiera en ny process med befintliga processdata på arbetsytan i AEM Forms{#initiating-a-new-process-with-existing-process-data-in-aem-forms-workspace}

Du kan initiera en ny process med data från en befintlig processdata. Behovet av att initiera en ny process från befintliga processdata uppstår när vi måste använda samma formulär ofta med få innehållsändringar som t.ex. för formulär som inte har betalats. Den här funktionen sparar tid och arbete åt användarna, särskilt när processen har långa formulär att fylla i.

Så här startar du en ny process från befintliga processdata:-

1. Gör något av följande:

   * Klicka på den processinstans vars data du vill använda i Spärra/knip. Klicka på den aktivitetsrad som motsvarar startpunkten i vyn Processhistorik i den högra rutan.
   * I Spärra/knip väljer du en sökmall som visar en lista med processinstanser. Markera instansen vars data du vill använda.
   * I **[!UICONTROL To-Do]** väljer du uppgiften. Klicka på **[!UICONTROL History]** och välj den åtgärd som initierade processinstansen.

   ![Välj uppgift](assets/start3_new.png) ![Välj uppgift](assets/start1_new.png)

1. Klicka på **[!UICONTROL Start]**. Ett adaptivt formulär för den nya processinstansen visas med förfyllda data.

1. Uppdatera data efter behov och klicka på antingen **[!UICONTROL Complete]** eller en lämplig knapp i formuläret.
