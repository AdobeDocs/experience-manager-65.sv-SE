---
title: Kodfallare
description: Vanliga kodfallsfall som ska undvikas vid utveckling för AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Kodfallare{#code-pitfalls}

## Undvik att skicka bindningar i Java-kod {#avoid-sling-bindings-in-java-code}

Sling Bindings är ett olämpligt sätt att få tillgång till en tjänst i 90 % av fallen. I stället bör du använda *@Referens* eller *@Input* anteckningar.

## Undvik tråd.avbrott i Java-kod {#avoid-thread-interrupt-in-java-code}

*Tråd.avbrott* är farligt eftersom det kan stänga filer, inklusive Lucene-filer och beständiga cachefiler, när de anropas vid fel tidpunkt.

## Undvik att blanda Java-synkronisering med ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Detta kan leda till ett tävlingsvillkor där koden till slut kommer att låsas.
