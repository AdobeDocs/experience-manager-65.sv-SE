---
title: Konfigurera AEM Forms för att skicka formulärdata till en AEM Forms på JEE-process
seo-title: Konfigurera AEM Forms för att skicka formulärdata till en AEM Forms på JEE-process
description: Med AEM Forms kan man integrera adaptiva formulär med AEM Forms i JEE-processer för bearbetning av formulärdata.
seo-description: Med AEM Forms kan man integrera adaptiva formulär med AEM Forms i JEE-processer för bearbetning av formulärdata.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Konfigurera AEM Forms för att skicka formulärdata till en AEM Forms på JEE-process{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Anpassningsbara formulär har stöd för att skicka data till en AEM Forms på JEE-process för vidare bearbetning. Med den kan du aktivera en AEM Forms on JEE-process med data som är tillgängliga från det skickade formuläret. Utför följande steg för att göra det möjligt för din AEM Forms-instans att skicka ett anpassat formulär till AEM Forms i JEE-processen:

## Konfigurera AEM Forms-servern {#configure-your-aem-forms-server}

Utför följande steg för att göra det möjligt för din AEM-formulärserver att skicka data till en AEM Forms på JEE-server:

1. Gå till webbkonfigurationskonsolen för AEM på https://[*host*]:[*port*]/system/console/configMgr.

1. Leta upp och klicka på **Adobe LiveCycle Client SDK Configuration** -komponenten.
1. Klicka för att redigera konfigurationsserverns URL, användarnamn och lösenord för AEM Forms på JEE-servern.
1. Granska inställningarna och klicka på **Spara**.

![SDK-konfiguration för Adobe LiveCycle Client](assets/clientsdkconfiguration.jpg)

## Mappa data med processfält {#map-data-with-process-fields}

När dina AEM-formulär har konfigurerats mappar du data-XML och bilagor från det skickade formuläret till fälten i AEM Forms on JEE-processen. Så här gör du:

1. I webbkonfigurationskonsolen för AEM klickar du för att redigera LiveCycle **Process Locator- och Invoker** -konfigurationen för guiden.
1. Ange följande parametrar:

   * **Namn på XML-parametern** data (obligatoriskt): Ange XML-egenskapsfilen för den AEM Forms on JEE-process som ska bearbeta skickade data. The default value is **dataxml**.

   * **Namn på parametern** för bifogade filer (valfritt): Ange listan med dokumentobjekt som AEM Forms on JEE-processen behöver behandla. The default value is **fileAttachmentsList**.

1. Granska inställningarna och klicka på **Spara**.

![Guide LiveCycle Process Locator and Invoker](assets/test3.jpg)

När åtgärden Skicka till formulärarbetsflöde är konfigurerad listas de AEM Forms på JEE-serverprocesser som innehåller den angivna xml-parametern för data.
