---
title: DSRP - Resursprovider för relativ databaslagring
description: Konfigurera AEM Communities för att använda en relationsdatabas som gemensam lagringsplats
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# DSRP - Resursprovider för relativ databaslagring {#dsrp-relational-database-storage-resource-provider}

## Om DSRP {#about-dsrp}

När AEM Communities har konfigurerats att använda en relationsdatabas som gemensam lagringsplats är användargenererat innehåll (UGC) tillgängligt från alla författare- och publiceringsinstanser utan behov av synkronisering eller replikering.

Se även [Egenskaper för SRP-alternativ](working-with-srp.md#characteristics-of-srp-options) och [Rekommenderade topologier](topologies.md).

## Krav {#requirements}

* [MySQL](#mysql-configuration), en relationsdatabas.
* [Apache Solr](#solr-configuration), en sökplattform.

>[!NOTE]
>
>Standardlagringskonfigurationen lagras nu i conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) istället för `etc` bana (`/etc/socialconfig/srpc/defaultconfiguration`). Du rekommenderas att följa [migreringssteg](#zerodt-migration-steps) så att standardinställningarna fungerar som förväntat.

## Konfiguration av relationsdatabas {#relational-database-configuration}

### MySQL-konfiguration {#mysql-configuration}

En MySQL-installation kan delas mellan aktiveringsfunktioner och en gemensam lagringsplats (DSRP) inom samma anslutningspool genom att använda olika databasnamn (schema) och även olika anslutningar (server:port).

Installations- och konfigurationsinformation finns i [MySQL-konfiguration för DSRP](dsrp-mysql.md).

### Solr-konfiguration {#solr-configuration}

En Solr-installation kan delas mellan nodbutiken (Oak) och den gemensamma lagringsplatsen (SRP) med olika samlingar.

Om både Oak- och SRP-samlingarna används intensivt kan en andra Solr installeras av prestandaskäl.

För produktionsmiljöer ger SolrCloud-läget bättre prestanda jämfört med fristående läge (en enda lokal Solr-inställning).

Installations- och konfigurationsinformation finns i [Solr-konfiguration för SRP](solr.md).

### Välj DSRP {#select-dsrp}

The [Konsol för lagringskonfiguration](srp-config.md) gör det möjligt att välja standardlagringskonfiguration, som identifierar vilken implementering av SRP som ska användas.

På författaren, för att komma åt lagringskonsolen

* Logga in med administratörsbehörighet
* Från **huvudmeny**

   * Välj **[!UICONTROL Tools]** (från den vänstra rutan)
   * Välj **[!UICONTROL Communities]**
   * Välj **[!UICONTROL Storage Configuration]**

      * Resultatet blir till exempel: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >Standardlagringskonfigurationen lagras nu i conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) istället för `etc` bana (`/etc/socialconfig/srpc/defaultconfiguration`). Du rekommenderas att följa [migreringssteg](#zerodt-migration-steps) så att standardinställningarna fungerar som förväntat.

  ![dsrp-config](assets/dsrp-config.png)

* Välj **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **Databaskonfiguration**

   * **[!UICONTROL JDBC datasource name]**

     Namnet som ges till MySQL-anslutningen måste vara detsamma som anges i [JDBC OSGi-konfiguration](dsrp-mysql.md#configurejdbcconnections)

     *standard*: communities

   * **[!UICONTROL Database name]**

     Namnet ges till schemat i [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

     *standard*: communities

* **SolrConfiguration**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) Värd**

     Lämna det här värdet tomt om du kör Solr med den interna ZooKeeper. Annars, när du kör i [SolrCloud-läge](solr.md#solrcloud-mode) med en extern ZooKeeper anger du det här värdet till URI:n för ZooKeeper, till exempel *my.server.com:80*

     *standard*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

     *standard*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr Collection]**

     *standard*: collection1

* Välj **[!UICONTROL Submit]**.

### Migreringssteg utan driftstopp för standardstart {#zerodt-migration-steps}

Kontrollera att standardsidan [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) fungerar som förväntat, gör så här:

1. Byta namn på banan vid `/etc/socialconfig` till `/etc/socialconfig_old`så att systemkonfigurationen återgår till jsrp (standard).
1. Gå till standardsidan [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), där jsrp är konfigurerat. Klicka på **[!UICONTROL submit]** så att en ny standardkonfigurationsnod skapas på `/conf/global/settings/community/srpc`.
1. Ta bort den skapade standardkonfigurationen `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Kopiera den gamla konfigurationen `/etc/socialconfig_old/srpc/defaultconfiguration` i stället för den borttagna noden (`/conf/global/settings/community/srpc/defaultconfiguration`) i föregående steg.
1. Ta bort gamla `etc` nod `/etc/socialconfig_old`.

## Publicera konfigurationen {#publishing-the-configuration}

DSRP måste identifieras som det gemensamma arkivet för alla författar- och publiceringsinstanser.

Så här gör du den identiska konfigurationen tillgänglig i publiceringsmiljön:

* On author:

   * Navigera från huvudmenyn till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**
   * Dubbelklicka **[!UICONTROL Activate Tree]**
   * **Startbana**:

      * Bläddra till `/etc/socialconfig/srpc/`

   * Säkerställ `Only Modified` är inte markerat.
   * Välj **[!UICONTROL Activate]**.

## Hantera användardata {#managing-user-data}

För information om *användare*, *användarprofiler* och *användargrupper*, som ofta används i publiceringsmiljön, går till:

* [Användarsynkronisering](sync.md)
* [Hantera användare och användargrupper](users.md)

## Indexerar om Solr för DSRP {#reindexing-solr-for-dsrp}

Om du vill indexera om DSRP Solr följer du dokumentationen för [omindexering av MSRP](msrp.md#msrp-reindex-tool)Använd i stället den här URL:en när du indexerar om för DSRP: **/services/social/datastore/rdb/reindex**

Ett CTRL-kommando för att indexera om DSRP ser ut så här:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
