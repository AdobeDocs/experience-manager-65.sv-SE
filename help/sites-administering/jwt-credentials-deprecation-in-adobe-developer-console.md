---
title: Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console
description: Läs om hur borttagning av JWT-inloggningsuppgifter påverkar AEM i Adobe Developer Console
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM som en molntjänst bör referera till [den jämförbara artikeln för AEMaaCS-versionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=sv-SE) för mer information.

Adobe-kunder använder [Adobe Developer Console](https://developer.adobe.com/console) för att generera autentiseringsuppgifter som möjliggör åtkomst till olika API:er. Kunderna väljer mellan olika typer av autentiseringsuppgifter, från OAuth Server-to-Server till Single-Page App. En av dessa autentiseringstyper, JWT-autentiseringsuppgifter (Service Account), har ersatts med autentiseringsuppgifterna för OAuth Server-till-Server. Det går inte att skapa nya JWT-referenser (Service Account) den 3 juni 2024 eller senare, och befintliga JWT-autentiseringsuppgifter fungerar inte den 27 januari 2025 eller senare. Du kan [läsa om borttagningen](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

I den här artikeln finns ytterligare information om hur Adobe Experience Manager (AEM) 6.5-kunder bör hantera borttagningen.

Det viktigaste är att AEM nu har stöd för de nya autentiseringsuppgifterna för OAuth Server-till-Server för AEM. Du kan ha fått ett e-postmeddelande med instruktioner om hur du migrerar dina JWT-autentiseringsuppgifter. Migreringen kan nu göras.

I avsnitten nedan listas de scenarier där kunderna måste (eller i vissa fall inte måste) ersätta sina JWT-referenser (Service Account) med OAuth Server-to-Server-autentiseringsuppgifter, som nu AEM stöder dem. [Läs hur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrerar autentiseringsuppgifterna.

## Integrera AEM med andra Adobe-lösningar {#integrating-aem-with-other-adobe-solutions}

**Åtgärd**: Migrera konfigurationen som AEM stöder nu OAuth-autentiseringsuppgifter.

**Relevanta AEM**: Adobe Managed Services (Service Pack 21 och senare).

AEM använder AEM för att konfigurera integreringar med alla andra Adobe-lösningar. Exempel: Adobe Target, Adobe Analytics med flera.

![Integrera AEM med andra lösningar](/help/sites-administering/assets/jwt-deprecation.png)

Se [Konfigurera IMS-integreringar för AEM](/help/sites-administering/setting-up-ims-integrations-for-aem.md) för mer information om hur du gör:

* skapa konfigurationer med OAuth-autentiseringsuppgifter
* migrera konfigurationer som har skapats med JWT-autentiseringsuppgifter för att använda OAuth-autentiseringsuppgifter

## Cloud Manager API:er {#cloud-manager-apis}

**Åtgärd**: Bekräfta när dessa kan migreras från JWT till OAuth-autentiseringsuppgifter.

**Relevanta AEM**: Adobe Managed Services (Service Pack 21 och senare).

Kunder skapar Adobe Developer Console-projekt så att de kan anropa [Cloud Manager API:er](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Autentiseringsuppgifterna i Adobe Developer-projektet ska migreras till autentiseringstypen OAuth Server-to-Server innan de inaktuella JWT-autentiseringsuppgifterna går ut i januari 2025.
