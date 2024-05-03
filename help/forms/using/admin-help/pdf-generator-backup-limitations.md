---
title: PDF Generator begränsningar för säkerhetskopiering
description: Läs mer om begränsningar för säkerhetskopiering i PDF Generator. Den temporära katalog som PDF Generator använder kan inte säkerhetskopieras eftersom den raderar innehållet i angivna intervall.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# PDF Generator begränsningar för säkerhetskopiering {#pdf-generator-backup-limitations}

Den tillfälliga katalog som PDF Generator använder för att konvertera filer kan inte säkerhetskopieras. Även om tjänsten återställs korrekt kan data gå förlorade eftersom PDF Generator granskar och rensar innehållet i den tillfälliga katalogen med angivna intervall.
