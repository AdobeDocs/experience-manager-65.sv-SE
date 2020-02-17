---
title: Kompilera testplanen
seo-title: Kompilera testplanen
description: De enskilda testfallen samlas i din testplan
seo-description: De enskilda testfallen samlas i din testplan
uuid: d83ef902-e0ef-4f84-9477-be12dfe91742
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 82b8a5f4-583b-47ba-9579-b47364b56aa2
docset: aem65
translation-type: tm+mt
source-git-commit: da08613be784f43ad3e3c3652b7e015640a48a9d

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

