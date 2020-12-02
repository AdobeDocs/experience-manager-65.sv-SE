---
title: Visa systeminformation
seo-title: Visa systeminformation
description: Lär dig hur du kan visa resursövervakningsdiagram och information om servern som kör AEM formulär.
seo-description: Lär dig hur du kan visa resursövervakningsdiagram och information om servern som kör AEM formulär.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '561'
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

**Virtuell dator:JVM-version (** Java Virtual Machine) på servern.

**Leverantör av virtuell dator:** Tillverkare av JVM.

**Version för virtuell dator:** JVM-versionsnummer

**Datornamn:** Värdnamn för servern där AEM är installerat.

**Starttid:** Den tid, i timmar och minuter, som servern har körts.

**Just-In-Time-kompilator:** Namnet på den kompilator som används.

**Kompileringstid:** Den tid som har ägnats åt kompileringen.

**Antal Live-trådar:** Det totala antalet trådar som för närvarande finns i AEM.

**Högsta antal trådar:** Största antal livetrådar som någonsin spelats in i systemet.

**Antal inlästa klasser:** Antal klasser som har lästs in i JVM.

**Antal ej inlästa klasser:** Antal klasser som inte har lästs in från JVM.

**Minsta heap:** Den minsta heap som användes.

**Maximal heap:** Den maximala heap som användes.

**Operativsystemnamn:** Namnet på det operativsystem som körs på AEM formulärserver.

**Operativsystemsversion:** Versionsnummer för det operativsystem som körs på AEM formulärserver.

**Operativsystemsark:** Den operativsystemsarkitektur som JVM körs på.

**Antal processorer:** Antalet processorer i systemet.

**Argument för virtuell dator:** Argumentet som används av JVM.

**Klasssökväg:** Klasssökvägen som används av JVM.

**Bibliotekssökväg:** Bibliotekssökvägen som används av JVM.

**Startklasssökväg:** Den startklasssökväg som används av JVM.

**Programservertyp:** Typ av programserver som används för att köra AEM formulär.

**Application Server-version:** Versionsnummer för den programserver som används för att köra AEM formulär.

**Application Server-leverantör:** Tillverkare av den programserver som används för att köra AEM formulär.

**Installationsdatum:** Datum (i formatet åååå-mm-dd) som AEM har installerats.

**AEM:** Version av AEM formulär som är installerade.

**Korrigeringsversion:** AEM formulärkorrigeringsnummer.

**Databasnamn:** Typ av databas som används av AEM formulär.

**Databasversion:** Versionsnummer för den databas som används av AEM formulär.

**Namn på databasenhet:** Namnet på den drivrutin som JVM använder för att ansluta till databasen.

**Databasdrivrutinsversion:** Den version av drivrutinen som JVM använder för att ansluta till databasen.

Med knappen **Spara** kan du spara systeminformationen i en egenskapsfil.
