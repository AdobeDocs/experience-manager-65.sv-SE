---
title: AEM Forms Workspace Architecture
seo-title: AEM Forms Workspace Architecture
description: Konceptuell information och översikt över arkitekturen för arbetsytan i LiveCycle AEM Forms.
seo-description: Konceptuell information och översikt över arkitekturen för arbetsytan i LiveCycle AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# AEM Forms Workspace Architecture {#aem-forms-workspace-architecture}

AEM Forms arbetsyta är ett webbprogram som finns på CRX™. När arbetsytan öppnas i en webbläsare öppnas en CRX-resurs och programmet återges som en HTML-sida i webbläsaren.

Programmet får åtkomst till AEM Forms-servern på REST-slutpunkter för att göra följande:

* Hämta användaruppgifter, processstartpunkter, processhistorik och användarinformation
* Utför åtgärd för uppgifter
* Fråga uppgifter i databasen
* Uppdatera användarinställningar med mera

AEM Forms-servern har åtkomst till AEM Forms-databasen via JDBC. Databasen innehåller uppgifter, processer och instanser, användare och relaterad information.

AEM Forms arbetsyta är utformad i modulära JavaScript™-komponenter som kan anpassas individuellt och återanvändas i andra webbprogram. Komponenterna baseras på BackBone, som är ett JavaScript-bibliotek som ger struktur åt webbprogram. En detaljerad artikel som beskriver interaktionen mellan komponenter med BackBone är [här](/help/forms/using/backbone-interaction.md). Komponenternas struktur i mappstrukturen för CRX beskrivs i [den här](/help/forms/using/folder-structure.md) artikeln.

Paket för AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: Det är ett CRX-paket, dvs. det kan distribueras i CRX med hjälp av pakethanteraren.
* `adobe-lc-workspace-<version>-src.zip`: Det är ett arkiv som innehåller fullständig kod för AEM Forms arbetsyta och skript för att skapa distributionspaketen Ship, Debug och Dev.
