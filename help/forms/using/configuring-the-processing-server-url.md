---
title: Konfigurera AEM DS-inställningar
description: Lär dig hur du anger bearbetningsserverns URL innan du skickar ett formulär.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Konfigurera AEM DS-inställningar{#configuring-aem-ds-settings}

I den här artikeln beskrivs hur du konfigurerar tjänsten **AEM DS-inställningar**. Den här inställningen kan användas i flera scenarier, till exempel:

* I korrespondenshantering

   * För konfigurering av AEM Forms Workflow
   * När du använder Forms Portal för att spara utkast/inskickning på fjärrbasis

* I adaptiva formulär, till exempel när ett adaptivt formulär skickas från en publiceringsinstans

Så här konfigurerar du **[!UICONTROL AEM DS Settings]**:

1. Öppna Configuration Manager på publiceringsinstansen med URL:en:\
   *https://localhost:port/system/console/configMgr*.

   ![AEM Konfiguration av webbkonsol](assets/web_configuration_console_new.png)

1. Leta reda på och klicka på alternativet **[!UICONTROL AEM DS Settings]** i fönstret **[!UICONTROL Adobe Experience Manager Web Console Configuration]**.

   ![DS-inställningar](assets/ds_settings_new.png)

1. Fönstret **[!UICONTROL AEM DS Settings Service]** visar de vanliga konfigurationsinställningarna för AEM DS-komponenter.

   ![DS-inställningstjänst](assets/ds_settings_service_new.png)

1. Lägg till följande information i respektive fält:

   **[!UICONTROL Processing Server URL]**: Bearbetningsservern är den server där Forms- eller AEM-arbetsflödet måste aktiveras. Detta kan vara samma URL som till den AEM författarinstansen eller den andra server-URL:en (d.v.s. https://localhost:port/).

   **[!UICONTROL Processing Server User Name]**: Arbetsflödesanvändarens användarnamn [baserat på den server-URL som används]

   **[!UICONTROL Processing Server Password]**: Lösenord för arbetsflödesanvändare

   >[!NOTE]
   >
   >
   >    
   >    
   >    * När du använder arbetsflödena Forms eller AEM måste du konfigurera tjänsten DS-inställningar innan du skickar något från publiceringsservern. I annat fall ska inlämningen av blanketten misslyckas.
   >    
   >
