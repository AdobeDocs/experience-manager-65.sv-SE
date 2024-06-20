---
title: Visa systeminformation
description: Lär dig hur du kan visa resursövervakningsdiagram och information om servern som kör AEM formulär.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Visa systeminformation {#view-system-information}

På fliken System visas resursövervakningsdiagram och information om servern som kör AEM formulär. Om du vill komma åt den här informationen klickar du på Hälsoövervakning i det övre högra hörnet på sidan i administrationskonsolen. Om du kör AEM formulär i en klustermiljö visas informationen för den nod som valts i serverlistan.

Om du vill spara den aktuella systeminformationen som en egenskapsfil klickar du på Spara.

I den högra rutan på fliken System visas grafiska representationer av följande information:

* Jobb- och arbetsräkningsobjekt
* Användning av heap och Allmän heap
* Användning utan heap och implementerad utan heap

Du kan dra pekaren längs tidslinjen för att hämta värden för en viss tidpunkt.

>[!NOTE]
>
>Diagramdata, serverinformationsvärden och klockslag uppdateras var 10:e minut. Informationen visas inte i realtid.

I den vänstra rutan på fliken System visas följande information om servern eller noden:

**Virtuell dator:** Java Virtual Machine-version (JVM) på servern.

**Leverantör av virtuell dator:** Tillverkare av JVM.

**Version för virtuell dator:** JVM-versionsnummer

**Datornamn:** Värdnamn för den server där AEM har installerats.

**Starttid:** Den tid, i timmar och minuter, som servern har körts.

**Just-in-time-kompilator:** Namnet på den kompilator som används.

**Kompileringstid:** Den tid som har ägnats åt kompileringen.

**Antal aktiva Threads:** Det totala antalet trådar som för närvarande finns i AEM.

**Antal Threads Peak:** Det största antalet livetrådar som någonsin spelats in i systemet.

**Antal inlästa klasser:** Antal klasser som har lästs in i JVM.

**Antal ej inlästa klasser:** Antal klasser som inte har lästs in från JVM.

**Minsta heap:** Den minsta stackmängden som användes.

**Maximal heap:** Den maximala stackmängden som användes.

**Operativsystemets namn:** Namnet på operativsystemet som körs på AEM Forms Server.

**Operativsystemsversion:** Versionsnummer för det operativsystem som körs på AEM Forms Server.

**Operativsystem:** Den operativsystemsarkitektur som JVM körs på.

**Antal processorer:** Antalet processorer i systemet.

**Argument för virtuell dator:** Argumentet som används av JVM.

**Klasssökväg:** Klasssökvägen som används av JVM.

**Bibliotekssökväg:** Bibliotekssökvägen som används av JVM.

**Startklasssökväg:** Den sökväg till startklassen som används av JVM.

**Programservertyp:** Typ av programserver som används för att köra AEM formulär.

**Programserverversion:** Versionsnummer för den programserver som används för att köra AEM formulär.

**Programserverleverantör:** Tillverkare av programservern som används för att köra AEM formulär.

**Installationsdatum:** Datum (i formatet åååå-mm-dd) när AEM har installerats.

**AEM:** Version av AEM som är installerad.

**Lappningsversion:** AEM formulärkorrigeringsnummer.

**Databasnamn:** Typ av databas som används av AEM formulär.

**Databasversion:** Versionsnummer för den databas som används av AEM formulär.

**Namn på databasenhet:** Namnet på den drivrutin som JVM använder för att ansluta till databasen.

**Databasdrivrutinsversion:** Den version av drivrutinen som JVM använder för att ansluta till databasen.

The **Spara** kan du spara den här systeminformationen i en egenskapsfil.
