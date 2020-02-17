---
title: Lagringskonfiguration
seo-title: Lagringskonfiguration
description: Åtkomst till lagringskonsolen
seo-description: Åtkomst till lagringskonsolen
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Lagringskonfiguration {#storage-configuration}

Lagringskonfiguration är ett sätt att identifiera det lagringsutrymme som valts för communityinnehåll, som också kallas användargenererat innehåll (UGC).

Den här inställningen informerar AEM Communities-koden om vilken implementering av lagringsresursprovidern som ska användas vid åtkomst till UGC och måste återspegla den topologi som fastställdes när AEM distribuerades.

En diskussion om lagringsalternativ och driftsättningstopologier finns på

* [Community Content Store](working-with-srp.md)
* [Rekommenderade topologier](topologies.md)

## Konsol för lagringskonfiguration {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

För att nå lagringskonsolen i redigeringsmiljön

* Från global navigering: **[!UICONTROL Verktyg > Communities > Storage Configuration]**

Så här väljer du ett annat lagringsalternativ än standard-JCR:

* välj ett alternativ
* Konfigurera korrekt

   * Se information om hur du [väljer MSRP](msrp.md#select-msrp)
   * Se information för [val av DSRP](dsrp.md#select-dsrp)
   * Se information om hur du [väljer ASRP](asrp.md#select-asrp)

* Välj **[!UICONTROL Skicka]**

### Om JCR-lagring {#about-jcr-storage}

Observera att om inget val görs är standardinställningen AEM-databasen JCR.

JCR är *inte* en vanlig butik som delas av författaren och publiceringsmiljöerna. Community-innehåll visas bara i den författar- eller publiceringsmiljö där det skapades.

Mer information finns i [JCR Store](jsrp.md) .

>[!NOTE]
>
>Om noden inte finns `srpc`under `/etc/socialconfig` visas standardlagret för [JCR](jsrp.md).

