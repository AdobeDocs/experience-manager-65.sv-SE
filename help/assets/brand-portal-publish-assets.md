---
title: Publicera resurser på varumärkesportalen
seo-title: Publicera resurser på varumärkesportalen
description: Lär dig hur du publicerar och avpublicerar resurser på varumärkesportalen.
seo-description: Lär dig hur du publicerar och avpublicerar resurser på varumärkesportalen.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 4c00385984a0ac315a60c768cb517832ab4289b4

---


# Publicera resurser på varumärkesportalen {#publish-assets-to-brand-portal}

Som administratör för Adobe Experience Manager-resurser (AEM) kan du publicera resurser och mappar i instansen av AEM Assets Brand Portal (eller schemalägga publiceringsarbetsflödet till ett senare datum/tid) för organisationen. Du måste dock först konfigurera AEM Assets med Brand Portal. Mer information finns i [Konfigurera AEM-resurser med varumärkesportalen](/help/assets/configure-aem-assets-with-brand-portal.md).

När replikeringen är klar kan du publicera resurser, mappar och samlingar på varumärkesportalen. Så här publicerar du resurser på varumärkesportalen:

>[!NOTE]
>
>Adobe rekommenderar att publiceringen staggats, helst under icke-topp-timmar, så att AEM-författaren inte tar upp för mycket resurser.

1. I resurskonsolen markerar du de resurser/mappar som du vill publicera och klickar på **[!UICONTROL Snabbpublicering]** i verktygsfältet.

   Du kan också välja de resurser du vill publicera på varumärkesportalen.

   ![publish2bp-2](assets/publish2bp.png)

1. Det finns två tillgängliga alternativ för att publicera resurserna på varumärkesportalen:
   * [Publicera resurser direkt](#publish-to-bp-now)
   * [Publicera resurser senare](#publish-to-bp-now)

## Publicera resurser nu {#publish-to-bp-now}

Gör något av följande om du vill publicera de markerade resurserna på varumärkesportalen:

* Välj **[!UICONTROL Snabbpublicering]** i verktygsfältet. Välj sedan **[!UICONTROL Publicera på varumärkesportalen]** på menyn.

* Välj **[!UICONTROL Hantera publikation]** i verktygsfältet.

   1. Välj sedan **[!UICONTROL Publicera på varumärkesportal]** i **[!UICONTROL Åtgärd]** och välj **[!UICONTROL Now]** i **[!UICONTROL Scheduling]**. Click **[!UICONTROL Next]**.

   2. Bekräfta ditt val inom **[!UICONTROL Omfattning]** och klicka på **[!UICONTROL Publicera på varumärkesportalen]**.

Ett meddelande visas som anger att resurserna har placerats i kö för publicering på varumärkesportalen. Logga in på gränssnittet för varumärkesportalen för att se de publicerade resurserna.

## Publicera resurser senare {#publish-to-bp-later}

Så här schemalägger du publicering av resurser på varumärkesportalen till ett senare datum eller en senare tidpunkt:

1. När du har valt resurser/mappar att publicera väljer du **[!UICONTROL Hantera publikation]** i verktygsfältet högst upp.

1. På sidan **[!UICONTROL Hantera publikation]** väljer du **[!UICONTROL Publicera på varumärkesportal]** från **[!UICONTROL åtgärd]** och väljer **[!UICONTROL Senare]** från **[!UICONTROL Schemaläggning]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Välj ett **[!UICONTROL aktiveringsdatum]** och ange tid. Click **[!UICONTROL Next]**.

1. Välj ett **aktiveringsdatum** och ange tid. Click **Next**.

1. Ange en **[!UICONTROL arbetsflödesrubrik]** i **[!UICONTROL arbetsflöden]**. Klicka på **[!UICONTROL Publicera senare]**.

   ![publicerat arbetsflöde](assets/publishworkflow.png)

Logga sedan in på Brand Portal för att se om de publicerade resurserna finns tillgängliga i gränssnittet för varumärkesportalen.

![bp_landing_page](assets/bp_landing_page.png)

