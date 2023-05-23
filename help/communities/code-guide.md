---
title: Riktlinjer för kodning
seo-title: Coding Guidelines
description: Användarforum, tips och tricks
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Riktlinjer för kodning {#coding-guidelines}

## Riktlinjer, tips och tricks {#guidelines-tips-and-tricks}

Arbetet med AEM Communities har utvecklats från att vara starkt beroende av Java Server Pages till flexibilitet när det gäller valet av skriptspråk där affärslogik, format och sidinnehåll skiljer sig från varandra.

Ytterligare flexibilitet när det gäller att arbeta med användargenererat innehåll (UGC) är via API:t SocialResourceProvider, som eliminerar behovet av att vara medveten om vilka [SRP](srp.md) för distributionen.

Nedan följer olika riktlinjer för kodning och metodtips för AEM Communities-utvecklare:

### Code {#code}

* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - hur du undviker att skriva ett program som bara fungerar när UGC lagras i JCR (JSRP).
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.
* [Namnkonventioner](naming-conventions.md) - namnkonventioner för anpassade Java-klasser.

### Skript {#scripts}

* [Komponenter för sidoinläsning av communities](sideloading.md) - hur du lägger till en komponent dynamiskt när sidan har lästs in.
* [Grundläggande om Rich Text Editor](rte.md) - Anpassa det RTF-gränssnitt som medlemmarna får för att publicera innehåll.

### IDE {#ide}

* [Använda Maven for Communities](maven.md) - hur du tar med Communities API jar.
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.
