---
title: Solr-konfiguration för SRP
seo-title: Solr-konfiguration för SRP
description: En Apache Solr-installation kan delas mellan nodbutiken (Oak) och den gemensamma lagringsplatsen (SRP) med hjälp av olika samlingar
seo-description: En Apache Solr-installation kan delas mellan nodbutiken (Oak) och den gemensamma lagringsplatsen (SRP) med hjälp av olika samlingar
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Solr-konfiguration för SRP {#solr-configuration-for-srp}

## Solr for AEM Platform {#solr-for-aem-platform}

En [Apache Solr](https://lucene.apache.org/solr/) -installation kan delas mellan [nodarkivet](../../help/sites-deploying/data-store-config.md) (Oak) och [Common Store](working-with-srp.md) (SRP) med olika samlingar.

Om både Oak- och SRP-samlingarna används intensivt kan en andra Solr installeras av prestandaskäl.

I produktionsmiljöer ger [SolrCloud-läget](#solrcloud-mode) bättre prestanda jämfört med fristående läge (en enda lokal Solr-inställning).

### Krav {#requirements}

Hämta och installera Apache Solr:

* [Version 4.10](https://archive.apache.org/dist/lucene/solr/4.10.4/) eller [version 5](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* Solr kräver Java 1.7 eller senare
* Ingen tjänst behövs
* Val av körningslägen:

   * Fristående läge
   * [SolrCloud-läge](#solrcloud-mode) (rekommenderas för produktionsmiljöer)

* Val av flerspråkig sökning (MLS)

   * [Installerar standard-MLS](#installing-standard-mls)
   * [Avancerad MLS installeras](#installing-advanced-mls)

## SolrCloud-läge {#solrcloud-mode}

[SolrCloud](https://cwiki.apache.org/confluence/display/solr/SolrCloud) -läge rekommenderas för produktionsmiljöer. När SolrCloud körs i SolrCloud-läge måste SolrCloud installeras och konfigureras innan flerspråkig sökning (MLS) installeras.

Rekommendationen är att följa instruktionerna i SolrCloud för att installera:

* 3 SolrCloud-noder på samma server
* En extern Apache ZooKeeper

Vi rekommenderar även att du konfigurerar JVM för att justera minnesanvändning och skräpinsamling.

### Exempel på JVM-konfiguration {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Kommandon för SolrCloud-konfiguration {#solrcloud-setup-commands}

När du kör i SolrCloud-läge måste du använda och känna till följande SolrCloud-konfigurationskommandon innan du installerar MLS.

#### 1. Överför en konfiguration till ZooKeeper {#upload-a-configuration-to-zookeeper}

Referens:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Användning:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost- *server:port* \
-confiname *myconfig-name *\
-solrhome *solr-home-path* \
-confidir *config-dir*

#### 2.Skapa en samling {#create-a-collection}

Referens:
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Användning: ./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p- *port*\
-s *antal kort* \
-rf *antal repliker*

#### 3. Länka en samling till en konfigurationsuppsättning {#link-a-collection-to-a-configuration-set}

Länka en samling till en konfiguration som redan har överförts till ZooKeeper.

Referens:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Användning:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost- *server:port* \
-collection *mycollection-name* \
-confiname *myconfig-name*

### Jämförelse av standard och avancerad MLS {#comparison-of-standard-and-advanced-mls}

Flerspråkig sökning (MLS) för AEM Communities är byggt för Solr-plattformen för att ge förbättrad sökning på alla språk som stöds, inklusive engelska.

MLS för AEM-communities är tillgängligt som standard-MLS eller avancerad MLS. Standard-MLS innehåller endast Solr-konfigurationsinställningar och utesluter alla plugin-program eller resursfiler. Advanced MLS är den mer omfattande lösningen och innehåller Solr-konfigurationsinställningar samt plugin-program och relaterade resurser

Standard-MLS innehåller förbättringar för innehållssökning för följande språk:

* Engelska: förbättrad ordstam för försök att matcha ordhärledning
* Japanska: förbättrad japansk tokenisering för halvbreddstecken

Avancerad MLS innehåller förbättringar för innehållssökning för följande språk:

* Engelska: ersatt stam med lemmatiker
* Tyska: added decomUnder
* Franska: extra elithantering
* Kinesiska (förenklad): har lagt till en smartare token
* Olika språk: har lagt till en ordlista, stoppordslista och en normaliserare.

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

**Obs**: AEM 6.1 avser AEM 6.1 Communities FP3 och tidigare.

![chlimage_1-283](assets/chlimage_1-283.png)

### Installerar standard-MLS {#installing-standard-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för standard Multilingual Search (MLS) måste två av Solr-konfigurationsfilerna ändras:

* **schema.xml**
* **solrconfig.xml**

Standard-MLS-filer (schema.xml, solrconfig.xml) för Solr 4.10

Standard-MLS-filer (schema.xml, solrconfig.xml) för Solr 5

Standardfilerna för MLS lagras i AEM-databasen.

**Obs**: Solr-filerna lagras i mappen msrp/, men de gäller även för DSRP (inga ändringar krävs).

**Nedladdningsinstruktioner**: ersätt `solrX` med `solr4` eller `solr5` på lämpligt sätt

1. Använda CRXDE|Lite, leta upp

   * /libs/social/config/datastore/msrp/*solrX*/**schema.xml**
   * /libs/social/config/datastore/msrp/*solrX*/**solrconfig.xml**

1. Hämta till den lokala servern där Solr är distribuerad

   * Leta reda på `jcr:content` nodens `jcr:data` egenskap
   * Välj `view` för att starta hämtningen
   * Se till att filerna sparas med rätt namn och kodning (UTF8)

1. Följ installationsanvisningarna för antingen fristående läge eller SolrCloud-läge

#### SolrCloud-läge - standard-MLS {#solrcloud-mode-standard-mls}

1. Installera och konfigurera Solr i SolrCloud-läge
1. Förbered en ny konfiguration:

   1. Skapa *ny-config-dir* , till exempel *solr-install-dir*/myconfig/

   1. Kopiera innehållet i den befintliga Solr-konfigurationskatalogen till *new-config-dir*

      * För Solr4: copy *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * För Solr5: copy *solr-install-dir*/server/solr/configsets/data_driven_schema_configs/&amp;ast;
   1. Kopiera den hämtade **schema.xml** och **solrconfig.xml** till *new-config-dir* för att skriva över befintliga filer


1. [Överför den nya konfigurationen](#upload-a-configuration-to-zookeeper) till ZooKeeper
1. [Skapa en samling](#create-a-collection) som anger nödvändiga parametrar, till exempel antal kort, antal kopior och konfigurationsnamn.
1. Om konfigurationsnamnet *inte angavs när samlingen skapades [länkar du den här samlingen](#link-a-collection-to-a-configuration-set) med konfigurationen överförd till ZooKeeper

1. För MSRP kör du omindexeringsverktyget [för](msrp.md#msrp-reindex-tool)MSRP, såvida det inte är en ny installation

#### Fristående läge - standard-MLS {#standalone-mode-standard-mls}

1. Installera Solr i fristående läge
1. Om du kör Solr5 skapar du en samling1 (liknande Solr4):

   * ./bin/solr start
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

1. Säkerhetskopiera **schema.xml** och **solrconfig.xml** i Solr-konfigurationsdir, till exempel:

   * För Solr4: *solr-install-dir*/example/solr/collection1/conf/
   * Skapat för Solr5: *solr-install-dir*/server/solr/collection1/conf/

1. Kopiera den hämtade **schema.xml** och **solrconfig.xml** till samma katalog

1. Starta om Solr
1. För MSRP kör du omindexeringsverktyget [för](#msrpreindextool)MSRP, såvida det inte är en ny installation

### Avancerad MLS installeras {#installing-advanced-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för avancerad MLS krävs nya Solr-plugin-program förutom ett anpassat schema och en Solr-konfiguration. Alla nödvändiga objekt paketeras i en nedladdningsbar zip-fil. Dessutom ingår ett installationsskript som ska användas när Solr distribueras i fristående läge.

Information om hur du får tillgång till det avancerade MLS-paketet finns i [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) i avsnittet om distribution i dokumentationen.

Så här kommer du igång med installationen av antingen SolrCloud eller fristående läge:

* Ladda ned zip-arkivet AEM-SOLR-MLS till värdservern Solr
* Packa upp arkivet

#### SolrCloud-läge - avancerad MLS {#solrcloud-mode-advanced-mls}

Installationsanvisningar - notera de få skillnaderna för Solr4 och Solr5:

1. Installera och konfigurera Solr i SolrCloud-läge
1. Extrahera innehållet i det avancerade MLS-paketet till disken. Innehållet bör omfatta:

   * **schema.xml**
   * **solrconfig.xml**
   * **stoppord/** mapp
   * **profiler/** mapp
   * **extra-libs/** folder

1. Förbered en ny konfiguration:

   1. Skapa en *ny-config-dir*

      * Till exempel *solr-install-dir*/myconfig/
      * Skapa undermappar med stoppord/ och språk/
   1. Kopiera innehållet i den befintliga Solr-konfigurationsdir till *new-config-dir*

      * För Solr4: Copy *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * För Solr5: Kopiera *solr-install-dir*/server/solr/configsets/data_driven_schema_configs/&amp;ast;
   1. Kopiera den extraherade **schema.xml** och **solrconfig.xml** till *new-config-dir* för att skriva över befintliga filer
   1. För Solr5: Kopiera *solr_install_dir*/server/solr/configsets/sample_techproducts_configs/conf/lang/&amp;ast;.txt&quot; till *new-config-dir*/lang/
   1. Kopiera de extraherade **stopporden/** mappen till *new-config-dir* , vilket resulterar i *new-config-dir*/stopwords/&amp;ast;.txt



1. [Överför den nya konfigurationen](#upload-a-configuration-to-zookeeper) till ZooKeeper
1. Kopiera de nya **profilerna/** mappen ...

   * För Solr4: Kopiera till varje nods resurser/mapp
   * För Solr5: Kopiera till varje Solr-installations server/resurser/-mapp. Om alla noder finns i samma installationskatalog för Solr utförs det här steget endast en gång.

1. Skapa en **lib/** -mapp i Solr-home-katalogen (innehåller solr.xml) för varje nod i SolrCloud. Kopiera burar från följande platser till den nya lib/-mappen på varje nod:

   * **extra libs/** extraherad från det avancerade MLS-paketet
   * *solr-install-dir/contribute/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contribute/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contribute/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contribute/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-speed*.jar
   * *solr-install-dir/contribute/analysis-extras/lib/*.jar
   * *solr-install-dir/contribute/analysis-extras/lucene-libs/*.jar

1. [Skapa en samling](#create-a-collection) som anger nödvändiga parametrar, till exempel antal kort, antal kopior och konfigurationsnamn.
1. Om konfigurationsnamnet *inte* tillhandahölls när samlingen skapades [länkar du den nyligen skapade samlingen](#link-a-collection-to-a-configuration-set) med konfigurationen överförd till ZooKeeper

1. För MSRP kör du omindexeringsverktyget [för](#msrpreindextool)MSRP, såvida det inte är en ny installation

#### Fristående läge - avancerad MLS {#standalone-mode-advanced-mls}

Ett installationsskript ingår i det avancerade MLS-paketet.

När innehållet i paketet har extraherats till servern som är värd för den fristående Solr-servern kör du bara installationsskriptet för att installera nödvändiga resurser och konfigurationsfiler.

* Installera Solr i fristående läge
* Om du kör Solr5 skapar du en samling1 (liknande Solr4):

   * ./bin/solr start
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

* Kör installationsskriptet: Install [-v 4|5] [-d solrhome] [-c collection path]where:

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

**Obs**:

* Installationsskriptet säkerhetskopierar schema.xml och solrconfig.xml innan nya versioner installeras genom att &quot;.orig&quot; läggs till

### Om solrconfig.xml {#about-solrconfig-xml}

Filen **solrconfig.xml** styr intervallet för automatisk implementering och söksynlighet och kommer att kräva testning och justering.

&lt;autoCommit>: Som standard är intervallet AutoCommit, som är en hård implementering av stabil lagring, inställt på 15 sekunder. Söksynligheten använder som standard indexvärdet före implementering.

Om du vill ändra sökningen till att använda ett index som har uppdaterats för att återspegla ändringar på grund av implementeringen ändrar du &lt;openSearcher> till true.

&lt;autoSoftCommit>: En &quot;soft&quot;-implementering ser till att ändringarna är synliga (indexet uppdateras), men säkerställer inte att ändringarna synkroniseras till stabil lagring (fast implementering). Resultatet blir en prestandaförbättring. Som standard är &lt;autoSoftCommit> inaktiverat med &lt;maxTime> inställt på -1.
