---
title: AEM Forms Workspace Architecture
seo-title: AEM Forms Workspace Architecture
description: Konceptuell information och översikt över arkitekturen för arbetsytan i LiveCycle AEM Forms.
seo-description: Conceptual information and overview of the architecture of LiveCycle AEM Forms workspace.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# AEM Forms Workspace Architecture {#aem-forms-workspace-architecture}

AEM Forms arbetsyta är ett webbprogram som finns på CRX™. När arbetsytan öppnas i en webbläsare öppnas en CRX-resurs och programmet återges som HTML i webbläsaren.

Programmet får åtkomst till AEM Forms-servern på REST-slutpunkter för att göra följande:

* Hämta användaruppgifter, processstartpunkter, processhistorik och användarinformation
* Utför åtgärd för uppgifter
* Fråga uppgifter i databasen
* Uppdatera användarinställningar med mera

AEM Forms-servern har åtkomst till AEM Forms-databasen via JDBC. Databasen innehåller uppgifter, processer och instanser, användare och relaterad information.

AEM Forms arbetsyta är utformad i modulära JavaScript™-komponenter som kan anpassas individuellt och återanvändas i andra webbprogram. Komponenterna baseras på BackBone, som är ett JavaScript-bibliotek som ger struktur åt webbprogram. En detaljerad artikel som beskriver hur komponenter samverkar med BackBone är [här](/help/forms/using/backbone-interaction.md). Hur komponenterna i mappstrukturen för CRX är organiserade beskrivs i [this](/help/forms/using/folder-structure.md) artikel.

Paket för AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: Det är ett CRX-paket, dvs. det kan distribueras i CRX med hjälp av pakethanteraren.
* `adobe-lc-workspace-<version>-src.zip`: Det är ett arkiv som innehåller fullständig kod för AEM Forms arbetsyta och skript för att skapa distributionspaketen Ship, Debug och Dev.
