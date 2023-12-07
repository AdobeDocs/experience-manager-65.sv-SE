---
title: Publicera mappar i Brand Portal
description: Lär dig hur du publicerar och avpublicerar mappar till Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 20%

---

# Publicera mappar i Brand Portal{#publish-folders-to-brand-portal}

Som Adobe Experience Manager (AEM) Assets-administratör kan du publicera resurser och mappar i AEM Assets Brand Portal-instansen (eller schemalägga publiceringsarbetsflödet till ett senare datum/tid) för din organisation. Du måste dock först integrera AEM Assets med Brand Portal. Mer information finns i [Konfigurera AEM Assets med varumärkesportalen](/help/assets/configure-aem-assets-with-brand-portal.md).

När du har publicerat en resurs eller mapp är den tillgänglig för användare i Brand Portal.

Om du gör senare ändringar i den ursprungliga resursen eller mappen i AEM Assets återspeglas inte ändringarna i Brand Portal förrän du publicerar resursen eller mappen på nytt. Funktionen säkerställer att pågående ändringar inte finns i varumärkesportalen. Endast godkända ändringar som publiceras av en administratör finns i varumärkesportalen.

## Publicera mappar i Brand Portal {#publish-folders-to-brand-portal-1}

1. I AEM Assets-gränssnittet för du pekaren över den önskade mappen och väljer **Publicera** från snabbåtgärderna.

   Du kan också markera önskad mapp och följa stegen nedan.

   ![publish2bp](assets/publish2bp.png)

1. **Publicera mappar nu**

   Gör något av följande för att publicera de markerade mapparna på varumärkesportalen:

   * Välj **Snabbpublicering**. Välj sedan **Publicera till Brand Portal**.

   * Välj **Hantera publikation**.

   1. Från **Åtgärd** välj **Publicera till Brand Portal**, från **Schemaläggning** välj **Nu** och klicka **Nästa.**
   1. Bekräfta ditt val i **Omfång** och klicka **Publicera till Brand Portal**.

   Ett meddelande visas som anger att mappen har placerats i kö för publicering på varumärkesportalen. Logga in i Brand Portal-gränssnittet för att se den publicerade mappen.

   **Publicera mappar senare**

   Så här schemalägger du publiceringen i Brand Portal-arbetsflödet för resursmappar till ett senare datum eller en senare tidpunkt:

   1. När du har valt resurser/mappar att publicera väljer du **Hantera publikation** i verktygsfältet högst upp.
   1. Från **Åtgärd** välj **Publicera till Brand Portal**, från **Schemaläggning** välj **Senare**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Välj ett **aktiveringsdatum** och ange en tid. Klicka på **Nästa**.
   1. Bekräfta ditt val i **Omfång**. Klicka på **Nästa**.
   1. Ange en arbetsflödestitel under **Arbetsflöden**. Klicka **Publicera senare**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Avpublicera mappar från Brand Portal {#unpublish-folders-from-brand-portal}

Du kan ta bort en resursmapp som publicerats till Brand Portal genom att avpublicera den från AEM författarinstans. När du har avpublicerat originalmappen har varumärkesportalens användare har inte längre tillgång till kopian.

Du kan avpublicera mappar från Brand Portal snabbt eller schemalägga dem för ett senare datum och en senare tidpunkt. Gör så här för att avpublicerar resursmappar från varumärkesportalen:

1. I AEM Assets-gränssnittet i AEM Author-instansen väljer du den mapp som du vill avpublicera.

   ![publish2bp-1](assets/publish2bp.png)

1. Klicka på i verktygsfältet **Hantera publikation**.

1. **Avpublicera från Brand Portal nu**

   Så här avpublicerar du snabbt den önskade mappen från Brand Portal:

   1. Välj **Hantera publikation**.
   1. Från **Åtgärd** välj **Avpublicera från Brand Portal**, från **Schemaläggning** välj **Nu** och klicka **Nästa.**
   1. Bekräfta ditt val i **Omfång** och klicka **Avpublicera från Brand Portal**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Avpublicera från Brand Portal senare**

   Så här schemalägger du publiceringen av en mapp från Brand Portal till ett senare datum och tid:

   1. Välj **Hantera publikation**.
   1. Från **Åtgärd** välj **Avpublicera från Brand Portal** och från **Schemaläggning** välj **Senare**.
   1. Välj en **Aktiveringsdatum** och ange tiden. Klicka på **Nästa**.
   1. Bekräfta ditt val i **Omfång** och klicka **Nästa**.
   1. Ange en **Arbetsflödets titel** in **Arbetsflöden**. Klicka **Avpublicera senare.**

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>Proceduren för att publicera/avpublicera en resurs till/från Brand Portal liknar motsvarande procedur för en mapp.
