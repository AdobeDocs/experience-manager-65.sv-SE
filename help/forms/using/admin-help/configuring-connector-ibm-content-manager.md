---
title: Konfigurera Connector för IBM Content Manager
seo-title: Konfigurera Connector för IBM Content Manager
description: Konfigurera Connector for IBM Content Manager för att möjliggöra kommunikation mellan AEM-formulär och IBM Content Manager.
seo-description: Konfigurera Connector for IBM Content Manager för att möjliggöra kommunikation mellan AEM-formulär och IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera Connector för IBM Content Manager{#configuring-connector-for-ibm-content-manager}

Koppling för IBM Content Manager möjliggör kommunikation mellan AEM-formulär och IBM Content Manager. Mer bakgrundsinformation finns i&quot;Connectors for ECM&quot; i [Services Reference](https://www.adobe.com/go/learn_aemforms_services_63).

## Konfigurera IBM Content Manager-anslutningen {#configure-the-ibm-content-manager-connection}

1. I administrationskonsolen klickar du på Tjänster > Koppling för IBM Content Manager.
1. Ange namnet på IBM Content Manager-datalagret som du vill ansluta till i rutan Datastornamn. Om databasen är lokal anger du databasens namn. Om databasen är fjärransluten anger du dess aliasnamn.
1. I rutan Användarnamn anger du användar-ID för en användare som ska ansluta till IBM Content Manager-datalagret.
1. Ange användarens lösenord i rutan Lösenord.
1. (Valfritt) I rutan Aliasanslutningssträng anger du ytterligare anslutningsargument. I de flesta fall ska den här rutan vara tom. Mer information finns i dokumentationen för IBM.
1. Klicka på Spara.

## Validering av tjänstinställningar {#validation-of-service-settings}

Om du anger fel alias, användarnamn eller lösenord för dataStore får du följande resultat beroende på om tjänsten Content Repository Connector för IBM Content Manager körs för närvarande:

* Om tjänsten stoppas visas inget fel när du sparar tjänstkonfigurationsinformationen. Nästa gång du startar tjänsten inträffar dock ett undantag och tjänsten kommer inte att starta.
* Om tjänsten startas försöker tjänsten att validera inloggningsinformationen omedelbart när du sparar tjänstkonfigurationsinformationen. I det här fallet inträffar ett fel och konfigurationsinformationen sparas inte.

