---
title: Integrering med Adobe Sign | Hantera användardata
description: AEM Forms integrerar Adobe Sign för e-signaturer i anpassningsbara formulär. Det har stöd för flera signeringsalternativ för olika arbetsflöden.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Integrering med Adobe Sign | Hantera användardata {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integrerar med[!DNL  Adobe Sign] för att möjliggöra arbetsflöden för e-signaturer i anpassningsbara formulär för att bearbeta formulär eller avtal för arbetsflöden för juridik, försäljning, lön och personalhantering. Det möjliggör signering för en eller flera användare, sekventiella och samtidiga signeringsarbetsflöden, signering av formulär som anonyma eller inloggade användare samt flera sätt att autentisera användare.

När en signerare eller flera signerare signerar och skickar ett adaptivt formulär [!DNL Adobe Sign] avtal skapas som innehåller information om signerare.

Mer information om [!DNL AEM Forms] integrering med [!DNL Adobe Sign], se [Använda Adobe Sign i en adaptiv form](/help/forms/using/working-with-adobe-sign.md).

## Användardata och datalager {#data}

[!DNL Adobe Sign] anpassningsbara formulär innehåller information om signerare och kan innehålla andra användardata som samlats in med det anpassningsbara formuläret. The [!DNL Adobe Sign] sparar användardata med signaturen i avtalet. Avtalet sparas på en [!DNL Adobe Sign] server konfigurerad i [!DNL AEM Forms] molntjänster. Om det adaptiva formuläret dessutom är konfigurerat att använda Forms Portal-åtgärden, sparas avtalsdata i Forms Portals datalager tillsammans med formulärdata.

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Användardata samlas in i avtalet men sparas inte i någon av tjänsttabellerna. [!DNL Adobe Sign] gör att administratörer kan göra egna val för att hantera de data som de styr i tjänsten. Sekretessadministratörer på [!DNL Adobe Sign] kan visa eller ta bort avtal baserat på e-postadressen till en begärande.

[!DNL Adobe Sign] erbjuder ett webbprogram som gör det möjligt att söka efter avtal av deltagare och vid behov ta bort dem. Mer information finns i [Adobe Sign - funktion: Ta bort användarinformation](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Avtalsdata för adaptiva formulär som har konfigurerats att använda Forms Portal-åtgärden för att skicka sparas också i Forms Portal-datalagret. Information om hur du får åtkomst till och tar bort data från Forms Portal-datalagret finns i [Forms Portal | Hantera användardata](/help/forms/using/forms-portal-handling-user-data.md).
