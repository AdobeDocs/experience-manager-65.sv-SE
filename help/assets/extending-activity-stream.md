---
title: Integrera [!DNL Assets] med aktivitetsström
description: Beskriver inspelningsfunktionerna i [!DNL Experience Manager] och hur du konfigurerar det för att spela in specifika händelser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# Integrera [!DNL Assets] med aktivitetsströmmen {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] -användare utför många åtgärder som att skapa, överföra och ta bort resurser. Dessa åtgärder kan spelas in så att du kan ge en historik över vad en användare har gjort. I det här avsnittet beskrivs inspelningsfunktionerna i [!DNL Experience Manager] och hur du konfigurerar [!DNL Experience Manager] för att spela in specifika händelser.

## Prestandaöverväganden och standardbeteende {#performance-considerations-and-default-behavior}

Den här integreringen kan ta processorkraft och diskutrymme, t.ex. vid bulkimport. Därför är [!DNL Assets]-integreringen med aktivitetsströmmen inaktiverad som standard.

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

## Konfigurera [!DNL Assets]-händelseinspelning {#configuring-aem-assets-events-recording}

[Webbkonsolen](/help/sites-deploying/configuring-osgi.md) ger åtkomst till funktionen för att ställa in Assets Event Recorder. Så här konfigurerar du inspelningsfunktionen för Assets-händelser:

1. Navigera till **[!UICONTROL Web Console]**

1. Klicka på **[!UICONTROL Configuration]**.

1. Dubbelklicka på **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Kontroll **[!UICONTROL Enables this service]**.

1. Kontrollera vilken **[!UICONTROL Event Types]** du vill spela in i användaraktivitetsströmmen.

1. Klicka på **[!UICONTROL Save]**.

## Läs registrerade händelser {#reading-recorded-events}

De registrerade händelserna lagras som aktiviteter. Du kan läsa dem programmatiskt med [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
