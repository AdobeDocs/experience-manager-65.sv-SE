---
title: Körningslägen
seo-title: Run Modes
description: Lär dig hur du trimmar AEM för särskilda syften med körningslägen.
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Körningslägen{#run-modes}

Med körningslägena kan du justera AEM för ett specifikt ändamål; till exempel författare eller publicera, testa, utveckla, intranät eller andra.

Du kan:

* [Definiera samlingar av konfigurationsparametrar för varje körningsläge](#defining-configuration-properties-for-a-run-mode).

  En grundläggande uppsättning konfigurationsparametrar används för alla körningslägen, och du kan sedan justera ytterligare uppsättningar efter syftet med den specifika miljön. Dessa används efter behov.

* [Definiera ytterligare paket som ska installeras för ett visst läge](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Alla inställningar och definitioner lagras i en databas och aktiveras genom att du anger **Körningsläge**.

## Körningslägen för installation {#installation-run-modes}

Installationslägen (eller fasta körningslägen) används vid installationen och korrigeras sedan för instansens hela livstid. De kan inte ändras.

Installationslägena är färdiga:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Detta är två par av ömsesidigt uteslutande körlägen. Du kan till exempel:

* definiera antingen `author` eller `publish`, inte båda samtidigt

* kombinera `author` med antingen `samplecontent` eller `nosamplecontent` (men inte båda)

>[!CAUTION]
>
>När du använder något av ovanstående körningslägen (författare, publicera, sampla innehåll, nosamplingsinnehåll), definierar det värde som används vid installationen körningsläget för *hela livstiden* av den installationen.
>
>För dessa körningslägen *inte* ändra dem efter installationen.

## Anpassade körningslägen {#customized-run-modes}

Du kan också skapa egna, anpassade körningslägen. Dessa kan kombineras för att omfatta scenarier som:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* efter behov. . .

Du kan också välja anpassade körningslägen vid varje start.

## Använda exempelinnehåll och nosamplingsinnehåll {#using-samplecontent-and-nosamplecontent}

Med dessa lägen kan du styra användningen av exempelinnehåll. Exempelinnehållet definieras innan snabbstarten byggs och kan innehålla paket, konfigurationer osv.:

* The `samplecontent` det här innehållet installeras i körningsläget (standardläget).

* The `nosamplecontent` exempelinnehållet installeras inte i det här läget.

Körningsläget nosampling-innehåll är utformat för produktionsinstallationer.

## Definiera konfigurationsegenskaper för ett körningsläge {#defining-configuration-properties-for-a-run-mode}

En samling värden för konfigurationsegenskaper, som används för ett visst körningsläge, kan sparas i databasen.

Körningsläget anges med ett suffix i mappnamnet. På så sätt kan du spara alla konfigurationer i en databas som. Till exempel:

* `config`

  Gäller för alla körningslägen

* `config.author`

  Används för författarens körningsläge

* `config.publish`

  Används för publiceringskörningsläge

* `config.<run-mode>`

  Används för tillämpligt körläge. till exempel config

Se [OSGi-konfiguration i databasen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) om du vill ha mer information om hur du definierar enskilda konfigurationsnoder i dessa mappar och om hur du skapar konfigurationer för kombinationer av flera körningslägen.

>[!NOTE]
>
>För [Körningslägen för installation](#installation-run-modes) (till exempel författare) Körningsläget kan inte ändras efter installationen. Ändringar av de enskilda konfigurationsegenskaperna börjar dock gälla efter omstart.

## Definiera ytterligare paket som ska installeras för ett körningsläge {#defining-additional-bundles-to-be-installed-for-a-run-mode}

Ytterligare paket som ska installeras för ett visst körläge kan också anges. För dessa definitioner används installationsmappar för att lagra paketen. Återigen anges körningsläget med ett prefix:

* `install.author`
* `install.publish`

De här mapparna är av typen `nt:folder` och ska innehålla rätt paket.

## Starta CQ med ett specifikt körningsläge {#starting-cq-with-a-specific-run-mode}

Om du har definierat konfigurationer för flera körningslägen måste du definiera vilka som ska användas vid start. Det finns flera metoder för att specificera vilket körningsläge som ska användas. Upplösningsordningen är

1. [systemegenskaper (](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [Filnamnsidentifiering](#filename-detection-renaming-the-jar-file)

När du använder en programserver kan du även [definiera körningsläget i web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Använda filen sling.properties {#using-the-sling-properties-file}

The `sling.properties` filen kan användas för att definiera det körningsläge som krävs:

1. Redigera konfigurationsfilen:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Lägg till följande egenskaper: följande exempel är för författaren:

   `sling.run.modes=author`

### Använda alternativet -r {#using-the-r-option}

Ett anpassat körningsläge kan aktiveras med `-r` när snabbstarten startas. Använd till exempel följande kommando för att starta en AEM med körningsläget inställt på dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Använda en systemegenskap i startskriptet {#using-a-system-property-in-the-start-script}

En systemegenskap i startskriptet kan användas för att ange körningsläget.

* Använd till exempel följande för att starta en instans som publiceringsinstans för produktion i USA:

  `-Dsling.run.modes=publish,prod,us`

### Filnamnsidentifiering - byta namn på filen jar {#filename-detection-renaming-the-jar-file}

Följande två installationskörningslägen kan aktiveras genom att man byter namn på installationsfilen före installationen:

* publicera
* författare

jar-filen måste ha samma namn:

`cq5-<run-mode>-p<port-number>`

Ange till exempel `publish` körningsläge genom att ge filen ett namn:

`cq5-publish-p4503`

### Definiera körningsläget i web.xml (med Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

När du använder en programserver kan du även konfigurera egenskapen:

`sling.run.modes`

i filen:

`WEB-INF/web.xml`

Det här är i AEM `war` filen och ska uppdateras före distributionen.

Se [Installera AEM med en programserver](/help/sites-deploying/application-server-install.md) för mer information.
