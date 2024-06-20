---
title: Tröskelvärde för högsta antal öppna markörer i oraclets databas
description: Lär dig hur du konfigurerar ett maxvärde för öppna markörer i Oraclet.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Tröskelvärde för högsta antal öppna markörer i oraclets databas {#oracle-database-maximum-open-cursors-threshold}

Om du vill konfigurera ett maxvärde för öppna markörer i Oracle kanske du måste justera det här värdet till ett värde som passar ditt program. Det är uppenbart att under en måttlig belastning var de genomsnittliga öppna markörerna 2 700. Vi rekommenderar att du börjar med en övre gräns på 3 000. Mer information finns på [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
