---
title: Aktivera skydd för aktiva länkar i Dynamic Media
description: Information om hur du aktiverar hot link-skydd i Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
translation-type: tm+mt
source-git-commit: 787f3b4cf5835b7e9b03e3f4e6f6597084adec8c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Aktiverar hot link-skydd i Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Aktiv länkning är när en tredjepartswebbplats använder HTML-kod för att visa en bild från din webbplats. De använder din bandbredd varje gång bilden efterfrågas eftersom besökarens webbläsare öppnar den direkt från servern. Hotlink *protection* är en metod som förhindrar att andra webbplatser direkt länkar till bilder, css eller JavaScript på dina webbsidor. Den här typen av skydd minskar onödig bandbreddsanvändning på ditt Dynamic Media-konto.

[Adobe ](https://helpx.adobe.com/support.html) Support kan konfigurera ett referensfilter på CDN-nivå (Content Delivery Network) så att Dynamic Media-innehåll endast kan användas på webbplatser i din lista över tillåtna webbplatser för domänen.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Eventuellt annat anpassat CDN stöds inte med den här funktionen. För att aktivera aktivering av hot link-skydd måste en administratör skapa en Adobe kundtjänstsupportbiljett för att begära konfigurationsändringen av ditt Dynamic Media-konto. Det kostar inget mer att aktivera skydd av aktiva länkar.
