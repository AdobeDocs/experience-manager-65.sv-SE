---
title: Integrering med Adobe Sign| Hantera användardata
seo-title: Integrering med Adobe Sign| Hantera användardata
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integrering med Adobe Sign| Hantera användardata {#integration-with-adobe-sign-handling-user-data}

AEM Forms kan integreras med Adobe Sign för att möjliggöra e-signaturarbetsflöden i adaptiva formulär för att bearbeta formulär eller avtal för arbetsflöden inom juridik, försäljning, lön och personalhantering. Det möjliggör signering för en eller flera användare, sekventiella och samtidiga signeringsarbetsflöden, signering av formulär som anonyma eller inloggade användare samt flera sätt att autentisera användare.

När en eller flera signerare signerar och skickar ett anpassat formulär skapas ett Adobe Sign-avtal som innehåller information om signerarna.

Mer information om AEM Forms-integrering med Adobe Sign finns i [Använda Adobe Sign i ett anpassningsbart formulär](/help/forms/using/working-with-adobe-sign.md).

## Användardata och datalager {#data}

Anpassningsbart formulär aktiverat för Adobe Sign innehåller information om signerare och kan innehålla andra användardata som samlats in med det adaptiva formuläret. Adobe Sign-tjänsten sparar användardata med signaturen i avtalet. Avtalet sparas på Adobe Sign-servern som är konfigurerad i molntjänsterna för AEM Forms. Om det adaptiva formuläret dessutom är konfigurerat att använda Forms Portal-åtgärden, sparas avtalsdata i formulärportalens datalager tillsammans med formulärdata.

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

Användardata samlas in i avtalet men sparas inte i någon av tjänsttabellerna. Med Adobe Sign kan administratörer själva välja hur de vill hantera data som de har kontroll över i tjänsten. Sekretessadministratörer för Adobe Sign-tjänsten kan lista eller ta bort avtal baserat på e-postadressen till en begärande.

Adobe Sign erbjuder ett webbprogram som gör att deltagare kan söka efter avtal och vid behov ta bort dem. Mer information finns i [Adobe Sign - funktion: Ta bort användarinformation](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Avtalsdata för adaptiva formulär som har konfigurerats att använda Forms Portal-åtgärden för att skicka sparas också i datalagret för formulärportalen. Information om hur du får åtkomst till och tar bort data från formulärportalens datalager finns i [Formulärportalen| Hantera användardata](/help/forms/using/forms-portal-handling-user-data.md).
