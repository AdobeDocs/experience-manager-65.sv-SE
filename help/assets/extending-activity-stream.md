---
title: Integrera resurser med aktivitetsströmmen
description: Beskriver inspelningsfunktionerna i AEM och hur du konfigurerar AEM för att spela in specifika händelser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Integrera resurser med aktivitetsströmmen {#integrating-assets-with-activity-stream}

Adobe Experience Manager Assets-användare (AEM) utför många åtgärder, till exempel att skapa, överföra och ta bort resurser. Dessa åtgärder kan spelas in så att du kan ge en historik över vad en användare har gjort. I det här avsnittet beskrivs inspelningsfunktionerna i AEM och hur du konfigurerar AEM för att registrera specifika händelser.

## Prestandaöverväganden och standardbeteende {#performance-considerations-and-default-behavior}

Den här integreringen kan ta processorkraft och diskutrymme, t.ex. vid bulkimport. Därför är AEM Assets-integreringen med aktivitetsströmmen inaktiverad som standard.

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

## Konfigurera inspelning av AEM Assets-händelser {#configuring-aem-assets-events-recording}

Via [webbkonsolen](/help/sites-deploying/configuring-osgi.md) får du tillgång till AEM Assets Event Recorder-justeringen. Så här konfigurerar du händelseinspelaren för AEM Assets:

1. Navigera till **[!UICONTROL webbkonsolen]**

1. Klicka på **[!UICONTROL Konfiguration]**.

1. Dubbelklicka på **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Markera **[!UICONTROL Aktiverar den här tjänsten]**.

1. Kontrollera vilka **[!UICONTROL händelsetyper]** du vill spela in i användaraktivitetsströmmen.

1. Click **[!UICONTROL Save]**.

## Läs inspelade händelser {#reading-recorded-events}

De registrerade händelserna lagras som aktiviteter. Du kan läsa dem programmatiskt med [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
