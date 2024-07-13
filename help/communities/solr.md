---
title: Solr-konfiguration för SRP
description: En Apache Solr-installation kan delas mellan nodbutiken (Oak) och den gemensamma lagringsplatsen (SRP) med olika samlingar
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---

# Solr-konfiguration för SRP {#solr-configuration-for-srp}

## Solr for AEM Platform {#solr-for-aem-platform}

En [Apache Solr](https://solr.apache.org/)-installation kan delas mellan [nodarkivet](../../help/sites-deploying/data-store-config.md) (Oak) och [den gemensamma lagringsplatsen](working-with-srp.md) (SRP) med olika samlingar.

Om både Oak- och SRP-samlingar används intensivt kan en andra Solr installeras av prestandaskäl.

I produktionsmiljöer ger [SolrCloud-läget](#solrcloud-mode) bättre prestanda jämfört med fristående läge (en enda lokal Solr-inställning).

### Krav {#requirements}

Hämta och installera Apache Solr:

* [Version 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr kräver Java™ 1.7 eller senare
* Ingen tjänst behövs
* Val av körningslägen:

   * Fristående läge
   * [SolrCloud-läge](#solrcloud-mode) (rekommenderas för produktionsmiljöer)

* Val av flerspråkig sökning (MLS)

   * [Installerar standard-MLS](#installing-standard-mls)
   * [Avancerad MLS installeras](#installing-advanced-mls)

## SolrCloud-läge {#solrcloud-mode}

Läget [SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) rekommenderas för produktionsmiljöer. När SolrCloud körs i SolrCloud-läge måste SolrCloud installeras och konfigureras innan flerspråkig sökning (MLS) installeras.

Rekommendationen är att följa instruktionerna i SolrCloud för att installera:

* 3 SolrCloud-noder på samma server.
* En extern Apache ZooKeeper.

Vi rekommenderar även att du konfigurerar JVM för att justera minnesanvändning och skräpinsamling.

### Exempel på JVM-konfiguration {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Kommandon för att konfigurera SolrCloud {#solrcloud-setup-commands}

När du kör i SolrCloud-läge måste du, innan du installerar MLS, använda och känna till följande SolrCloud-konfigurationskommandon.

#### 1. Överför en konfiguration till ZooKeeper {#upload-a-configuration-to-zookeeper}

Referens:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Användning:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confiname *myconfig-name *\
-solrhome *solr-home-path* \
-confidir *config-dir*

#### 2. Skapa en samling {#create-a-collection}

Referens:
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

Användning:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *port*\
-s *antal delningar* \
-rf *antal-repliker*

#### 3. Länka en samling till en konfigurationsuppsättning {#link-a-collection-to-a-configuration-set}

Länka en samling till en konfiguration som redan har överförts till ZooKeeper.

Referens:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Användning:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confiname *myconfig-name*

### Jämförelse av standard och avancerad MLS {#comparison-of-standard-and-advanced-mls}

Flerspråkig sökning (MLS) för AEM Communities är byggd för Solr-plattformen för att ge bättre sökning på alla språk som stöds, inklusive engelska.

MLS för AEM Communities finns antingen som Standard MLS eller Advanced MLS. Standard-MLS innehåller endast Solr-konfigurationsinställningar och utesluter alla plugin-program eller resursfiler. Advanced MLS är den mer omfattande lösningen och innehåller Solr-konfigurationsinställningar, plugin-program och relaterade resurser

Standard-MLS innehåller förbättringar för innehållssökning för följande språk:

* Engelska: Förbättrad ordstammare för att matcha ordhärledning.
* Japanska: Förbättrad japansk tokenisering för halvbreddstecken.

Avancerad MLS innehåller förbättringar för innehållssökning för följande språk:

* Engelska: Ersatt ordstam med lemmatizer.
* Tyska: Lagt till decomunder.
* Franska: Uteslutningshantering har lagts till.
* Kinesiska (förenklad): En smartare tokeniserare har lagts till.
* Olika språk: har lagt till en ordlista, stoppordlista och en normaliserare.

Följande 33 språk stöds i avancerad MLS.

| Arabiska | Tyska | Norska |
|---|---|---|
| Bulgariska | Grekiska | Polska |
| Kinesiska (förenklad) | Haitiska Creole | Portugisiska |
| Kinesiska (traditionell) | Hebreiska | Rumänska |
| Tjeckiska | Ungerska | Ryska |
| Danska | Indonesiska | Slovakiska |
| Nederländska | Italienska | Slovenska |
| Engelska | Japanska | Spanska |
| Estniska | Koreanska | Svenska |
| Finska | Lettiska | Thailändska |
| Franska | Litauiska | Turkiska |

#### Jämförelse av AEM 6.1 Solr-sökning, Standard MLS och Advanced MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Obs!**: AEM 6.1 hänvisar till AEM 6.1 Communities FP3 och tidigare.

![compare-solr-mls](assets/compare-solr-mls.png)

### Installerar standard-MLS {#installing-standard-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för standard Multilingual Search (MLS) måste två av Solr-konfigurationsfilerna ändras:

* **schema.xml**
* **solrconfig.xml**

Standard-MLS-filer (schema.xml, solrconfig.xml) för Solr 4.10.

Standard-MLS-filer (schema.xml, solrconfig.xml) för Solr 5.x.

Standard-MLS-filerna lagras i AEM.

**Obs!** Solr-filerna lagras i mappen msrp/, men är även för DSRP (inga ändringar krävs).

**Hämtningsinstruktioner**: Ersätt `solrX` med `solr4` eller `solr5` efter behov.

1. Använd CRXDE|Lite, leta upp:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Hämta till den lokala servern där Solr är distribuerad.

   * Leta reda på `jcr:content`-nodens `jcr:data`-egenskap.
   * Välj `view` om du vill starta hämtningen.
   * Se till att filerna sparas med rätt namn och kodning (UTF8).

1. Följ installationsanvisningarna för antingen fristående läge eller SolrCloud-läge.

#### SolrCloud-läge - standard-MLS {#solrcloud-mode-standard-mls}

1. Installera och konfigurera Solr i SolrCloud-läge.
1. Förbered en ny konfiguration:

   1. Skapa ny-config-dir* som `solr-install-dir*/myconfig/`

   1. Kopiera innehållet i befintlig Solr-konfigurationskatalog till *new-config-dir*

      * För Solr4: copy `solr-install-dir/example/solr/collection1/conf/`
      * För Solr5: kopia `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. Kopiera den hämtade **schema.xml** och **solrconfig.xml** till *new-config-dir* om du vill skriva över befintliga filer.

1. [Överför den nya konfigurationen](#upload-a-configuration-to-zookeeper) till ZooKeeper.
1. [Skapa en samling](#create-a-collection) som anger de parametrar som krävs, till exempel antal skevningar, antal replikeringar och konfigurationsnamn.
1. Om konfigurationsnamnet *inte angavs när samlingen skapades [länkar du den nyligen skapade samlingen](#link-a-collection-to-a-configuration-set) med konfigurationen överförd till ZooKeeper.

1. Kör [MSRP Reindex Tool](msrp.md#msrp-reindex-tool) för MSRP, om inte den här installationen är ny.

#### Fristående läge - standard-MLS {#standalone-mode-standard-mls}

1. Installera Solr i fristående läge.
1. Om du kör Solr5 skapar du en samling1 (liknande Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Säkerhetskopiera **schema.xml** och **solrconfig.xml** i Solr-konfigurationsdir, till exempel:

   * För Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Skapad för Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Kopiera den hämtade **schema.xml** och **solrconfig.xml** till samma katalog.

1. Starta om Solr.
1. Kör [MSRP Reindex Tool](#msrpreindextool) för MSRP, om inte den här installationen är ny.

### Avancerad MLS installeras {#installing-advanced-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för avancerad MLS krävs nya Solr-plugin-program förutom ett anpassat schema och en Solr-konfiguration. Alla nödvändiga objekt paketeras i en nedladdningsbar zip-fil. Dessutom ingår ett installationsskript som ska användas när Solr distribueras i fristående läge.

Om du vill hämta det avancerade MLS-paketet läser du [AEM avancerad MLS](deploy-communities.md#aem-advanced-mls) i avsnittet om distribution i dokumentationen.

Så här kommer du igång med installationen av antingen SolrCloud eller fristående läge:

* Ladda ned zip-arkivet AEM-SOLR-MLS till värdservern Solr.
* Packa upp arkivet.

#### SolrCloud-läge - avancerad MLS {#solrcloud-mode-advanced-mls}

Installationsanvisningar - notera de få skillnaderna för Solr4 och Solr5:

1. Installera och konfigurera Solr i SolrCloud-läge.
1. Extrahera innehållet i det avancerade MLS-paketet till disken. Innehållet bör omfatta:

   * **schema.xml**
   * **solrconfig.xml**
   * mappen **stopwords/**
   * mappen **profiler/**
   * mappen **extra-libs/**

1. Förbered en ny konfiguration:

   1. Skapa en *ny-config-dir*

      * Till exempel `solr-install-dir/myconfig/`
      * Skapa undermappar `stopwords/` och `lang/`

   1. Kopiera innehållet i den befintliga Solr-konfigurationsdir till *new-config-dir*

      * För Solr4: Kopiera `solr-install-dir/example/solr/collection1/conf/`
      * För Solr5: Kopiera `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. Kopiera den extraherade **schema.xml** och **solrconfig.xml** till *new-config-dir* om du vill skriva över befintliga filer.
   1. För Solr5: Kopiera `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` till `new-config-dir/lang/`
   1. Kopiera den extraherade mappen **stopwords/** till *new-config-dir* vilket resulterar i `new-config-dir/stopwords/*.txt`

1. [Överför den nya konfigurationen](#upload-a-configuration-to-zookeeper) till ZooKeeper
1. Kopiera den nya mappen **profiles/** ...

   * För Solr4: Kopiera till varje nods resurser/mapp
   * För Solr5: Kopiera till varje Solr-installations server/resurser/mapp. Om alla noder finns i samma installationskatalog för Solr utförs det här steget endast en gång.

1. Skapa en **lib/**-mapp i SolrCloud-katalogen (innehåller solr.xml) för varje nod i SolrCloud. Kopiera burar från följande platser till den nya lib/-mappen på varje nod:

   * **extra-libs/** har extraherats från det avancerade MLS-paketet
   * *solr-install-dir/contribute/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/Contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contribute/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contribute/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contribute/analysis-extras/lib/*.jar
   * *solr-install-dir/contribute/analysis-extras/lucene-libs/*.jar

1. [Skapa en samling](#create-a-collection) som anger de parametrar som krävs, till exempel antal skevningar, antal replikeringar och konfigurationsnamn.
1. Om konfigurationsnamnet *inte* angavs när samlingen skapades [länkar du den nyligen skapade samlingen](#link-a-collection-to-a-configuration-set) med konfigurationen överförd till ZooKeeper.

1. Kör [MSRP Reindex Tool](#msrpreindextool) för MSRP, om inte den här installationen är ny.

#### Fristående läge - avancerad MLS {#standalone-mode-advanced-mls}

Ett installationsskript ingår i det avancerade MLS-paketet.

När innehållet i paketet har extraherats till servern som är värd för den fristående Solr-servern kör du installationsskriptet för att installera nödvändiga resurser och konfigurationsfiler.

* Installera Solr i fristående läge.
* Om du kör Solr5 skapar du en samling1 (liknande Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Kör installationsskriptet: Installera [-v 4|5] [-d solrhome] [-c-samlingssökväg]
där:

   * -d solrhome

     Installationskatalog för Solr

   * -c samlingssökväg

     Samlingsbana i skarp form

   * —help

     Skriv ut kommandoradsalternativ

   * -v [4|5]

     Ange version för soler

* Exempel för Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Exempel för Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Obs!**:

* Installationsskriptet säkerhetskopierar schema.xml och solrconfig.xml innan nya versioner installeras genom att &quot;.orig&quot; läggs till

### Om solrconfig.xml {#about-solrconfig-xml}

Filen **solrconfig.xml** styr intervallet för automatisk implementering och söksynlighet och kräver testning och justering.

`<autoCommit>`: Som standard är intervallet AutoCommit, som är en hård implementering av stabil lagring, inställt på 15 sekunder. Söksynligheten använder som standard indexvärdet före implementering.

Om du vill ändra sökningen till att använda ett index som har uppdaterats för att återspegla ändringar på grund av implementeringen, ändrar du `openSearcher` i innehållet till true.

`autoSoftCommit`: En implementering av mjuk säkerställer att ändringar är synliga (indexet uppdateras), men säkerställer inte att ändringar synkroniseras till stabil lagring (fast implementering). Resultatet blir en prestandaförbättring. Som standard är `autoSoftCommit` inaktiverad med `maxTime` som finns som -1.
