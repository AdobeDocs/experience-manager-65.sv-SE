---
title: DSRP - Resursprovider för relativ databaslagring
seo-title: DSRP - Resursprovider för relativ databaslagring
description: Konfigurera AEM Communities så att en relationsdatabas används som gemensam butik
seo-description: Konfigurera AEM Communities så att en relationsdatabas används som gemensam butik
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: b7c790681034e9950aa43738310f7af8b1dd0085

---


# DSRP - Resursprovider för relativ databaslagring {#dsrp-relational-database-storage-resource-provider}

## Om DSRP {#about-dsrp}

När AEM Communities är konfigurerat att använda en relationsdatabas som gemensam lagringsplats är användargenererat innehåll (UGC) tillgängligt från alla författare och publiceringsinstanser utan behov av synkronisering eller replikering.

Se även [egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [rekommenderade topologier](topologies.md).

## Krav {#requirements}

* [MySQL](#mysql-configuration), en relationsdatabas
* [Apache Solr](#solr-configuration), en sökplattform

>[!NOTE]
>
>Standardlagringskonfigurationen lagras nu i conf-sökvägen(`/conf/global/settings/community/srpc/defaultconfiguration`) i stället för etc-sökvägen (`/etc/socialconfig/srpc/defaultconfiguration`). Du rekommenderas att följa [migreringsstegen](#zerodt-migration-steps) för att få standardinställningarna att fungera som förväntat.


## Konfiguration av relationsdatabas {#relational-database-configuration}

### MySQL-konfiguration {#mysql-configuration}

En MySQL-installation kan delas mellan aktiveringsfunktioner och en gemensam lagringsplats (DSRP) inom samma anslutningspool genom att använda olika databasnamn (schema) och även olika anslutningar (server:port).

Installations- och konfigurationsinformation finns i [MySQL-konfiguration för DSRP](dsrp-mysql.md).

### Solr-konfiguration {#solr-configuration}

En Solr-installation kan delas mellan nodbutiken (Oak) och den gemensamma lagringsplatsen (SRP) med hjälp av olika samlingar.

Om både Oak- och SRP-samlingarna används intensivt kan en andra Solr installeras av prestandaskäl.

För produktionsmiljöer ger SolrCloud-läget bättre prestanda jämfört med fristående läge (en enda lokal Solr-inställning).

Installations- och konfigurationsinformation finns i [Solr Configuration for SRP](solr.md).

### Välj DSRP {#select-dsrp}

Med konsolen [för](srp-config.md) lagringskonfiguration kan du välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

På författaren, för att komma åt lagringskonsolen

* Logga in med administratörsbehörighet
* Från **huvudmenyn**

   * Välj **[!UICONTROL Verktyg]** (från den vänstra rutan)
   * Välj **[!UICONTROL Communities]**
   * Välj **[!UICONTROL lagringskonfiguration]**

      * Som ett exempel är den resulterande platsen: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >Standardlagringskonfigurationen lagras nu i conf-sökvägen(`/conf/global/settings/community/srpc/defaultconfiguration`) i stället för etc-sökvägen (`/etc/socialconfig/srpc/defaultconfiguration`). Du rekommenderas att följa [migreringsstegen](#zerodt-migration-steps) för att få standardinställningarna att fungera som förväntat.

![chlimage_1-128](assets/chlimage_1-128.png)

* Välj **[!UICONTROL provider för databaslagringsresurs (DSRP)]**
* **Databaskonfiguration**

   * **[!UICONTROL Namn på JDBC-datakälla]**

      Namnet som ges till MySQL-anslutningen måste vara samma som det som anges i [JDBC OSGi-konfigurationen](dsrp-mysql.md#configurejdbcconnections)

      *standard*: communities

   * **[!UICONTROL Databasnamn]**

      Namn som ges till schema i [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) -skript

      *standard*: communities

* **SolrConfiguration**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)-värd **

      Lämna det här värdet tomt om du kör Solr med den interna ZooKeeper. Om du kör i [SolrCloud-läge](solr.md#solrcloud-mode) med en extern ZooKeeper anger du det här värdet till URI:n för ZooKeeper, till exempel *my.server.com:80*

      *standard*: *&lt;blank>*

   * **[!UICONTROL Solr-URL]**

      *standard*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr Collection]**

      *standard*: collection1

* Välj **[!UICONTROL Skicka]**.

### Migreringssteg utan driftstopp för standardstart {#zerodt-migration-steps}

Följ de här stegen för att se till att standardsidan [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) fungerar som förväntat:

1. Byt namn på sökvägen `/etc/socialconfig` till `/etc/socialconfig_old`, så att systemkonfigurationen återgår till jsrp (standard).
1. Gå till standardsidan [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)där jsrp är konfigurerat. Klicka på knappen **[!UICONTROL Skicka]** så att en ny standardkonfigurationsnod skapas `/conf/global/settings/community/srpc`.
1. Ta bort den skapade standardkonfigurationen `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Kopiera den gamla konfigurationen `/etc/socialconfig_old/srpc/defaultconfiguration` i stället för den borttagna noden (`/conf/global/settings/community/srpc/defaultconfiguration`) i föregående steg.
1. Ta bort den gamla etc-noden `/etc/socialconfig_old`.

## Publicera konfigurationen {#publishing-the-configuration}

DSRP måste identifieras som det gemensamma arkivet för alla författar- och publiceringsinstanser.

Så här gör du den identiska konfigurationen tillgänglig i publiceringsmiljön:

* On author:

   * Navigera från huvudmenyn till **[!UICONTROL Verktyg > Åtgärder > Replikering]**
   * Dubbelklicka på **Aktivera träd **
   * **Startsökväg:**

      * Bläddra till `/etc/socialconfig/srpc/`
   * Kontrollera att `Only Modified` inte är markerat.
   * Välj **[!UICONTROL Aktivera]**


## Hantera användardata {#managing-user-data}

Information om *användare*, *användarprofiler* och *användargrupper* som ofta används i publiceringsmiljön finns på

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## Indexerar om Solr för DSRP {#reindexing-solr-for-dsrp}

Om du vill indexera om DSRP Solr följer du dokumentationen för [omindexering av MSRP](msrp.md#msrp-reindex-tool), men när du omindexerar för DSRP använder du den här URL:en i stället: **/services/social/datastore/rdb/reindex**

Ett CTRL-kommando för att indexera om DSRP ser ut så här:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

