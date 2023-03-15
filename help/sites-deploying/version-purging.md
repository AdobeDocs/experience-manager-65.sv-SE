---
title: Rensning av version
seo-title: Version Purging
description: I den här artikeln beskrivs de tillgängliga alternativen för att rensa versioner.
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Rensning av version{#version-purging}

I en standardinstallation AEM en ny version av en sida eller nod när du aktiverar en sida efter att innehållet har uppdaterats.

>[!NOTE]
>
>Om inga innehållsändringar görs visas ett meddelande om att sidan har aktiverats, men ingen ny version skapas

Du kan skapa ytterligare versioner på begäran med **Versionshantering** sidosparkens flik. Dessa versioner lagras i databasen och kan återställas om det behövs.

Dessa versioner rensas aldrig, så databasstorleken kommer att öka med tiden och måste därför hanteras.

AEM levereras med olika mekanismer som hjälper dig att hantera din databas:

* den [Versionshanteraren](#version-manager)
Detta kan konfigureras för att rensa gamla versioner när nya versioner skapas.

* den [Rensa versioner](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) -verktyg Detta används som en del i övervakningen och underhållet av din databas.
Du kan ingripa för att ta bort gamla versioner av en nod, eller en hierarki av noder, enligt följande parametrar:

   * Det maximala antalet versioner som ska behållas i databasen.
När den här siffran överskrids tas den äldsta versionen bort.

   * Högsta ålder för alla versioner som lagras i databasen.
När en versions ålder överskrider det här värdet rensas den från databasen.

* den [Underhållsaktivitet för versionsrensning](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Du kan schemalägga underhållsaktiviteten Rensa version så att tidigare versioner tas bort automatiskt. Därför minimeras behovet av att manuellt använda verktygen för versionsrensning.

>[!CAUTION]
>
>För att optimera databasstorleken bör du köra versionsrensningen ofta. Uppgiften bör schemaläggas utanför kontorstid när trafiken är begränsad.

## Versionshanteraren {#version-manager}

Förutom explicit rensning med rensningsverktyget kan Version Manager konfigureras för att rensa gamla versioner när nya versioner skapas.

Så här konfigurerar du versionshanteraren: [skapa en konfiguration](/help/sites-deploying/configuring-osgi.md) for:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Följande alternativ är tillgängliga:

* `versionmanager.createVersionOnActivation` (Boolean, standard: true) Anger om en version ska skapas när sidor aktiveras.
En version skapas såvida inte replikeringsagenten har konfigurerats för att förhindra att versioner skapas, vilket stöds av versionshanteraren.
En version skapas bara om aktiveringen sker på en sökväg som finns i `versionmanager.ivPaths` (se nedan).

* `versionmanager.ivPaths`(String[], standard: `{"/"}`) Anger sökvägarna som versioner skapas implicit vid aktivering om `versionmanager.createVersionOnActivation` är inställt på true.

* `versionmanager.purgingEnabled` (Boolean, standard: false) Anger om rensning ska aktiveras när nya versioner skapas eller inte.

* `versionmanager.purgePaths` (String[], standard: {&quot;/content&quot;}) Anger på vilka sökvägar versioner ska rensas när nya versioner skapas.

* `versionmanager.maxAgeDays` (int, standard: 30) Vid versionsrensning tas alla versioner som är äldre än det konfigurerade värdet bort. Om värdet är mindre än 1 utförs inte rensning baserat på versionens ålder.

* `versionmanager.maxNumberVersions` (int, standard 5) Vid versionsrensning tas alla versioner som är äldre än den n:te nyaste versionen bort. Om värdet är mindre än 1 utförs inte rensning baserat på antalet versioner.

* `versionmanager.minNumberVersions` (int, standard 0) Det minsta antal versioner som behålls oavsett ålder. Om värdet är mindre än 1 behålls inget minsta antal versioner.

>[!NOTE]
>
>Vi rekommenderar inte att du behåller ett stort antal versioner i databasen. Så när du konfigurerar versionsrensningsåtgärden bör du tänka på att inte utesluta för många versioner från rensningen, eftersom databasstorleken då inte optimeras korrekt. Om du har ett stort antal versioner på grund av verksamhetskrav kontaktar du supporten för Adobe för att hitta alternativa sätt att optimera databasstorleken.

### Kombinera kvarhållningsalternativ {#combining-retention-options}

Alternativen som definierar hur versionerna ska behållas ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`) kan kombineras beroende på dina behov.

Om du till exempel definierar det maximala antalet versioner som ska behållas OCH den äldsta versionen som ska behållas:

* Inställning:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Med:

   * 10 versioner under de senaste 60 dagarna
   * 3 av dessa versioner har skapats under de senaste 30 dagarna

* Betyder det:

   * De senaste 3 versionerna behålls

Om du till exempel definierar det högsta OCH lägsta antalet versioner som ska behållas OCH den äldsta versionen som ska behållas:

* Inställning:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Med:

   * 5 versioner för 60 dagar sedan

* Betyder det:

   * 3 versioner behålls

## Rensa versioner {#purge-versions-tool}

The [Rensa versioner](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) är avsett för att rensa versioner av en nod eller en hierarki av noder i din databas. Dess främsta syfte är att hjälpa dig att minska storleken på databasen genom att ta bort tidigare versioner av dina noder.
