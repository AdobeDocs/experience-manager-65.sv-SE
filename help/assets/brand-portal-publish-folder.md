---
title: Publicera mappar på varumärkesportalen
seo-title: Publicera mappar på varumärkesportalen
description: Lär dig hur du publicerar och avpublicerar mappar på varumärkesportalen.
seo-description: Lär dig hur du publicerar och avpublicerar mappar på varumärkesportalen.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Publicera mappar på varumärkesportalen{#publish-folders-to-brand-portal}

Som administratör för Adobe Experience Manager-resurser (AEM) kan du publicera resurser och mappar i instansen av AEM Assets Brand Portal (eller schemalägga publiceringsarbetsflödet till ett senare datum/tid) för organisationen. Du måste dock först integrera AEM Assets med varumärkesportalen. Mer information finns i [Konfigurera AEM-resurser med varumärkesportalen](/help/assets/configure-aem-assets-with-brand-portal.md).

När du har publicerat en resurs eller mapp är den tillgänglig för användare i varumärkesportalen.

Om du gör senare ändringar av den ursprungliga resursen eller mappen i AEM Resurser återspeglas inte ändringarna i Varumärkeportalen förrän du publicerar resursen eller mappen på nytt. Den här funktionen ser till att pågående ändringar inte är tillgängliga i varumärkesportalen. Endast godkända ändringar som publiceras av en administratör är tillgängliga i varumärkesportalen.

## Publicera mappar på varumärkesportalen {#publish-folders-to-brand-portal-1}

1. I gränssnittet för AEM Resurser håller du pekaren över den önskade mappen och väljer **alternativet Publicera** bland snabbåtgärderna.

   Du kan också markera önskad mapp och följa stegen nedan.

   ![publish2bp](assets/publish2bp.png)

1. **Publicera mappar nu**

   Om du vill publicera de markerade mapparna på varumärkesportalen gör du något av följande:

   * Välj **Snabbpublicering** i verktygsfältet. Välj sedan **Publicera på varumärkesportalen** på menyn.

   * Välj **Hantera publikation** i verktygsfältet.
   1. Från **Åtgärd** väljer du **Publicera på varumärkesportal**. Från **Schemaläggning** väljer du **nu** och klickar sedan på **Nästa.**
   1. Bekräfta ditt val i **Omfång** och klicka på **Publicera på varumärkesportal**.
   Det visas ett meddelande om att mappen har placerats i kö för publicering på varumärkesportalen. Logga in i gränssnittet för varumärkesportalen för att se den publicerade mappen.

   **Publicera mappar senare**

   Så här schemalägger du arbetsflödet för publicering till varumärkesportalen för resursmappar till ett senare datum eller en senare tidpunkt:

   1. När du har valt resurser/mappar att publicera väljer du **Hantera publikation** i verktygsfältet högst upp.
   1. Från **Åtgärd** väljer du **Publicera på varumärkesportal**. Från **Schemaläggning** väljer du **Senare**.

      ![publiclaterbp](assets/publishlaterbp.png)

   1. Välj ett **aktiveringsdatum** och ange tid. Click **Next**.
   1. Bekräfta ditt val i **Omfång**. Click **Next**.
   1. Ange en arbetsflödesrubrik under **Arbetsflöden**. Klicka på **Publicera senare**.

      ![manageschedulepub](assets/manageschedulepub.png)



## Avpublicera mappar från varumärkesportalen {#unpublish-folders-from-brand-portal}

Du kan ta bort alla resursmappar som publicerats på varumärkesportalen genom att avpublicera dem från AEM Author-instansen. När du har avpublicerat originalmappen är dess kopia inte längre tillgänglig för användare av varumärkesportalen.

Du kan avpublicera mappar från varumärkesportalen snabbt eller schemalägga dem för ett senare datum och en senare tidpunkt. Så här avpublicerar du resursmappar från varumärkesportalen:

1. I gränssnittet AEM Resurser i AEM Author-instansen väljer du den mapp du vill avpublicera.

   ![publish2bp-1](assets/publish2bp.png)

1. Klicka på **Hantera publikation** i verktygsfältet.

1. **Avpublicera från varumärkesportalen nu**

   Så här avpublicerar du snabbt den önskade mappen från varumärkesportalen:

   1. Välj **Hantera publikation** i verktygsfältet.
   1. I **Åtgärd** väljer du **Avpublicera från varumärkesportalen**, **välj Schemaläggning** **nu** och klicka sedan på **Nästa.**
   1. Bekräfta ditt val i **Omfång** och klicka på **Avpublicera från varumärkesportalen**.
   ![bekräfta-avpublicera](assets/confirm-unpublish.png)

   **Avpublicera från varumärkesportalen senare**

   Så här schemalägger du publiceringen av en mapp från varumärkesportalen till ett senare datum och en senare tidpunkt:

   1. Välj **Hantera publikation** i verktygsfältet.
   1. Från **Åtgärd** väljer du **Avpublicera från varumärkesportalen** och från **Schemaläggning** väljer du **Senare**.
   1. Välj ett **aktiveringsdatum** och ange tid. Click **Next**.
   1. Bekräfta ditt val i **Omfång** och klicka på **Nästa**.
   1. Ange en **arbetsflödesrubrik** i **arbetsflöden**. Klicka på **Avpublicera senare.**

      ![ej publicerade arbetsflöden](assets/unpublishworkflows.png)


>[!NOTE]
>
>Proceduren för att publicera/avpublicera en resurs till/från varumärkesportalen liknar motsvarande procedur för en mapp.

