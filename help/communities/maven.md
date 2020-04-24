---
title: Använda Maven for Communities
seo-title: Använda Maven for Communities
description: AEM Communities API jar och AEM Uber API jar
seo-description: AEM Communities API jar och AEM Uber API jar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# Använda Maven for Communities {#using-maven-for-communities}

## Översikt {#overview}

Det här avsnittet av dokumentationen för AEM Communities innehåller följande:

* [Skapa AEM-projekt med Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Det finns nu två&quot;uber&quot;-artefakter som ersätter enskilda artefakter:

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Jar-artefakt för Communities-API {#communities-api-jar-artifact}

Här följer ett exempel på en GAV för API-behållaren för AEM Communities:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

Kontrollera att den angivna versionen motsvarar den version av webbcommunityn som är installerad för AEM Communities. Så här verifierar du det installerade versionsnumret:

1. Logga in med administratörsbehörighet.
1. Bläddra till [Pakethanteraren](../../help/sites-administering/package-manager.md). Till exempel [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Leta reda på paketet *cq-socialcommunities-pkg-1.x.xxx*
1. Extrahera versionen från paketnamnet:
   * Den första versionen för AEM 6.3 är version 1.11.170.
   * Funktionspaket blir version 1.12.xxx.

>[!NOTE]
>
>Vi rekommenderar att du håller dig uppdaterad med den senaste versionen av Communities.
>
>Gå till avsnittet [Senaste versioner](deploy-communities.md#latest-releases) för att identifiera den senaste versionen.


## Exempel på Maven Dependency {#maven-dependency-example}

Communities API jar måste anges före Uber API jar.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
