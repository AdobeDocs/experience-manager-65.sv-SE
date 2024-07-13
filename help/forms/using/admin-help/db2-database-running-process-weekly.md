---
title: "DB2&reg; database: Kör en process varje vecka"
description: Lär dig hur du kan förbättra prestandan i din AEM Forms DB2&reg;-databas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# DB2®-databas: Köra en process varje vecka{#db-database-running-a-process-weekly}

Om AEM Forms DB2®-databasen börjar köras långsamt kan prestanda förbättras om du kör följande process varje vecka:

1. Start DB2® Control Center:

   (Windows) Välj Start > Program > IBM® DB2® > General Administration Tools > Control Center.

   (Linux® och UNIX®) Skriv kommandot `db2jcc` från en kommandotolk.

1. Klicka på Alla databaser i objektträdet i DB2® Control Center.
1. Klicka på databasen som du skapade för AEM Forms och klicka på mappen Tabeller.
1. Markera alla databastabeller i innehållsrutan, högerklicka på dem och välj sedan Kör statistik.
1. Gå till Statistik > Indexstatistik.
1. Välj Samla statistik för alla index, välj Samla statistik för index med utökad detaljerad statistik och klicka sedan på OK.

Ett meddelande visas när processen har slutförts. Stäng meddelandet.
