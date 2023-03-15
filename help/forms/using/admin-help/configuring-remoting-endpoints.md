---
title: Konfigurerar fjärrslutpunkter
seo-title: Configuring Remoting endpoints
description: Lär dig hur du konfigurerar fjärrslutpunkter.
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Konfigurerar fjärrslutpunkter {#configuring-remoting-endpoints}

En fjärrslutpunkt gör att ett program som skapats med Flex kan anropa tjänsten med hjälp av (borttaget för AEM formulär) AEM form Remoting. En fjärrslutpunkt skapas automatiskt för varje aktiverad tjänst. Ett Flex-mål som har samma namn som slutpunkten skapas, och Flex-klienter kan skapa fjärrobjekt som pekar på det här målet för att anropa åtgärder på den aktuella tjänsten.

## Tar bort slutpunktsinställningar {#remoting-endpoint-settings}

**Autentiseringsmetod för Flex-klient:** Bestämmer vilken typ av svar som servern skickar tillbaka till klienten när den anropade tjänsten är säkerhetsaktiverad, den anropade åtgärden inte stöder anonyma anrop och klienten skickar antingen inga eller ogiltiga autentiseringsuppgifter.
