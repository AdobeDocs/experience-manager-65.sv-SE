---
title: Använda ett anpassat formulär i HTML Workspace
seo-title: Använda ett anpassat formulär i HTML Workspace
description: Använda ett anpassat formulär i HTML Workspace
seo-description: Använda ett anpassat formulär i HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Använda ett anpassat formulär i HTML Workspace{#using-an-adaptive-form-in-html-workspace}

Med AEM Forms on JEE kan man använda ett adaptivt formulär i HTML Workspace.

Eftersom man kan välja en XDP-fil under processdesignen har man lagt till möjligheten att bläddra i en befintlig AEM-databas med adaptiva formulär. Funktionen ger processdesignern möjlighet att konfigurera ett adaptivt formulär i både startpunkten och i uppgiften.

## Processdesignupplevelse {#process-design-experience}

Gör följande för att aktivera anpassade formulär som ska användas i processdesign:

* I Tilldela uppgift och Startpunkt kan du bläddra till en adaptiv formulärresurs i CRX-databasen när du tilldelar en formulärresurs till en uppgift.
* I egenskapsbladet Tilldela uppgift/Startpunkt för Workbench kan du dölja det översta/globala verktygsfältet i ett anpassat formulär.
* Du kan använda nya åtgärdsprofiler för att rendera och skicka åtgärder i anpassningsbara formulär.

### Export och import av LiveCycle-program {#livecycle-application-export-and-import}

Eftersom anpassningsbara formulär finns i AEM-databasen innehåller LiveCycle-programexporten endast referenser för anpassade formulär som används. Därför är export och import av LiveCycle-program en tvåstegsprocess. LiveCycle innehåller processdefinitioner osv. Ett separat paket som innehåller adaptiva formulär exporteras som en ZIP-fil från AEM. Vid import importeras LiveCycle-programmet via Workbench och adaptiva formulär importeras via AEM.

## Användarupplevelsen av anpassningsbara formulär i HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace innehåller vissa adaptiva formulärspecifika kontroller utöver kontroller som är tillgängliga för mobilformulär. En användare kan lägga till bilagor, spara, signera, skicka och navigera i de anpassade formulären i HTML Workspace när användaren öppnar en uppgift eller startpunkt. Nedan beskrivs närmare:

1. Om du vill bifoga filer använder du uppgiftsbilagor på samma sätt som i mobilformulär. Alla knappar av typen bifogad fil i anpassat formulär är dolda.

1. Om du vill spara ett anpassat formulär klickar du på **Spara**, vilket var fallet i Mobila formulär. Alla knappar av typen Spara i anpassat formulär är dolda.

1. Om du vill skicka in ett anpassat formulär använder du knappen **Skicka** eller de tillgängliga ruttåtgärderna, vilket var fallet i mobilformulär. Alla knappar av typen Skicka i anpassat formulär är dolda.

1. **Global verktygsfältsynlighet** för adaptiv form: Om processdesignern döljer det globala verktygsfältet/verktygsfältet på den översta nivån visas inte verktygsfältet och knapparna i anpassningsbara formulär.

1. **Navigeringskontroller för anpassningsbara formulär**: Knapparna Nästa/Föregående är tillgängliga tillsammans med knapparna Spara, Skicka och Vidarebefordra åtgärd för ett anpassat formulär i HTML Workspace. Klicka på knapparna Nästa/Föregående för att navigera i paneler med adaptiva formulär i HTML Workspace. Knapparna Nästa/Föregående ger djup navigering, på liknande sätt som navigeringskontrollerna i mobilvyn för adaptiva formulär.

1. **eSign-tjänster och komponenten i sammanfattning av det adaptiva formuläret**: Sammanfattningskomponenten fungerar inte i HTML Workspace. Det innebär att om ett adaptivt formulär har en Sammanfattningskomponent visas det inte på arbetsytan. I stället för att skicka automatiskt i eSign-komponenten klickar arbetsyteanvändaren på åtgärden Skicka eller en vägåtgärd i HTML-arbetsytan. När ett dokument har signerats visas det som ett platt signerat dokument. Klicka på **Skicka** eller en vägåtgärd för att stänga/slutföra uppgiften eller Startpunkten.\
   Det signerade dokumentet samlas in från eSign-servern och XML-datafilen vidarebefordras till nästa steg i processen.

## Steg för att använda adaptiva formulär i processdesign {#steps-to-use-adaptive-forms-in-process-design}

1. Öppna Adobe Experience Manager Forms Workbench.

1. Gå till **Arkiv > Nytt > Program** eller använd det befintliga programmet för att skapa ett program.

   ![Skapa nytt program](assets/create_new_appl.png)

   Skapa nytt program

1. Skapa en process eller använd en befintlig process i programmet.

   ![Skapa ny process](assets/create_new_process.png)

   Skapa ny process

1. Skapa en startpunkt eller Tilldela uppgift och dubbelklicka på den.
1. Under **[!UICONTROL Presentation &amp; Data]** väljer du **[!UICONTROL Använd en CRX-resurs]** och klickar på ellipserna före resursen.

   ![Använda en CRX-resurs](assets/use_crx_asset.png)

   Använda en CRX-resurs

1. Markera det adaptiva formulär som har skapats med användargränssnittet Hantera resurser och klicka på **[!UICONTROL OK]**.

   ![Välj ett anpassat formulär](assets/selecting_form.png)

   Välj ett anpassat formulär

   >[!NOTE]
   >
   >Mer information om hur du skapar ett anpassat formulär finns i [Skapa ett anpassat formulär](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Mer information om hur du skapar en process finns i [Skapa och hantera processer](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).

