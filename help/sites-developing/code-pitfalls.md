---
title: Kodfallare
seo-title: Code pitfalls
description: Vanliga kodfall som ska undvikas vid utveckling för AEM
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Kodfallare{#code-pitfalls}

## Undvik att skicka bindningar i Java-kod {#avoid-sling-bindings-in-java-code}

Sling Bindings är ett olämpligt sätt att få tillgång till en tjänst i 90 % av fallen. I stället bör du använda *@Referens* eller *@Input* anteckningar.

## Undvik tråd.avbrott i Java-kod {#avoid-thread-interrupt-in-java-code}

*Tråd.avbrott* är farligt eftersom det kan stänga filer, inklusive Lucene-filer och beständiga cachefiler, när de anropas vid fel tidpunkt.

## Undvik att blanda Java-synkronisering med ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Detta kan leda till ett tävlingsvillkor där koden till slut kommer att låsas.
