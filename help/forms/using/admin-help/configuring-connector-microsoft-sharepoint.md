---
title: Configuring Connector for Microsoft SharePoint
description: Konfigurera Connector for Microsoft SharePoint för att möjliggöra kommunikation mellan AEM och Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Configuring Connector for Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Koppling för Microsoft SharePoint möjliggör kommunikation mellan AEM och Microsoft SharePoint. Mer bakgrundsinformation finns i &quot;Connectors for ECM&quot; i [Tjänstreferens](https://www.adobe.com/go/learn_aemforms_services_63).

1. I administrationskonsolen klickar du på Tjänster > Koppling för Microsoft SharePoint.
1. Ange följande inställningar för din SharePoint-server:

   **Värdnamn för SharePoint-server:** Webbprogrammets värdnamnsportnummer på SharePoint-servern, i formatet `[hostname]:'port'`.

   **Användarnamn:** Användarkontot som används för att ansluta till SharePoint-servern.

   **Lösenord:** Lösenord för användarkontot som används för att ansluta till SharePoint-servern

   **Domännamn:** Domän där SharePoint-servern finns.

1. Klicka på Spara.

## Konfigurationstjänst för Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Konfigurationstjänsten för Microsoft SharePoint `(MSSharePointConfigService)` I kan du ange autentiseringsuppgifter för den användare av AEM formulär som har personifieringsbehörigheter. Mer information om personifieringsbehörigheter finns i [Configuring Connector for Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Följ de här stegen för att ange inställningar för `MSSharePointConfigService`:

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Navigera i listan över tjänster och klicka på `MSSharePointConfigService`.
1. Ange följande inställningar på konfigurationssidan:

   * Användarnamn för en användare med personifieringsbehörigheter
   * Lösenord för ovanstående användare

1. Klicka på Spara.
