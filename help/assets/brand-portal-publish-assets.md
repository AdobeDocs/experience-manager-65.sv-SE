---
title: Publicera resurser på varumärkesportalen
seo-title: Publish assets to Brand Portal
description: Lär dig hur du publicerar och avpublicerar resurser på Brand Portal.
seo-description: Learn how to publish and unpublish assets to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 42%

---

# Publicera resurser på varumärkesportalen {#publish-assets-to-brand-portal}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/brandportal/brand-portal-publish-assets.html?lang=en) |

Som Adobe Experience Manager (AEM) Assets-administratör kan du publicera resurser och mappar i AEM Assets Brand Portal-instansen (eller schemalägga publiceringsarbetsflödet till ett senare datum/tid) för din organisation. Du måste dock först konfigurera AEM Assets med varumärkesportalen. Mer information finns i [Konfigurera AEM Assets med varumärkesportalen](/help/assets/configure-aem-assets-with-brand-portal.md).

När replikeringen är klar kan du publicera resurser, mappar och samlingar till Brand Portal. Så här publicerar du resurser på Brand Portal:

>[!NOTE]
>
>Adobe rekommenderar stegvis publicering, helst vid tidpunkter med låg belastning, för att AEM-författaren inte ska uppta för mycket resurser.

1. I resurskonsolen markerar du de resurser/mappar som du vill publicera och klickar på **[!UICONTROL Quick Publish]** i verktygsfältet.

   Du kan också välja de mediefiler du vill publicera till Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Följande två alternativ är tillgängliga när du vill publicera mediefiler till Brand Portal:
   * [Publicera resurser direkt](#publish-to-bp-now)
   * [Publicera resurser senare](#publish-to-bp-now)

## Publicera resurser nu {#publish-to-bp-now}

Gör något av följande för att publicera de markerade resurserna på varumärkesportalen:

* Välj **[!UICONTROL Quick Publish]** i verktygsfältet. Välj sedan **[!UICONTROL Publish to Brand Portal]**.

* Välj **[!UICONTROL Manage Publication]** i verktygsfältet.

   1. Från **[!UICONTROL Action]** välj **[!UICONTROL Publish to Brand Portal]** och från **[!UICONTROL Scheduling]** välj **[!UICONTROL Now]**. Klicka på **[!UICONTROL Next]**.

   2. Inom **[!UICONTROL Scope]**, bekräfta ditt val och klicka på **[!UICONTROL Publish to Brand Portal]**.

Ett meddelande visas som anger att resurserna har placerats i kö för publicering på varumärkesportalen. Logga in på gränssnittet för varumärkesportalen för att visa de publicerade resurserna.

## Publicera resurser senare {#publish-to-bp-later}

Gör så här för att schemalägga publicering av resurser på varumärkesportalen till ett senare datum eller en senare tid:

1. När du har valt resurser/mappar att publicera väljer du **[!UICONTROL Manage Publication]** i verktygsfältet högst upp.

1. På **[!UICONTROL Manage Publication]** sida, markera **[!UICONTROL Publish to Brand Portal]** från **[!UICONTROL Action]** och markera **[!UICONTROL Later]** från **[!UICONTROL Scheduling]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Markera en **[!UICONTROL Activation date]** och ange en tid. Klicka på **[!UICONTROL Next]**.

1. Välj ett **aktiveringsdatum** och ange en tid. Klicka på **Nästa**.

1. Ange en **[!UICONTROL Workflow title]** i **[!UICONTROL Workflows]**. Klicka på **[!UICONTROL Publish Later]**.

   ![publishworkflow](assets/publishworkflow.png)

Logga sedan in på Brand Portal för att se om de publicerade resurserna finns tillgängliga i Brand Portal gränssnitt.

![bp_landingpage](assets/bp_landingpage.png)
