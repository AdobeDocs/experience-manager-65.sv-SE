---
title: Resursavlastare för arbetsflöde
seo-title: Resursavlastare för arbetsflöde
description: Lär dig mer om Assets Workflow Offloader.
seo-description: Lär dig mer om Assets Workflow Offloader.
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Resursavlastare för arbetsflöde{#assets-workflow-offloader}

Med resursarbetsflödesavlastaren kan du aktivera flera instanser av Adobe Experience Manager-resurser (AEM) för att minska bearbetningsbelastningen på den primära (ledande) instansen. Bearbetningsinläsningen fördelas mellan ledarinstansen och de olika förinläsarinstanser (arbetare) som du lägger till i den. Genom att distribuera bearbetningslasten ökar effektiviteten och hastigheten med vilken AEM Assets bearbetar resurser. Dessutom kan du tilldela dedikerade resurser för att bearbeta resurser av en viss MIME-typ. Du kan till exempel tilldela en specifik nod i din topologi till att endast bearbeta InDesign-resurser.

## Konfigurera offloader-topologi {#configure-offloader-topology}

Använd Configuration Manager för att lägga till URL:en för ledarinstansen och värdnamnen för offloader-instanser för anslutningsbegäranden i ledarinstansen.

1. Tryck/klicka på AEM-logotypen och välj **Verktyg** > **Åtgärder** > **Webbkonsol** för att öppna Configuration Manager.
1. På webbkonsolen väljer du **Sling** > **Topology Management**.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Tryck/klicka på länken **Configure Discovery.Oak Service** på sidan Topology Management.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. På sidan Konfiguration av sökningstjänst anger du anslutnings-URL:en för ledarinstansen i fältet **Topology Connector URL** .

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. I fältet **Topology Connector Whitelist** anger du IP-adress eller värdnamn för avlastarinstanser som tillåts ansluta till ledarinstansen. Tryck/klicka på **Spara**.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Om du vill se vilka avlastarinstanser som är anslutna till ledarinstansen går du till **Verktyg** > **Distribution** > **Topologi** och trycker/klickar på klustervyn.

## Inaktivera avlastning {#disable-offloading}

1. Tryck/klicka på AEM-logotypen och välj **Verktyg** > **Distribution** > **Avlastning**. På sidan **Avlastande webbläsare** visas ämnen och serverinstanser som kan använda ämnena.

   ![chlimage_1-48](assets/chlimage_1-48a.png)

1. Inaktivera ämnet *com/adobe/granite/workflow/avlastning* om de ledande instanser som användarna interagerar med för att överföra eller ändra AEM-resurser.

   ![chlimage_1-49](assets/chlimage_1-49a.png)

## Konfigurera startprogram för arbetsflöden i ledarinstansen {#configure-workflow-launchers-on-the-leader-instance}

Konfigurera arbetsflödesstarter så att arbetsflödet för **DAM Update Asset Offloading** används i ledarinstansen i stället för i arbetsflödet för **DAM Update Asset** .

1. Tryck/klicka på AEM-logotypen och välj **Verktyg** > **Arbetsflöde** > **Starta** för att öppna **Workflow Launchers** -konsolen.

   ![chlimage_1-50](assets/chlimage_1-50a.png)

1. Leta reda på de två startkonfigurationerna med händelsetypen **Node Created** respektive **Node Modified** , som kör arbetsflödet **DAM Update Asset** .
1. För varje konfiguration markerar du kryssrutan före den och trycker/klickar på ikonen **Visa egenskaper** i verktygsfältet för att visa dialogrutan **Startegenskaper** .

   ![chlimage_1-51](assets/chlimage_1-51a.png)

1. I listan **Arbetsflöde** väljer du Avlastning **av** DAM-uppdateringsresurs och trycker/klickar på **Spara**.

   ![chlimage_1-52](assets/chlimage_1-52a.png)

1. Tryck/klicka på AEM-logotypen och välj **Verktyg** > **Arbetsflöde** > **Modeller** för att öppna sidan **Arbetsflödesmodeller** .
1. Välj arbetsflödet **DAM Update Asset Offloading** och tryck/klicka på **Edit** (Redigera) i verktygsfältet för att visa information om det.

   ![chlimage_1-53](assets/chlimage_1-53a.png)

1. Visa snabbmenyn för steget **DAM-arbetsflödesavlastning** och välj **Redigera**. Kontrollera posten i fältet **Jobbämne** på fliken **Generiska argument** i konfigurationsdialogrutan.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

## Inaktivera startfunktioner för arbetsflödet för offloader-instanser {#disable-the-workflow-launchers-on-the-offloader-instances}

Inaktivera arbetsflödet som startar arbetsflödet som kör arbetsflödet för **DAM-uppdatering av resurs** på ledarinstansen.

1. Tryck/klicka på AEM-logotypen och välj **Verktyg** > **Arbetsflöde** > **Starta** för att öppna **Workflow Launchers** -konsolen.

   ![chlimage_1-55](assets/chlimage_1-55a.png)

1. Leta reda på de två startkonfigurationerna med händelsetypen **Node Created** respektive **Node Modified** , som kör arbetsflödet **DAM Update Asset** .
1. För varje konfiguration markerar du kryssrutan före den och trycker/klickar på ikonen **Visa egenskaper** i verktygsfältet för att visa dialogrutan **Startegenskaper** .

   ![chlimage_1-56](assets/chlimage_1-56a.png)

1. I avsnittet **Aktivera** drar du reglaget för att inaktivera startprogrammet för arbetsflödet och inaktiverar det genom att trycka/klicka på **Spara** .

   ![chlimage_1-57](assets/chlimage_1-57a.png)

1. Överför alla resurser av typen bild vid ledarinstansen. Kontrollera miniatyrbilderna som genereras och porteras tillbaka för resursen av den avlastade instansen.

