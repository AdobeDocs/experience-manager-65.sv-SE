---
title: Konfigurera koppling för IBM&reg; Content Manager
description: Konfigurera anslutningsprogrammet för IBM&reg; Content Manager för att aktivera kommunikation mellan AEM och IBM&reg; Content Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Konfigurera Connector för IBM® Content Manager{#configuring-connector-for-ibm-content-manager}

Koppling för IBM® Content Manager möjliggör kommunikation mellan AEM och IBM® Content Manager. Mer bakgrundsinformation finns i &quot;Connectors for ECM&quot; i [Services Reference](https://www.adobe.com/go/learn_aemforms_services_63).

## Konfigurera IBM® Content Manager-anslutningen {#configure-the-ibm-content-manager-connection}

1. I administrationskonsolen klickar du på Tjänster > Koppling för IBM® Content Manager.
1. Ange namnet på datalagret för IBM® Content Manager som du vill ansluta till i rutan Datastornamn. Om databasen är lokal anger du databasens namn. Om databasen är fjärransluten anger du dess aliasnamn.
1. I rutan Användarnamn anger du användar-ID för en användare som ska ansluta till datalagret för IBM® Content Manager.
1. Ange användarens lösenord i rutan Lösenord.
1. (Valfritt) I rutan Aliasanslutningssträng anger du ytterligare anslutningsargument. Vanligtvis ska den här rutan vara tom. Mer information finns i dokumentationen för IBM®.
1. Klicka på Spara.

## Validering av tjänstinställningar {#validation-of-service-settings}

Om du anger fel alias, användarnamn eller lösenord för dataStore får du följande resultat, beroende på om tjänsten Content Repository Connector för IBM® Content Manager körs:

* Om tjänsten stoppas visas inget fel när du sparar tjänstkonfigurationsinformationen. Nästa gång du startar tjänsten genereras dock ett undantag och tjänsten startar inte.
* Om tjänsten startas försöker tjänsten att validera inloggningsinformationen omedelbart när du sparar tjänstkonfigurationsinformationen. I det här fallet inträffar ett fel och konfigurationsinformationen sparas inte.
