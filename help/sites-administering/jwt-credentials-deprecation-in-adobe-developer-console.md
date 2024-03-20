---
title: Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console
description: Läs om hur borttagning av JWT-autentiseringsuppgifter påverkar AEM i Adobe Developer Console
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM som en molntjänst bör referera till [den här artikeln](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) för mer information.

Adobe-kunder använder [Adobe Developer Console](https://developer.adobe.com/console) för att generera autentiseringsuppgifter som möjliggör åtkomst till olika API:er. Kunderna väljer mellan olika typer av autentiseringsuppgifter, från OAuth Server-to-Server till Single-Page App. En av dessa autentiseringstyper, JWT-autentiseringsuppgifter (Service Account), har ersatts med autentiseringsuppgifterna för OAuth Server-till-Server. Det går inte att skapa nya JWT-autentiseringsuppgifter den 1 maj 2024 eller senare, och befintliga JWT-autentiseringsuppgifter fungerar inte den 1 januari 2025 eller senare. Du kan [läs om borttagningen](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

I den här artikeln finns ytterligare information om hur AEM 6.5-kunder ska hantera borttagningen.

Den största takten i nuläget är att AEM funktioner ännu inte stöder de nya autentiseringsuppgifterna för OAuth Server-till-Server. Support kommer snart - i mitten av april 2024 genom ett särskilt kompatibilitetspaket som installeras för AEM 6.5, om du kör den senaste Service Pack 20 eller tidigare (Service Pack 21 eller senare kommer att inkludera den automatiskt). Du kan ha fått ett e-postmeddelande med instruktioner om hur du migrerar JWT-inloggningsuppgifterna, men du kan vara säker på att du kan och bör hålla kvar när du migrerar autentiseringsuppgifterna tills AEM har stöd för den nya autentiseringstypen OAuth Server-till-Server.

I avsnitten nedan listas de scenarier där kunderna måste (eller i vissa fall inte måste) ersätta sina JWT-referenser (Service Account) med OAuth Server-to-Server-autentiseringsuppgifter, när AEM har stöd för dem i mitten av april. [Läs om](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) för att ersätta inloggningsuppgifterna i framtiden.

## Integrera AEM med andra Adobe-lösningar {#integrating-aem-with-other-adobe-solutions}

**Åtgärd**: Vänta tills efter mitten av april 2024 när AEM stöder det.

**Relevanta AEM**: Adobe Managed Services (Service Pack 20 och tidigare).


AEM använder användargränssnittet AEM Author för att konfigurera integreringar med alla andra Adobe-lösningar. Exempel: Adobe Target, Adobe Analytics, Adobe Launch, AFCS och många fler.

![Integrera AEM med andra lösningar](/help/sites-administering/assets/jwt-deprecation.png)

Här är några exempel [instruktionerna](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) för att konfigurera integrationen med Adobe Target. API-nyckeln i [Slutför IMS-konfigurationen i AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) -avsnittet ska migreras till autentiseringstypen OAuth Server-to-Server, när AEM har stöd för dessa autentiseringsuppgifter i mitten av april. Instruktionerna kommer att uppdateras i mitten av april så att du kan använda de nya autentiseringsuppgifterna för OAuth Server-till-Server.

## API:er för Cloud Manager {#cloud-manager-apis}

**Åtgärd**: Vänta tills efter mitten av april 2024 när AEM stöder det.

**Relevanta AEM**: Adobe Managed Services (Service Pack 20 och tidigare).

Kunder skapar Adobe Developer Console-projekt så att de kan starta [API:er för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Autentiseringsuppgifterna i Adobe Developer-projektet ska migreras till autentiseringstypen OAuth Server-to-Server när AEM och Cloud Manager har stöd för det.
