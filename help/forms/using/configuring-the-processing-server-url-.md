---
title: Konfigurera AEM DS-inställningar
seo-title: Konfigurera AEM DS-inställningar
description: Du måste ange URL:en för bearbetningsservern innan du skickar ett formulär.
seo-description: Du måste ange URL:en för bearbetningsservern innan du skickar ett formulär.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Konfigurera AEM DS-inställningar{#configuring-aem-ds-settings}

I den här artikeln beskrivs hur du konfigurerar **AEM DS Settings Service**. Den här inställningen kan användas i flera scenarier, till exempel:

* I korrespondenshantering

   * För konfigurering av AEM Forms Workflow
   * När du använder formulärportalen för att spara utkast/inskickning på fjärrbasis

* I adaptiva formulär för fall när adaptiv form skickas från publiceringsinstansen

Så här konfigurerar du **[!UICONTROL AEM DS Settings]**:

1. Öppna Configuration Manager på publiceringsinstansen med URL:en:\
   *https://localhost:port/system/console/configMgr*.

   ![Konfiguration av AEM webbkonsol](assets/web_configuration_console_new.png)

1. I fönstret **[!UICONTROL Adobe Experience Manager Web Console Configuration]** letar du reda på och klickar på alternativet **[!UICONTROL AEM DS Settings]**.

   ![DS-inställningar](assets/ds_settings_new.png)

1. Fönstret **[!UICONTROL AEM DS Settings Service]** visar de vanliga konfigurationsinställningarna för AEM DS-komponenter.

   ![Tjänsten DS Settings](assets/ds_settings_service_new.png)

1. Lägg till följande information i respektive fält:

   **[!UICONTROL Processing Server URL]**: Bearbetningsservern är den server där Forms- eller AEM-arbetsflödet måste aktiveras. Detta kan vara samma som URL:en för den AEM författarinstansen eller den andra server-URL:en (d.v.s. https://localhost:port/).

   **[!UICONTROL Processing Server User Name]**: Användarnamn för arbetsflöde  [baserat på den server-URL som används]

   **[!UICONTROL Processing Server Password]**: Lösenord för arbetsflödesanvändare

   >[!NOTE]
   >
   >
   >    
   >    
   >    * När du använder arbetsflödena Forms eller AEM måste du konfigurera tjänsten DS-inställningar innan du skickar något från publiceringsservern. I annat fall ska inlämningen av formuläret misslyckas.



