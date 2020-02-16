---
title: AEM Forms Workspace-arkitektur
seo-title: AEM Forms Workspace-arkitektur
description: Konceptuell information och översikt över arkitekturen för arbetsytan i LiveCycle AEM Forms.
seo-description: Konceptuell information och översikt över arkitekturen för arbetsytan i LiveCycle AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Forms Workspace-arkitektur {#aem-forms-workspace-architecture}

Arbetsytan i AEM Forms är ett webbprogram med CRX™ som värd. När arbetsytan öppnas i en webbläsare öppnas en CRX-resurs och programmet återges som en HTML-sida i webbläsaren.

Programmet får åtkomst till AEM Forms-servern på REST-slutpunkter för att göra följande:

* Hämta användaruppgifter, processstartpunkter, processhistorik och användarinformation
* Utför åtgärd för uppgifter
* Fråga uppgifter i databasen
* Uppdatera användarinställningar med mera

AEM Forms-servern har åtkomst till AEM Forms-databasen via JDBC. Databasen innehåller uppgifter, processer och instanser, användare och relaterad information.

Arbetsytan i AEM Forms är utformad för modulära JavaScript™-komponenter som kan anpassas individuellt och återanvändas i andra webbprogram. Komponenterna baseras på BackBone, som är ett JavaScript-bibliotek som ger struktur åt webbprogram. En detaljerad artikel som beskriver hur komponenter samverkar med BackBone finns [här](/help/forms/using/backbone-interaction.md). Hur komponenterna i mappstrukturen för CRX är organiserade beskrivs i [den här](/help/forms/using/folder-structure.md) artikeln.

Paket som levereras för AEM Forms-arbetsytan:

* `adobe-lc-workspace-pkg-<version>.zip`: Det är ett CRX-paket, dvs. det kan distribueras i CRX med hjälp av pakethanteraren.
* `adobe-lc-workspace-<version>-src.zip`: Det är ett arkiv som innehåller fullständig kod för arbetsytan i AEM Forms och skript för att skapa distributionspaketen Ship, Debug och Dev.

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
