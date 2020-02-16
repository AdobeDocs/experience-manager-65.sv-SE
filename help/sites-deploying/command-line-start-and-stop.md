---
title: Kommandoradens start och stopp
seo-title: Kommandoradens start och stopp
description: Lär dig hur du startar och stoppar AEM från kommandoraden.
seo-description: Lär dig hur du startar och stoppar AEM från kommandoraden.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Kommandoradens start och stopp{#command-line-start-and-stop}

## Starta Adobe Experience Manager från kommandoraden {#starting-adobe-experience-manager-from-the-command-line}

Skriptet är tillgängligt under `start` katalogen &lt;cq-installation>/bin ** . Det finns både Unix- och Windows-versioner. Skriptet startar instansen som är installerad i katalogen *&lt;cq-installation>* .

Dessa två versioner har stöd för en lista med miljövariabler som kan användas för att starta och justera AEM-instansen.

<table>
 <tbody>
  <tr>
   <td><strong>Miljövariabel </strong></td>
   <td><strong>Beskrivning </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>TCP-port som används för stopp- och statusskript<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Värdnamn<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Gränssnitt som den här servern ska lyssna på<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>Körningsläge(n) avgränsade med kommatecken<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Namn på jarfile<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Användning av JAAS (om true)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>Sökväg till JAAS-konfigurationen<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>JVM-standardalternativ<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Observera att vissa körningslägen, bland annat författare och publicering, måste anges innan AEM startas första gången och inte kan ändras efteråt. Innan du konfigurerar en AEM-instans som ska användas i produktionen bör du läsa dokumentationen [för](/help/sites-deploying/configure-runmodes.md) körningslägen för mer information.

### Exempel på Windows-plattformen start.bat-skript {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exempel på startskript för Unix-plattformen {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>Startskriptet startar den AEM Quickstart som finns installerad under *mappen &lt;cq-installation>/app* .

## Stoppar Adobe Experience Manager {#stopping-adobe-experience-manager}

Om du vill stoppa AEM gör du något av följande:

* Beroende på vilken plattform du använder:

   * Om du startade AEM från antingen ett skript eller kommandoraden trycker du på **Ctrl+C** för att stänga servern.
   * Om du har använt startskriptet på UNIX måste du använda stoppskriptet för att stoppa AEM.

* Om du startade AEM genom att dubbelklicka på burkfilen klickar du på knappen **På** i startfönstret (knappen ändras sedan till **Av**) för att stänga servern.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Stoppa Adobe Experience Manager från kommandoraden {#stopping-adobe-experience-manager-from-the-command-line}

Skriptet är tillgängligt under `stop` katalogen &lt;cq-installation>/bin ** . Det finns både Unix- och Windows-versioner. Skriptet stoppar den instans som körs och som är installerad i katalogen *&lt;cq-installation>* .

### Exempel på stoppskript för Unix-plattformen {#unix-platform-stop-script-example}

```shell
./stop
```

### Exempel på stop.bat-skript för Windows-plattformen {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Om du bara vill förkonfigurera databasen (utan att flytta den) behöver du bara:

* extrahera `repository.xml` till önskad plats

* uppdatera `repository.xml` efter behov

* skapa `bootstrap.properties` och definiera `repository.config`

Återigen, innan du startar den faktiska installationen.

