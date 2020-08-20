---
title: Konfigurera cacheminne för adaptiva formulär
seo-title: Konfigurera cacheminne för adaptiva formulär
description: 'Cacheminnet för anpassningsbara formulär är särskilt utformat för anpassningsbara formulär och dokument. Den cache-lagrar adaptiva formulär och adaptiva dokument i syfte att minska den tid som krävs för att återge ett adaptivt formulär eller dokument på klienten. '
seo-description: 'Cacheminnet för anpassningsbara formulär är särskilt utformat för anpassningsbara formulär och dokument. Den cache-lagrar adaptiva formulär och adaptiva dokument i syfte att minska den tid som krävs för att återge ett adaptivt formulär eller dokument på klienten. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---


# Konfigurera cacheminne för adaptiva formulär {#configure-adaptive-forms-cache}

Ett cacheminne är en mekanism som förkortar dataåtkomsttider, minskar latensen och förbättrar I/O-hastigheter (input/output). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-strukturen i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär eller dokument på klienten. Den är särskilt utformad för adaptiva formulär och stöder även adaptiva dokument.

>[!NOTE]
>
>När du använder cacheminnet för adaptiva formulär använder du AEM [!DNL Dispatcher] för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär eller dokument.

>[!NOTE]
>
>När du utvecklar anpassade komponenter på servern som används för utveckling ska du inaktivera cachen för anpassade formulär.

## Konfigurera cacheminnet {#configure-the-cache}

Utför följande steg för att konfigurera cachen för adaptiva formulär:

1. Gå till konfigurationshanteraren AEM webbkonsolen på https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Klicka **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** för att redigera dess konfigurationsvärden.
1. I [!UICONTROL edit configuration values] dialogrutan anger du det maximala antalet formulär eller dokument som en instans av den AEM [!DNL Forms] servern kan cachelagra i **[!UICONTROL Number of Adaptive Forms]** fältet. Standardvärdet är 100.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet **0** i fältet Antal adaptiva Forms. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

   ![Konfigurationsdialogruta för HTML-cache för adaptiva formulär](assets/cache-configuration-edit.png)

1. Klicka **[!UICONTROL Save]** för att spara konfigurationen.
