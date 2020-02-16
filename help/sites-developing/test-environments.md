---
title: Vilka testmiljöer behövs?
seo-title: Vilka testmiljöer behövs?
description: Flera miljöer bör beaktas som en del av testningen
seo-description: Flera miljöer bör beaktas som en del av testningen
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Vilka testmiljöer behövs?{#which-test-environments-will-be-needed}

För att definiera vilka konfigurationer som ska testas bör du tänka på följande:

**Utveckling** - För enhet och vissa integreringstester.

**Testning** - För merparten av testerna.

**Live** - För slutliga prestanda- och stresstester. Även för godkännandetester med kunden.

Du måste också bestämma vilka instanser du behöver var (vanligtvis minst en av varje för alla testnivåer):

**Författare** - Den här instansen tillåter författare att ange och publicera innehåll.

**Publicera** - Den här instansen visar webbplatsen i dess publicerade form så att besökarna kan komma åt den.

Testas tillsammans med Dispatcher.

Slutligen måste den faktiska maskinvaran beaktas - alla prestandatester bör göras på ett system så nära som möjligt i konfigurationen till den slutliga livemiljön. Därför rekommenderar vi även att du delar upp projektstarten i en

**Soft Launch** - minskad tillgänglighet; som ger tid för prestandatester, justering och optimering under realistiska förhållanden i produktionsmiljön.

**Hård start** - fullständig tillgänglighet.
