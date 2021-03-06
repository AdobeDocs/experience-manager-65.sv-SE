---
title: Publicera Dynamic Media Assets
description: Publicera Dynamic Media-material
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publicering
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 2%

---

# Publicera Dynamic Media-resurser {#publishing-dynamic-media-assets}

Du publicerar dina Dynamic Media-resurser genom att välja de resurser du redan har överfört och trycka på **[!UICONTROL Publish]** eller **[!UICONTROL Quick Publish]**. När dina Dynamic Media-resurser har publicerats kan du inkludera dem på en webbsida via en URL eller genom att bädda in koden på sidan.

Du kan också publicera resurser som du överför direkt - utan att behöva göra något från användaren. Se [Konfigurera Dynamic Media - Scene7-läge](config-dms7.md).
Eller så kan du selektivt publicera resurser på antingen Dynamic Media eller Adobe Experience Manager, som utesluter varandra, med **[!UICONTROL Selective Publish]** på mappnivå. Se [Arbeta med selektiv publicering i Dynamic Media](/help/assets/selective-publishing.md).

I **[!UICONTROL Card View]** visas en liten globala ikon direkt under namnet på en resurs och till vänster om datumet och tiden för att ange att den publiceras. I **[!UICONTROL List View]** anger kolumnen **[!UICONTROL Published]** vilka resurser som har publicerats och inte.

>[!NOTE]
>
>Om en resurs redan är publicerad använder du Experience Manager för att flytta resursen till en annan mapp och publicera den på nytt från den nya platsen. Den ursprungliga publicerade resursplatsen är fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för Experience Manager och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

Om du tänker publicera videomaterial direkt efter kodningen kontrollerar du att kodningen är klar. När videofilmer kodas talar systemet om för dig att ett arbetsflöde för videobearbetning pågår. När videokodningen är klar kan du förhandsgranska videoåtergivningarna. Då är det säkert att publicera videoklippen utan att det uppstår några publiceringsfel.

Se även [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

Se även [Bädda in Dynamic Media Video eller Image Viewer på en webbsida](embed-code.md)

>[!NOTE]
>
>* Resurser måste publiceras för att kunna använda URL:en. Om resurserna inte publiceras fungerar inte det att kopiera och klistra in URL-adressen i en webbläsare.
>* Bildförinställningar och visningsförinställningar måste aktiveras och publiceras för direktleverans.

>



Mer information om hur du publicerar en uppsättning eller resurs finns i [Publicera resurser](manage-assets.md).

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

Experience Manager stöder nu leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar kommunikationen mellan webbläsare och servrar, vilket ger bättre respons och laddningstider för alla dina Dynamic Media-resurser.

Mer information finns i [HTTP/2-leverans av innehåll, vanliga frågor och svar](/help/sites-administering/scene7-http2faq.md).
