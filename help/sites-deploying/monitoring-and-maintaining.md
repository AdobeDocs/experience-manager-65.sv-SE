---
title: Övervaka och underhålla din AEM-instans
seo-title: Övervaka och underhålla din AEM-instans
description: Lär dig övervaka AEM.
seo-description: Lär dig övervaka AEM.
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Övervaka och underhålla din AEM-instans{#monitoring-and-maintaining-your-aem-instance}

När dina AEM-instanser har distribuerats behövs vissa uppgifter för att övervaka och underhålla deras åtgärder, prestanda och integritet.

En nyckelfaktor här är att för att identifiera potentiella problem måste du veta hur dina system ser ut och beter sig under normala förhållanden. Detta görs bäst genom att övervaka systemet och samla in information över en tidsperiod.

| Kontroll | Överväganden | Kommentar/åtgärder |
|---|---|---|
| Planen för säkerhetskopiering. |  | Se hur du [säkerhetskopierar din instans](/help/sites-deploying/monitoring-and-maintaining.md#backups). |
| plan för katastrofåterställning. | Företagets riktlinjer för katastrofåterställning. |  |
| Det finns ett felspårningssystem för rapportering av problem. | Till exempel [bugzilla](https://www.bugzilla.org/), [jira](https://www.atlassian.com/software/jira/)eller någon av många andra. |  |
| Filsystemen övervakas. | CRX-databasen &quot;fryser&quot; om det inte finns tillräckligt med ledigt diskutrymme. Den återupptas när det finns utrymme tillgängligt. | &quot; `*ERROR* LowDiskSpaceBlocker`&quot;-meddelanden kan visas i loggfilen när det lediga utrymmet börjar ta slut. |
| [Loggfiler](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) övervakas. |  |  |
| Systemövervakning körs kontinuerligt i bakgrunden. | Inklusive processor-, minnes-, disk- och nätverksanvändning. Med exempelvis iostat / vmstat / permon. | Loggade data visas och kan användas för att spåra prestandaproblem. Rådata är också tillgängliga. |
| [AEM-prestanda övervakas](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | Inklusive [begäranderäknare](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) för övervakning av trafiknivåer. | Om en betydande eller långsiktig förlust av resultat konstateras bör en detaljerad undersökning göras. |
| Du övervakar dina [replikeringsagenter](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents). &quot; |  |  |
| Rensa arbetsflödesinstanser regelbundet. | Databasstorlek och arbetsflödets prestanda. | Se [Vanlig tömning av arbetsflödesinstanser](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances). |

## Säkerhetskopior {#backups}

Det är god praxis att säkerhetskopiera

* Programvaruinstallationen - före/efter viktiga ändringar i konfigurationen
* Innehållet i databasen - regelbundet

Företaget kommer förmodligen att ha en säkerhetskopieringsprincip som du måste följa, ytterligare överväganden om vad som ska säkerhetskopieras och när inkluderar:

* hur viktigt systemet och data är.
* hur ofta ändringar görs i antingen programvaran eller data.
* datavolym, kapacitet kan ibland vara ett problem, liksom den tid som behövs för att utföra säkerhetskopieringen.
* huruvida din säkerhetskopiering kan göras medan användarna är online; och, om möjligt, vilken är prestandapåverkan.
* användarnas geografiska utbredning, d.v.s. när är det bästa tillfället att säkerhetskopiera (för att minimera påverkan)?
* din återställningspolicy, Det finns riktlinjer för var säkerhetskopierade data ska lagras (t.ex. utanför platsen, ett visst medium).

Ofta utförs en fullständig säkerhetskopiering med regelbundna intervall (t.ex. dagligen, veckovis eller månadsvis), med inkrementella säkerhetskopieringar mellan (t.ex. varje timme, dag eller vecka).

>[!CAUTION]
>
>När du implementerar säkerhetskopieringar av produktionsinstanser *måste* du göra tester för att se till att säkerhetskopian kan återställas.

>Utan detta kan säkerhetskopieringen vara oanvändbar (värsta scenariot).
>
>[!NOTE]
Mer information om säkerhetskopieringsprestanda finns i avsnittet [Säkerhetskopieringsprestanda](/help/sites-deploying/configuring-performance.md#backup-performance) .

### Säkerhetskopiera programvaruinstallationen {#backing-up-your-software-installation}

När installationen är klar, eller om konfigurationen har ändrats på ett betydande sätt, gör du en säkerhetskopia av programvaruinstallationen.

Om du vill göra det måste du [säkerhetskopiera hela databasen](#backing-up-your-repository) och sedan:

1. Stoppa AEM.
1. Säkerhetskopiera hela `<cq-installation-dir>` filen från filsystemet.

>[!CAUTION]
Om du använder en programserver från en annan tillverkare kan ytterligare mappar finnas på en annan plats och behöver också säkerhetskopieras. Information om hur du installerar programservrar finns i [Installera AEM med en programserver](/help/sites-deploying/application-server-install.md) . [](/content/docs/en/aem/6-3/deploy/installing.md#installing adobe experience manager with an application server)

>[!CAUTION]
Inkrementell säkerhetskopiering av fillagringen stöds. När du använder stegvis säkerhetskopiering för andra komponenter (till exempel Lucene-index) måste du se till att borttagna filer också markeras som borttagna i säkerhetskopian.

>[!NOTE]
Diskspegling kan också användas som en säkerhetskopieringsmekanism.

### Säkerhetskopiera databasen {#backing-up-your-repository}

Avsnittet [Säkerhetskopiering och återställning](/help/sites-administering/backup-and-restore.md) i CRX-dokumentationen omfattar alla problem som rör säkerhetskopiering av CRX-databasen.

Mer information om hur du skapar en &quot;hot&quot;-säkerhetskopiering online finns i [Skapa en onlinesäkerhetskopiering](/help/sites-administering/backup-and-restore.md#online-backup).

## Rensning av version {#version-purging}

Verktyget **Rensa versioner** är avsett att rensa versioner av en nod eller en hierarki av noder i databasen. Dess främsta syfte är att hjälpa dig att minska storleken på databasen genom att ta bort tidigare versioner av dina noder.

I det här avsnittet behandlas underhållsåtgärder som rör versionshanteringsfunktionen i AEM. Verktyget **Rensa version** är avsett att rensa versioner av en nod eller en hierarki av noder i databasen. Dess främsta syfte är att hjälpa dig att minska storleken på databasen genom att ta bort tidigare versioner av dina noder.

### Översikt {#overview}

Verktyget **Rensa versioner** finns i **[verktygskonsolen](/help/sites-administering/tools-consoles.md)under **Versionshantering****eller direkt på:

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**Startbana** En absolut sökväg som rensningen måste göras på. Du kan välja Startsökväg genom att klicka på databasträdnavigatören.

**Rekursiv** När du rensar data kan du välja mellan att utföra åtgärden på en nod eller i en hel hierarki genom att välja Rekursiv. I det sista fallet definierar den angivna sökvägen rotnoden i hierarkin.

**Högsta antal versioner som ska behållas** Högsta antal versioner som får behållas för en nod. När de här siffrorna överskrider det här värdet rensas de äldsta versionerna.

**Högsta versionsålder** Högsta ålder för en nods version. När en versions ålder överskrider det här värdet rensas den.

**Torr körning** Eftersom borttagning av versioner av ditt innehåll är definierat och inte kan återställas utan återställning av en säkerhetskopia, har verktyget Rensa versioner ett torrt körningsläge som gör att du kan förhandsgranska rensade versioner. Klicka på Torr körning om du vill starta en torr tömningsprocess.

**Rensa** Starta rensningen av versionerna på noden som definieras av startsökvägen.

### Rensa versioner av en webbplats {#purging-versions-of-a-web-site}

Så här rensar du versioner av en webbplats:

1. Gå till **[verktygskonsolen](/help/sites-administering/tools-consoles.md)**,**välj**Versionshantering **och dubbelklicka på****Rensa versioner.**
1. Ange startsökvägen för innehållet som ska rensas (t.ex. `/content/geometrixx-outdoors`).

   * Om du bara vill rensa den nod som definieras av sökvägen avmarkerar du **Rekursiv**.
   * Om du vill rensa noden som definieras av sökvägen och dess underordnade ska du välja **Rekursiv**.

1. Ange maximalt antal versioner (för varje nod) som du vill behålla. Lämna tomt om du inte vill använda den här inställningen.

1. Ange den maximala versionsåldern i dagar (för varje nod) som du vill behålla. Lämna tomt om du inte vill använda den här inställningen.

1. Klicka på **Torr körning** för att förhandsgranska vad tömningsprocessen skulle göra.
1. Klicka på **Rensa** för att starta processen.

>[!CAUTION]
Det går inte att återställa rensade noder utan att återställa databasen. Du bör ta hand om konfigurationen, så vi rekommenderar att du alltid utför en torr körning innan du tömmer den.

### Analyserar konsolen {#analyzing-the-console}

Processerna **Torr körning** och **Töm** listar alla noder som har bearbetats. Under processen kan en nod ha någon av följande status:

* `ignore (not versionnable)`: noden stöder inte versionshantering och ignoreras under processen.

* `ignore (no version)`: noden har ingen version och ignoreras under processen. &quot;

* `retained`: noden rensas inte.
* `purged`: noden rensas.

Konsolen ger dessutom användbar information om versionerna:

* `V 1.0`: versionsnumret.
* `V 1.0.1`*: stjärnan anger att versionen är den aktuella.

* `Thu Mar 15 2012 08:37:32 GMT+0100`: datum för versionen.

I nästa exempel:

* Versionerna **Shirts** rensas eftersom versionsåldern är större än 2 dagar.
* The **Tonga Fashions!** versionerna rensas eftersom deras antal versioner är större än 5.

![global_version_screenshot](assets/global_version_screenshot.png)

## Arbeta med granskningsposter och loggfiler {#working-with-audit-records-and-log-files}

Granskningsposter och loggfiler för Adobe Experience Manager (AEM) finns på olika platser. Här följer en översikt över vad du kan hitta.

### Arbeta med loggar {#working-with-logs}

AEM WCM registrerar detaljerade loggar. När du har packat upp och startat Quickstart hittar du loggar in:

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### Rotation av loggfil {#log-file-rotation}

Rotation av loggfiler avser den process som begränsar filens tillväxt genom att skapa nya filer med jämna mellanrum. I AEM roteras en loggfil med namnet `error.log` en gång om dagen enligt följande regler:

* Filens namn ändras enligt mönstret {original_filename} `error.log` `.yyyy-MM-dd`. Exempel: den 11 juli 2010 får den aktuella loggfilen ett nytt namn `error.log-2010-07-10`och en ny `error.og` skapas.

* Tidigare loggfiler tas inte bort, så det är ditt ansvar att regelbundet rensa gamla loggfiler för att begränsa diskanvändningen.

>[!NOTE]
Om du uppgraderar din AEM-installation bör du tänka på att alla befintliga loggfiler som inte längre används av AEM finns kvar på disken. Du kan ta bort dem utan risk. Alla nya loggposter skrivs i de nya loggfilerna.

### Hitta loggfilerna {#finding-the-log-files}

Olika loggfiler finns på den filserver där du installerade AEM:

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
Alla åtkomstbegäranden till AEM WCM och databasen registreras här.

   * `audit.log`
Modereringsåtgärder registreras här.

   * `error.log`
Felmeddelanden (av varierande allvarlighetsgrad) registreras här.

   * [ Den `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_image_server_log.html)här loggen används bara om Dynamic Media är aktiverat. Det innehåller statistik och analysinformation som används för att analysera beteendet i den interna ImageServer-processen.

   * `request.log`
Varje åtkomstbegäran registreras här tillsammans med svaret.

   * [ Den `s7access-<yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_Access_Log.html)här loggen används bara om Dynamic Media är aktiverat. I s7access-loggen registreras varje begäran som gjorts till Dynamic Media via `/is/image` och `/is/content`.

   * `stderr.log`
Innehåller felmeddelanden, återigen av varierande allvarlighetsgrad, som genereras under start. Som standard är loggnivån inställd på `Warning` ( `WARN`)

   * `stdout.log`
Innehåller loggningsmeddelanden som anger händelser under start.

   * `upgrade.log`
Innehåller en logg över alla uppgraderingsåtgärder som körs från `com.day.compat.codeupgrade` - och `com.adobe.cq.upgradesexecutor` paketen.

* `<*cq-installation-dir*>/crx-quickstart/repository`

   * `revision.log`
Information om revideringsjournaler.

>[!NOTE]
ImageServer- och s7access-loggarna ingår inte i **Download Full **paketet som genereras från sidan **system/console/status-Bundlelist **. Om du har problem med dynamiska media bör du av supportskäl även bifoga loggarna för ImageServer och s7access när du kontaktar kundsupport.

### Aktivera felsökningsloggnivån {#activating-the-debug-log-level}

Standardloggnivån ([konfiguration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)för Apache Sling-loggning) är Information, så felsökningsmeddelanden loggas inte.

Om du vill aktivera felsökningsloggnivån för en loggare anger du egenskapen `org.apache.sling.commons.log.level` till felsökning i databasen. Exempel: på `/libs/sling/config/org.apache.sling.commons.log.LogManager` för att konfigurera [global Apache Sling-loggning](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration).

>[!CAUTION]
Lämna inte loggen på felsökningsloggnivån längre än nödvändigt eftersom den genererar många loggposter och förbrukar därmed resurser.

En rad i felsökningsfilen börjar oftast med DEBUG och anger sedan loggnivån, installationsåtgärden och loggmeddelandet. Exempel:

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Loggnivåerna är följande:

| 0 | Allvarligt fel | Åtgärden misslyckades och installationsprogrammet kan inte fortsätta. |
|---|---|---|
| 1 | Fel | Åtgärden misslyckades. Installationen fortsätter, men en del av AEM WCM installerades inte korrekt och kommer inte att fungera. |
| 2 | Varning | Åtgärden har slutförts men problem uppstod. AEM WCM fungerar eventuellt inte korrekt. |
| 3 |  Information | Åtgärden har slutförts. |

### Skapa en anpassad loggfil {#create-a-custom-log-file}

>[!NOTE]
När du arbetar med Adobe Experience Manager finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommendationer finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

I vissa fall kanske du vill skapa en anpassad loggfil med en annan loggnivå. Du kan göra detta i databasen genom att:

1. Om den inte redan finns skapar du en ny konfigurationsmapp ( `sling:Folder`) för projektet `/apps/<*project-name*>/config`.
1. Under `/apps/<*project-name*>/config`skapar du en nod för den nya [loggningskonfigurationen](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)för Apache Sling-loggning:

   * Namn: `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (eftersom detta är en loggare)

      Där `<*identifier*>` ersätts av fri text som du (måste) anger för att identifiera förekomsten (du kan inte utelämna den här informationen).

      Exempel, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Typ: `sling:OsgiConfig`
   >[!NOTE]
   Även om det inte är ett tekniskt krav är det tillrådligt att göra `<*identifier*>` unikt.

1. Ange följande egenskaper för den här noden:

   * Namn: `org.apache.sling.commons.log.file`

      Typ:Sträng

      Värde: Ange loggfilen.
till exempel `logs/myLogFile.log`

   * Namn: `org.apache.sling.commons.log.names`

      Typ: Sträng[] (String + Multi)

      Värde: Ange de OSGi-tjänster som loggningsmeddelanden ska användas för. till exempel alla följande:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * Namn: `org.apache.sling.commons.log.level`

      Typ:Sträng

      Värde: Ange den loggnivå som krävs ( `debug`, `info`, `warn` eller `error`). till exempel `debug`

   * Konfigurera de andra parametrarna efter behov:

      * Namn: `org.apache.sling.commons.log.pattern`

         Typ: `String`

         Värde: Ange loggmeddelandets mönster efter behov. till exempel

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   `org.apache.sling.commons.log.pattern` stöder upp till sex argument.

   >{0}{1}{2} the time stamp of type `java.util.Date`{1} the log marker{3} the name of the current thread{4} the log level{5} the log message

   >Om logganropet innehåller en `Throwable` stackspårning läggs den till i meddelandet.

   >[!CAUTION]
   org.apache.sling.Commons.log.names måste ha ett värde.

   >[!NOTE]
   Loggskrivarsökvägarna är relativa till `crx-quickstart` platsen.
   Därför har en loggfil angetts som:
   `logs/thelog.log`

   >skriver till:
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   Och en loggfil har angetts som:
   `../logs/thelog.log`

   >skriver till en katalog:
   ` <*cq-installation-dir*>/logs/`
&quot;(dvs. bredvid ` `&lt;*cq-installation-dir*>/`crx-quickstart/`)

1. Det här steget är bara nödvändigt när ett nytt skrivprogram krävs (dvs. med en konfiguration som inte är densamma som standardskrivaren).

   >[!CAUTION]
   En ny loggningsskrivarkonfiguration krävs bara när den befintliga standardinställningen inte är lämplig.

   >Om inget explicit skrivprogram är konfigurerat genereras automatiskt ett implicit skrivprogram baserat på standardvärdet.

   Under `/apps/<*project-name*>/config`skapar du en nod för den nya skrivarkonfigurationen [för](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)Apache Sling Logging Writer:

   * Namn: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (eftersom detta är ett skrivprogram)

      Precis som med Logger `<*identifier*>` ersätts den av fri text som du (måste) anger för att identifiera instansen (du kan inte utelämna den här informationen). Exempel, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Typ: `sling:OsgiConfig`
   >[!NOTE]
   Även om det inte är ett tekniskt krav är det tillrådligt att göra `<*identifier*>` unikt.

   Ange följande egenskaper för den här noden:

   * Namn: `org.apache.sling.commons.log.file`

      Typ: `String`

      Värde: Ange loggfilen så att den överensstämmer med den fil som anges i loggboken.

      i det här exemplet, `../logs/myLogFile.log`.

   * Konfigurera de andra parametrarna efter behov:

      * Namn: `org.apache.sling.commons.log.file.number`

         Typ: `Long`

         Värde: Ange hur många loggfiler du vill behålla.
till exempel `5`

      * Namn: `org.apache.sling.commons.log.file.size`

         Typ: `String`

         Värde: Ange vad som krävs för att kontrollera filens rotation efter storlek/datum.
till exempel `'.'yyyy-MM-dd`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` styr rotationen av loggfilen genom att ange antingen:
   >
   >* maximal filstorlek
   >* ett tids-/datumschema
   >
   >för att ange när en ny fil ska skapas (och den befintliga filen får ett nytt namn enligt namnmönstret).
   >
   >* En storleksgräns kan anges med ett tal. Om ingen storleksindikator anges används detta som antal byte, eller så kan du lägga till en av storleksindikatorerna - `KB`, `MB`eller `GB` (versaler ignoreras).
   >* Ett tids-/datumschema kan anges som ett `java.util.SimpleDateFormat` mönster. Detta anger den tidsperiod efter vilken filen ska roteras. det suffix som läggs till i den roterade filen (för identifiering).
   >
   >Standardvärdet är &#39;.&#39;yyyy-MM-dd (för daglig loggrotation)
   >
   >Så vid midnatt den 20 januari 2010 (eller när det första loggmeddelandet efter detta blir exakt) kommer ../logs/error.log att byta namn till ../logs/error.log.2010-01-20. Loggning för den 21 januari kommer att skickas till (en ny och tom) ../logs/error.log tills den överförs vid nästa ändring av dagen.
   >
   >| `&#39;.&#39;yyyy-MM`|Rotation i början av varje månad|
   >|---|---|
   >| `&#39;.&#39;yyyy-ww`|Rotation på den första dagen i varje vecka (beroende på språkområde). |
   >| `&#39;.&#39;yyyy-MM-dd`|Rotation vid midnatt varje dag. |
   >| `&#39;.&#39;yyyy-MM-dd`|Rotation vid midnatt och middag varje dag. |
   >| `&#39;.&#39;yyyy-MM-dd-HH`|Rotation överst i varje timme. |
   >| `&#39;.&#39;yyyy-MM-dd-HH-mm`|Rotation i början av varje minut. |
   >
   >Obs! När du anger tid/datum:
   >1. Du bör&quot;escape&quot;-text inom ett par enkla citattecken (&#39; &#39;);
   >   Detta gör du för att undvika att vissa tecken tolkas som mönsterbokstäver.
   >1. Använd bara tecken som är tillåtna för ett giltigt filnamn var som helst i alternativet.

1. Läs den nya loggfilen med det verktyg du valt.

   Loggfilen som skapas i det här exemplet blir `../crx-quickstart/logs/myLogFile.log`.

Felix Console innehåller även information om stöd för loggning på `../system/console/slinglog`. till exempel `https://localhost:4502/system/console/slinglog`.

### Söka efter granskningsposter {#finding-the-audit-records}

Granskningsregister förs för att visa vem som gjorde vad och när. Olika granskningsposter genereras för både AEM WCM- och OSGi-händelser.

#### AEM WCM-granskningsposter visas vid sidredigering {#aem-wcm-audit-records-shown-when-page-authoring}

1. Öppna en sida.
1. I sidosparken kan du välja fliken med låsikonen och sedan dubbelklicka på **Granskningslogg...**
1. Ett nytt fönster öppnas med en lista över granskningsposter för den aktuella sidan.

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. Klicka på **OK** när du vill stänga fönstret.

#### AEM WCM-granskningsposter i databasen {#aem-wcm-auditing-records-within-the-repository}

Granskningsposter sparas i `/var/audit` mappen enligt resursen. Du kan gå nedåt tills du ser de enskilda posterna och den information de innehåller.

Dessa poster innehåller samma information som den som visas när du redigerar en sida.

#### OSGi Granskningsposter från webbkonsolen {#osgi-audit-records-from-the-web-console}

OSGi-händelser genererar också granskningsposter som kan visas på fliken **Konfigurationsstatus** -> **Loggfiler **fliken i AEM Web Console:

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## Övervaka replikeringsagenter {#monitoring-your-replication-agents}

Du kan övervaka dina [replikeringsköer](/help/sites-deploying/replication.md) för att identifiera när en kö är avstängd eller blockerad, vilket i sin tur kan tyda på ett problem med en publiceringsinstans eller ett externt system:

* Är alla obligatoriska köer aktiverade?
* Krävs det fortfarande inaktiverade köer?
* alla `enabled` köer ska ha status `idle` eller `active`, vilket anger normal drift, inga köer ska vara `blocked`vilket ofta är ett tecken på problem på mottagarsidan.

* om storleken på kön ökar över tiden kan detta ange en blockerad kö.

Så här övervakar du en replikeringsagent:

1. Gå till fliken **Verktyg** i AEM.
1. Klicka på **Replikering**.
1. Dubbelklicka på länken till agenterna för lämplig miljö (antingen vänster eller höger ruta). till exempel **Agenter på författare**.

   I det resulterande fönstret visas en översikt över alla dina replikeringsagenter för redigeringsmiljön, inklusive mål och status.

1. Klicka på lämpligt agentnamn (som är en länk) för att visa detaljerad information om agenten:

   ![chlimage_1](assets/chlimage_1.jpeg)

   Här kan du:

   * Se om agenten är aktiverad.
   * Se målet för alla replikeringar.
   * Kontrollera om replikeringskön är aktiv (aktiverad).
   * Se om det finns några objekt i kön.
   * **Uppdatera** eller **Rensa** för att uppdatera visningen av köposter. så att du lättare kan se objekt komma in i och lämna kön.

   * **Visa logg** för att komma åt loggen för eventuella åtgärder som utförs av replikeringsagenten.
   * **Testa Connection** till målinstansen.
   * **Tvinga Försök igen** för alla köobjekt om det behövs.
   >[!CAUTION]
   Använd inte länken Testa anslutning för den omvända replikeringsutkorgen på en publiceringsinstans.
   Om ett replikeringstest utförs för en Utkorgskö kommer alla objekt som är äldre än testreplikeringen att bearbetas på nytt med varje omvänd replikering.
   Om sådana objekt redan finns i en kö kan de hittas med följande XPath JCR-fråga och bör tas bort.
   `/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

Även här kan du utveckla en lösning för att identifiera alla replikeringsagenter (som finns under `/etc/replication/author` eller `/etc/replication/publish`) och sedan kontrollera status för agenten (, `enabled`) och den underliggande kön ( `disabled`, `active`, `idle``blocked`).

## Övervakningsprestanda {#monitoring-performance}

[Prestandaoptimering](/help/sites-deploying/configuring-performance.md) är en interaktiv process som får fokus under utvecklingen. Efter distributionen granskas den vanligtvis efter specifika intervall eller händelser.

Metoder som används för att samla in information för optimering kan också användas för kontinuerlig övervakning.

>[!NOTE]
Specifika [konfigurationer som är tillgängliga för att förbättra prestanda](/help/sites-deploying/configuring-performance.md#configuring-for-performance) kan också kontrolleras.

Nedan visas vanliga prestandaproblem som uppstår, tillsammans med förslag på hur du kan hitta och motverka dem.

| Yta | Symtom | Öka kapaciteten.. | Minska volymen... |
|---|---|---|---|
| Klient | Hög klientprocessoranvändning. | Installera en klientprocessor med högre prestanda. | Förenkla (HTML) layouten. |
|  | Låg processoranvändning på servern. | Uppgradera till en snabbare webbläsare. | Förbättra cacheminnet på klientsidan. |
|  | Vissa kunder är snabba, vissa långsamma. |  |  |
| Server |  |  |  |
| Nätverk | CPU-användningen låg på både servrar och klienter. | Ta bort eventuella flaskhalsar i nätverket. | Förbättra/optimera konfigurationen av klientcachen. |
|  | Det går snabbt att bläddra lokalt på servern (relativt). | Öka nätverkets bandbredd. | Minska&quot;vikten&quot; på dina webbsidor (t.ex. färre bilder, optimerad HTML). |
| Webbserver | Processoranvändningen på webbservern är hög. | Klustra dina webbservrar. | Minska antalet träffar per sida (besök). |
|  |  | Använd en maskinvarubaserad belastningsutjämnare. |  |
| Program | Serverns processoranvändning är hög. | Klustera dina AEM-instanser. | Sök efter, och eliminera, processor- och minnesgropar (använd kodgranskning, tidsutdata osv.). |
|  | Hög minnesförbrukning. |  | Förbättra cachelagringen på alla nivåer. |
|  | Låga svarstider. |  | Optimera mallar och komponenter (t.ex. struktur, logik). |
| Databas |  |  |  |
| Cache |  |  |  |

Prestandaproblem kan bero på ett antal orsaker som inte har något att göra med webbplatsen, bland annat tillfälliga avbrott i anslutningshastigheten, processorbelastningen och många andra.

Det kan även påverka alla besökare eller bara en del av dem.

All denna information måste hämtas, sorteras och analyseras innan du kan optimera den allmänna prestandan eller lösa specifika problem.

* Innan du upplever ett prestandaproblem:

   * Samla in så mycket information som möjligt för att bygga upp goda kunskaper om systemet under normala förhållanden

* När du får ett prestandaproblem:

   * försök att replikera den med en (eller helst med flera) standardwebbläsare, på en annan klient som du vet har bra allmänna prestanda och/eller på själva servern (om möjligt)
   * kontrollera om något (relaterat till systemet) har ändrats inom en lämplig tidsperiod och om någon av dessa ändringar kan ha påverkat prestandan
   * ställa frågor som:

      * inträffar problemet endast vid vissa tidpunkter?
      * uppstår problemet endast på vissa sidor?
      * Påverkas andra förfrågningar?
   * Samla in så mycket information som möjligt för att jämföra med dina kunskaper om systemet under normala förhållanden:


### Verktyg för övervakning och analys av prestanda {#tools-for-monitoring-and-analyzing-performance}

Nedan ges en kort översikt över några av de verktyg som är tillgängliga för övervakning och analys av prestanda.

Vissa av dessa kommer att vara beroende av operativsystemet.

<table>
 <tbody>
  <tr>
   <td>Verktyg</td>
   <td>Används för att analysera..</td>
   <td>Användning/Mer information..</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>Svarstider och samtidighet.</td>
   <td><a href="#interpreting-the-request-log">Tolkar request.log</a>.</td>
  </tr>
  <tr>
   <td>truss/strace</td>
   <td>Sidinläsning</td>
   <td><p>Unix/Linux-kommandon för att spåra systemanrop och signaler. Öka loggnivån till <code>INFO</code>.</p> <p>Analysera antalet sidinläsningar per begäran, vilka sidor, osv.</p> </td>
  </tr>
  <tr>
   <td>Tråddumpar</td>
   <td>Observera JVM-trådar. Identifiera innehåll, lås och långa löptider.</td>
   <td><p><br /> Beroende på operativsystem: - Unix/Linux: <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows (konsolläge): Ctrl-Break<br /> </p> <p>Analysverktyg finns också tillgängliga, till exempel <a href="https://java.net/projects/tda/">TDA</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td>Heap Dumps</td>
   <td>Slut på minne som orsakar långsamma prestanda.</td>
   <td><p><br /> Lägg till: <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> till java-anropet till AEM.</p> <p>Se <a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">felsökningsguiden för Java SE 6 med HotSpot VM</a>.</p> </td>
  </tr>
  <tr>
   <td>Systemanrop</td>
   <td>Identifiera timingproblem.</td>
   <td><p>Anrop till <code>System.currentTimeMillis()</code> eller <code>com.day.util</code>.Timing används för att generera tidsstämplar från koden eller via <a href="#html-comments">HTML-kommentarer</a>.</p> <p><strong></strong> Obs! Dessa bör implementeras så att de kan aktiveras/avaktiveras efter behov. När ett system fungerar smidigt behövs inte de allmänna kostnaderna för att samla in statistik.</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>Identifiera minnesläckor och analysera responstiden selektivt.</td>
   <td><p>grundanvändningen är:</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>Mer information finns på <a href="#apache-bench">Apache Bench</a> och <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">ab man page</a> .</p> </td>
  </tr>
  <tr>
   <td>Sökanalys</td>
   <td> </td>
   <td>Kör sökfrågor offline, identifiera svarstid för frågan, testa och bekräfta resultatuppsättningen.<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>Belastnings- och funktionstester.</td>
   <td><a href="https://jakarta.apache.org/jmeter/">https://jakarta.apache.org/jmeter/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>Detaljerad processor- och minnesprofilering.</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>Observera JVM-statistik och trådar.</td>
   <td><p>Användning: jconsole</p> <p>Se <a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">jconsole</a> och <a href="#monitoring-performance-using-jconsole">Monitoring Performance med JConsole</a>.</p> <p><strong></strong> Obs! Med JDK 1.6 kan JConsole byggas ut med plugin-program. till exempel Top eller TDA (Thread Dump Analyzer).</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>Observera JVM-statistik, trådar, minne och profilering.</td>
   <td><p>Användning: jvisualvm eller visualvm<br /> </p> <p>Se <a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">jvisualvm</a>, <a href="https://visualvm.dev.java.net/">visualvm</a> och <a href="#monitoring-performance-using-j-visualvm">Övervakningsprestanda med (J)VisualVM</a>.</p> <p><strong></strong> Obs! Med JDK 1.6 kan VisualVM utökas med plugin-program.</p> </td>
  </tr>
  <tr>
   <td>truss/strace, lsof</td>
   <td>Ingående kernelanrop och processanalys (Unix).</td>
   <td>Unix/Linux-kommandon.</td>
  </tr>
  <tr>
   <td>Timingstatistik</td>
   <td>Se timingstatistik för sidåtergivning.</td>
   <td><p>Om du vill se tidsstatistik för sidåtergivning kan du använda <strong>Ctrl-Skift-U</strong> tillsammans med <code>?debugClientLibs=true</code> inställningen i URL:en.</p> </td>
  </tr>
  <tr>
   <td>Verktyg för processor- och minnesprofilering<br /> </td>
   <td><a href="#interpreting-the-request-log">Används vid analys av långsamma begäranden under utveckling</a>.</td>
   <td>Till exempel <a href="https://www.yourkit.com/">YourKit</a>.</td>
  </tr>
  <tr>
   <td><a href="#information-collection">Informationsinsamling</a></td>
   <td>Installationens aktuella tillstånd.</td>
   <td>Om du vet så mycket som möjligt om din installation kan det också hjälpa dig att spåra vad som kan ha orsakat prestandaförändringar och om dessa ändringar är motiverade. Dessa mätvärden måste samlas in med regelbundna intervall så att du enkelt kan se betydande ändringar.</td>
  </tr>
 </tbody>
</table>

### Tolka request.log {#interpreting-the-request-log}

Den här filen registrerar grundläggande information om alla förfrågningar som görs till AEM. Denna värdefulla slutsats kan extraheras.

Det `request.log` erbjuder ett inbyggt sätt att se hur lång tid det tar att begära. I utvecklingssyfte är det användbart för användaren `tail -f` och `request.log` för att hålla utkik efter långsamma svarstider. Om du vill analysera en större `request.log` effekt rekommenderar vi att du [använder `rlog.jar` den för att sortera och filtrera efter svarstider](#using-rlog-jar-to-find-requests-with-long-duration-times).

Vi rekommenderar att du isolerar de&quot;långsamma&quot; sidorna från `request.log`och sedan justerar dem individuellt för att få bättre prestanda. Detta görs vanligtvis genom att prestandamätningar per komponent inkluderas eller genom att ett prestandaprofileringsverktyg som ` [yourkit](https://www.yourkit.com/)`.

#### Övervaka trafik på din webbplats {#monitoring-traffic-on-your-website}

Begärandeloggen registrerar varje begäran som gjorts, tillsammans med svaret:

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

Genom att summera alla GET-poster inom en viss period (t.ex. under olika 24-timmarsperioder) kan du göra utdrag om den genomsnittliga trafiken på din webbplats.

#### Övervaka svarstider med request.log {#monitoring-response-times-with-the-request-log}

En bra utgångspunkt för prestandaanalys är begärandeloggen:

`<*cq-installation-dir*>/crx-quickstart/logs/request.log`

Loggen ser ut så här (raderna förkortas för enkelhetens skull):

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

Den här loggen har en rad per begäran eller svar:

* Det datum då varje begäran eller svar gjordes.
* Numret på begäran, inom hakparentes. Numret matchar för begäran och svaret.
* En pil som anger om det är en begäran (pil som pekar till höger) eller ett svar (pilen till vänster).
* För begäranden innehåller raden:

   * metoden (vanligtvis GET, HEAD eller POST)
   * begärd sida
   * protokollet

* För svar innehåller raden:

   * statuskoden (200 betyder &quot;lyckades&quot;, 404 betyder &quot;sidan hittades inte&quot;
   * MIME-typen
   * svarstid

Med små skript kan du extrahera den information som behövs från loggfilen och sammanställa den statistik som du vill ha. Därifrån ser du vilka sidor eller typer av sidor som är långsamma och om de totala prestandan är tillfredsställande.

#### Övervaka söksvarstider med request.log {#monitoring-search-response-times-with-the-request-log}

Sökbegäranden registreras också i loggfilen:

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

Så som ovan kan du använda skript för att extrahera relevant information och bygga upp statistik.

När du väl har bestämt svarstiden kan du behöva analysera varför begäran tar den tid som behövs och vad som kan göras för att förbättra svaret.

#### Övervaka antalet samtidiga användare och deras inverkan {#monitoring-the-number-and-impact-of-concurrent-users}

Återigen `request.log` kan den användas för att övervaka samtidighet och systemets reaktion på den.

Testerna måste göras för att avgöra hur många samtidiga användare som systemet kan hantera innan en negativ påverkan ses. Återigen kan du använda skript för att extrahera resultat från loggfilen:

* övervaka hur många förfrågningar som görs inom en viss tidsperiod, t.ex. en minut
* testa effekterna av ett visst antal användare som alla gör samma förfrågningar samtidigt (så nära som möjligt), t.ex. 30 användare klickar på **Spara** samtidigt.

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### Använda rlog.jar för att hitta begäranden med lång varaktighet {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM innehåller olika hjälpverktyg som finns i:
`<*cq-installation-dir*>/crx-quickstart/opt/helpers`

En av dessa `rlog.jar`kan användas för att snabbt sortera `request.log` så att förfrågningar visas med varaktighet, från längsta till kortaste tid.

Följande kommando visar möjliga argument:

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

Du kan till exempel köra den och ange `request.log` filen som en parameter och visa de 10 första begäranden som har längst varaktighet:

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

Du kan behöva sammanfoga de enskilda `request.log` filerna om du behöver utföra den här åtgärden på ett stort dataprov.

### Apache Bench {#apache-bench}

För att minimera effekten av specialfall (t.ex. skräpinsamling) rekommenderar vi att du använder ett verktyg som `apachebench` (se t.ex. [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) för mer dokumentation) för att identifiera minnesläckor och selektivt analysera svarstiden.

Apache Bench kan användas på följande sätt:

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

Siffrorna ovan hämtas från en vanlig bärbar MAcBook Pro-dator (mitten av 2010) som har åtkomst till företagssidan geometrixx, som ingår i en standard-AEM-installation. Sidan är mycket enkel, men inte optimerad för prestanda.

`apachebench` visar också tiden per begäran som medelvärde för alla samtidiga begäranden, se `Time per request: 54.595 [ms]` (medelvärde, för alla samtidiga begäranden). Du kan ändra värdet på parametern concurrency `-c` (antal flera begäranden som ska utföras samtidigt) för att se eventuella effekter.

### Begäranräknare {#request-counters}

Information om begärandetrafik (antal förfrågningar under en viss tidsperiod) ger dig en indikation på belastningen på din instans. Den här informationen kan extraheras från [request.log](#interpreting-the-request-log), men med räknare kan du automatisera datainsamlingen för att se:

* signifikanta skillnader i aktivitet (dvs. skillnader mellan&quot;många förfrågningar&quot; och&quot;låg aktivitet&quot;)
* när en instans inte används
* alla omstarter (räknarna återställs till 0)

Om du vill automatisera informationsinsamlingen kan du även installera ett RequestFilter för att öka antalet räknare vid varje begäran. Flera räknare kan användas för olika tidsperioder.

De insamlade uppgifterna kan användas för att ange

* betydande förändringar i verksamheten
* en redundant instans
* alla omstarter (räknaren återställs till 0)

### HTML-kommentarer {#html-comments}

Vi rekommenderar att alla projekt innehåller `html comments` serverprestanda. Många bra exempel finns. Välj en sida, öppna sidkällan för visning och bläddra längst ned. Kod som följande kan visas:

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### Övervaka prestanda med JConsole {#monitoring-performance-using-jconsole}

Verktygskommandot `jconsole` är tillgängligt med JDK.

1. Starta din AEM-instans.
1. Kör `jconsole.`
1. Välj din AEM-instans och **anslut**.

1. Dubbelklicka i `Local` programmet `com.day.crx.quickstart.Main`; Översikten visas som standard:

   ![chlimage_1-1](assets/chlimage_1-1.png)

   Därefter kan du välja andra alternativ.

### Övervakningsprestanda med (J)VisualVM {#monitoring-performance-using-j-visualvm}

Verktygskommandot är `jvisualvm` tillgängligt sedan JDK 1.6. När du har installerat JDK 1.6 kan du:

1. Starta din AEM-instans.

   >[!NOTE]
   Om du använder Java 5 kan du lägga till argumentet på den Java-kommandorad som startar JVM:en. `-Dcom.sun.management.jmxremote` JMX är aktiverat som standard med Java 6.

1. Kör antingen:

   * `jvisualvm`: i mappen JDK 1.6 bin (testversion)
   * `visualvm`: kan laddas ned från [VisualVM](https://visualvm.dev.java.net/) (avkodningsversion)

1. Dubbelklicka i `Local` programmet `com.day.crx.quickstart.Main`; Översikten visas som standard:

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Därefter kan du välja andra alternativ, bland annat Bildskärm:

   ![chlimage_1-3](assets/chlimage_1-3.png)

Du kan använda det här verktyget för att generera tråddumpar och minnesdumpar. Den här informationen begärs ofta av den tekniska supportteamet.

### Informationsinsamling {#information-collection}

Om du vet så mycket som möjligt om din installation kan det hjälpa dig att spåra vad som kan ha orsakat prestandaförändringar och om dessa ändringar är motiverade. Dessa mätvärden måste samlas in med regelbundna intervall så att du enkelt kan se betydande ändringar.

Följande information kan vara användbar:

* [Hur många författare arbetar med systemet?](#how-many-authors-are-working-with-the-system)
* [Vilket är det genomsnittliga antalet sidaktiveringar per dag?](#what-is-the-average-number-of-page-activations-per-day)
* [Hur många sidor har du i det här systemet?](#how-many-pages-do-you-currently-maintain-on-this-system)
* [Om du använder MSM, vilket är det genomsnittliga antalet utrullningar per månad?](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [Vilket är det genomsnittliga antalet Live-kopior per månad?](#what-is-the-average-number-of-live-copies-per-month)
* [Om du använder AEM Assets, hur många resurser har du för närvarande i Assets?](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [Vilken är den genomsnittliga storleken på resurserna?](#what-is-the-average-size-of-the-assets)
* [Hur många mallar används för närvarande?](#how-many-templates-are-currently-used)
* [Hur många komponenter används för närvarande?](#how-many-components-are-currently-used)
* [Hur många förfrågningar per timme har du på författarsystemet vid maximal tid?](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [Hur många begäranden per timme har du i publiceringssystemet vid maximal tid?](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### Hur många författare arbetar med systemet? {#how-many-authors-are-working-with-the-system}

Använd kommandoraden för att se hur många författare som har använt systemet sedan installationen:

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

Så här ser du hur många författare som arbetar ett visst datum:

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### Vilket är det genomsnittliga antalet sidaktiveringar per dag? {#what-is-the-average-number-of-page-activations-per-day}

Om du vill se det totala antalet sidaktiveringar sedan serverinstallationen använder en databasfråga, via CRXDE - Tools - Query:

* **Typ**`XPath`

* **Bana**`/`

* **Fråga**`//element(*, cq:AuditEvent)[@cq:type='Activate']`

Beräkna sedan medelvärdet genom att beräkna antalet dagar som har gått sedan installationen.

#### Hur många sidor har du i det här systemet? {#how-many-pages-do-you-currently-maintain-on-this-system}

Om du vill se antalet sidor som för närvarande finns på servern använder du en databasfråga; via CRXDE - Tools - Query:

* **Typ**`XPath`

* **Bana**`/`

* **Fråga**`//element(*, cq:Page)`

#### Om du använder MSM, vilket är det genomsnittliga antalet utrullningar per månad? {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

För att fastställa det totala antalet utrullningar sedan installationen använder du en databasfråga. via CRXDE - Tools - Query:

* **Typ**`XPath`

* **Bana**`/`

* **Fråga**`//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

Beräkna medelvärdet genom att beräkna antalet månader som har gått sedan installationen.

#### Vilket är det genomsnittliga antalet Live-kopior per månad? {#what-is-the-average-number-of-live-copies-per-month}

För att fastställa det totala antalet live-kopior som gjorts sedan installationen använder du en databasfråga. via CRXDE - Tools - Query:

* **Typ**`XPath`

* **Bana**`/`

* **Fråga**`//element(*, cq:LiveSyncConfig)`

Använd återigen antalet månader som har gått sedan installationen för att beräkna genomsnittet.

#### Om du använder AEM Assets, hur många resurser har du för närvarande i Assets? {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

Om du vill se hur många DAM-resurser du för närvarande har använder du en databasfråga; via CRXDE - Tools - Query:

* **Typ**`XPath`
* **Bana**`/`
* **Fråga**`/jcr:root/content/dam//element(*, dam:Asset)`

#### Vilken är den genomsnittliga storleken på resurserna? {#what-is-the-average-size-of-the-assets}

Så här avgör du den totala storleken på `/var/dam` mappen:

1. Använd WebDAV för att mappa databasen till det lokala filsystemet.

1. Använd kommandoraden:

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   Om du vill få fram den genomsnittliga storleken dividerar du den globala storleken med det totala antalet resurser i `/var/dam` (som hämtas ovan).

#### Hur många mallar används för närvarande? {#how-many-templates-are-currently-used}

Om du vill se antalet mallar som för närvarande finns på servern använder du en databasfråga. via CRXDE - Tools - Query:

* **Typ**`XPath`
* **Bana**`/`
* **Fråga**`//element(*, cq:Template)`

#### Hur många komponenter används för närvarande? {#how-many-components-are-currently-used}

Om du vill se antalet komponenter som för närvarande finns på servern använder du en databasfråga. via CRXDE - Tools - Query:

* **Typ**`XPath`
* **Bana**`/`
* **Fråga**`//element(*, cq:Component)`

#### Hur många förfrågningar per timme har du på författarsystemet vid maximal tid? {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

Så här tar du reda på begäranden per timme som du har på författarsystemet vid maximal tid:

1. Använd kommandoraden för att bestämma det totala antalet begäranden sedan installationen:

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. Så här bestämmer du start- och slutdatum:

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   Använd dessa värden för att beräkna antalet timmar som har gått sedan installationen, och sedan det genomsnittliga antalet begäranden per timme.

#### Hur många begäranden per timme har du i publiceringssystemet vid maximal tid? {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

Upprepa proceduren ovan på din publiceringsinstans.

## Analyserar specifika scenarier {#analyzing-specific-scenarios}

Här följer en lista med förslag på vad du ska kontrollera om du får vissa prestandaproblem. Listan är tyvärr inte helt heltäckande.

>[!NOTE]
Se även följande artiklar för mer information:
* [Tråddumpar](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
* [Analysera minnesproblem](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
* [Analysera med inbyggd profilerare](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
* [Analysera långsamma och blockerade processer](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)



### CPU vid 100 % {#cpu-at}

Om datorns CPU hela tiden körs med 100 % kan du se:

* Kunskapsbasen:

   * [Analysera långsamma och blockerade processer](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### Slut på minne {#out-of-memory}

Även om sådana fel bör identifieras under utveckling och testning kan vissa scenarier gå igenom.

Om minnet håller på att ta slut kan du se det på olika sätt, bland annat på prestandaförsämringar och felmeddelanden, inklusive undertexten:

`java.lang.OutOfMemoryError`

I dessa fall ska du kontrollera:

* JVM-inställningarna som används för att [starta AEM](/help/sites-deploying/deploy.md#getting-started)
* Kunskapsbasen:

   * [Analysera minnesproblem](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### Skiva-I/O {#disk-i-o}

Om det inte finns tillräckligt med diskutrymme på datorn eller om disktrassel börjar visas följande:

* Om du har inaktiverat samling av felsökningsinformation. detta kan konfigureras på olika platser, bland annat:

   * [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Konfiguration av Apache Sling-loggning](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM-felsökningsfilter](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [Loggare](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)[](/help/sites-deploying/configuring.md#loggersandwritersforindividualservices)

* Om och hur du har konfigurerat [versionsrensning](/help/sites-deploying/version-purging.md)
* Kunskapsbasen:

   * [För många öppna filer](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [Journalen förbrukar för mycket diskutrymme](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### Regelbunden prestandaförsämring {#regular-performance-degradation}

Om du ser att prestanda för instansen försämras efter varje omstart (ibland en vecka eller mer senare) kan du kontrollera följande:

* [Slut på minne](#outofmemory)
* Kunskapsbasen:

   * [Oavslutade sessioner](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM-justering {#jvm-tuning}

Java Virtual Machine (JVM) har kraftigt förbättrats när det gäller justering (särskilt sedan Java 7). Därför är det ofta lämpligt att ange en rimlig fast JVM-storlek och att använda standardvärdena.

Om standardinställningarna inte är lämpliga är det viktigt att fastställa en metod för att övervaka och utvärdera prestandan för global katalog innan du försöker justera den virtuella datorn. Detta kan inbegripa övervakningsfaktorer som stackstorlek, algoritm och andra aspekter.

Några vanliga alternativ är:

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

Den resulterande loggen kan importeras av en GC-visualiserare som:

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

Eller JConsole:

* De här inställningarna gäller för en &quot;bred&quot; JMX-anslutning:

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* Anslut sedan till JVM med JConsole; se:
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

Detta hjälper dig att se hur mycket minne som används, vilka GC-algoritmer som används, hur lång tid det tar att köra dem och vilken effekt detta har på programmets prestanda. Utan detta är finjustering bara &quot;slumpmässigt virvlande knoppar&quot;.

>[!NOTE]
För Oracles virtuella dator finns även information på:
[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)