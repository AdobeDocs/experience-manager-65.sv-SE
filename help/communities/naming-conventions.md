---
title: Namnkonventioner i Java&trade; paketnamn
description: Lär dig mer om namnkonventioner och hur du använder bindestreck i Java&trade;-paketnamnet.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Namnkonventioner {#naming-conventions}

## Bindestreck i Java™-paketnamn {#hyphens-in-java-package-name}

När du skapar en plats för en Java™-klass måste paketnamnet matcha databasmappens namn med eventuella bindestreck i sökvägen.

När du använder bindestreck i namn på databasobjekt bör du AEM att använda bindestreck, men bindestreck är inte tillåtna i Java™-paketnamn.

Den underliggande CRX-plattformen måste kunna skilja mellan ett faktiskt understreck `_ `och ett bindestreck `-`. I JCR måste därför bindestrecket ersättas med Unicode-värdet (u002d) och escape-konverteras med ett understreck `_`.

Om databassökvägen till exempel är **/apps/my-example/component/info/Info.java**, ska paketnamnet vara `java package apps.my_002dexample.component.info;`

Observera att ett understreck måste undantas på liknande sätt, så att `_` blir `_005f`.
