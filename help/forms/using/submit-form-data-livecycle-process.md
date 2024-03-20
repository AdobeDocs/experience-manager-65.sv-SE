---
title: Konfigurera AEM Forms för att skicka data till en AEM Forms om JEE-process
description: Integrera adaptiva blanketter med AEM Forms i JEE-processer för bearbetning av blankettdata.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Konfigurera AEM Forms för att skicka formulärdata till ett AEM formulär i en JEE-process{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Adaptiva formulär har stöd för att skicka data till AEM Forms om JEE-processen för vidare bearbetning. Med den kan du starta en AEM Forms on JEE-process med data som är tillgängliga från det skickade formuläret. Utför följande steg så att du kan aktivera din AEM Forms-instans för att skicka ett anpassat formulär till AEM Forms i JEE-processen:

## Konfigurera AEM Forms Server {#configure-your-aem-forms-server}

Så här gör du för att AEM Forms Server ska kunna skicka data till en AEM Forms på en JEE-server:

1. Gå till AEM webbkonfigurationskonsol på https://[*värd*]:[*port*]/system/console/configMgr.

1. Leta reda på och klicka på **SDK-konfiguration för Adobe-klient** -komponenten.
1. Klicka för att redigera konfigurationsserverns URL, användarnamn och lösenord för AEM Forms på JEE-servern.
1. Granska inställningarna och klicka på **Spara**.

![SDK-konfiguration för LiveCyclet Adobe](assets/clientsdkconfiguration.jpg)

## Mappa data med processfält {#map-data-with-process-fields}

När du har konfigurerat AEM Forms mappar du XML-data och bilagor från det skickade formuläret till fälten i AEM Forms om JEE-processen. Gör följande:

1. I den AEM webbkonfigurationskonsolen klickar du för att redigera **Guide LiveCycle Process Locator och Invoker** konfiguration.
1. Ange följande parametrar:

   * **Namn på xml-parametern data** (obligatoriskt): Ange den XML-egenskapsfil för AEM Forms on JEE-processen som måste bearbeta skickade data. Standardvärdet är **dataxml**.

   * **Namn på parametern för bifogade filer** (valfritt): Ange listan med dokumentobjekt som AEM Forms on JEE-processen måste behandla. Standardvärdet är **fileAttachmentsList**.

1. Granska inställningarna och klicka på **Spara**.

![Guide LiveCycle Process Locator och Invoker](assets/test3.jpg)

När åtgärden Skicka till Forms Workflow har konfigurerats listas de AEM Forms på JEE-serverprocesser som innehåller den angivna XML-parametern.
