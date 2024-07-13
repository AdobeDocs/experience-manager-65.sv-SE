---
title: Bädda in Dynamic Media Video, Image Viewer eller Dimensional Viewer på en webbsida
description: Lär dig bädda in Dynamic Media-video, bilder eller 3D-bilder på en webbsida
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 20%

---

# Bädda in Dynamic Media Video, Image Viewer eller Dimensional Viewer på en webbsida {#embedding-the-video-or-image-viewer-on-a-web-page}

Använd funktionen **[!UICONTROL Embed Code]** när du vill spela upp videon eller visa en resurs som är inbäddad på en webbsida. Du kopierar inbäddningskoden till Urklipp så att du kan klistra in den på webbsidorna. Det är inte tillåtet att redigera koden i dialogrutan **[!UICONTROL Embed Code]**.

Du bäddar bara in URL:er om du *inte* använder Adobe Experience Manager som WCM-fil. Om du använder Experience Manager som WCM-fil [lägger du till resurserna direkt på sidan](adding-dynamic-media-assets-to-pages.md).

Se [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

Se [Leverera optimerade bilder för en responsiv webbplats](responsive-site.md).

>[!NOTE]
>
>Inbäddningskoden kan inte kopieras förrän du har publicerat den valda resursen. Dessutom måste du även publicera visningsförinställningen eller bildförinställningen.
>
>Se [Publish-resurser](publishing-dynamicmedia-assets.md).
>
>Se [Förinställningar för Publish Viewer](managing-viewer-presets.md#publishing-viewer-presets).
>
>Se [Publish bildförinställningar](managing-image-presets.md#publishing-image-presets).

**Så här bäddar du in Dynamic Media Video, Image Viewer eller Dimensional Viewer på en webbsida:**

1. Navigera till den *publicerade* videon eller bildresurs vars inbäddningskod du vill kopiera.

   Kom ihåg att inbäddningskoden endast går att kopiera *efter* att du har *publicerat* resurserna. Dessutom måste visningsförinställningen eller bildförinställningen också publiceras.

   Se [Publish-resurser](publishing-dynamicmedia-assets.md).

   Se [Förinställningar för Publish Viewer](managing-viewer-presets.md#publishing-viewer-presets).

   Se [Publish bildförinställningar](managing-image-presets.md#publishing-image-presets).

1. Markera listrutan i den vänstra listen och välj **[!UICONTROL Viewers]**.
1. Välj ett namn på visningsförinställningen i den vänstra listen. Visningsförinställningen används på resursen.
1. Välj **[!UICONTROL Embed]**.
1. I dialogrutan **[!UICONTROL Embed Code]** kopierar du hela koden till Urklipp och väljer sedan **[!UICONTROL Close]**.
1. Klistra in inbäddningskoden på dina webbsidor.

## Använd HTTP/2 för att leverera Dynamic Media-material {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](http2.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.
