---
title: Konfigurera ett Dynamic Media-företagskonto
description: Lär dig hur du konfigurerar ett företagalias i Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Konfigurera ett Dynamic Media-företagskonto {#about-dm-alias-acct}

Dynamic Media URL:er och visningsprogrammets inbäddningskod innehåller företagskontots namn. Det här kontonamnet skapades när Dynamic Media etablerades. Det kan finnas scenarier där ditt företag har genomgått ett förvärv, en omprofilering eller där du bara vill använda ett mer minnesvärt namn. I sådana fall är det inte enkelt att manuellt uppdatera företagskontots namn i alla URL:er och visningsprogrammets inbäddningskod som kommer ut ur kartongen. Dessutom finns det en möjlighet att du kan påverka din befintliga Dynamic Media-databas eller påverka direktinnehåll. Du kan lösa det här problemet genom att konfigurera ett Dynamic Media-företagskonto för alias.

Ett Dynamic Media-företagskonto som alias ser till att alla färdiga Dynamic Media-URL:er och visningsprograminbäddningskod i användargränssnittet återspeglar alla uppdateringar som görs i ditt företagskontext, till exempel omprofilering. Ett aliaskonto har också en positiv effekt på SEO (sökmotoroptimering) eftersom Dynamic Media URL:er och visningsprogrammets inbäddningskod återspeglar det nya företagskontots namn.

Tänk på följande när du konfigurerar ett Dynamic Media-företagskonto:

* Alla befintliga Dynamic Media-URL:er eller visningsprograminbäddningskod för dina *live*-digitala egenskaper måste uppdateras manuellt för att det nya aliasnamnet ska återspeglas. Alla URL-adresser och visningsprogram som bäddar in kod med ditt ursprungliga Dynamic Media-företagsnamn fortsätter dock att fungera för befintliga eller nya resurser.
* Dynamic Media aliaskonto är begränsat till Experience Manager Assets redigeringsläge och leverans. Företagets aliasnamn fungerar inte med Experience Manager Sites. WCM-komponenter (Web Content Management) har inte uppdaterats för den här ändringen. Dessa komponenter fortsätter att fungera med Dynamic Media ursprungliga företagsnamn för hämtning av Dynamic Media-resurser.
* Du kan bara konfigurera ett företagalias-konto på sidan **[!UICONTROL Edit Dynamic Media Configuration]**. Du kan dock skapa så många alias-konton som ett supportärende och manuellt spegla det nödvändiga aliasnamnet i Dynamic Media URL:er eller visningsprogrammets inbäddningskod.
* Funktionen [Cacheinvalidering](/help/assets/invalidate-cdn-cache-dynamic-media.md) i Dynamic Media som är klar att användas gör URL-adresserna ogiltiga med konton för både företags- och företagsalias konfigurerade på Dynamic Media konfigurationssida i Cloud Service.
* När du konfigurerar ett företagalias-konto på sidan **[!UICONTROL Edit Dynamic Media Configuration]** måste du göra URL:er för *både* **[!UICONTROL Company]**-kontot och **[!UICONTROL Company Alias]** ogiltiga samtidigt för att cacheminnet ska lyckas.

Se även [Skapa en Dynamic Media-konfiguration i Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Konfigurera ett Dynamic Media-företagalias Konto {#configure-dm-alias-account}

Du börjar konfigurera ett Dynamic Media-företagskonto genom att först skicka ett supportärende. Det här steget är obligatoriskt.

1. [Skapa ett supportärende](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) med Admin Console.
1. Ange följande information i ditt supportärende:

   * Det Dynamic Media-företagets alias som du vill använda. Namnet får bara innehålla ** bokstäver (blandat skiftläge tillåts), siffror, bindestreck och understreck.
   * Din region.
   * Anger om [regeluppsättningar](/help/assets/using-rulesets-to-transform-urls.md) används tidigare för att hantera Dynamic Media-innehåll med ett alternativt företagskontonamn för Dynamic Media.

1. När Dynamic Media alias-kontot har skapats av Support väljer du as a Cloud Service logotypen för Experience Manager i Experience Manager as a Cloud Service Author för att komma åt den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** i den vänstra rutan (markera inte mappikonen till vänster om **[!UICONTROL global]**). Välj sedan **[!UICONTROL Edit]**.

   ![Textfältet Dynamic Media Company Alias](/help/assets/assets-dm/dm-company-alias.png)

1. På sidan **[!UICONTROL Edit Dynamic Media Configuration]** skriver du Dynamic Media alias-kontonamnet som du angav i ditt supportärende tidigare i textfältet **[!UICONTROL Company Alias]**.
1. Välj **[!UICONTROL Save]** i det övre högra hörnet på sidan.
Dynamic Media alias-konto för företag har nu sparats och aktiverats. Alla URL:er och visningsprogrammets inbäddningskod för befintliga och nya resurser återspeglar nu det nya företagets aliasnamn.
