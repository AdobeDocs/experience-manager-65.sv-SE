---
title: Felsökning av Adobe Experience Manager
description: Läs om hur du felsöker problem som kan uppstå med Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Felsökning av Adobe Experience Manager {#troubleshooting-aem}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM (Adobe Experience Manager), samt förslag på hur du felsöker dem.

>[!NOTE]
>
>Om du felsöker redigeringsproblem i AEM, se [Felsökning för författare.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>När du får problem är det också värt att kontrollera listan över [kända fel](/help/release-notes/release-notes.md) för din instans (release- och servicepaket).

## Felsökningsscenarier för administratörer {#troubleshooting-scenarios-for-administrators}

I följande tabell visas en översikt över problem som administratörer kan felsöka:

<table>
 <tbody>
  <tr>
   <td><strong>Roll</strong></td>
   <td><strong>Problem </strong></td>
  </tr>
  <tr>
   <td>Systemadministratör</td>
   <td><p>Om du dubbelklickar på Quickstart-behållaren händer ingenting och filen öppnas i ett annat program (t.ex. arkivhanteraren)</p> </td>
  </tr>
  <tr>
   <td><p>Systemadministratör</p> </td>
   <td><p>Mitt program som körs på CRX orsakar fel av typen slut på minne</p> </td>
  </tr>
  <tr>
   <td><p>Systemadministratör</p> </td>
   <td><p>Välkomstskärmen i AEM visas inte i webbläsaren när du har dubbelklickat på AEM CM QuickStart</p> </td>
  </tr>
  <tr>
   <td><p>Systemadministratör</p> <p>admin-användare</p> </td>
   <td><p>Göra en tråddump</p> </td>
  </tr>
  <tr>
   <td><p>Systemadministratör</p> <p>admin-användare</p> </td>
   <td><p>Söker efter oavslutade JCR-sessioner</p> </td>
  </tr>
 </tbody>
</table>

## Installationsproblem {#installation-issues}

Mer information om följande felsökningsscenarier finns i [Vanliga installationsproblem](/help/sites-deploying/troubleshooting.md#common-installation-issues):

* Att dubbelklicka på Quickstart-behållaren har ingen effekt och JAR-filen har ingen effekt med ett annat program (t.ex. arkivhanteraren).
* Program som körs på CRX orsakar fel av typen slut på minne.
* Välkomstskärmen i AEM visas inte i webbläsaren när du har dubbelklickat på AEM Quickstart.

## Metoder för felsökningsanalys {#methods-for-troubleshooting-analysis}

### Göra en tråddump {#making-a-thread-dump}

Tråddumpen är en lista över alla Java™-trådar som är aktiva. Om AEM inte svarar som det ska kan du identifiera problem med låsning eller andra problem med tråddumpen.

### Använda Sling Thread Dumper {#using-sling-thread-dumper}

1. Öppna **AEM Web Console**, till exempel `https://localhost:4502/system/console/`.
1. Välj fliken **Threads** under **Status** .

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Använda jstack (kommandorad) {#using-jstack-command-line}

1. Hitta PID (process-id) för AEM Java™-instansen.

   Du kan till exempel använda `ps -ef` eller `jps`.

1. Kör:

   `jstack <pid>`

1. Visar tråddumpen.

>[!NOTE]
>
>Du kan lägga till tråddumpar i en loggfil med hjälp av `>>`-utdataomdirigeringen:
>
>`jstack <pid> >> /path/to/logfile.log`

Mer information finns i [Så här tar du trådmodeller från en JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html) -dokumentation

### Söker efter oavslutade JCR-sessioner {#checking-for-unclosed-jcr-sessions}

När funktioner utvecklas för AEM WCM kan JCR-sessioner öppnas (vilket kan jämföras med att öppna en databasanslutning). Om de öppnade sessionerna aldrig stängs kan systemet få följande symtom:

* Systemet blir långsammare.
* Du kan se mycket av CacheManager: resizeAll-poster i loggfilen. Följande nummer (size=&lt;x>) visar antalet cacheminnen, varje session öppnar flera cacheminnen.
* Från tid till annan har systemet slut på minne (efter några timmar, dagar eller veckor - beroende på allvarlighetsgraden).

Information om hur du börjar analysera oavslutade sessioner finns i kunskapsbasartikeln [Ostängd resurslösare](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23761).

### Använda Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi-paketens status kan också ge en tidig indikation på eventuella problem.

1. Öppna **AEM Web Console**, till exempel `https://localhost:4502/system/console/`.
1. Välj **Paket** under fliken **OSGI**.
1. Kontrollera:

   * paketens status. Om något är inaktivt eller missnöjt kan du försöka stoppa och starta om paketet. Om problemet kvarstår bör du undersöka det ytterligare med andra metoder.
   * om något av paketen saknar beroenden. Den här typen av information kan du se genom att klicka på det enskilda paketnamnet, som är en länk (följande exempel har inga problem):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
