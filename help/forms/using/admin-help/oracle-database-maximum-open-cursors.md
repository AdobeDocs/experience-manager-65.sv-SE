---
title: Tröskelvärde för högsta antal öppna markörer i oraclets databas
seo-title: Oracle database maximum open cursors threshold
description: Lär dig hur du konfigurerar ett maxvärde för öppna markörer i Oraclet.
seo-description: Learn about configuring a maximum value for open cursors in Oracle.
uuid: c1d20997-f853-4772-b1c6-8cea73221d0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d3565776-1b7d-498c-9840-b17f80170d9b
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# Tröskelvärde för högsta antal öppna markörer i oraclets databas {#oracle-database-maximum-open-cursors-threshold}

Om du vill konfigurera ett maxvärde för öppna markörer i Oracle kanske du måste justera det här värdet till ett värde som passar ditt program. Det är uppenbart att under en måttlig belastning var de genomsnittliga öppna markörerna 2 700. Vi rekommenderar att du börjar med en övre gräns på 3 000. Mer information finns på [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
