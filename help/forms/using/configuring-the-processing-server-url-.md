---
title: Konfigurerar AEM DS-inställningar
seo-title: Konfigurerar AEM DS-inställningar
description: Du måste ange URL:en för bearbetningsservern innan du skickar ett formulär.
seo-description: Du måste ange URL:en för bearbetningsservern innan du skickar ett formulär.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Konfigurerar AEM DS-inställningar{#configuring-aem-ds-settings}

I den här artikeln beskrivs hur du konfigurerar **AEM DS-inställningstjänsten**. Den här inställningen kan användas i flera scenarier, till exempel:

* I korrespondenshantering

   * För konfigurering av AEM Forms Workflow
   * När du använder formulärportalen för att spara utkast/inskickning på fjärrbasis

* I adaptiva formulär för fall när adaptiv form skickas från publiceringsinstansen

Så här konfigurerar du **[!UICONTROL AEM DS-inställningarna]**:

1. Öppna Configuration Manager på publiceringsinstansen med URL:en:\
   *https://localhost:port/system/console/configMgr*.

   ![Konfiguration av AEM Web Console](assets/web_configuration_console_new.png)

1. I fönstret Konfiguration **[!UICONTROL av]** Adobe Experience Manager Web Console letar du upp och klickar på alternativet **[!UICONTROL AEM DS-inställningar]** .

   ![DS-inställningar](assets/ds_settings_new.png)

1. I fönstret **[!UICONTROL AEM DS Settings Service]** visas de vanliga konfigurationsinställningarna för AEM DS Components.

   ![Tjänsten DS Settings](assets/ds_settings_service_new.png)

1. Lägg till följande information i respektive fält:

   **[!UICONTROL Bearbetar server-URL]**: Bearbetningsservern är den server där Forms- eller AEM-arbetsflödet måste aktiveras. Detta kan vara samma som URL:en för AEM-författarinstansen eller den andra server-URL:en (d.v.s. https://localhost:port/).

   **[!UICONTROL Användarnamn]** för bearbetningsserver: Användarnamn för arbetsflöde [baserat på den server-URL som används]

   **[!UICONTROL Lösenord]** för bearbetningsserver: Lösenord för arbetsflödesanvändare

   >[!NOTE]
   >
   >
   >    
   >    
   >    * När du använder antingen Forms- eller AEM-arbetsflöden måste du konfigurera tjänsten DS-inställningar innan du skickar något från publiceringsservern. I annat fall ska inlämningen av formuläret misslyckas.


