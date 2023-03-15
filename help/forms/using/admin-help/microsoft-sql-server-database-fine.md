---
title: "Microsoft SQL Server-databas: Finjustera konfigurationen"
seo-title: "Microsoft SQL Server database: Fine-tuning the configuration"
description: Lär dig hur du kan finjustera konfigurationen av din Microsoft SQL Server-databas.
seo-description: Learn how you can fine tune the configuration of your Microsoft SQL Server database.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Microsoft SQL Server-databas: Finjustera konfigurationen {#microsoft-sql-server-database-fine-tuning-the-configuration}

Du bör ändra standardkonfigurationsinställningarna när du använder Microsoft SQL Server. Högerklicka på den lokala servern i Oracle Enterprise Manager för att öppna egenskapsdialogrutan.

## Minnesinställningar {#memory-settings}

Ändra den minsta minnesallokeringen till ett så stort tal som möjligt. Om databasen körs på en separat dator ska du använda allt minne. Standardinställningarna tilldelar inte mycket minne, vilket förhindrar prestandan i nästan alla databaser. Du borde vara mest aggressiv när du tilldelar minne till produktionsmaskiner.

## Processorinställningar {#processor-settings}

Ändra processorinställningarna och markera kryssrutan Öka SQL Server-prioritet i Windows så att servern använder så många cykler som möjligt. Inställningen Använd NT Fibers är mindre viktig, men du kan också markera den.

## Databasinställningar {#database-settings}

Ändra databasinställningarna. Den viktigaste inställningen är Återställningsintervall, som anger den längsta väntetiden efter en krasch. Standardinställningen är en minut. Om du använder ett större värde, från 5 till 15 minuter, förbättras prestandan eftersom det ger servern mer tid att skriva ändringar från databasloggen tillbaka till databasfilerna.

>[!NOTE]
>
>Den här inställningen påverkar inte transaktionsbeteendet eftersom den endast ändrar längden på loggfilsreaptionen som måste utföras vid start.

Ange att storleken på det tilldelade utrymmet för både loggen och datafilen ska vara mycket större än den ursprungliga databasen. Tänk på hur mycket databasen kan växa över ett år. Helst fördelas logg- och datafilerna i en sammanhängande utsträckning så att data inte fragmenteras över hela disken.
