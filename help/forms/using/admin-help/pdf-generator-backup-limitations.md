---
title: PDF Generator begränsningar för säkerhetskopiering
description: Läs mer om begränsningar för säkerhetskopiering i PDF Generator. Den temporära katalog som PDF Generator använder kan inte säkerhetskopieras eftersom den raderar innehållet i angivna intervall.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# PDF Generator begränsningar för säkerhetskopiering {#pdf-generator-backup-limitations}

Den tillfälliga katalog som PDF Generator använder för att konvertera filer kan inte säkerhetskopieras. Även om tjänsten återställs korrekt kan data gå förlorade eftersom PDF Generator granskar och rensar innehållet i den tillfälliga katalogen med angivna intervall.
