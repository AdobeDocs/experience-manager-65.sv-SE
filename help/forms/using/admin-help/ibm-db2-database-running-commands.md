---
title: "IBM DB2-databas: Kör kommandon för regelbundet underhåll"
description: I det här dokumentet visas IBM DB2-kommandon som rekommenderas för regelbundet underhåll av AEM formulärdatabas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# IBM DB2-databas: Kör kommandon för regelbundet underhåll {#ibm-db-database-running-commands-for-regular-maintenance}

Följande IBM DB2-kommandon rekommenderas för regelbundet underhåll av AEM formulärdatabas. Detaljerad information om underhåll och prestandajustering för din DB2-databas finns i *Administrationshandbok för IBM DB2*.

* **runstats:** Det här kommandot uppdaterar statistik som beskriver de fysiska egenskaperna i en databastabell, tillsammans med tillhörande index. Dynamiska SQL-satser som genereras av AEM formulär använder automatiskt denna uppdaterade statistik, men statiska SQL-satser som skapats inuti en databas kräver att `db2rbind` kan även köras.
* **db2rbind:** Det här kommandot binder om alla paket i databasen. Använd det här kommandot när du har kört `runstats` för att validera alla paket i databasen.
* **omordningstabell eller index:** Det här kommandot kontrollerar om det krävs en omorganisering av vissa tabeller och index.

  I takt med att databaserna växer och förändras är det viktigt att tabellstatistiken beräknas om för att förbättra databasens prestanda och bör göras regelbundet. Dessa kommandon kan köras antingen manuellt med skript eller med ett cron-jobb.

>[!NOTE]
>
>Innan du kör `runstats` måste databasen innehålla data och minst en katalogsynkronisering måste ha utförts.

För en liten databas, till exempel för 10 000 användare eller 2 500 grupper, räcker det att anropa `runstats` om du vill minska synkroniseringstiderna.

För större databaser, till exempel för 100 000 användare eller 10 000 grupper, kör du `reorg` innan du kör `runstats` -kommando.

## Använd kommandot runstats i AEM formulärdatabas {#use-the-runstats-command-on-your-aem-forms-database}

Kör `runstats` på följande AEM formulär databastabeller och index.

>[!NOTE]
>
>The `runstats` -kommandot behöver bara köras under den första databassynkroniseringen. Den måste dock köras två gånger under den processen: en gång under synkroniseringen av användare och grupper och sedan under synkroniseringen av gruppmedlemmar. Kontrollera att skriptet körs fullständigt varje gång du kör det.

Korrekt syntax och användning finns i dokumentationen från databastillverkaren. Nedan, `<schema>` används för att ange det schema som är associerat med ditt DB2-användarnamn. Om du har en enkel standardinstallation av DB2 är detta databasens schemanamn.

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

## Kör kommandot reortera i AEM formulärdatabas {#run-the-reorg-command-on-your-aem-forms-database}

Kör `reorg` på följande AEM formulär databastabeller och index. Korrekt syntax och användning finns i dokumentationen från databastillverkaren.

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
