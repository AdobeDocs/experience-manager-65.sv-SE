---
title: Leverera Dynamic Media-material
description: Lär dig hur du levererar Dynamic Media-material, som video och bilder, till dina webbsidor.
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: 7f8cfe155af3b8831e746ced89c11c971e429f69
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# Leverera Dynamic Media-material{#delivering-dynamic-media-assets}

Hur du kan leverera dina Dynamic Media-resurser - både video och bilder - beror på hur webbplatsen implementeras.

Med Dynamic Media har du flera alternativ:

* Om webbplatsen finns på Adobe Experience Manager vill du lägga till Dynamic Media-resurserna direkt på sidan.
* Om din webbplats inte finns på Experience Manager kan du välja något av följande:

   * Bädda in videon eller bilden på webbplatsen.
   * Länka URL:er till webbprogrammet. Använd länkning när du vill leverera en videospelare som ett popup-fönster eller modalt fönster.
   * Om din webbplats är responsiv kan du [leverera optimerade bilder](/help/assets/responsive-site.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](/help/assets/imaging-faq.md) för mer information.

Mer information finns i följande avsnitt:

* [Lägga till Dynamic Media-resurser på webbsidor](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/embed-code.md)
* [Aktivera hotlink-skydd i Dynamic Media](/help/assets/hotlink-protection.md)
* [Länka URL:er till ditt webbprogram](/help/assets/linking-urls-to-yourwebapplication.md)
* [Leverera optimerade bilder för en responsiv webbplats](/help/assets/responsive-site.md)
* [Leverera innehåll med HTTP2](/help/assets/http2.md)
* [Gör CDN-cachen ogiltig med Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Använd regeluppsättningar för att omforma URL:er](/help/assets/using-rulesets-to-transform-urls.md)


## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

Experience Manager stöder nu leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla era Dynamic Media-resurser.

Mer information finns på [HTTP/2-leverans av innehåll, vanliga frågor](/help/sites-administering/scene7-http2faq.md).
