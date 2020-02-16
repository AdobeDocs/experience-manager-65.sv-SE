---
title: AEM Foundation & Repository
description: Versionsinformation om Adobe Experience Manager 6.3 AEM Platform och Repository.
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM Foundation &amp; Repository{#aem-foundation-repository}

## Ändringslista {#list-of-changes}

### Databas {#repository}

* Grunden till Adobe Experience Manager 6.5 ligger bakom uppdaterade versioner av det OSGi-baserade ramverket (Apache Sling och Apache Felix) och Java Content Repository: Apache Jackrabbit Oak 1.10.2.
* Se [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) och [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) för en fullständig översikt över åtgärdade problem.

>[!CAUTION]
>
>* Den nya versionen av Oak Segment-taggen som finns sedan AEM 6.3 kräver en databasmigrering. Det här steget är obligatoriskt om du uppgraderar från en äldre version av tarMK eller vill växla den nya segmenttaggen från en annan typ av beständighet. Mer information om fördelarna med de nya segmenttjärna finns i Vanliga frågor och svar om [migrering till Oak Segment-tjära](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Java-stöd {#java-support}

* Nytt stöd för Java 11 samt Java 8 som redan stöds
* För optimala prestanda bör du åsidosätta GC-standardvärden med andra värden. Mer information finns i avsnittet [Installera och uppdatera](/help/sites-deploying/custom-standalone-install.md) .
* Underhållsuppdateringar för Java 11 och Java 8 kommer att distribueras av Adobe för kundanvändning i AEM-relaterade projekt, om de inte är allmänt tillgängliga från Oracle

### OSGI {#osgi}

* Tillagda OSGi-utfästelser och verktygsbibliotek för konverterare

### Projekt och arbetsflöden {#projects-and-workflows}

* Den nya redigeraren för arbetsflödesmodeller som introducerades i 6.4 har förbättrats så att den omfattar fler åtgärder som Kopiera och Publicera, Variabelstöd i arbetsflödessteg samt förbättrade OR- och AND-delningar.

### Sök {#searching}

* Sök i Oak har nu stöd för dynamiska aspekter. Filterfältet i resurssökningen visar till exempel det uppskattade resultatbeloppet.
* QueryBuilder utökades för att ge resultat med dynamiska aspekter

### Dokumentskydd {#security}

* Lösenordet har lagts till för administratörsanvändaren.

### Användargränssnitt {#user-interface}

Ett antal förbättringar har gjorts i användargränssnittet för att göra det mer produktivt och enklare att använda.

* I AEM 6.5 introduceras ett nytt användargränssnitt för behörighetshantering för användare och grupper som gör det enklare att visa och konfigurera hela uppsättningen behörigheter och begränsningar utan att behöva gå till CRXDE.
* Kolumnvyer läser nu bara in poster som är synliga på skärmen och som bara läses in mer när användaren börjar rulla. List- och kortvyn gjorde redan det sedan 6.0 (förbättrat i 6.4)
* Kolumnvyer innehåller nu arbetsflödesstatus för sidor/resurser när det är tillämpligt
* Åtgärden Markera allt är ett snabbt sätt att utföra en åtgärd med alla sidor/resurser i samma mapp
* Åtgärden Markera alla försöker utföra åtgärden på alla sidor/resurser, inte bara på vad som har lästs in. En varningsdialogruta visas om åtgärden inte har uppgraderats för att hantera gruppåtgärder

>[!CAUTION]
>
>* Adobe planerar inte att göra fler förbättringar av det klassiska användargränssnittet. AEM 6.5 innehåller det klassiska användargränssnittet, och kunder som uppgraderar från tidigare versioner kan fortsätta använda det som det är. Observera att Classic-användargränssnittet fortfarande stöds fullt ut när det är borttaget [Läs mer](/help/sites-deploying/ui-recommendations.md).
>



### Uppgradera {#upgrade}

* Uppgraderingsförfarandet är i stort sett detsamma i 6.5.
* Vi fortsätter att stödja funktionerna Bakåtkompatibilitet, utvärdering av uppgraderingskomplexitet och hållbar uppgradering som introducerades i 6.4. Det har gjorts versionsspecifika uppdateringar av dessa områden där det behövs.
* Pattern Detector har förenklats och det kommer att finnas ett paket som utvärderar uppgraderingar till 6.5 för de tillgängliga källversionerna.
* Mer information om uppgraderingsproceduren finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md) .

### Webbserver {#web-server}

* För Quickstart-distributionen används Eclipse Jetty 9.4.15 som servermotor (AEM 6.4 levererad med 9.3.22)

