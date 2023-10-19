---
title: Använda socialt diagram
description: Lär dig hur du lägger till följande komponent på en sida där inloggade communitymedlemmar kan följa aktiviteter eller följa aktiviteter.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Använda socialt diagram {#using-social-graph}

## Introduktion {#introduction}

Möjlighet för en community-medlem att följa [verksamhet](activities.md) och ska följas genom två komponenter: `Follow` och `Following`.

The `Follow` måste vara associerad med en annan resurs, och den här associationen har redan upprättats för communitymedlemmar och funktioner.

The `Following` listar bara de medlemmar som antingen följer den aktuella medlemmen eller som följs av den aktuella medlemmen. Det här sociala diagrammet över relationerna mellan medlemmar ingår i den användarprofil som upprättats för en [communitywebbplats](overview.md#communitiessites).

## Lägga till följande på en sida {#adding-following-to-a-page}

Om du vill lägga till en `Following` till en sida i redigeringsläge, leta reda på komponenten `Communities / Following` och dra den till rätt plats på en sida där det sociala diagrammet ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](essentials-socialgraph.md#essentials-for-client-side) ingår så här `Following` visas:

![följande](assets/following.png)

## Konfigurera följande {#configuring-following}

För närvarande är det nödvändigt att ställa in egenskapen för att avgöra om komponenten visar `follows` eller `following` relation.

## Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om sociala diagram](essentials-socialgraph.md) för utvecklare.
