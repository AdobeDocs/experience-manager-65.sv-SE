---
title: Hantera PreferencesNodes programmatiskt
description: Använd Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Hantera inställningsnoderna programmatiskt {#programmatically-managing-the-preferencesnodes}

**Exempel och exempel i det här dokumentet gäller endast för AEM Forms i JEE-miljö.**

I det här avsnittet beskrivs hur du kan använda Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.

Du kan ändra konfigurationsinställningarna manuellt från administratörsgränssnittet. Navigera till `Home>Settings>User Management> Configuration>Manual Configuration` om du vill ändra alternativen. Importera `config.xml` när du har gjort ändringarna kommer du att märka att alla ändringar förutom de som har gjorts på noden `/Adobe/Adobe Experience Manager Forms/Config/UM persist` går förlorade. Förhandsgranskningen av Import och export av användarhantering stöder inte ändring av konfigurationsinställningar för andra komponenter. Dessa ändringar kan nu göras med `PreferencesManagerServiceClient` API:er.

**Sammanfattning av steg** Utför följande steg om du vill hantera noderna i Inställningar programmatiskt:

1. Inkludera projektfiler.
1. Skapa en PreferencesManagerService-klient
1. Anropa lämpliga roll- eller behörighetsåtgärder

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PreferencesManagerService-klient**

Innan du programmässigt kan utföra en PreferencesManagerService-åtgärd måste du skapa en PreferencesManagerService-klient. Med Java-API:t uppnås detta genom att ett PreferencesManagerServiceClient-objekt skapas.

**Anropa lämplig roll eller lämpliga behörighetsåtgärder**

När du har skapat tjänstklienten kan du sedan anropa Preferences Manager-åtgärderna. Med tjänstklienten kan du läsa och ange behörigheter.
