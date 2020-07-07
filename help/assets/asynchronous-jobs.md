---
title: Konfigurera asynkrona åtgärder i [!DNL Adobe Experience Manager].
description: Slutför asynkront vissa resurskrävande åtgärder för att optimera prestandan i [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---


# Asynkrona åtgärder {#asynchronous-operations}

För att minska den negativa inverkan på prestanda behandlar [!DNL Adobe Experience Manger Assets] vissa långvariga och resurskrävande resursoperationer asynkront. Asynkron bearbetning innebär att du måste placera flera uppgifter i kö och sedan utföra dem på ett seriellt sätt beroende på om det finns systemresurser tillgängliga. Dessa åtgärder omfattar:

* Tar bort många resurser.
* Flytta många resurser eller resurser med många referenser.
* Exportera och importera resursmetadata i grupp.
* Hämtar resurser från en fjärrdistribution [!DNL Experience Manager] som är mer än en angiven tröskelgräns. Gränsen är för antalet tillgångar.

Du kan visa status för asynkrona uppgifter från **[!UICONTROL Async Job Status]** sidan.

>[!NOTE]
>
>Som standard körs åtgärderna [!DNL Assets] parallellt. Om `N` är antalet processorkärnor kan `N/2` uppgifter köras parallellt som standard. Om du vill använda anpassade inställningar för uppgiftskön ändrar du **[!UICONTROL Async Operation Default Queue]** konfigurationen från [!UICONTROL Web Console]. Mer information finns i [Kökonfigurationer](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Övervaka status för asynkrona åtgärder {#monitoring-the-status-of-asynchronous-operations}

När [!DNL Assets] en åtgärd bearbetas asynkront får du ett meddelande i din [!DNL Experience Manager] Inkorg [](/help/sites-authoring/inbox.md) och via ett e-postmeddelande. Om du vill visa status för asynkrona åtgärder i detalj går du till **[!UICONTROL Async Job Status]** sidan.

1. In the [!DNL Experience Manager] interface click **[!UICONTROL Operations]** > **[!UICONTROL Jobs]**.

1. Granska informationen om åtgärderna på **[!UICONTROL Async Job Status]** sidan.

   ![Status och information för asynkrona åtgärder](assets/AsyncOperation-status.png)

   Information om förloppet för en åtgärd finns i **[!UICONTROL Status]** kolumnen. Beroende på förloppet visas ett av följande statusvärden:

   * **[!UICONTROL Active]**: Åtgärden bearbetas.
   * **[!UICONTROL Success]**: Åtgärden har slutförts.
   * **[!UICONTROL Fail]** eller **[!UICONTROL Error]**: Det gick inte att bearbeta åtgärden.
   * **[!UICONTROL Scheduled]**: Åtgärden är schemalagd för bearbetning vid ett senare tillfälle.

1. Om du vill avbryta en aktiv åtgärd markerar du den i listan och klickar på **[!UICONTROL Stop]** stoppikonen ![](assets/do-not-localize/stop_icon.svg) i verktygsfältet.

1. Om du vill visa extra information, till exempel beskrivning och loggar, markerar du åtgärden och klickar på **[!UICONTROL Open]** open_icon ![](assets/do-not-localize/edit_icon.svg) i verktygsfältet. Sidan med aktivitetsinformation visas.

   ![Information om en metadataimportaktivitet](assets/job_details.png)

1. Om du vill ta bort åtgärden från listan väljer du **[!UICONTROL Delete]** den i verktygsfältet. Om du vill hämta information i en CSV-fil klickar du på **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Du kan inte ta bort en uppgift om dess status är aktiv eller köad.

## Töm slutförda uppgifter {#purge-completed-tasks}

[!DNL Experience Manager Assets] kör en rensningsåtgärd varje dag i 010 timmar för att ta bort slutförda asynkrona uppgifter som är mer än en dag gamla.

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

Du kan ändra schemat för rensningsaktiviteten och hur länge information om slutförda uppgifter sparas innan de tas bort. Du kan också konfigurera det maximala antalet slutförda uppgifter för vilka information sparas när som helst.

1. In the [!DNL Experience Manager] interface click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Adobe CQ DAM Async Jobs Purge Scheduled]** uppgiften.
1. Ange tröskelvärdet för antal dagar efter vilka slutförda uppgifter tas bort och det högsta antalet uppgifter som detaljerna sparas för i historiken. Spara ändringarna.

   ![Konfiguration som schemalägger rensning av asynkrona uppgifter](assets/configmgr_purge_asyncjobs.png)

## Konfigurera tröskelvärde för asynkrona borttagningsåtgärder {#configure-thresholds-for-asynchronous-delete-operations}

Om antalet resurser eller mappar som ska tas bort överstiger det angivna tröskelvärdet, utförs borttagningsåtgärden asynkront.

1. In the [!DNL Experience Manager] interface click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna [!UICONTROL Web Console]konfigurationen från **[!UICONTROL Async Delete Operation Job Processing]** .
1. I **[!UICONTROL Threshold number of assets]** rutan anger du tröskelvärden för att ta bort resurser, mappar eller referenser asynkront. Spara ändringarna.

   ![Ange tröskelgräns för när resurser ska tas bort för aktiviteten](assets/delete_threshold.png)

## Konfigurera tröskelvärde för asynkrona flyttåtgärder {#configure-thresholds-for-asynchronous-move-operations}

Om antalet resurser, mappar eller referenser som ska flyttas överstiger det angivna tröskelvärdet, utförs flyttåtgärden asynkront.

1. In the [!DNL Experience Manager] interface, click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna [!UICONTROL Web Console]konfigurationen från **[!UICONTROL Async Move Operation Job Processing]** .
1. I **[!UICONTROL Threshold number of assets/references]** rutan anger du tröskelvärden för att flytta resurser, mappar eller referenser asynkront. Spara ändringarna.

   ![Ange tröskelgräns för när resurser ska flyttas för aktiviteten](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Konfigurera e-post i Experience Manager](/help/sites-administering/notification.md).
>* [Importera och exportera resursmetadata gruppvis](/help/assets/metadata-import-export.md).
>* [Använd anslutna resurser för att dela DAM-resurser från fjärrdistributioner](/help/assets/use-assets-across-connected-assets-instances.md).

