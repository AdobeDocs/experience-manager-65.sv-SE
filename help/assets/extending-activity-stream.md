---
title: Integrera [!DNL Assets] med aktivitetsström
description: Beskriver inspelningsfunktionerna i [!DNL Experience Manager] och hur du konfigurerar det för att registrera specifika händelser.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Integrera [!DNL Assets] med aktivitetsström {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] -användare utför många åtgärder som att skapa, överföra och ta bort resurser. Dessa åtgärder kan spelas in så att du kan ge en historik över vad en användare har gjort. I det här avsnittet beskrivs inspelningsfunktionerna i [!DNL Experience Manager] och konfigurera [!DNL Experience Manager] för att registrera specifika händelser.

## Prestandaöverväganden och standardbeteende {#performance-considerations-and-default-behavior}

Den här integreringen kan ta processorkraft och diskutrymme, t.ex. vid bulkimport. Av dessa anledningar [!DNL Assets] integrering med aktivitetsströmmen är inaktiverad som standard.

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

## Konfigurera [!DNL Assets] inspelning av händelser {#configuring-aem-assets-events-recording}

The [Webbkonsol](/help/sites-deploying/configuring-osgi.md) ger åtkomst till justering av händelseinspelning för resurser. Så här konfigurerar du inspelningsfunktionen för Assets-händelser:

1. Navigera till **[!UICONTROL Web Console]**

1. Klicka på **[!UICONTROL Configuration]**.

1. Dubbelklicka **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Kontrollera **[!UICONTROL Enables this service]**.

1. Kontrollera vilken **[!UICONTROL Event Types]** du vill spelas in i användaraktivitetsströmmen.

1. Klicka på **[!UICONTROL Save]**.

## Läs inspelade händelser {#reading-recorded-events}

De registrerade händelserna lagras som aktiviteter. Du kan läsa dem programmatiskt med [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
