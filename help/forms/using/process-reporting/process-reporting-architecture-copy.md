---
title: Hur processrapportering fungerar
seo-title: Hur processrapportering fungerar
description: Beskrivning av de tjänster som utgör AEM Forms on JEE Process Reporting och en introduktion till gränssnittet för processrapportering
seo-description: Beskrivning av de tjänster som utgör AEM Forms on JEE Process Reporting och en introduktion till gränssnittet för processrapportering
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hur processrapportering fungerar {#how-process-reporting-works}

Processrapportering är rapporteringsmodulen för AEM Forms on JEE.

Med Process Reporting kan du köra rapporter om AEM Forms-processer och -uppgifter.

Processrapportering använder den inbäddade Process Reporting-databasen för att publicera formulärdata. Sedan används dessa data för att köra rapporter.

Processrapportering består av följande moduler:

* [ProcessDataPublisher-tjänst](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [Tjänsten ProcessDataStorage](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi-tjänst](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [Frågedataserver](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Användargränssnittet för processrapportering](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Processrapporteringsarkitektur {#process-reporting-architecture-br}

![processrapportarkitektur](assets/processreportingarchitecture.png)

## Processrapporteringsmoduler {#process-reporting-modules}

### ProcessDataPublisher-tjänst {#processdatapublisher-service-br}

ProcessDataPublisher-servern körs regelbundet i AEM Forms-databasen och extraherar de data som har ändrats sedan den senaste körningen av tjänsten. Sedan publiceras data till datalagringstjänsten för processdata.

Mer information om hur du konfigurerar tjänsten finns i [Konfigurera tjänsten](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)ProcessDataPublisher.

### Tjänsten ProcessDataStorageProvider {#processdatastorageprovider-service-br}

ProcessDataStorageProvider-tjänsten tar emot processdata från ProcessDataPublisher-tjänsten och sparar data i Process Reporting-databasen.

Mer information om hur du konfigurerar tjänsten finns i [Konfigurera tjänsten](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)ProcessDataStorageProvider.

### OSGi-tjänst {#osgi-service-br}

QueryDataServlet använder den här tjänsten för att hämta rapportdata från Process Reporting-databasen.

### Tjänsten QueryDataServlet {#querydataservlet-service-br}

Tjänsten QueryDataServlet accepterar frågor från användargränssnittet för processrapportering.

Tjänsten använder sedan OSGi-tjänster för att hämta relevanta rapporteringsdata, bearbetar data och returnerar data till användargränssnittet.

### Användargränssnittet för processrapportering {#process-reporting-user-interface-br}

Användargränssnittet Process Reporting är ett webbläsarbaserat gränssnitt. Du använder det här gränssnittet för att visa process- och uppgiftsinformation som publiceras från AEM Forms-databasen.

### Tjänsten QueryDataServlet {#querydataservlet-service-br-1}

Tjänsten QueryDataServlet accepterar frågor från användargränssnittet för processrapportering.

Tjänsten använder sedan OSGi-tjänster för att hämta relevanta rapporteringsdata, bearbetar data och returnerar data till användargränssnittet.

### Anpassade rapporter {#custom-reports-br}

Du kan skapa egna anpassade rapporter och visa dessa rapporter på fliken Anpassade rapporter i användargränssnittet för processrapportering.

Anvisningar om hur du skapar en anpassad rapport finns i Skapa en anpassad rapport i artikeln [Anpassade rapporter i processrapportering](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
