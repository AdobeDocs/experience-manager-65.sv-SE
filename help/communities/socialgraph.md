---
title: Använda socialt diagram
description: Lär dig hur du lägger till följande komponent på en sida där inloggade communitymedlemmar kan följa aktiviteter eller följa aktiviteter.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Använda socialt diagram {#using-social-graph}

## Introduktion {#introduction}

Möjligheten för en community-medlem att följa [aktiviteter](activities.md) och följas har etablerats genom två komponenter: `Follow` och `Following`.

Komponenten `Follow` måste vara associerad med en annan resurs och den här associationen har redan upprättats för community-medlemmar och funktioner.

Komponenten `Following` visar bara de medlemmar som antingen följer den aktuella medlemmen eller som följs av den aktuella medlemmen. Det här sociala diagrammet över relationerna mellan medlemmar ingår i den användarprofil som har upprättats för en [communitywebbplats](overview.md#communitiessites).

## Lägga till följande på en sida {#adding-following-to-a-page}

Om du vill lägga till en `Following`-komponent på en sida i redigeringsläge, letar du reda på komponenten `Communities / Following` och drar den på plats på en sida där det sociala diagrammet ska visas.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-socialgraph.md#essentials-for-client-side) inkluderas visas `Following`-komponenten så här:

![följande](assets/following.png)

## Konfigurera följande {#configuring-following}

För närvarande är det nödvändigt att ställa in egenskapen för att avgöra om komponenten visar relationen `follows` eller relationen `following`.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Grundläggande om sociala diagram](essentials-socialgraph.md) för utvecklare.
