---
title: Publicera samlingar på varumärkesportalen
seo-title: Publicera samlingar på varumärkesportalen
description: Lär dig hur du publicerar och avpublicerar samlingar till Brand Portal.
seo-description: Lär dig hur du publicerar och avpublicerar samlingar till Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 26%

---

# Publicera samlingar på varumärkesportalen {#publish-collections-to-brand-portal}

Som Adobe Experience Manager (AEM) Assets-administratör kan du publicera samlingar till AEM Assets Brand Portal-instansen för din organisation. Du måste dock först integrera AEM Assets med Brand Portal. Mer information finns i [Konfigurera AEM Assets med varumärkesportalen](/help/assets/configure-aem-assets-with-brand-portal.md).

Om du gör senare ändringar i den ursprungliga samlingen i AEM Assets återspeglas inte ändringarna i Brand Portal förrän du publicerar samlingen igen. Den här egenskapen ser till att ändringar i pågående arbete inte är tillgängliga i Brand Portal. Endast godkända ändringar som publiceras av en administratör finns i varumärkesportalen.

>[!NOTE]
>
>Det går inte att publicera innehållsfragment på varumärkesportalen. Om du väljer innehållsfragment på AEM Author är **åtgärden Publicera på Brand Portal** därför inte tillgänglig.
>
>Om samlingar som innehåller innehållsfragment publiceras från AEM Author till Brand Portal, replikeras allt innehåll i mappen utom innehållsfragment till Brand Portal-gränssnittet.

## Publicera en samling på Brand Portal {#publish-a-collection-to-brand-portal}

1. Klicka på AEM-logotypen i användargränssnittet för AEM Assets.
1. Gå till **Resurser > Samlingar** från sidan **Navigering**.
1. På Samlingar-konsolen väljer du den samling du vill publicera till Brand Portal.

   ![select_collection](assets/select_collection.png)

1. Klicka på **Publicera till Brand Portal** i verktygsfältet.
1. Klicka på **Publicera** i bekräftelsedialogrutan.
1. Stäng bekräftelsemeddelandet.
1. Logga in på Brand Portal som administratör. Den publicerade samlingen är tillgänglig i samlingskonsolen.

   ![published collection](assets/published_collection.png)

## Avpublicera samlingar {#unpublish-collections}

Du kan avpublicera samlingar som du publicerar från AEM Assets till Brand Portal. När du har avpublicerat originalsamlingen är kopian inte längre tillgänglig för Brand Portal-användare.

1. Gå till Samlingar-konsolen för din AEM Assets-instans och välj den samling som du vill avpublicera.

   ![select_collection-1](assets/select_collection-1.png)

1. Klicka på ikonen **Ta bort från Brand Portal** i verktygsfältet.
1. Klicka på **Avpublicera** i dialogrutan.
1. Stäng bekräftelsemeddelandet. Samlingen tas bort från varumärkesportalens gränssnitt.
