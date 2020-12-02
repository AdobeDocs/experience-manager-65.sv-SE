---
title: MSRP - lagringsresursprovider för MongoDB
seo-title: MSRP - lagringsresursprovider för MongoDB
description: Konfigurera AEM Communities för att använda en relationsdatabas som gemensam lagringsplats
seo-description: Konfigurera AEM Communities för att använda en relationsdatabas som gemensam lagringsplats
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---


# MSRP - MongoDB-lagringsresursprovidern {#msrp-mongodb-storage-resource-provider}

## Om MSRP {#about-msrp}

När AEM Communities har konfigurerats att använda MSRP som gemensam lagringsplats är användargenererat innehåll (UGC) tillgängligt från alla författare- och publiceringsinstanser utan behov av synkronisering eller replikering.

Se även [Egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [Rekommenderade topologier](topologies.md).

## Krav {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Version 2.6 eller senare
   * Du behöver inte konfigurera mongor eller delningar
   * Rekommendera starkt en [replikuppsättning](#mongoreplicaset)
   * Kan köras på samma värd som AEM eller fjärrköras

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr version 7.0
   * Solr kräver Java 1.7 eller senare
   * Ingen tjänst behövs
   * Val av körningslägen:
      * Fristående läge
      * [SolrCloud-läge](solr.md#solrcloud-mode)  (rekommenderas för produktionsmiljöer)
   * Val av flerspråkig sökning (MLS):
      * [Installerar standard-MLS](solr.md#installing-standard-mls)
      * [Avancerad MLS installeras](solr.md#installing-advanced-mls)

## MongoDB-konfiguration {#mongodb-configuration}

### Välj MSRP {#select-msrp}

Med konsolen [Lagringskonfiguration](srp-config.md) kan du välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

På författaren, för att komma åt lagringskonsolen:

* Välj **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Storage Configuration]** från global navigering.

![msrp](assets/msrp.png)

* Välj **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL mongoDB Configuration]**

   * **[!UICONTROL mongoDB URI]**

      *standard*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB Database]**

      *standard*: communities

   * **[!UICONTROL mongoDB UGC Collection]**

      *standard*: innehåll

   * **[!UICONTROL mongoDB Attachment Collection]**

      *standard*: bilagor

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) ZookeeperHost**

      När du kör i [SolrCloud-läge](solr.md#solrcloud-mode) med en extern ZooKeeper anger du det här värdet till `HOST:PORT` för ZooKeeper, till exempel *my.server.com:2181*

      För ZooKeeper Ensemble anger du kommaavgränsade `HOST:PORT`-värden, till exempel *host1:2181,host2:2181*

      Lämna tomt om du kör Solr i fristående läge med den interna ZooKeeper.
      *Standard*:  *&lt;blank>*

      * **[!UICONTROL Solr URL]**
Den URL som används för att kommunicera med Solr i fristående läge.
Lämna tomt om du kör i SolrCloud-läge.

         *Standard*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr Collection]**
Solr-samlingens namn.

         *Standard*: collection1

* Välj **[!UICONTROL Submit]**

>[!NOTE]
>
>MongoDB-databasen, som har standardvärdet `communities`, ska inte anges till namnet på en databas som används för [nodarkiv eller datalager (binära)](../../help/sites-deploying/data-store-config.md). Se även [Lagringselement i AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### MongoDB-replikuppsättning {#mongodb-replica-set}

För produktionsmiljön rekommenderar vi starkt att du skapar en replikuppsättning, ett kluster av MongoDB-servrar som implementerar primär-sekundär replikering och automatiserad failover.

Mer information om replikuppsättningar finns i dokumentationen för MongoDB [Replication](https://docs.mongodb.org/manual/replication/).

Om du vill arbeta med replikuppsättningar och lära dig hur du definierar anslutningar mellan program och MongoDB-instanser går du till dokumentationen för MongoDB:s [URI-format för anslutningssträng](https://docs.mongodb.org/manual/reference/connection-string/).

#### Exempel-URL för anslutning till en replikuppsättning {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr-konfiguration {#solr-configuration}

En Solr-installation kan delas mellan nodbutiken (Oak) och den gemensamma lagringsplatsen (MSRP) med hjälp av olika samlingar.

Om både Oak- och MSRP-samlingarna används intensivt kan en andra Solr installeras av prestandaskäl.

För produktionsmiljöer ger [SolrCloud-läge](solr.md#solrcloud-mode) bättre prestanda jämfört med fristående läge (en enda lokal Solr-inställning).

Mer konfigurationsinformation finns i [Solr Configuration for SRP](solr.md).

### Uppgraderar {#upgrading}

Om du uppgraderar från en tidigare version som konfigurerats med MSRP måste du:

1. Uppgradera [till AEM Communities](upgrade.md)
1. Installera nya Solr-konfigurationsfiler
   * För [standard-MLS](solr.md#installing-standard-mls)
   * För [avancerad MLS](solr.md#installing-advanced-mls)
1. Indexera om MSRP
Se avsnitt [MSRP Reindex Tool](#msrp-reindex-tool)

## Publicera konfigurationen {#publishing-the-configuration}

MSRP måste identifieras som det gemensamma arkivet på alla författar- och publiceringsinstanser.

Om du vill göra den identiska konfigurationen tillgänglig i publiceringsmiljön loggar du in på författarinstansen och följer stegen:

* Navigera från huvudmenyn till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**.
* Välj **[!UICONTROL Activate Tree]**
* **[!UICONTROL Start Path]**:
   * Bläddra till `/etc/socialconfig/srpc/`
* Välj **[!UICONTROL Activate]**

## Hantera användardata {#managing-user-data}

Mer information om *användare*, *användarprofiler* och *användargrupper*, som ofta anges i publiceringsmiljön, finns på

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## MSRP Reindex Tool {#msrp-reindex-tool}

Det finns en HTTP-slutpunkt för omindexering av Solr för MSRP när nya konfigurationsfiler installeras eller ett skadat Solr-index repareras.

Med det här verktyget är MongoDB källan till *sanningen* för MSRP; säkerhetskopior behöver bara tas från MongoDB.

Hela UGC-trädet kan indexeras om, eller endast ett visst underträd, enligt parametern *path *data.

Det här verktyget kan köras från kommandoraden med cURL eller något annat HTTP-verktyg.

Vid omindexering sker en kompromiss mellan minne och prestanda som styrs av parametern *batchSize *data, som anger hur många UGC-poster som omindexeras per batch.

Ett rimligt standardvärde är 5000:

* Om det är problem med minnet anger du ett mindre tal
* Om hastigheten är ett problem anger du ett större tal för att öka hastigheten

### Kör MSRP-omindexeringsverktyget med cURL-kommandot {#running-msrp-reindex-tool-using-curl-command}

Följande cURL-kommando visar vad som krävs för att en HTTP-begäran ska kunna indexera om UGC som lagras i MSRP.

Grundformatet är:

cURL -u *inloggning* -d *data* *reindex-url*

*signin* = administrator-id:password Till exempel: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = hur många UGC-poster som ska indexeras om per operation 
`/content/usergenerated/asi/mongo/`

*path* = rotplatsen för UGC-trädet som ska indexeras om

* Om du vill indexera om all UGC anger du värdet för egenskapen `asipath`för
   `/etc/socialconfig/srpc/defaultconfiguration`
* Om du vill begränsa indexvärdet till en del UGC anger du ett underträd på `asipath`

*reindex-url* = slutpunkten för omindexering av SRP 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Om du [indexerar om DSRP Solr](dsrp.md) är URL:en **/services/social/datastore/rdb/reindex**

### Exempel på omindexering av MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Demo av MSRP {#how-to-demo-msrp}

Information om hur du konfigurerar MSRP för en demonstration- eller utvecklingsmiljö finns i [HowTo Setup MongoDB for Demo](demo-mongo.md).

## Felsökning {#troubleshooting}

### UGC är inte synlig i MongoDB {#ugc-not-visible-in-mongodb}

Kontrollera att MSRP har konfigurerats som standardprovider genom att kontrollera konfigurationen av lagringsalternativet. Som standard är lagringsresursprovidern JSRP.

Gå till [lagringskonsolen](srp-config.md) för alla författare och publicera AEM eller kontrollera AEM:

* I JCR, om [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Innehåller ingen [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)-nod, vilket betyder att lagringsprovidern är JSRP.
   * Om srpc-noden finns och innehåller noden [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), ska standardkonfigurationens egenskaper definiera MSRP som standardprovider.

### UGC försvinner efter uppgradering {#ugc-disappears-after-upgrade}

Om du uppgraderar från en befintlig AEM Communities 6.0-plats måste eventuell befintlig UGC konverteras så att den överensstämmer med den struktur som krävs för API:t [SRP](srp.md) efter uppgradering till AEM Communities 6.3.

Det finns ett verktyg med öppen källkod tillgängligt på GitHub för detta ändamål:

* [AEM Communities UGC-migreringsverktyg](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

Migreringsverktyget kan anpassas för att exportera UGC från tidigare versioner av AEM sociala communities för import till AEM Communities 6.1 eller senare.

### Fel - odefinierat fält provider_id {#error-undefined-field-provider-id}

Om följande fel visas i loggarna anger det att Solr-schemafilen inte är korrekt konfigurerad.

#### JsonMappingException: odefinierad fältprovider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

För att åtgärda felet måste du kontrollera följande när du följer instruktionerna för [Installera standard-MLS](solr.md#installing-standard-mls):

* XML-konfigurationsfilerna kopierades till rätt Solr-plats.
* Solr startades om efter att de nya konfigurationsfilerna ersatt de befintliga.

### Säker anslutning till MongoDB misslyckas {#secure-connection-to-mongodb-fails}

Om ett försök att skapa en säker anslutning till MongoDB-servern misslyckas på grund av att en klassdefinition saknas, är det nödvändigt att uppdatera MongoDB-drivrutinspaketet `mongo-java-driver`, som är tillgängligt från den offentliga maven-databasen.

1. Hämta drivrutinen från [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (version 2.13.2 eller senare).
1. Kopiera paketet till mappen&quot;crx-quickstart/install&quot; för en AEM instans.
1. Starta om AEM.

## Resurser {#resources}

* [AEM med MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB-dokumentation](https://docs.mongodb.org/)

