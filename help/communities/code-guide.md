---
title: Riktlinjer för kodning
seo-title: Riktlinjer för kodning
description: Användarforum, tips och tricks
seo-description: Användarforum, tips och tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Riktlinjer för kodning {#coding-guidelines}

## Riktlinjer, tips och tricks {#guidelines-tips-and-tricks}

Arbetet med AEM Communities har utvecklats från att vara starkt beroende av Java Server Pages till flexibilitet när det gäller valet av skriptspråk där affärslogik, format och sidinnehåll skiljer sig från varandra.

Ytterligare flexibilitet när det gäller att arbeta med användargenererat innehåll (UGC) är via API:t SocialResourceProvider, som eliminerar behovet av att känna till vilket [SRP](srp.md) -alternativ som valdes för distributionen.

Nedan följer olika riktlinjer för kodning och god praxis för utvecklare av AEM Communities:

### Kod {#code}

* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - så undviker du att skriva ett program som bara fungerar när UGC lagras i JCR (JSRP).
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.
* [Namnkonventioner](naming-conventions.md) - namnkonventioner för anpassade Java-klasser.

### Skript {#scripts}

* [Inläsning av communitykomponenter](sideloading.md) - hur du lägger till en komponent dynamiskt när sidan har lästs in.
* [Grundläggande](rte.md) om Rich Text Editor - Hur man anpassar det RTF-gränssnitt som medlemmarna får för att publicera innehåll.

### IDE {#ide}

* [Använda Maven for Communities](maven.md) - How to include the Communities API jar.
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.

