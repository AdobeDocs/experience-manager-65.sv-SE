---
title: Distribuera AEM Forms-app
seo-title: Distribuera AEM Forms-app
description: Använd MDM (Mobile Device Management) för storskalig driftsättning av appar på mobila enheter.
seo-description: Använd MDM (Mobile Device Management) för storskalig driftsättning av appar på mobila enheter.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Distribuera AEM Forms-app {#distribute-aem-forms-app}

MDM (Mobile Device Management) möjliggör storskalig driftsättning av appar på mobila enheter.

>[!NOTE]
>
>Distributionen gäller endast iOS- och Android-enheter.

## De viktigaste funktionerna i MDM-lösningar: {#main-features-generally-provided-by-mdm-solutions}

* Aktivera enhetsregistrering i företagsmiljön
* Tillåt konfiguration och uppdatering av enhetsinställningar
* Säkerställ regelefterlevnaden.
* Säker mobil åtkomst till företagsresurser

En MDM-lösning tillsammans med hantering av mobilappar gör att du kan hantera interna, offentliga och köpta appar på företagets mobila enheter.

MDM-administratören kan överföra både ipa- och apk-filer till MDM-servern och styra vilka användare som kan komma åt ipa- eller apk-filerna. Administratören kan också styra profilinställningarna för respektive program.

## Profilinställningar som påverkar AEM Forms-appen {#profile-settings-affecting-the-aem-forms-app-br}

Följande profilinställningar på enheten påverkar hur AEM Forms-appen fungerar på din enhet:

* **Tillåt användning av** kameran i avsnittet  **Device** function

Om du inaktiverar **Tillåt användning av kamera** fungerar inte kamerafunktionen i [fotoanteckningen](/help/forms/using/add-attachments.md). Du måste aktivera det här alternativet om du vill använda kameran i appen.

* **Kräv lösenord för** enheten i avsnittet Lösenordspolicyer

Om du vill aktivera **kryptering av programdata** rekommenderar vi att du aktiverar **lösenordet** på enheten. Om lösenordet inte har angetts på enheten krypteras inte programdata som lagras på enheten.
