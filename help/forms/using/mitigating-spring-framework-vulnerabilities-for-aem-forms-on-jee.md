---
title: Minska riskerna för vårramverk för AEM Forms i JEE
description: Minska riskerna för vårramverk för AEM Forms i JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Minska vårens ramverk - sårbarheter för AEM Forms i JEE

I det här dokumentet finns vägledning om hur du åtgärdar två allvarliga säkerhetsluckor i Spring Framework som påverkar AEM Forms i JEE:

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**: Sårbarhet för genomgång av sökväg i funktionella webbramverk
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**: Fjäderrams-undantag för DataBinder Case-känslig matchning

## Berörda versioner

- Adobe Experience Manager 6.5 Forms on JEE
- Versioner av AEM 6.5 Forms GA till 6.5.22.0

## Upplösning

### Versionsspecifika lösningar

| AEM Forms Version | Nödvändig åtgärd |
|-------------------|-----------------|
| 6.5.22.0 | 1. [Hämta snabbkorrigeringen för din miljö](/help/release-notes/aem-forms-hotfix.md). </br> 2. Installera den här korrigeringen genom att följa instruktionerna för att [installera Service Pack på ett AEM-formulär på JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). |
| 6.5.17.0 - 6.5.21.0 | [Använd manuell reducering &#x200B;](#manual-mitigation-steps). |
| 6.5 - 6.5.16.0 | 1. [Installera den senaste Service Pack-versionen](/help/release-notes/release-notes.md)<br>2. [Implementera lämplig lösning](#version-specific-solutions) baserat på din uppdaterade version. |

> **Obs!**: AEM Forms stöder officiellt endast de sex senaste Service Pack-paketen. Användare med äldre versioner bör först uppgradera till det senaste Service Pack-paketet och sedan installera den snabbkorrigering som krävs.

## Överväganden vid distribution

### För klustrade miljöer

När du arbetar med en klustrad distribution:

- Tillämpa JAR-filersättningar (steg 4) på **alla noder** i klustret
- Bibehåll enhetligheten genom att använda identiska JAR-versioner på alla servrar
- Slutför uppdateringar på alla noder innan du startar om tjänsten
- Implementera en samordnad startstrategi för att minimera driftstopp i systemet

### För ennodsmiljöer

När du arbetar med en fristående distribution:

- Följ en förenklad process eftersom det inte finns några lokaliseringsservrar att hantera
- Utelämna alla steg som rör konfigurationen eller starten av positionerarservern
- Slutför alla andra steg enligt instruktionerna, särskilt JAR-ersättningar och manifestuppdateringar
- Starta om programservern när du har implementerat alla ändringar

## Manuella åtgärder

1. Stoppa programservrarna.
1. Stopp- och lokaliseringsservrar.
1. Ta bort fjäder-JAR från Core EAR:
   1. Navigera till `[Adobe_Experience_Manager_Forms installation directory]/deploy`.
   1. Öppna filen `adobe-core-<appserver>.ear` med ett arkivhanterarverktyg. Var `<appserver>` kan vara JBoss, WebLogic eller WebSphere, beroende på din miljö:
   - **För JBoss:** Navigera till mappen `ear/lib` och ta bort följande JAR-filer:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **För WebLogic eller WebSphere:** Ta bort följande JAR-filer från EAR-roten:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **För alla programservrar:** På rotnivån för `adobe-core-<appserver>.ear` öppnar du filen `adobe-dscf.jar` och redigerar filen `META-INF/MANIFEST.MF` för att ta bort referenser till följande JAR-filer:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Ersätt JAR-filer från Geode-distribution:
   1. Navigera till `<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. Ersätt de befintliga JAR-filerna med de uppdaterade versionerna:
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   Hämta de nyare JAR-filerna genom att hämta filen spring-6.1.14-jars.zip från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip) och extrahera ZIP-filen för att komma åt de uppdaterade JAR-filerna för Spring Framework.

   1. Uppdatera MANIFEST.MF-filerna i följande JAR-filer:
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   För varje JAR:
   - Öppna JAR med hjälp av ett arkivhanteringsverktyg
   - Hitta och extrahera filen `META-INF/MANIFEST.MF`
   - Redigera filen MANIFEST.MF i en textredigerare
   - Hitta avsnittet &quot;Class-Path&quot; och uppdatera alla vårens ramverksreferenser:
      - `spring-core-<version>.jar` till `spring-core-6.1.14.jar`
      - `spring-web-<version>.jar` till `spring-web-6.1.14.jar`
      - `spring-context-<version>.jar` till `spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar` till `spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar` till `spring-jcl-6.1.14.jar`
   - Spara den ändrade filen MANIFEST.MF
   - Ersätt den ursprungliga MANIFEST.MF i JAR med den uppdaterade versionen
   - Spara JAR-filen

   1. Vanliga problem att bevaka:
      - Kontrollera att det inte finns några dubblettposter i manifestet
      - Underhåll rätt radslut
      - Kontrollera att alla refererade JAR finns på de angivna platserna

   1. Verifieringssteg:
      - Kontrollera om manifestet har uppdaterats korrekt
      - Kontrollera att alla fjäderberoenden refereras korrekt
      - Kontrollera att inga gamla versionsreferenser finns kvar
      - Testa programmet för att bekräfta att det inte finns några inläsningsproblem för klassen

1. Kör Configuration Manager.

1. Starta om servrar:
   - Starta Locator-servrarna med JDK 17
   - Starta programservrarna med samma JDK-version (JDK 8 eller JDK 11) som tidigare användes.
