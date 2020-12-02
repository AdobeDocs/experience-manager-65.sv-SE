---
title: '"IBM DB2-databas: Kör kommandon för regelbundet underhåll"'
seo-title: '"IBM DB2-databas: Kör kommandon för regelbundet underhåll"'
description: I det här dokumentet visas IBM DB2-kommandon som rekommenderas för regelbundet underhåll av AEM formulärdatabas.
seo-description: I det här dokumentet visas IBM DB2-kommandon som rekommenderas för regelbundet underhåll av AEM formulärdatabas.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# IBM DB2-databas: Kör kommandon för regelbundet underhåll {#ibm-db-database-running-commands-for-regular-maintenance}

Följande IBM DB2-kommandon rekommenderas för regelbundet underhåll av AEM formulärdatabas. Detaljerad information om underhåll och prestandajustering för databasen DB2 finns i *Administrationshandboken för IBM DB2*.

* **körningsstatistik:** Det här kommandot uppdaterar statistik som beskriver de fysiska egenskaperna för en databastabell, tillsammans med tillhörande index. Dynamiska SQL-satser som genereras av AEM formulär använder automatiskt den uppdaterade statistiken, men statiska SQL-satser som skapats i en databas kräver att kommandot `db2rbind` också körs.
* **db2rbind:** Det här kommandot binder om alla paket i databasen. Använd det här kommandot när du har kört verktyget `runstats` för att validera alla paket i databasen igen.
* **rapporttabell eller index:** Det här kommandot kontrollerar om det krävs en omorganisering av vissa tabeller och index.

   I takt med att databaserna växer och förändras är det viktigt att tabellstatistiken beräknas om för att förbättra databasens prestanda och bör göras regelbundet. Dessa kommandon kan köras antingen manuellt med skript eller med ett cron-jobb.

>[!NOTE]
>
>Innan du kör kommandot `runstats` måste databasen innehålla data och minst en katalogsynkronisering måste ha utförts.

För en liten databas, t.ex. för 10 000 användare eller 2 500 grupper, räcker det att anropa kommandot `runstats` för att minska synkroniseringstiderna.

För större databaser, till exempel för 100 000 användare eller 10 000 grupper, kör du kommandot `reorg` innan du kör kommandot `runstats`.

## Använd kommandot runstats i AEM formulärdatabas {#use-the-runstats-command-on-your-aem-forms-database}

Kör kommandot `runstats` på följande AEM databastabeller och index.

>[!NOTE]
>
>Kommandot `runstats` behöver bara köras under den första databassynkroniseringen. Den måste dock köras två gånger under den processen: en gång under synkroniseringen av användare och grupper och sedan under synkroniseringen av gruppmedlemmar. Kontrollera att skriptet körs fullständigt varje gång du kör det.

Korrekt syntax och användning finns i dokumentationen från databastillverkaren. Nedan används `<schema>` för att ange det schema som är associerat med ditt DB2-användarnamn. Om du har en enkel standardinstallation av DB2 är detta databasens schemanamn.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## Kör organisationskommandot på AEM formulärdatabas {#run-the-reorg-command-on-your-aem-forms-database}

Kör kommandot `reorg` på följande AEM databastabeller och index. Korrekt syntax och användning finns i dokumentationen från databastillverkaren.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```

