---
title: Namnkonventioner i Java&trade; package name
description: Lär dig mer om namnkonventioner och hur du använder bindestreck i Java&trade; package name.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Namnkonventioner {#naming-conventions}

## Bindestreck i Java™-paketnamn {#hyphens-in-java-package-name}

När du skapar en plats för en Java™-klass måste paketnamnet matcha databasmappens namn med eventuella bindestreck i sökvägen.

När du använder bindestreck i namn på databasobjekt bör du AEM att använda bindestreck, men bindestreck är inte tillåtna i Java™-paketnamn.

Den underliggande CRX-plattformen måste kunna skilja mellan det faktiska understrecket `_ ` och bindestrecket `-`. I JCR måste därför bindestrecket ersättas med Unicode-värdet (u002d) och escape-konverteras med understrecket `_`.

Om databassökvägen till exempel är **/apps/my-example/component/info/Info.java** ska paketnamnet vara `java package apps.my_002dexample.component.info;`

Observera att ett understreck måste undantas på liknande sätt, så att `_` blir `_005f`.
