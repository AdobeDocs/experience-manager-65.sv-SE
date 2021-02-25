---
title: Hantera PreferencesNodes programmatiskt
seo-title: Hantera PreferencesNodes programmatiskt
description: Använd Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.
seo-description: Använd Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Hantera inställningsnoderna {#programmatically-managing-the-preferencesnodes} programmatiskt

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

I det här avsnittet beskrivs hur du kan använda Preferences Manager Service API (Java) för att programmässigt hantera Preferences Nodes.

Du kan ändra konfigurationsinställningarna manuellt från administratörsgränssnittet. Navigera till `Home>Settings>User Management> Configuration>Manual Configuration` om du vill ändra alternativen. Om du importerar `config.xml` efter att du har gjort ändringarna kommer du att märka att alla ändringar förutom de som har gjorts i noden `/Adobe/Adobe Experience Manager Forms/Config/UM persist` går förlorade. Förhandsgranskningen av Import och export av användarhantering stöder inte ändring av konfigurationsinställningar för andra komponenter. Dessa ändringar kan nu göras med hjälp av `PreferencesManagerServiceClient` API:er.

**Sammanfattning av** stegSå här hanterar du noderna i Inställningar programmatiskt:

1. Inkludera projektfiler.
1. Skapa en PreferencesManagerService-klient
1. Anropa lämpliga roll- eller behörighetsåtgärder

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en PreferencesManagerService-klient**

Innan du programmässigt kan utföra en PreferencesManagerService-åtgärd måste du skapa en PreferencesManagerService-klient. Med Java-API:t uppnås detta genom att ett PreferencesManagerServiceClient-objekt skapas.

**Anropa lämpliga roll- eller behörighetsåtgärder**

När du har skapat tjänstklienten kan du sedan anropa Preferences Manager-åtgärderna. Med tjänstklienten kan du läsa och ange behörigheter.
