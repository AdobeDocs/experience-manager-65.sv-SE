---
title: Kodfallare
seo-title: Kodfallare
description: Vanliga kodfallsfall att undvika vid utveckling för AEM
seo-description: Vanliga kodfallsfall att undvika vid utveckling för AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Kodfallare{#code-pitfalls}

## Undvik att skicka bindningar i Java-kod {#avoid-sling-bindings-in-java-code}

Sling Bindings är ett olämpligt sätt att få tillgång till en tjänst i 90 % av fallen. Du bör i stället använda *@Reference* eller *@Inject* -anteckningar.

## Undvik tråd.avbrott i Java-kod {#avoid-thread-interrupt-in-java-code}

*Thread.Intert* är farligt eftersom det kan stänga filer, inklusive Lucene-filer och beständiga cachefiler, när de anropas vid fel tidpunkt.

## Undvik att blanda Java-synkronisering med ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Detta kan leda till ett tävlingsvillkor där koden till slut kommer att låsas.
