---
title: Leverera Dynamic Media Assets
description: Lär dig leverera dynamiska medieresurser
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 1%

---


# Delivering Dynamic Media Assets{#delivering-dynamic-media-assets}

Hur du kan leverera dynamiska medieresurser - både video och bilder - beror på hur webbplatsen implementeras.

I Dynamic Media finns flera alternativ:

* Om din webbplats ligger hos AEM vill du lägga till de dynamiska medieresurserna direkt på sidan.
* Om din webbplats inte finns på AEM kan du välja något av följande:

   * Bädda in videon eller bilden på webbplatsen.
   * Länka URL:er till webbprogrammet. Använd länkning när du vill leverera en videospelare som ett popup-fönster eller modalt fönster.
   * Om webbplatsen är responsiv kan du [leverera optimerade bilder.](/help/assets/responsive-site.md)

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart](/help/assets/imaging-faq.md) Imaging.

Mer information finns i följande avsnitt:

* [Lägga till Dynamic Media-resurser på webbsidor](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/embed-code.md)
* [Aktivera hotlink-skydd i Dynamic Media](hotlink-protection.md)
* [Länka URL:er till ditt webbprogram](/help/assets/linking-urls-to-yourwebapplication.md)
* [Leverera optimerade bilder för en responsiv webbplats](/help/assets/responsive-site.md)
* [HTTP2-leverans av innehåll](/help/assets/http2.md)
* Jag [validerar ditt cachelagrade CDN-innehåll](/help/assets/invalidate-cdn-cached-content.md)
* [Använda regeluppsättningar för att omforma URL:er](/help/assets/using-rulesets-to-transform-urls.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

AEM har nu stöd för leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar kommunikationen mellan webbläsare och servrar, vilket ger bättre respons och laddningstider för alla dina Dynamic Media-resurser.

Mer information finns i [HTTP/2 Delivery of Content Frequently Asked Questions](/help/sites-administering/scene7-http2faq.md) .
