---
title: Hantera PreferencesNodes programmatiskt
seo-title: Programmatically managing the PreferencesNodes
description: Använd Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.
seo-description: Use the Preferences Manager Service API (Java) to programmatically manage the Preferences Nodes.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Hantera inställningsnoderna programmatiskt {#programmatically-managing-the-preferencesnodes}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

I det här avsnittet beskrivs hur du kan använda Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.

Du kan ändra konfigurationsinställningarna manuellt från administratörsgränssnittet. Om du vill ändra alternativen går du till `Home>Settings>User Management> Configuration>Manual Configuration`. Importera `config.xml` när du har gjort ändringarna kommer du att märka att alla ändringar förutom ändringar som gjorts på noden `/Adobe/Adobe Experience Manager Forms/Config/UM persist` är vilse. Förhandsgranskningen av Import och export av användarhantering stöder inte ändring av konfigurationsinställningar för andra komponenter. Nu kan dessa ändringar göras med `PreferencesManagerServiceClient` API:er.

**Sammanfattning av steg** Så här hanterar du noderna i Inställningar programmatiskt:

1. Inkludera projektfiler.
1. Skapa en PreferencesManagerService-klient
1. Anropa lämpliga roll- eller behörighetsåtgärder

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PreferencesManagerService-klient**

Innan du programmässigt kan utföra en PreferencesManagerService-åtgärd måste du skapa en PreferencesManagerService-klient. Med Java-API:t uppnås detta genom att ett PreferencesManagerServiceClient-objekt skapas.

**Anropa lämpliga roll- eller behörighetsåtgärder**

När du har skapat tjänstklienten kan du sedan anropa Preferences Manager-åtgärderna. Med tjänstklienten kan du läsa och ange behörigheter.
