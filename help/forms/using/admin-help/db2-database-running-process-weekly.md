---
title: "DB2-databas: Köra en process varje vecka"
seo-title: "DB2 database: Running a process weekly"
description: Se hur du kan förbättra prestandan för din AEM DB2-databas.
seo-description: See how you can improve the performance of your AEM forms DB2 database.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# DB2-databas: Köra en process varje vecka{#db-database-running-a-process-weekly}

Om AEM formulär DB2-databasen börjar köras långsamt kan prestanda förbättras om du kör följande process varje vecka:

1. Start DB2 Control Center:

   (Windows) Välj Start > Program > IBM DB2 > Allmänna administrationsverktyg > Kontrollcenter.

   (Linux och UNIX) I en kommandotolk skriver du `db2jcc` -kommando.

1. Klicka på Alla databaser i objektträdet i DB2 Control Center.
1. Klicka på databasen som du skapade för AEM formulär och klicka på mappen Tabeller.
1. Markera alla databastabeller i innehållsrutan, högerklicka på dem och välj Kör statistik.
1. Gå till Statistik > Indexstatistik.
1. Välj Samla statistik för alla index, välj Samla statistik för index med utökad detaljerad statistik och klicka sedan på OK.

Ett meddelande visas när processen har slutförts. Stäng meddelandet.
