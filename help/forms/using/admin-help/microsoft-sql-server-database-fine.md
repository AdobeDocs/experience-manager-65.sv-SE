---
title: '"Microsoft SQL Server-databas: Finjustera konfigurationen"'
seo-title: '"Microsoft SQL Server-databas: Finjustera konfigurationen"'
description: Lär dig hur du kan finjustera konfigurationen av din Microsoft SQL Server-databas.
seo-description: Lär dig hur du kan finjustera konfigurationen av din Microsoft SQL Server-databas.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Microsoft SQL Server-databas: Finjustera konfigurationen {#microsoft-sql-server-database-fine-tuning-the-configuration}

Du bör ändra standardkonfigurationsinställningarna när du använder Microsoft SQL Server. Högerklicka på den lokala servern i Oracle Enterprise Manager för att öppna dialogrutan med egenskaper.

## Minnesinställningar {#memory-settings}

Ändra den minsta minnesallokeringen till ett så stort tal som möjligt. Om databasen körs på en separat dator ska du använda allt minne. Standardinställningarna tilldelar inte mycket minne, vilket förhindrar prestandan i nästan alla databaser. Du borde vara mest aggressiv när du tilldelar minne till produktionsmaskiner.

## Processorinställningar {#processor-settings}

Ändra processorinställningarna och markera kryssrutan Öka SQL Server-prioritet i Windows så att servern använder så många cykler som möjligt. Inställningen Använd NT Fibers är mindre viktig, men du kan också markera den.

## Databasinställningar {#database-settings}

Ändra databasinställningarna. Den viktigaste inställningen är Återställningsintervall, som anger den längsta väntetiden efter en krasch. Standardinställningen är en minut. Om du använder ett större värde, från 5 till 15 minuter, förbättras prestandan eftersom det ger servern mer tid att skriva ändringar från databasloggen tillbaka till databasfilerna.

>[!NOTE]
>
>Den här inställningen påverkar inte transaktionsbeteendet eftersom den endast ändrar längden på loggfilsreaptionen som måste utföras vid start.

Ange att storleken på det tilldelade utrymmet för både loggfilen och datafilen ska vara mycket större än den ursprungliga databasen. Tänk på hur mycket databasen kan växa över ett år. Helst fördelas logg- och datafilerna i en sammanhängande utsträckning så att data inte fragmenteras över hela disken.
