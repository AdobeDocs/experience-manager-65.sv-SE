---
title: Vilka testmiljöer behövs?
seo-title: Which Test Environments are needed?
description: Flera miljöer bör beaktas som en del av testningen
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Vilka testmiljöer behövs?{#which-test-environments-will-be-needed}

För att definiera vilka konfigurationer som ska testas bör du tänka på följande:

**Utveckling** - För enhetstester och vissa integreringstester.

**Testning** - För merparten av testerna.

**Live** - För slutliga prestanda- och stresstester. Även för godkännandetester med kunden.

Du måste också bestämma vilka instanser du behöver var (vanligtvis minst en av varje för alla testnivåer):

**Upphovsman** - Den här instansen tillåter författare att mata in och publicera innehåll.

**Publicera** - Den här instansen visar webbplatsen i dess publicerade form så att besökarna kan komma åt den.

Testas tillsammans med Dispatcher.

Slutligen måste den faktiska maskinvaran beaktas - alla prestandatester bör göras på ett system så nära som möjligt i konfigurationen till den slutliga livemiljön. Därför rekommenderar vi även att du delar upp projektstarten i en

**Soft Launch** - Minskad tillgänglighet. som ger tid för prestandatester, justering och optimering under realistiska förhållanden i produktionsmiljön.

**Hård start** - Full tillgänglighet.
