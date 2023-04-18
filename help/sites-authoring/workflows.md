---
title: Arbeta med arbetsflöden
description: Med arbetsflöden i Adobe Experience Manager kan du automatisera en serie steg som utförs på en sida eller en resurs.
uuid: c4442d2a-c6b0-49d4-a1ce-384017c45bf0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 7cb99618-d903-4cfb-b0d9-b23d189f6e78
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Arbeta med arbetsflöden{#working-with-workflows}

AEM arbetsflöden gör att du kan automatisera en serie steg som utförs på (en eller flera) sidor och/eller resurser.

Vid publicering måste till exempel en redigerare granska innehållet innan en webbplatsadministratör aktiverar sidan. Ett arbetsflöde som automatiserar det här exemplet meddelar varje deltagare när det är dags att utföra det arbete de behöver:

1. Författaren tillämpar arbetsflödet på sidan.
1. Redigeraren får ett arbetsobjekt som anger att de måste granska sidinnehållet. När de är klara anger de att deras arbetsuppgifter är slutförda.
1. Webbplatsadministratören får sedan ett arbetsobjekt som begär att sidan aktiveras. När de är klara anger de att deras arbetsuppgifter är slutförda.

Vanligtvis:

* Innehållsförfattare använder arbetsflöden både på sidor och i arbetsflöden.
* De arbetsflöden du använder är specifika för organisationens affärsprocesser.

Följande sidor omfattar:

* [Använda arbetsflöden på sidor](/help/sites-authoring/workflows-applying.md)
* [Delta i arbetsflöden](/help/sites-authoring/workflows-participating.md)
