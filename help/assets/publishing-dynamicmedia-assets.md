---
title: Publicera Dynamic Media Assets
description: Lär dig hur du publicerar Dynamic Media-resurser, t.ex. videor och bilder, inklusive HTTP/2-leverans av sådana resurser.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 2%

---

# Publish Dynamic Media-resurser {#publishing-dynamic-media-assets}

Du publicerar dina Dynamic Media-resurser genom att välja de resurser som du redan har överfört och trycka på **[!UICONTROL Publish]** eller **[!UICONTROL Quick Publish]**. När dina Dynamic Media-resurser har publicerats kan du inkludera dem på en webbsida via en URL-adress eller genom att bädda in koden på webbsidan.

Du kan också publicera resurser som du överför direkt - utan att behöva göra något från användaren. Se [Konfigurera Dynamic Media - Scene7 ](config-dms7.md).
Eller så kan du selektivt publicera resurser till antingen Dynamic Media eller Adobe Experience Manager, som utesluter varandra, med **[!UICONTROL Selective Publish]** på mappnivå. Se [Arbeta med selektiv Publish i Dynamic Media](/help/assets/selective-publishing.md).

I **[!UICONTROL Card View]** visas en liten globala ikon direkt under namnet på en resurs och till vänster om datumet och tiden för att ange att den är publicerad. I **[!UICONTROL List View]** anger kolumnen **[!UICONTROL Published]** vilka resurser som har publicerats och inte.

>[!NOTE]
>
>Om en resurs redan är publicerad använder du Experience Manager för att flytta resursen till en annan mapp och publicera den på nytt från den nya platsen. Den ursprungliga publicerade resursplatsen är fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för Experience Manager och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

Om du tänker publicera videomaterial direkt efter kodningen kontrollerar du att kodningen är klar. När videofilmer kodas talar systemet om för dig att ett arbetsflöde för videobearbetning pågår. När videokodningen är klar kan du förhandsgranska videoåtergivningarna. Då är det säkert att publicera videoklippen utan att det uppstår några publiceringsfel.

Se även [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

Se även [Bädda in Dynamic Media Video eller Image Viewer på en webbsida](embed-code.md)

>[!NOTE]
>
>* Assets måste publiceras för att kunna använda URL:en. Om resurserna inte publiceras fungerar inte det att kopiera och klistra in URL-adressen i en webbläsare.
>* Bildförinställningar och visningsförinställningar måste aktiveras och publiceras för direktleverans.
>

Mer information om hur du publicerar en uppsättning eller resurs finns i [Publish-resurser](manage-assets.md).

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

Experience Manager stöder nu leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla era Dynamic Media-resurser.

Mer information finns i [HTTP/2-leverans av innehåll, vanliga frågor och svar](/help/sites-administering/scene7-http2faq.md).
