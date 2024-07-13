---
title: Riktlinjer för kodning
description: Användarforum, tips och tricks
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Riktlinjer för kodning {#coding-guidelines}

## Riktlinjer, tips och tricks {#guidelines-tips-and-tricks}

Arbetet med AEM Communities har utvecklats från att vara starkt beroende av Java Server Pages till flexibilitet när det gäller valet av skriptspråk där affärslogik, format och sidinnehåll skiljer sig från varandra.

Ytterligare flexibilitet när det gäller att arbeta med användargenererat innehåll (UGC) är via SocialResourceProvider-API:t, vilket eliminerar behovet av att känna till vilket [SRP](srp.md)-alternativ som valdes för distributionen.

Nedan följer olika riktlinjer för kodning och metodtips för AEM Communities-utvecklare:

### Code {#code}

* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - så här undviker du att skriva ett program som bara fungerar när UGC lagras i JCR (JSRP).
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.
* [Namnkonventioner](naming-conventions.md) - namnkonventioner för anpassade Java-klasser.

### Skript {#scripts}

* [Inläsning av communitykomponenter](sideloading.md) - hur du lägger till en komponent dynamiskt när sidan har lästs in.
* [Grundläggande om Rich Text Editor](rte.md) - hur du anpassar det RTF-gränssnitt som medlemmarna får för att publicera innehåll.

### IDE {#ide}

* [Använder Maven för Communities](maven.md) - så här tar du med Communities API jar.
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.
