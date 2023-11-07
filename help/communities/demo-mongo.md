---
title: Så här konfigurerar du MongoDB för demo
description: Konfigurera MSRP för en författarinstans och en publiceringsinstans
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Så här konfigurerar du MongoDB för demo {#how-to-setup-mongodb-for-demo}

## Introduktion {#introduction}

I den här självstudiekursen beskrivs hur du konfigurerar [MSRP](msrp.md) for *en författare* instans och *en publicering* -instans.

Med den här konfigurationen är communityinnehållet tillgängligt både från författare- och publiceringsmiljöer utan att du behöver vidarebefordra eller omvända replikera användargenererat innehåll (UGC).

Den här konfigurationen är lämplig för *icke-produktion* miljöer som utveckling och/eller demonstration.

**A *produktion* miljön bör:**

* Kör MongoDB med en replikuppsättning
* Använd SolrCloud
* Innehåller flera utgivarinstanser

## MongoDB {#mongodb}

### Installera MongoDB {#install-mongodb}

* Hämta MongoDB från [https://www.mongodb.com/](https://www.mongodb.com/)

   * Val av operativsystem:

      * Linux®
      * Mac 10.8
      * Windows 7

   * Val av version:

      * Använd minst version 2.6

* Grundkonfiguration

   * Följ installationsanvisningarna för MongoDB.
   * Konfigurera för mongod:

      * Du behöver inte konfigurera mongor eller delningar.

   * Den installerade MongoDB-mappen anropas &lt;mongo-install>.
   * Den definierade datakatalogsökvägen anropas &lt;mongo-dbpath>.

* MongoDB kan köras på samma värd som AEM eller fjärrköras.

### Starta MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

Detta startar en MongoDB-server med standardport 27017.

* För Mac ökar du ulimit med start arg &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Om MongoDB startas *efter* AEM, **starta** alla **AEM** -instanser så att de kan ansluta till MongoDB.

### Demo Production Option: Konfigurera MongoDB-replikuppsättning {#demo-production-option-setup-mongodb-replica-set}

Följande kommandon är ett exempel på hur du konfigurerar en replikuppsättning med 3 noder på localhost:

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Installera Solr {#install-solr}

* Hämta Solr från [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Passar alla operativsystem.
   * Solr version 7.0.
   * Solr kräver Java™ 1.7 eller senare.

* Grundkonfiguration

   * Följ exemplet Solr-konfigurationen.
   * Ingen tjänst behövs.
   * Den installerade Solr-mappen anropas &lt;solr-install>.

### Konfigurera Solr för AEM Communities {#configure-solr-for-aem-communities}

Om du vill konfigurera en Solr-samling för MSRP för demo måste du fatta två beslut (markera länkarna till huvuddokumentationen för mer information):

1. Kör Solr i fristående eller [SolrCloud-läge](msrp.md#solrcloudmode).
1. Installera [standard](msrp.md#installingstandardmls) eller [avancerat](msrp.md#installingadvancedmls) flerspråkig sökning (MLS).

### Fristående solr {#standalone-solr}

Metoden för att köra Solr kan variera beroende på version och installationssätt. The [Referenshandbok för solenergi](https://archive.apache.org/dist/lucene/solr/ref-guide/) är den officiella dokumentationen.

För enkelhetens skull kan du använda version 4.10 som exempel genom att starta Solr i fristående läge:

* cd till &lt;solrinstall>/example
* Java™ -jar start.jar

Den här processen startar en Solr HTTP-server med standardport 8983. Du kan bläddra till Solr Console för att få en Solr-konsol för testning.

* standardSolr-konsol: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Om Solr Console inte är tillgänglig kontrollerar du loggarna under &lt;solrinstall>/example/logs. Kontrollera om SOLR försöker binda till ett specifikt värdnamn som inte kan matchas (till exempel &quot;user-macbook-pro&quot;).
>
Uppdatera i så fall `etc/hosts` fil med en ny post för det här värdnamnet (till exempel 127.0.0.1 user-macbook-pro) för att stjärngradera Solr korrekt.

### SolrCloud {#solrcloud}

Om du vill köra en grundkonfiguration (inte en produktion) av molnet börjar du med:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identifiera MongoDB som Common Store {#identify-mongodb-as-common-store}

Starta författaren och publicera AEM om det behövs.

Om AEM kördes innan MongoDB startades måste AEM startas om.

Följ instruktionerna på huvuddokumentationssidan: [MSRP - MongoDB Common Store](msrp.md)

## Testa {#test}

Om du vill testa och verifiera den gemensamma lagringsplatsen för MongoDB skickar du en kommentar på publiceringsinstansen och visar den på författarinstansen, och visar UGC:n i MongoDB och Solr:

1. I publiceringsinstansen bläddrar du till [Guide för communitykomponenter](http://localhost:4503/content/community-components/en/comments.html) och väljer kommentarkomponenten.
1. Logga in för att publicera en kommentar:
1. Ange text i kommentartextrutan och klicka på **[!UICONTROL Post]**

   ![efter kommentar](assets/post-comment.png)

1. Visa bara kommentaren i [författarinstans](http://localhost:4502/content/community-components/en/comments.html) (troligen fortfarande inloggad som administratör/administratör).

   ![view-comment](assets/view-comment.png)

   Obs! Det finns JCR-noder under *asipath* När du har skrivit är de här noderna för SCF-ramverket. Den faktiska UGC:n finns inte i JCR, utan i MongoDB.

1. Se användargenerationen i mongudb **[!UICONTROL Communities]** > **[!UICONTROL Collections]** > **[!UICONTROL Content]**

   ![ugc-content](assets/ugc-content.png)

1. Visa användargenererat innehåll i Solr:

   * Bläddra till Solr-instrumentpanelen: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Användare `core selector` för att markera `collection1`.
   * Välj `Query`.
   * Välj `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Felsökning {#troubleshooting}

### Ingen UGC visas {#no-ugc-appears}

1. Kontrollera att MongoDB är installerat och körs korrekt.

1. Kontrollera att MSRP har konfigurerats som standardprovider:

   * Om du skriver och publicerar AEM kan du gå till [Konsol för lagringskonfiguration](srp-config.md)eller kontrollera AEM:

   * I JCR, om [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) innehåller inte [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) -nod betyder det att lagringsprovidern är JSRP.
   * Om srpc-noden finns och innehåller nod [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)ska standardkonfigurationens egenskaper definiera MSRP som standardprovider.

1. Se till att AEM startades om när MSRP har valts.
