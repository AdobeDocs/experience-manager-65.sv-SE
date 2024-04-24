---
title: Lagringskonfiguration
description: Lär dig mer om lagringskonsolen som ett sätt att identifiera det lagringsutrymme som valts för communityinnehåll, vilket också kallas användargenererat innehåll.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Lagringskonfiguration {#storage-configuration}

Lagringskonfiguration är ett sätt att identifiera det lagringsutrymme som valts för communityinnehåll, som också kallas användargenererat innehåll (UGC).

Den här inställningen informerar AEM Communities-koden om vilken implementering av lagringsresursprovidern (SRP) som används vid åtkomst till UGC. Den måste återspegla den topologi som fastställdes när Adobe Experience Manager (AEM) distribuerades.

En diskussion om lagringsalternativ och driftsättningstopologier finns på:

* [Community Content Store](working-with-srp.md)
* [Rekommenderade topologier](topologies.md)

## Konsol för lagringskonfiguration {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

I redigeringsmiljön kommer du till lagringskonsolen.

* Välj **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Storage Configuration]**

Så här väljer du ett annat lagringsalternativ än standard-JCR:

* Välj ett alternativ
* Konfigurera korrekt

   * Mer information finns [välja MSRP](msrp.md#select-msrp)
   * Mer information finns [välja DSRP](dsrp.md#select-dsrp)
   * Mer information finns [markera ASRP](asrp.md#select-asrp)

* Välj **[!UICONTROL Submit]**.

### Om JCR-lagring {#about-jcr-storage}

Om du inte gör något är standarddatabasen AEM JCR.

JCR är *not* en gemensam butik som delas av redigerings- och publiceringsmiljöerna. Community-innehåll visas bara i författar- eller publiceringsmiljön som det skapades i.

Besök [JCR Store](jsrp.md) om du vill ha mer information.

>[!NOTE]
>
>Nodens frånvaro `srpc` under `/etc/socialconfig` anger standardvärdet [JCR-butik](jsrp.md).
