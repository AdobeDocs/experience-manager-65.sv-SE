---
title: Integrera [!DNL Assets] med aktivitetsströmmen.
description: Beskriver inspelningsfunktionerna [!DNL Experience Manager] och hur du konfigurerar dem för att spela in specifika händelser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# Integrera [!DNL Assets] med aktivitetsströmmen {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] -användare utför många åtgärder som att skapa, överföra och ta bort resurser. Dessa åtgärder kan spelas in så att du kan ge en historik över vad en användare har gjort. I det här avsnittet beskrivs inspelningsfunktionerna för [!DNL Experience Manager] och hur du konfigurerar [!DNL Experience Manager] för att spela in specifika händelser.

## Prestandaöverväganden och standardbeteende {#performance-considerations-and-default-behavior}

Den här integreringen kan ta processorkraft och diskutrymme, t.ex. vid bulkimport. Av dessa skäl är [!DNL Assets] integreringen med aktivitetsströmmen inaktiverad som standard.

## Åtgärdshändelser som stöds {#supported-action-events}

Följande händelser kan konfigureras för inspelning:

* Licensen har godkänts (ACCEPTED)
* Skapad resurs (ASSET_CREATED)
* Resurs flyttad (ASSET_MOVED)
* Resursen har tagits bort (ASSET_REMOVED)
* Licensen avvisades (avvisades)
* Hämtade resurser (HÄMTADE)
* Resursversion (VERSIONED)
* Resursversionen har återställts (RESTORED)
* Metadata för resurs har uppdaterats (METADATA_UPDATED)
* Tillgång publicerad till externt system (PUBLISHED_EXTERNAL)
* Resursens ursprungliga uppdaterade (ORIGINAL_UPDATED)
* Resursåtergivning uppdaterad (RENDITION_UPDATED)
* Resursåtergivning borttagen (RENDITION_REMOVED)
* Undertillgången har uppdaterats (SUBASSET_UPDATED)
* Deltillgång borttagen (SUBASSET_REMOVED)

## Konfigurera inspelning av [!DNL Assets] händelser {#configuring-aem-assets-events-recording}

Via [webbkonsolen](/help/sites-deploying/configuring-osgi.md) får du tillgång till inställningarna för händelseredigering av resurser. Så här konfigurerar du inspelningsfunktionen för Assets-händelser:

1. Navigate to the **[!UICONTROL Web Console]**

1. Klicka på **[!UICONTROL Configuration]**.

1. Dubbelklicka **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Kontroll **[!UICONTROL Enables this service]**.

1. Kontrollera vilka **[!UICONTROL Event Types]** du vill spela in i användaraktivitetsströmmen.

1. Klicka på **[!UICONTROL Save]**.

## Läs inspelade händelser {#reading-recorded-events}

De registrerade händelserna lagras som aktiviteter. Du kan läsa dem programmatiskt med [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
