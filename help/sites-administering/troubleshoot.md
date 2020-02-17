---
title: Felsökning av AEM
seo-title: Felsökning av AEM
description: Läs mer om felsökning av problem med AEM.
seo-description: Läs mer om felsökning av problem med AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Felsökning av AEM {#troubleshooting-aem}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.

>[!NOTE]
>
>Om du felsöker redigeringsproblem i AEM, se [Felsökning för författare.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>När du får problem är det också värt att kontrollera listan med [kända fel](/help/release-notes/known-issues.md) för din instans (release- och servicepaket).

## Felsökningsscenarier för administratörer {#troubleshooting-scenarios-for-administrators}

Följande tabell innehåller en översikt över problem som administratörer kan behöva felsöka:

<table>
 <tbody>
  <tr>
   <td><strong>Roll(er)</strong></td>
   <td><strong>Problem </strong></td>
  </tr>
  <tr>
   <td>Systemadministratör</td>
   <td><p>Att dubbelklicka på Quickstart-behållaren har ingen effekt eller öppnar burken-filen med ett annat program (t.ex. arkivhanteraren)</p> </td>
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

Mer information om följande felsökningsscenarier finns i [Vanliga installationsproblem](/help/sites-deploying/troubleshooting.md#common-installation-issues) :

* Att dubbelklicka på Quickstart-behållaren har ingen effekt och JAR-filen har ingen effekt med ett annat program (t.ex. arkivhanteraren).
* Program som körs på CRX orsakar fel av typen slut på minne.
* Välkomstskärmen i AEM visas inte i webbläsaren när du har dubbelklickat på AEM Quickstart.

## Metoder för felsökningsanalys {#methods-for-troubleshooting-analysis}

### Göra en tråddump {#making-a-thread-dump}

Tråddumpen är en lista över alla Java-trådar som är aktiva. Om AEM inte svarar korrekt kan tråddumpen hjälpa dig att identifiera lås eller andra problem.

### Använda Sling Thread Dumper {#using-sling-thread-dumper}

1. Öppna **AEM Web Console**; till exempel på `https://localhost:4502/system/console/`.
1. Välj **Trådar** under **fliken Status** .

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Använda jstack (kommandorad) {#using-jstack-command-line}

1. Hitta PID (process-id) för AEM Java-instansen.

   Du kan till exempel använda `ps -ef` eller `jps`.

1. Kör:

   `jstack <pid>`

1. Då visas tråddumpen.

>[!NOTE]
>
>Du kan lägga till tråddumpar i en loggfil genom att använda `>>` utdataomdirigering:
>
>`jstack <pid> >> /path/to/logfile.log`

Mer information finns i [Så här tar du trådmodeller från en JVM](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) -dokumentation

### Söker efter oavslutade JCR-sessioner {#checking-for-unclosed-jcr-sessions}

När funktioner utvecklas för AEM WCM kan JCR-sessioner öppnas (vilket kan jämföras med att öppna en databasanslutning). Om de öppnade sessionerna aldrig stängs kan systemet få följande symtom:

* Systemet blir långsammare.
* Du kan se många CacheManager: resizeAlla poster i loggfilen. följande nummer (size=&lt;x>) visar antalet cacheminnen. Varje session öppnar flera cacheminnen.
* Från tid till annan har systemet slut på minne (efter några timmar, dagar eller veckor - beroende på allvarlighetsgraden).

Om du vill analysera oavslutade sessioner och ta reda på vilken kod som inte stänger en session kan du läsa artikeln [Analysera oavslutade sessioner](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html)i kunskapsbasen.

### Använda Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi-paketens status kan också ge en tidig indikation på eventuella problem.

1. Öppna **AEM Web Console**; till exempel på `https://localhost:4502/system/console/`.
1. Välj **Paket** under fliken **OSGI** .
1. Kontroll:

   * paketens status. Om något är inaktivt eller missnöjt försöker du stoppa och starta om paketet. Om problemet kvarstår kan du behöva undersöka det ytterligare med andra metoder.
   * om något av paketen saknar beroenden. Den här typen av information kan du se genom att klicka på det enskilda paketnamnet, som är en länk (följande exempel har inga problem):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)

