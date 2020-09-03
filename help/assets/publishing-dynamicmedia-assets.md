---
title: Publicera dynamiska medieresurser
description: Publicera dynamiska medieresurser
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: 7a1da89805799f392f4397b1582bcc83d9bc67de
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

Du publicerar dina dynamiska medieresurser genom att välja de resurser du redan har överfört och trycka på **[!UICONTROL Publish]** eller **[!UICONTROL Quick Publish.]** när dina dynamiska medieresurser har publicerats är de tillgängliga för dig så att du kan inkludera dem på en webbsida via en URL eller genom att bädda in koden på sidan.

Du kan också publicera resurser som du överför direkt - utan att behöva göra något från användaren. Se [Konfigurera Dynamic Media - Scene7-läge.](config-dms7.md)
Eller så kan du selektivt publicera resurser till antingen Dynamic Media eller AEM, som inte är ömsesidigt oberoende av varandra, med hjälp **[!UICONTROL Selective Publish]** av mappnivån. Se [Arbeta med selektiv publicering i dynamiska media.](/help/assets/selective-publishing.md)

I **[!UICONTROL Card View]** visas en liten globikon direkt under namnet på en resurs och till vänster om datumet och tiden för att ange att den publiceras. I **[!UICONTROL List View]** anger kolumnen **[!UICONTROL Published]** vilka resurser som har publicerats och inte.

>[!NOTE]
>
>Om en resurs redan är publicerad använder du AEM för att flytta resursen till en annan mapp och publicera på nytt från den nya platsen, men den ursprungliga publicerade resursplatsen är fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för AEM och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

Om du tänker publicera videomaterial direkt efter kodningen bör du kontrollera att kodningen är helt klar. När videoklipp fortfarande kodas visas ett arbetsflöde för videobearbetning. När videokodningen är klar bör du kunna förhandsgranska videoåtergivningarna. Då är det säkert att publicera videoklippen utan att det uppstår några publiceringsfel.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

See also [Embedding the Dynamic Media Video or Image viewer on a web page](embed-code.md)

>[!NOTE]
>
>* Resurser måste publiceras för att kunna använda URL:en. Om resurserna inte publiceras kommer det inte att gå att kopiera och klistra in URL-adressen i en webbläsare.
>* Bildförinställningar och visningsförinställningar måste aktiveras och publiceras för direktleverans.

>



Mer information om hur du publicerar en uppsättning eller resurs finns i [Publicera resurser.](managing-assets-touch-ui.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

AEM har nu stöd för leverans av allt dynamiskt medieinnehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla dynamiska medieresurser.

Mer information finns i [HTTP/2-leverans av innehåll med vanliga frågor](/help/sites-administering/scene7-http2faq.md) .
