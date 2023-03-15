---
title: Begränsningar för säkerhetskopiering i PDF Generator
seo-title: PDF Generator backup limitations
description: Läs mer om begränsningar för säkerhetskopiering i PDF Generator.
seo-description: Learn about PDF Generator backup limitations.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# Begränsningar för säkerhetskopiering i PDF Generator {#pdf-generator-backup-limitations}

Den temporära katalog som PDF Generator använder för att konvertera filer kan inte säkerhetskopieras. Även om tjänsten återställs korrekt kan data gå förlorade eftersom PDF Generator granskar och rensar innehållet i den tillfälliga katalogen med angivna intervall.
