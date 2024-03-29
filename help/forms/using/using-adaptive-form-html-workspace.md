---
title: Använda ett anpassat formulär på arbetsytan i HTML
description: Lär dig hur du använder ett adaptivt formulär på arbetsytan i HTML där fältarbetare kan få åtkomst till formuläret på sina enheter.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Använda ett anpassat formulär på arbetsytan i HTML{#using-an-adaptive-form-in-html-workspace}

Med AEM Forms på JEE kan du använda ett anpassningsbart formulär i arbetsytan i HTML.

Eftersom man kan välja en XDP-fil under processdesignen har man lagt till möjligheten att bläddra i en befintlig databas AEM adaptiva formulär. Funktionen ger processdesignern möjlighet att konfigurera ett anpassningsbart formulär i Startpunkten och i Aktivitet.

## Processdesignupplevelse {#process-design-experience}

Gör följande för att aktivera anpassade formulär som ska användas i processdesign:

* I Tilldela uppgift och Startpunkt kan du bläddra till en adaptiv formulärresurs i CRX-databasen när du tilldelar en formulärresurs till en uppgift.
* I egenskapsbladet Tilldela uppgift/Startpunkt för Workbench kan du dölja det översta/globala verktygsfältet i ett anpassat formulär.
* Du kan använda nya åtgärdsprofiler för att rendera och skicka åtgärder i anpassningsbara formulär.

### Export och import av LiveCyclen {#livecycle-application-export-and-import}

Eftersom adaptiva formulär finns i AEM innehåller LiveCyclets programexport endast referenser för adaptiva formulär som används. Därför är export och import av LiveCyclen en tvåstegsprocess. LiveCyclet innehåller processdefinitioner osv. Ett separat paket som innehåller adaptiva formulär exporteras som en ZIP-fil från AEM. Vid import importeras LiveCyclet via Workbench och anpassningsbara formulär importeras via AEM.

## Användarupplevelse av anpassningsbara formulär på arbetsytan i HTML {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace innehåller vissa adaptiva formulärspecifika kontroller förutom kontroller som är tillgängliga för mobilformulär. En användare kan lägga till bilagor, spara, signera, skicka och navigera i anpassade formulär i HTML Workspace när användaren öppnar en uppgift eller startpunkt. Nedan beskrivs närmare:

1. Om du vill bifoga filer använder du uppgiftsbilagor, vilket var fallet i Mobile Forms. Alla knappar av typen bifogad fil i anpassat formulär är dolda.

1. Om du vill spara ett anpassat formulär klickar du på **Spara**, som i Mobile Forms. Alla knappar av typen Spara i anpassat formulär är dolda.

1. Använd **Skicka** knappar eller ruttåtgärder är tillgängliga, vilket var fallet i Mobile Forms. Alla knappar av typen Skicka i anpassat formulär är dolda.

1. **Global verktygsfältsynlighet för anpassat formulär**: Om Process Designer döljer det globala verktygsfältet/verktygsfältet på den översta nivån visas inte verktygsfältet och knapparna i anpassningsbara formulär.

1. **Navigeringskontroller för arbetsytan i Adaptive Forms**: Knapparna Nästa/Föregående är tillgängliga tillsammans med knapparna Spara, Skicka och Vidarebefordra åtgärd för ett anpassat formulär i arbetsytan HTML. Klicka på knapparna Nästa/Föregående så att du kan navigera i paneler med anpassningsbara formulär på arbetsytan i HTML. Knapparna Nästa/Föregående ger djup navigering, på liknande sätt som navigeringskontrollerna i mobilvyn för adaptiva formulär.

1. **eSign-tjänster och sammanfattningskomponent i anpassat formulär**: Sammanfattningskomponenten fungerar inte i HTML Workspace. Det innebär att om ett adaptivt formulär har en Sammanfattningskomponent visas det inte på arbetsytan. I stället för att skicka automatiskt i e-signeringskomponenten klickar arbetsyteanvändaren på åtgärden Skicka eller en vägåtgärd i arbetsytan HTML. När ett dokument har signerats visas det som ett platt signerat dokument. Klicka **Skicka** eller en vägåtgärd så att du kan stänga/slutföra uppgiften eller startpunkten.\
   Det signerade dokumentet samlas in från eSign-servern och XML-datafilen vidarebefordras till nästa steg i processen.

## Steg för att använda adaptiva formulär i processdesign {#steps-to-use-adaptive-forms-in-process-design}

1. Öppna Adobe Experience Manager Forms Workbench.

1. Gå till **Arkiv > Nytt > Program** eller använd det befintliga programmet för att skapa ett program.

   ![Skapa nytt program](assets/create_new_appl.png)

   Skapa program

1. Skapa en process eller använd en befintlig process i programmet.

   ![Skapa ny process](assets/create_new_process.png)

   Skapa process

1. Skapa en startpunkt eller Tilldela uppgift och dubbelklicka på den.
1. Under **[!UICONTROL Presentation & Data]** avsnitt, markera **[!UICONTROL use a CRX asset]** och klicka på ellipserna före resursen.

   ![Använda en CRX-resurs](assets/use_crx_asset.png)

   Använda en CRX-resurs

1. Markera det adaptiva formuläret som skapats med användargränssnittet Hantera resurser och klicka på **[!UICONTROL OK]**.

   ![Välj ett anpassat formulär](assets/selecting_form.png)

   Välj ett anpassat formulär

   >[!NOTE]
   >
   >Mer information om hur du skapar ett anpassat formulär finns i [Skapa ett anpassat formulär](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Mer information om hur du skapar en process finns i [Skapa och hantera processer](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
