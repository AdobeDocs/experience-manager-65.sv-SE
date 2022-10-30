---
title: Integrering med Adobe Sign | Hantera användardata
seo-title: Integration with Adobe Sign | Handling user data
description: Integrering med Adobe Sign | Hantera användardata
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Integrering med Adobe Sign | Hantera användardata {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integrerar med[!DNL  Adobe Sign] för att möjliggöra arbetsflöden för e-signaturer i anpassningsbara formulär för att bearbeta formulär eller avtal för arbetsflöden för juridik, försäljning, lön och personalhantering. Det möjliggör signering för en eller flera användare, sekventiella och samtidiga signeringsarbetsflöden, signering av formulär som anonyma eller inloggade användare samt flera sätt att autentisera användare.

När en signerare eller flera signerare signerar och skickar ett adaptivt formulär [!DNL Adobe Sign] avtal skapas som innehåller information om signerare.

Mer information om [!DNL AEM Forms] integrering med [!DNL Adobe Sign], se [Använda Adobe Sign i en adaptiv form](/help/forms/using/working-with-adobe-sign.md).

## Användardata och datalager {#data}

[!DNL Adobe Sign] anpassningsbara formulär innehåller information om signerare och kan innehålla andra användardata som samlats in med det anpassningsbara formuläret. The [!DNL Adobe Sign] sparar användardata med signaturen i avtalet. Avtalet sparas på [!DNL Adobe Sign] server konfigurerad i [!DNL AEM Forms] molntjänster. Om det adaptiva formuläret dessutom är konfigurerat att använda Forms Portal-åtgärden, sparas avtalsdata i formulärportalens datalager tillsammans med formulärdata.

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Användardata samlas in i avtalet men sparas inte i någon av tjänsttabellerna. [!DNL Adobe Sign] gör att administratörer kan göra egna val när det gäller att hantera data som de har kontroll över i tjänsten. Sekretessadministratörer på [!DNL Adobe Sign] kan visa eller ta bort avtal baserat på e-postadressen till en begärande.

[!DNL Adobe Sign] erbjuder ett webbprogram som gör det möjligt att söka efter avtal av deltagare och vid behov ta bort dem. Mer information finns i [Adobe Sign - funktion: Ta bort användarinformation](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Avtalsdata för adaptiva formulär som har konfigurerats att använda Forms Portal-åtgärden för att skicka sparas också i datalagret för formulärportalen. Information om hur du får åtkomst till och tar bort data från formulärportalens datalager finns i [Forms portal | Hantera användardata](/help/forms/using/forms-portal-handling-user-data.md).
