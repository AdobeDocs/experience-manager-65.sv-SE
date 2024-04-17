---
title: Vilka testmiljöer behövs?
description: Flera miljöer bör beaktas som en del av testningen
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Vilka testmiljöer behövs?{#which-test-environments-will-be-needed}

För att definiera vilka konfigurationer som ska testas bör du tänka på följande:

**Utveckling** - För enhetstester och vissa integreringstester.

**Testning** - För de flesta av testerna.

**Live** - För slutliga prestanda- och stresstester. Även för godkännandetester med kunden.

Bestäm vilka instanser du behöver och var (vanligtvis minst en av varje för alla testnivåer):

**Upphovsman** - Den här instansen tillåter författare att mata in och publicera innehåll.

**Publicera** - Den här instansen visar webbplatsen i dess publicerade form så att besökarna kan komma åt den.

Testad med Dispatcher.

Slutligen måste den faktiska maskinvaran beaktas - alla prestandatester bör göras på ett system så nära som möjligt i konfigurationen till den slutliga livemiljön. Därför rekommenderar vi även att du delar upp projektstarten i en

**Soft Launch** - Minskad tillgänglighet, vilket ger tid för prestandatester, justering och optimering under realistiska förhållanden i produktionsmiljön.

**Hård start** - Full tillgänglighet.
