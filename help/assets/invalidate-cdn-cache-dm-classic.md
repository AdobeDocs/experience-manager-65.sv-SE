---
title: CDN-cachen har inte verifierats med Dynamic Media Classic
description: Om du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media Classic, i stället för att vänta på att cachen ska upphöra att gälla.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN-cache,Dynamic Media Classic
role: Business Practitioner, Administrator
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 17%

---

# CDN-cachen har inte verifierats med Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Dynamic Media resurser cachas av CDN (Content Delivery Network) för snabb leverans. När du uppdaterar en resurs vill du dock att ändringarna ska börja gälla omedelbart. Om du validerar ditt CDN-cachelagrade innehåll kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Eventuellt annat anpassat CDN stöds inte med den här funktionen.

>[!IMPORTANT]
>
>Följande steg gäller endast för Dynamic Media i AEM 6.5, Service Pack 5 (AEM 6.5.5) eller tidigare.<br>Om du använder Dynamic Media i AEM 6.5, Service Pack 6 (AEM 6.5.6) eller senare, följer du stegen i  [Invalidera CDN-cachen med Dynamic Media](/help/assets/invalidate-cdn-cache-dynamic-media.md).

Se även [Cacheöversikt i Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Så här gör du CDN-cachen ogiltig med Dynamic Media Classic:**

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app) och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. I det övre högra hörnet av sidan trycker du på **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]**.
1. Gå till textrutan **[!UICONTROL CDN Invalidation Template]** under grupprubriken Servrar på sidan Allmänna inställningar för program.

1. Ange den mall som används för att ogiltigförklara CDN-cachen (Content Delivery Network).

   Anta till exempel att du anger en bild-URL (inklusive bildförinställningar eller modifierare) som refererar till `<ID>`, i stället för ett specifikt bild-ID som i följande exempel:

   `https://server.com/is/image/Company/<ID>?$product$`

   Om mallen bara innehåller `<ID>` fylls Dynamic Media i `https://<server>/is/image` där `<server>` är det publiceringsservernamn som definieras i Allmänna inställningar och &lt;ID> är de resurser som markerats som ogiltiga.

1. I sidans nedre högra hörn klickar du på **[!UICONTROL Close]**.
1. I Dynamic Media Classic-användargränssnittet väljer du en eller flera resurser och klickar sedan på **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**. Du ser en lista över en eller flera URL-adresser som genererats från mallen som du skapade och de resurser som du markerade. Den använder den server-URL som anges under &quot;Publicerat servernamn&quot; under Allmänna inställningar för programmet.

   Anta till exempel att du har valt en enda bild med namnet `Backpack_B` när du har angett en mall för CDN-validering i föregående steg. När du trycker på **[!UICONTROL File > Invalidate CDN]** resulterar det i följande genererade URL i användargränssnittet för CDN-validering:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. I listrutan URL trycker du på **[!UICONTROL Continue]** för att rensa cachen för varje specifik URL. Du kan redigera en URL-adress eller lägga till en URL-adress genom att skriva eller klistra in den i URL-listrutan; Du behöver inte ställa in CDN Invalidate Template i förväg.

   När du har klickat på **[!UICONTROL Continue]** visas en indikator som ger dig en uppskattning av hur lång tid det tar att rensa cachen.

   Om du har markerat flera resurser och sedan trycker på **[!UICONTROL File > Invalidate CDN]** refereras varje resurs i den sparade **[!UICONTROL Template URL]**. Därför kan du definiera en **[!UICONTROL CDN Invalidate Template]** som refererar till varje URL-bildförinställning som refereras på webbplatsen (t.ex. produktinformation och sökresultat). När du sedan väljer en eller flera bilder som ska ogiltigförklaras från cachen fylls gränssnittet automatiskt i med URL:erna.

   >[!NOTE]
   >
   >När du markerar resurser och sedan klickar på **[!UICONTROL File > Invalidate CDN]** använder Dynamic Media en mall för att automatiskt skapa URL:er som ska ogiltigförklaras i leveransnätverket (CDN, Content Delivery Network). Om det inte finns något i textrutan **[!UICONTROL CDN Invalidate Template]** visas en tom URL-lista. Cachelagring i leveransnätverket (CDN) är inte resursbaserad utan URL-baserad. Därför är det nödvändigt att känna till de fullständiga URL:erna på webbplatsen. När du har definierat dessa URL:er kan du lägga till dem i textrutan **[!UICONTROL Invalidate CDN Template]** tidigare i stegen. Sedan kan du markera dessa resurser och göra URL:erna ogiltiga i ett enda steg.
   >
   >Ett annat alternativ är att lägga till fullständiga URL:er i **[!UICONTROL Invalidate CDN]**-listan. Om du väljer det här sättet behöver du inte markera resurser i Dynamic Media Classic innan du går till alternativet **[!UICONTROL File > Invalidate CDN]**.
