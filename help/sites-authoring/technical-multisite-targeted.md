---
title: Så här struktureras hantering av flera webbplatser för riktat innehåll
seo-title: Så här struktureras hantering av flera webbplatser för riktat innehåll
description: Ett diagram visar hur stöd för flera webbplatser för riktat innehåll är strukturerat
seo-description: Ett diagram visar hur stöd för flera webbplatser för riktat innehåll är strukturerat
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 13%

---


# Så här struktureras hantering av flera webbplatser för riktat innehåll{#how-multisite-management-for-targeted-content-is-structured}

I följande diagram visas hur stöd för flera webbplatser för riktat innehåll är strukturerat.

Områden visas under **/content/campaign/&lt;brand>** och som standard har varje varumärke ett överordnad område, som skapas automatiskt. Varje område innehåller egna aktiviteter, upplevelser och erbjudanden.

![chlimage_1-268](assets/chlimage_1-268.png)

Om du vill söka efter riktat innehåll kan sidorna eller platserna mappas till ett område. Om det inte finns något konfigurerat område återgår AEM till det överordnad området för det specifika varumärket.

Följande diagram är ett exempel på hur logiken fungerar för tre platser, som kallas site1, site2 och site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 söker upp myarea1 för brand1 och other area2 för brand2 baserat på områdesmappning.
* site2 söker upp myarea1 för brand1 och överordnad area för brand2 eftersom endast områdesmappningen för brand1 har definierats.
* site3 söker upp det överordnad området för brand1 och brand2 eftersom ingen annan områdesmappning har definierats alls för den här webbplatsen.

