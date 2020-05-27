---
title: Asynkrona åtgärder
description: Experience Manager Assets optimerar prestanda genom att utföra vissa resurskrävande uppgifter asynkront.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 2%

---


# Asynkrona åtgärder {#asynchronous-operations}

För att minska den negativa inverkan på prestandan bearbetar Adobe Experience Manager Assets vissa långvariga och resurskrävande resursoperationer asynkront.

Dessa åtgärder omfattar:

* Tar bort många resurser
* Flytta många resurser eller resurser med många referenser
* Exporterar/importerar resursmetadata i grupp.
* Hämtar resurser, som ligger över den angivna tröskelgränsen, från en fjärrdistribution av Experience Manager.

Asynkron bearbetning innebär att du måste placera flera jobb i kö och sedan köra dem på ett seriellt sätt beroende på om det finns systemresurser tillgängliga.

Du kan visa status för asynkrona jobb från **[!UICONTROL Async Job Status]** sidan.

>[!NOTE]
>
>Som standard körs jobb i Assets parallellt. Om N är antalet processorkärnor kan N/2-jobb köras parallellt som standard. Om du vill använda anpassade inställningar för jobbkön ändrar du **[!UICONTROL Async Operation Default Queue]** konfigurationen från webbkonsolen. Mer information finns i [Kökonfigurationer](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Övervaka status för asynkrona åtgärder {#monitoring-the-status-of-asynchronous-operations}

När Assets bearbetar en åtgärd asynkront får du ett meddelande i inkorgen och via e-post.

Om du vill visa status för asynkrona åtgärder i detalj går du till **[!UICONTROL Async Job Status]** sidan.

1. Klicka på **[!UICONTROL Operations]** > **[!UICONTROL Jobs]** i Experience Manager-gränssnittet.

1. Granska informationen om åtgärderna på **[!UICONTROL Async Job Status]** sidan.

   ![Status och information för asynkrona åtgärder](assets/AsyncOperation-status.png)

   Om du vill kontrollera förloppet för en viss åtgärd kan du se värdet i **[!UICONTROL Status]** kolumnen. Beroende på förloppet visas ett av följande statusvärden:

   * **[!UICONTROL Active]**: Åtgärden bearbetas

   * **[!UICONTROL Success]**: Åtgärden har slutförts

   * **[!UICONTROL Fail]** eller **[!UICONTROL Error]**: Det gick inte att bearbeta åtgärden

   * **[!UICONTROL Scheduled]**: Åtgärden är schemalagd för bearbetning vid ett senare tillfälle

1. Om du vill avbryta en aktiv åtgärd markerar du den i listan och klickar på **[!UICONTROL Stop]** i verktygsfältet.

   ![stop_icon](assets/stop_icon.png)

1. Om du vill visa extra information, till exempel beskrivning och loggar, väljer du åtgärden och klickar på **[!UICONTROL Open]** i verktygsfältet.

   ![open_icon](assets/open_icon.png)

   Sidan med jobbinformation visas.

   ![job_details](assets/job_details.png)

1. Om du vill ta bort åtgärden från listan väljer du **[!UICONTROL Delete]** den i verktygsfältet. Om du vill hämta information i en CSV-fil klickar du på **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Du kan inte ta bort ett jobb om dess status är aktiv eller köad.

## Töm slutförda jobb {#purging-completed-jobs}

Experience Manager Assets kör ett rensningsjobb varje dag klockan 1:00 för att ta bort slutförda asynkrona jobb som är mer än en dag gamla.

Du kan ändra schemat för rensningsjobbet och hur länge detaljer om slutförda jobb behålls innan de tas bort. Du kan också konfigurera det maximala antalet slutförda jobb för vilka information sparas när som helst.

1. I Experience Manager-gränssnittet klickar du **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Adobe CQ DAM Async Jobs Purge Scheduled]** jobbet.
1. Ange tröskelvärdet för antal dagar efter vilka slutförda jobb tas bort och det maximala antalet jobb för vilka information sparas i historiken.

   ![Konfiguration för att schemalägga rensning av asynkrona jobb](assets/configmgr_purge_asyncjobs.png)

1. Spara ändringarna.

## Konfigurera tröskelvärden för asynkron bearbetning {#configuring-thresholds-for-asynchronous-processing}

Du kan konfigurera tröskelvärdet för antal resurser eller referenser för Assets för att bearbeta en viss åtgärd asynkront.

### Konfigurera tröskelvärden för asynkrona borttagningsåtgärder {#configuring-thresholds-for-asynchronous-delete-operations}

Om antalet resurser eller mappar som ska tas bort överstiger tröskelvärdet, utförs borttagningsåtgärden asynkront.

1. I Experience Manager-gränssnittet klickar du **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Async Delete Operation Job Processing]** konfigurationen från webbkonsolen.
1. I **[!UICONTROL Threshold number of assets]** rutan anger du tröskelvärdet för antal resurser/mappar för asynkron bearbetning av borttagningsåtgärder.

   ![delete_threshold](assets/delete_threshold.png)

1. Spara ändringarna.

### Konfigurera tröskelvärden för asynkrona flyttåtgärder {#configuring-thresholds-for-asynchronous-move-operations}

Om antalet resurser/mappar eller referenser som ska flyttas överstiger tröskelvärdet, utförs flyttåtgärden asynkront.

1. I Experience Manager-gränssnittet klickar du **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Async Move Operation Job Processing]** konfigurationen från webbkonsolen.
1. I **[!UICONTROL Threshold number of assets/references]** rutan anger du tröskelvärdet för antal resurser/mappar eller referenser för asynkron bearbetning av flyttningsåtgärder.

   ![move_threshold](assets/move_threshold.png)

1. Spara ändringarna.
