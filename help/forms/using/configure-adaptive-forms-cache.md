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
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Konfigurera cacheminne för adaptiva formulär{#configure-adaptive-forms-cache}

Ett cacheminne är en mekanism som förkortar dataåtkomsttider, minskar latensen och förbättrar I/O-hastigheter (input/output). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-strukturen i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär eller dokument på klienten. Den är särskilt utformad för adaptiva formulär och stöder även adaptiva dokument.

>[!NOTE]
>
>När du använder cacheminnet för adaptiva formulär använder du AEM Dispatcher för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär eller dokument.

>[!NOTE]
>
>När du utvecklar anpassade komponenter på servern som används för utveckling ska du inaktivera cachen för anpassade formulär.

## Konfigurera cacheminnet {#configure-the-cache}

Utför följande steg för att konfigurera cachen för adaptiva formulär:

1. Gå till konfigurationshanteraren för AEM-webbkonsolen på https://[server]:[port]/system/console/configMgr.
1. Klicka på **Adaptiv form och Interactive Communication Web Channel Configuration** för att redigera dess konfigurationsvärden.
1. I dialogrutan Redigera konfigurationsvärden anger du det maximala antalet formulär eller dokument som en instans av AEM Forms-servern kan cachelagra i fältet **Antal adaptiva formulär** . Standardvärdet är 100.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet **0** i fältet Antal adaptiva formulär. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

   ![Konfigurationsdialogruta för HTML-cache för adaptiva formulär](assets/cache-configuration-edit.png)

1. Klicka på **Spara** för att spara konfigurationen.

