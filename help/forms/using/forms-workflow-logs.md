---
title: Logga in i arbetsflöden för AEM Forms
seo-title: Logga in i arbetsflöden för AEM Forms
description: Använd loggar för att felsöka arbetsflödesproblem i AEM Forms.
seo-description: Använd loggar för att felsöka arbetsflödesproblem i AEM Forms.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Logga in i arbetsflöden för AEM Forms{#logging-in-aem-forms-workflows}

I formulärarbetsflödesstegen finns detaljerade loggar som du kan använda för att felsöka arbetsflödesrelaterade problem. Aktivera felsökningsloggning för arbetsflöden i AEM Forms för att visa loggarna.

Som standard är all loggningsinformation tillgänglig i filen **error.log** i katalogen */crx-database/logs/* .

Felsökningsloggarna för formulärarbetsflöden innehåller:

* Inmatning av varje arbetsflödessteg. Exempel:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Avsluta varje arbetsflödessteg. Exempel:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Meddelanden om serviceanrop. Exempel:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Meddelanden om tjänstavslutning. Exempel:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variabler som läses från metadatamappningen. Exempel:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variabler skrivna i JCR-databasen. Exempel:

   ```
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Undantagsmeddelanden med fullständig stackspårning. Exempel:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Metadataparametrar för dynamiskt steg. Exempel:

   ```
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

I följande exempel visas loggarna för steget Signera dokument:

```xml
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Använd loggarna för att utvärdera att:

* Du använder en korrekt konfiguration för Adobe Sign.
* Adobe Sign-tjänsten avslutas när ett avtal har skapats.
* Signera dokument-steget avslutas med ett meddelande om att åtgärden lyckades.

Om det finns ett undantag kan du visa hela stackspårningen för att utvärdera orsaken till felet.

## Aktivera felsökningsloggning för arbetsflöden i AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Utför följande steg för att aktivera felsökningsloggning för arbetsflöden i AEM Forms:

1. Gå till konfigurationshanteraren för AEM-webbkonsolen på:

   https://[server]:[port]/system/console/configMgr

1. Välj **[!UICONTROL Sling]** > **[!UICONTROL Loggstöd]**.
1. Tryck på **[!UICONTROL Lägg till ny loggare.]**
1. Välj **[!UICONTROL Felsök]** som **[!UICONTROL loggnivå]**.
1. Ange platsen för loggfilen. Standardplatsen för loggfilen är: *loggar\error.log*
1. Ange paketets namn som **com.adobe.granite.workflow.core** i kolumnen **[!UICONTROL Logger]** .

   Om du utför dessa steg kan du lagra felsökningsloggarna för paketet **com.adobe.granite.workflow.core** . Tryck **[!UICONTROL +]** och lägg till följande paketnamn i listan:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

