---
title: Kompilera testplanen
seo-title: Compiling your Test Plan
description: De enskilda testfallen samlas i din testplan
seo-description: The individual test cases are amalgamated into your Test Plan
uuid: d83ef902-e0ef-4f84-9477-be12dfe91742
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 82b8a5f4-583b-47ba-9579-b47364b56aa2
docset: aem65
exl-id: ee5df2c8-ab31-4be9-8ede-3c96f26fc626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Kompilera testplanen{#compiling-your-test-plan}

De enskilda testfallen sammanförs sedan i din testplan, som också kommer att definiera:

**Prioriteringar**

Vissa tester kommer att ha större betydelse än andra, så det är tillrådligt att ange deras prioritet.

Vissa tester kan t.ex. påverka ett Go-/No-Go-beslut och måste därför bekräftas vid varje testad interimsrelease.

**Iterationer**

Om ditt projekt använder någon form av utvecklingsiteration (med flera releaser tillgängliga) kan du behöva eller vill ha en indikation på resultatet för varje iteration. Detta kan användas för att ange:

* vilka tester som ska omfattas av upprepningen.
* resultaten av tester som upprepas i olika iterationer.
* att prioritetstester och tester av grundläggande funktioner upprepas med regelbundna mellanrum.

**Tester**

Vid något tillfälle kan du antingen utse rätt testgrupp eller en specifik testperson (eventuellt beroende på tillgänglighet och/eller erfarenhet).

**Sammanfattning eller översikt**

För rapportering vill du ge en översikt över testresultaten:

* Procentandel av tester som redan omfattas.
* Procent lyckade/misslyckade.
* Specifika siffror för de prioriterade testerna.
