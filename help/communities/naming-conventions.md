---
title: Namnkonventioner
seo-title: Naming Conventions
description: Bindestreck i Java-paketnamn
seo-description: Hyphens in Java Package Name
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Namnkonventioner {#naming-conventions}

## Bindestreck i Java-paketnamn {#hyphens-in-java-package-name}

När du skapar en plats för en Java-klass måste du vara medveten om att paketnamnet måste matcha databasmappens namn med eventuella bindestreck i sökvägen som escape-konverterats.

När du använder bindestreck i namn på databasobjekt rekommenderas AEM utveckling, men bindestreck är ogiltiga i Java-paketnamn.

Den underliggande CRX-plattformen måste kunna skilja mellan ett faktiskt understreck `_ `och ett bindestreck `-`. I JCR måste därför bindestrecket ersättas med sitt unicode-värde (u002d) och escape-konverteras med ett understreck `_`.

Om databassökvägen till exempel är **/apps/my-example/component/info/Info.java**, ska paketnamnet vara `java package apps.my_002dexample.component.info;`

Observera att ett understreck måste undantas på liknande sätt, så att `_` blir `_005f`.
