---
title: Konfigurerar fjärrslutpunkter
seo-title: Konfigurerar fjärrslutpunkter
description: Lär dig hur du konfigurerar fjärrslutpunkter.
seo-description: Lär dig hur du konfigurerar fjärrslutpunkter.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurerar fjärrslutpunkter {#configuring-remoting-endpoints}

En slutpunkt för fjärrhantering gör att ett program som skapats med Flex kan anropa tjänsten med hjälp av (borttaget för AEM-formulär) AEM-formulärborttagning. En fjärrslutpunkt skapas automatiskt för varje aktiverad tjänst. Ett Flex-mål som har samma namn som slutpunkten skapas, och Flex-klienter kan skapa fjärrobjekt som pekar på det här målet för att anropa åtgärder på den relevanta tjänsten.

## Tar bort slutpunktsinställningar {#remoting-endpoint-settings}

**** Autentiseringsmetod för Flex-klient: Bestämmer vilken typ av svar som servern skickar tillbaka till klienten när den anropade tjänsten är säkerhetsaktiverad, den anropade åtgärden inte stöder anonyma anrop och klienten skickar antingen inga eller ogiltiga autentiseringsuppgifter.
