---
title: Global dokumentlagringskatalog
description: Den globala dokumentlagringskatalogen (GDS) är en katalog som används för att lagra långlivade filer som används i en process.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Global dokumentlagringskatalog{#global-document-storage-directory}

The *global dokumentlagring (GDS)* katalog är en katalog som används för att lagra långlivade filer som används i en process. Dessa filer innehåller PDF, profiler och formulärmallar. Långvariga filer är en viktig del av det övergripande tillståndet för många AEM. Om vissa eller alla långlivade dokument förloras eller skadas kan Forms Server bli instabil. Indatadokument för asynkrona jobbanrop lagras också i GDS-katalogen och måste vara tillgängliga för bearbetning av begäranden. Det är viktigt att du tar hänsyn till tillförlitligheten i det filsystem som är värd för GDS-katalogen. Använd en redundant matris med oberoende diskar (RAID) eller annan teknik som är lämplig för din kvalitet och nivå av servicebehov.

Långa filer kan innehålla känslig användarinformation. Den här informationen kan kräva särskilda autentiseringsuppgifter när den används med AEM formulär-API:er eller användargränssnitt. Det är viktigt att GDS-katalogen är ordentligt skyddad via operativsystemet. Det är bara administratörskontot som används för att köra programservern som ska ha läs- och skrivåtkomst till GDS-katalogen.

Förutom att välja en säker katalog med hög tillgänglighet för GDS kan du även välja att aktivera dokumentlagring i databasen. Observera att även om du använder AEM formulärdatabas för dokumentlagring, kräver AEM fortfarande GDS-katalogen. (Se [Alternativ för säkerhetskopiering när databasen används för dokumentlagring](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM formulärprogramdata finns i GDS-katalogen och AEM formulärdatabas. I följande tabell beskrivs data och dess platser.

<table>
 <thead>
  <tr>
   <th><p>AEM</p></th>
   <th><p>Databas</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Programdata (användare, roller, processer, principer, slutpunkter, händelser och så vidare).</p></td>
   <td><p>Ja</p></td>
   <td><p>Nej</p></td>
  </tr>
  <tr>
   <td><p>Distribuerade tjänstbehållare</p></td>
   <td><p>Ja</p></td>
   <td><p>Nej</p></td>
  </tr>
  <tr>
   <td><p>Document Manager </p></td>
   <td><p>Nej</p></td>
   <td><p>Ja</p></td>
  </tr>
  <tr>
   <td><p>Forms Repository</p></td>
   <td><p>Ja</p></td>
   <td><p>Nej</p></td>
  </tr>
  <tr>
   <td><p>Systemkonfiguration</p></td>
   <td><p>Ja</p></td>
   <td><p>Nej</p></td>
  </tr>
  <tr>
   <td><p>Bevakade mappar</p></td>
   <td><p>Nej</p></td>
   <td><p>Ja</p></td>
  </tr>
 </tbody>
</table>

## Konfigurera GDS-katalogen {#configuring-the-gds-directory}

Platsen för GDS-katalogen kan konfigureras manuellt under installationen av AEM formulär. Om platsinställningen är tom under installationen blir platsen som standard en katalog under programserverinstallationen enligt följande:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Ändra standardplats för GDS {#change-the-default-gds-location}

Du kan ändra GDS-platsen i administrationskonsolen när installationen av AEM formulär har slutförts. Flytta data manuellt för att slutföra processen.

>[!NOTE]
>
>Migrera data på följande sätt, annars inträffar dataförluster.

1. Logga in på administrationskonsolen och klicka på Inställningar > Systeminställningar > Konfigurationer.
1. Ange den fullständiga sökvägen till den nya GDS-katalogen i rutan Global Document Storage och klicka sedan på OK.
1. Stäng programservern omedelbart.
1. Flytta alla filer från den gamla GDS-katalogen till den nya platsen och behåll den interna katalogstrukturen.
1. Starta om programservern.

## Om distributionsfiler {#about-deployment-files}

AEM består av två typer av distributionsfiler, servicebehållarna och Java 2 Platform, Enterprise Edition (J2EE) EAR-filer. EAR-filerna består av J2EE-standardprogrampaket som innehåller kärnfunktionaliteten i AEM formulär. Programserverspecifika EAR-filer är följande:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

Implementera AEM innebär att du distribuerar sammansatta EAR-filer och stödfiler till programservern där du tänker köra din AEM formulärlösning. Om du konfigurerade och satte ihop flera moduler paketeras de driftsättningsbara modulerna i de driftsättningsbara EAR-filerna. Om du vill distribuera de här filerna kopierar du dem till *[appserver - startsida]*\server\all\deploy.

Moduler och AEM arkivfiler för formulär paketeras i JAR-filer. Eftersom de inte är J2EE-typfiler distribueras de inte till programservern. I stället kopieras de till GDS-katalogen och en referens till deras plats lagras i AEM formulärdatabas. Därför måste GDS-katalogen delas mellan alla noder i klustret. Alla noder måste ha tillgång till den centrala lagringskatalogen för DSC:er.

>[!NOTE]
>
>Kontrollera att du har skapat och konfigurerat GDS-katalogen innan du distribuerar tjänstbehållarna. (Se [Konfigurera GDS-katalogen](global-document-storage-directory.md#configuring-the-gds-directory))
