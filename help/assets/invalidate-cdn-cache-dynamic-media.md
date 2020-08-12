---
title: Invalidera CDN-cachen med hjälp av Dynamic Media
description: Genom att du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska förfalla.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---


# Invalidera CDN-cachen med hjälp av Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Dynamiska mediefiler cachas av CDN (Content Delivery Network) för snabb leverans till dina kunder. När du uppdaterar dessa resurser kanske du vill att ändringarna ska börja gälla omedelbart på webbplatsen. Genom att rensa eller göra CDN-cachen ogiltig kan du snabbt uppdatera resurser som levereras av Dynamic Media. I stället för att vänta på att cachen ska förfalla med ett TTL-värde (Time To Live) (standard är 10 timmar) kan du skicka en begäran från Dynamic Media om att cachen ska förfalla omedelbart.

>[!IMPORTANT]
>
>De här stegen gäller endast för Dynamic Media - Scene7-läge i AEM 6.5, Service Pack 6 eller senare. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Se även Översikt över [cachelagring i Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Så här gör du ditt CDN-cachelagrade innehåll för dynamiska medieresurser ogiltigt:**

1. I AEM 6.5.6 eller senare trycker du på **[!UICONTROL Tools > Assets > CDN Invalidation.]**

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Ange önskade alternativ på sidan CDN-validering:

   | Alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Invalidate asset associated image presets in CDN]** | När du markerar det här alternativet kan du välja ett eller flera Dynamic Media-resurser, oavsett MIME-typ och deras associerade bildförinställningar för att göra cacheminnet ogiltigt.<br>Du kan välja en eller flera mappar som innehåller resurser, men Adobe rekommenderar inte det här tillvägagångssättet. Du bör i stället välja enskilda resursfiler.<br>Fortsätt till nästa steg. |
   | **[!UICONTROL Invalidation based on template]** | När du markerar det här alternativet kan du välja Dynamic Media-resurser och den mall för validering som du har skapat tidigare. Använd det här alternativet med |
   | **[!UICONTROL Add Assets]** | Blah |
   | **[!UICONTROL Add URL]** | Lägg manuellt till fullständiga URL-sökvägar till Dynamic Media-resurser vars cache du vill ogiltigförklara. |

1. 
1. Tryck på **[!UICONTROL Next.]**
1. 
