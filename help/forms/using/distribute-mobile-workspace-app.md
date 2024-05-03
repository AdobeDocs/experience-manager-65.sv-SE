---
title: Distribuera AEM Forms-app
description: Använd MDM (Mobile Device Management) för storskalig driftsättning av appar på mobila enheter.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Distribuera AEM Forms-app {#distribute-aem-forms-app}

MDM (Mobile Device Management) möjliggör storskalig driftsättning av appar på mobila enheter.

>[!NOTE]
>
>Distributionen gäller endast iOS- och Android™-enheter.

## De viktigaste funktionerna i MDM-lösningar: {#main-features-generally-provided-by-mdm-solutions}

* Aktivera enhetsregistrering i företagsmiljön
* Tillåt konfiguration och uppdatering av enhetsinställningar
* Säkerställ regelefterlevnaden.
* Säker mobil åtkomst till företagsresurser

En MDM-lösning tillsammans med hantering av mobilappar gör att du kan hantera interna, offentliga och köpta appar på företagets mobila enheter.

MDM-administratören kan överföra både ipa- och apk-filer till MDM-servern och styra vilka användare som kan komma åt ipa- eller apk-filerna. Administratören kan också styra de profilinställningar som motsvarar respektive program.

## Profilinställningar som påverkar AEM Forms-programmet {#profile-settings-affecting-the-aem-forms-app-br}

Följande profilinställningar på enheten påverkar hur AEM Forms-appen fungerar på enheten:

* **Tillåt användning av kamera** i **Enhetsfunktioner** section

Om du inaktiverar **Tillåt användning av kamera**, kamerans funktion i [Fotografanteckning](/help/forms/using/add-attachments.md) fungerar inte. Aktivera det här alternativet om du vill använda kameran i appen.

* **Kräv lösenord på enheten** i avsnittet Lösenordspolicyer

Aktivera **kryptering av programdata** rekommenderar vi att du aktiverar **lösenord** på din enhet. Om lösenordet inte är inställt på enheten krypteras inte de programdata som lagras på enheten.
