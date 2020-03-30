---
title: Konfigurerar Connector för Microsoft SharePoint
seo-title: Konfigurerar Connector för Microsoft SharePoint
description: Konfigurera Connector för Microsoft SharePoint för att aktivera kommunikation mellan AEM-formulär och Microsoft SharePoint.
seo-description: Konfigurera Connector för Microsoft SharePoint för att aktivera kommunikation mellan AEM-formulär och Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Konfigurerar Connector för Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Koppling för Microsoft SharePoint möjliggör kommunikation mellan AEM-formulär och Microsoft SharePoint. Mer bakgrundsinformation finns i&quot;Connectors for ECM&quot; i [Services Reference](https://www.adobe.com/go/learn_aemforms_services_63).

1. I administrationskonsolen klickar du på Tjänster > Koppling för Microsoft SharePoint.
1. Ange följande inställningar för SharePoint-servern:

   **Värdnamn för SharePoint-server:** Webbprogrammets värdnamnsportnummer på SharePoint-servern i formatet `[hostname]:'port'`.

   **Användarnamn:** Användarkontot som används för att ansluta till SharePoint-servern.

   **Lösenord:** Lösenord för användarkontot som används för att ansluta till SharePoint-servern

   **Domännamn:** Domän där SharePoint-servern finns.

1. Klicka på Spara.

## Konfigurationstjänst för Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Med konfigurationstjänsten för Microsoft SharePoint `(MSSharePointConfigService)` kan du ange autentiseringsuppgifter för den AEM-formuläranvändare som har personifieringsbehörigheter. Mer information om personifieringsbehörigheter finns i [Konfigurera Connector för Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Följ de här stegen för att ange inställningar för `MSSharePointConfigService`:

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Navigera i listan med tjänster och klicka på `MSSharePointConfigService`.
1. Ange följande inställningar på konfigurationssidan:

   * Användarnamn för en användare med personifieringsbehörigheter
   * Lösenord för ovanstående användare

1. Klicka på Spara.

