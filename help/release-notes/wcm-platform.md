---
title: AEM Foundation och arkiv
description: Versionsinformation för Adobe Experience Manager plattform och databas.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# AEM Foundation och databas {#aem-foundation-repository}

## Lista över ändringar {#list-of-changes}

### Databas {#repository}

* Grunden till Adobe Experience Manager 6.5 bygger på uppdaterade versioner av det OSGi-baserade ramverket (Apache Sling och Apache Felix) och Java Content Repository: Apache Jackrabbit Oak 1.10.2.
* En översikt över åtgärdade problem finns i [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) och [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>Den nya versionen av Oak Segment-taggen som finns sedan AEM 6.3 kräver en databasmigrering. Det här steget är obligatoriskt om du uppgraderar från en äldre version av tarMK eller vill växla den nya segmenttaggen från en annan typ av beständighet. Mer information om fördelarna med de nya segmenttjärna finns i [Vanliga frågor och svar om migrering till Oak Segment-tjära](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

### Java-stöd {#java-support}

* Nytt stöd för Java 11 och Java 8 som redan stöds.
* För optimala prestanda bör du åsidosätta GC-standardvärden med andra värden. Mer information finns i avsnittet [Installera och uppdatera](/help/sites-deploying/custom-standalone-install.md).
* Underhållsuppdateringar för Java 11 och Java 8 distribueras av Adobe för kundanvändning i AEM projekt, när de inte är allmänt tillgängliga från Oracle.

### OSGI {#osgi}

* Tillagda OSGi Promises- och Converter-verktygsbibliotek.

### Projekt och arbetsflöden {#projects-and-workflows}

* Den nya redigeraren för arbetsflödesmodeller som introducerades i 6.4 har förbättrats så att den omfattar fler åtgärder som Kopiera och Publicera, Variabelstöd i arbetsflödessteg och förbättrad `OR`- och `AND`-delning.

### Sökning {#searching}

* Sök i Oak har nu stöd för dynamiska aspekter. Filterfältet i resurssökningen visar t.ex. den uppskattade mängden resultat.
* QueryBuilder utökades för att ge resultat med dynamiska aspekter.

### Dokumentskydd {#security}

* Lösenordet har lagts till för administratörsanvändaren.

### Användargränssnitt {#user-interface}

Ett antal förbättringar har gjorts i användargränssnittet för att göra det mer produktivt och enklare att använda.

* I AEM 6.5 introduceras ett nytt användargränssnitt för behörighetshantering för användare och grupper som gör det enklare att visa och konfigurera hela uppsättningen behörigheter och begränsningar utan att behöva gå till CRXDE.
* Kolumnvyer läser nu bara in poster som är synliga på skärmen och som bara läses in mer när användaren börjar rulla. List- och kortvyn gjorde redan det sedan 6.0 (förbättrat i 6.4).
* Kolumnvyer innehåller nu arbetsflödesstatus för sidor/resurser när det är tillämpligt.
* Åtgärden Markera alla är ett snabbt sätt att köra en åtgärd med alla sidor/resurser i samma mapp.
* Åtgärden Markera alla försöker utföra åtgärden på alla sidor/resurser, inte bara det som har lästs in. Om åtgärden inte har uppgraderats för att hantera gruppåtgärder visas en varning.

>[!CAUTION]
>
>Adobe kommer inte att göra fler förbättringar av det klassiska användargränssnittet. Experience Manager 6.5 innehåller Classic UI för bakåtkompatibilitet. Klassiskt användargränssnitt stöds inte fullt ut medan [Läs mer](/help/sites-deploying/ui-recommendations.md) är föråldrat.

### Uppgradera {#upgrade}

* Uppgraderingsförfarandet är i stort sett detsamma i 6.5.
* Vi fortsätter att stödja funktionerna Bakåtkompatibilitet, utvärdering av uppgraderingskomplexitet och hållbar uppgradering som introducerades i 6.4. Det har gjorts versionsspecifika uppdateringar av dessa områden där det behövs.
* Pattern Detector har förenklats och det kommer att finnas ett paket som utvärderar uppgraderingar till 6.5 för de tillgängliga källversionerna.
* Mer information om uppgraderingsproceduren finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md).

### Webbserver {#web-server}

* Vid QuickStart-distributionen används Eclipse Jetty 9.4.15 som serverkomponent (AEM 6.4 levererades med 9.3.22).
