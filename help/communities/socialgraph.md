---
title: Använda socialt diagram
seo-title: Använda socialt diagram
description: Lägga till en följande komponent på en sida
seo-description: Lägga till en följande komponent på en sida
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Använda socialt diagram {#using-social-graph}

## Introduktion {#introduction}

Möjligheten för en community-medlem att följa [aktiviteter](activities.md) och följa aktiviteter är fastställd genom två komponenter: `Follow` och `Following`.

Komponenten `Follow` måste vara associerad med en annan resurs, och den här associationen har redan upprättats för community-medlemmar och funktioner.

Komponenten `Following` visar bara de medlemmar som antingen följer den aktuella medlemmen eller som följs av den aktuella medlemmen. Det här sociala diagrammet över relationerna mellan medlemmar ingår i den användarprofil som har upprättats för en [community-plats](overview.md#communitiessites).

## Lägger till följande på en sida {#adding-following-to-a-page}

Om du vill lägga till en `Following`-komponent på en sida i redigeringsläge, letar du reda på komponenten `Communities / Following` och drar den på plats på en sida där det sociala diagrammet ska visas.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-socialgraph.md#essentials-for-client-side) inkluderas visas `Following`-komponenten så här:

![följande](assets/following.png)

## Konfigurerar följande {#configuring-following}

För närvarande är det nödvändigt att ställa in egenskapen för att avgöra om komponenten visar relationen `follows` eller relationen `following`.

## Ytterligare information {#additional-information}

Mer information finns på [sidan Essentials för sociala diagram](essentials-socialgraph.md) för utvecklare.
