---
title: Publicera samlingar på varumärkesportalen
seo-title: Publicera samlingar på varumärkesportalen
description: Lär dig hur du publicerar och avpublicerar samlingar på varumärkesportalen.
seo-description: Lär dig hur du publicerar och avpublicerar samlingar på varumärkesportalen.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
translation-type: tm+mt
source-git-commit: 9c73abc3291f2847c705cb649d2993fb186b0993

---


# Publicera samlingar på varumärkesportalen {#publish-collections-to-brand-portal}

Som administratör för Adobe Experience Manager-resurser (AEM) kan du publicera samlingar till instansen AEM Assets Brand Portal för din organisation. Du måste dock först integrera AEM Assets med varumärkesportalen. Mer information finns i [Konfigurera AEM Assets-integrering med varumärkesportalen](/help/assets/brand-portal-configuring-integration.md).

Om du gör senare ändringar i den ursprungliga samlingen i AEM Resurser återspeglas inte ändringarna i varumärkesportalen förrän du publicerar samlingen igen. Den här egenskapen ser till att ändringar i pågående arbete inte är tillgängliga i varumärkesportalen. Endast godkända ändringar som publiceras av en administratör är tillgängliga i varumärkesportalen.

>[!NOTE]
>
>Det går inte att publicera innehållsfragment till varumärkesportalen. Om du väljer innehållsfragment på AEM Author är åtgärden **Publicera på varumärkesportalen** därför inte tillgänglig.
>
>Om samlingar som innehåller innehållsfragment publiceras från AEM Author till Brand Portal replikeras allt innehåll i mappen, förutom innehållsfragment, till gränssnittet Brand Portal.

## Publicera en samling på varumärkesportalen {#publish-a-collection-to-brand-portal}

1. Klicka på AEM-logotypen i användargränssnittet för AEM-resurser.
1. Gå till **Resurser > Samlingar** på **** navigeringssidan.
1. På Samlingar-konsolen väljer du den samling du vill publicera på varumärkesportalen.

   ![select_collection](assets/select_collection.png)

1. Klicka på **Publicera till varumärkesportal** i verktygsfältet.
1. Klicka på **Publicera** i bekräftelsedialogrutan.
1. Stäng bekräftelsemeddelandet.
1. Logga in på varumärkesportalen som administratör. Den publicerade samlingen är tillgänglig i Samlingar-konsolen.

   ![publicerad samling](assets/published_collection.png)

## Avpublicera samlingar {#unpublish-collections}

Du kan avpublicera samlingar som du publicerar från AEM Assets till varumärkesportalen. När du har avpublicerat den ursprungliga samlingen är dess kopia inte längre tillgänglig för Brand Portal-användare.

1. Från Samlingar-konsolen i din AEM Resurser-instans och välj den samling du vill avpublicera.

   ![select_collection-1](assets/select_collection-1.png)

1. Klicka på ikonen **Ta bort från varumärkesportalen** i verktygsfältet.
1. Klicka på **Avpublicera** i dialogrutan.
1. Stäng bekräftelsemeddelandet. Samlingen tas bort från gränssnittet för varumärkesportalen.

