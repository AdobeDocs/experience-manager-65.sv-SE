---
title: Konfigurerar fjärrslutpunkter
description: Lär dig hur du konfigurerar fjärrslutpunkter. I det här dokumentet beskrivs hur du aktiverar program som skapats med Flex för att anropa tjänsten med hjälp av AEM Remoting.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# Konfigurerar fjärrslutpunkter {#configuring-remoting-endpoints}

En fjärrslutpunkt gör att ett program som skapats med Flex kan anropa tjänsten med hjälp av (borttaget för AEM formulär) AEM form Remoting. En fjärrslutpunkt skapas automatiskt för varje aktiverad tjänst. Ett Flex-mål som har samma namn som slutpunkten skapas, och Flex-klienter kan skapa fjärrobjekt som pekar på det här målet för att anropa åtgärder på den aktuella tjänsten.

## Tar bort slutpunktsinställningar {#remoting-endpoint-settings}

**Autentiseringsmetod för Flex-klient:** Bestämmer vilken typ av svar som servern skickar tillbaka till klienten när den anropade tjänsten är säkerhetsaktiverad, den anropade åtgärden inte stöder anonyma anrop och klienten skickar antingen inga eller ogiltiga autentiseringsuppgifter.
