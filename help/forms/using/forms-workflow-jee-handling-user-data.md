---
title: Forms JEE-arbetsflöden | Hantera användardata
seo-title: Forms JEE workflows | Handling user data
description: Forms JEE-arbetsflöden | Hantera användardata
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Admin
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Forms JEE-arbetsflöden | Hantera användardata {#forms-jee-workflows-handling-user-data}

AEM Forms JEE-arbetsflöden innehåller verktyg för att utforma, skapa och hantera affärsprocesser. En arbetsflödesprocess består av en serie steg som körs i en angiven ordning. Varje steg utför en specifik åtgärd, till exempel att tilldela en uppgift till en användare eller skicka ett e-postmeddelande. En process kan samverka med resurser, användarkonton och tjänster och kan aktiveras på något av följande sätt:

* Starta en process från AEM Forms Workspace
* Använda SOAP eller RESTful-tjänsten
* Skicka ett anpassat formulär
* Använda bevakad mapp
* Använda e-post

Mer information om hur du skapar arbetsflöden i AEM Forms JEE finns i [Workbench - hjälp](https://www.adobe.com/go/learn_aemforms_workbench_65).

## Användardata och datalager {#user-data-and-data-stores}

När en process aktiveras och fortskrider, hämtas data om processdeltagarna, data som anges av deltagarna i det formulär som är kopplat till processen samt bilagor som läggs till i formuläret. Data lagras i AEM Forms JEE-serverdatabasen, och om de är konfigurerade lagras vissa data, som bilagor, i GDS-katalogen (Global Document Storage). GDS-katalogen kan konfigureras på ett delat filsystem eller en databas.

## Få åtkomst till och ta bort användardata {#access-and-delete-user-data}

När en process aktiveras genereras ett unikt processinstans-ID och ett långlivat anrops-ID som associeras med processinstansen. Du kan komma åt och ta bort data för en processinstans baserat på det långvariga anrops-ID:t. Du kan ta fram det långvariga anrops-ID:t för en processinstans med användarnamnet för processinitieraren eller processdeltagarna som har skickat sina uppgifter.

Du kan dock inte identifiera processens instans-ID för en initierare i följande scenarier:

* **Processen utlöses via en bevakad mapp**: Det går inte att identifiera en processinstans med dess initierare om processen aktiveras av en bevakad mapp. I det här fallet kodas användarinformationen i de lagrade data.
* **Processen har initierats från AEM**: Alla processinstanser som aktiveras från AEM publiceringsinstans samlar inte in information om initieraren. Användardata kan dock hämtas i det format som är associerat med processen, som lagras i arbetsflödesvariabler.
* **Process initierad via e-post**: Avsändarens e-post-ID hämtas som en egenskap i en ogenomskinlig blobkolumn i `tb_job_instance` databastabell, som inte kan läsas direkt.

### Identifiera processinstans-ID när arbetsflödesinitieraren eller deltagaren är känd {#initiator-participant}

Utför följande steg för att identifiera processinstans-ID för en arbetsflödesinitierare eller en deltagare:

1. Kör följande kommando i AEM Forms serverdatabas om du vill hämta det primära ID:t för arbetsflödesinitieraren eller deltagaren från `edcprincipalentity` databastabell.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   Frågan returnerar det huvud-ID som har angetts `user_ID`.

1. (**För arbetsflödesinitierare**) Kör följande kommando för att hämta alla uppgifter som är associerade med initierarens huvud-ID från `tb_task` databastabell.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   Frågan returnerar uppgifter som initierats av den angivna `initiator`_ `principal_id`. Det finns två typer av uppgifter:

   * **Slutförda uppgifter**: Dessa uppgifter har skickats in och ett alfanumeriskt värde visas i `process_instance_id` fält. Observera alla processinstans-ID:n för skickade uppgifter och fortsätt med stegen.
   * **Aktiviteter som initierats men inte slutförts**: Dessa uppgifter har initierats men inte skickats ännu. Värdet i `process_instance_id` fältet för dessa uppgifter är **0** (noll). I det här fallet bör du tänka på motsvarande uppgifts-ID och se [Arbeta med överblivna uppgifter](#orphan).

1. (**För arbetsflödesdeltagare**) Kör följande kommando för att hämta processinstans-ID:n som är associerade med processdeltagarens huvud-ID för initieraren från `tb_assignment` databastabell.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   Frågan returnerar instans-ID:n för alla processer som är associerade med deltagaren, inklusive de där deltagaren inte har skickat någon uppgift.

   Observera alla processinstans-ID:n för skickade uppgifter och fortsätt med stegen.

   För överblivna uppgifter eller uppgifter där `process_instance_id` är 0 (noll), observera motsvarande uppgifts-ID och se [Arbeta med överblivna uppgifter](#orphan).

1. Följ instruktionerna i [Rensa användardata från arbetsflödesinstanser baserat på processens instans-ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) för att ta bort användardata för identifierade processinstans-ID:n.

### Identifiera processens instans-ID när användardata lagras i primitiva variabler {#primitive}

Ett arbetsflöde kan utformas så att användardata hämtas i en variabel som lagras som en blob i databasen. I sådana fall kan du bara fråga efter användardata om de lagras i någon av följande primitiva variabeltyper:

* **Sträng**: Innehåller användar-ID direkt eller som en delsträng och kan frågas med SQL.
* **Numeriskt**: Innehåller användar-ID:t direkt.
* **XML**: Innehåller användar-ID som en delsträng i texten som lagras som textkolumner i databasen och kan frågas som strängar.

Utför följande steg för att avgöra om ett arbetsflöde som lagrar data i primitiva variabler innehåller data för användaren:

1. Kör följande databaskommando:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   Frågan returnerar ett tabellnamn i `tb_<number>` format för det angivna programmet ( `app_name`) och arbetsflöde ( `workflow_name`).

   >[!NOTE]
   >
   >Värdet för `name` -egenskapen kan vara komplicerad om arbetsflödet är kapslat i undermappar i programmet. Se till att du anger den exakta fullständiga sökvägen till arbetsflödet, som du kan hämta från `omd_object_type` databastabell.

1. Granska `tb_<number>` tabellschema. Tabellen innehåller variabler som lagrar användardata för det angivna arbetsflödet. Variablerna i tabellen motsvarar variablerna i arbetsflödet.

   Identifiera och notera variabeln som motsvarar arbetsflödesvariabeln som innehåller användar-ID:t. Om den identifierade variabeln är av primitiv typ kan du köra en fråga för att avgöra vilka arbetsflödesinstanser som är kopplade till ett användar-ID.

1. Kör följande databaskommando. I det här kommandot `user_var` är den primitiva variabeltypen som innehåller användar-ID.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   Frågan returnerar alla processinstans-ID:n som är associerade med den angivna `user_ID`.

1. Följ instruktionerna i [Rensa användardata från arbetsflödesinstanser baserat på processens instans-ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) för att ta bort användardata för identifierade processinstans-ID:n.

### Rensa användardata från arbetsflödesinstanser baserat på processens instans-ID {#purge}

Nu när du har identifierat de processinstans-ID som är kopplade till en användare gör du följande för att ta bort användardata från respektive processinstans.

1. Kör följande kommando för att hämta det länge inaktuella anrops-ID:t och statusen för en processinstans från `tb_process_instance` tabell.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   Frågan returnerar det långvariga anrops-ID:t och statusen för den angivna `process_instance_id`.

1. Skapa en instans av allmänheten `ProcessManager` klient ( `com.adobe.idp.workflow.client.ProcessManager`) med `ServiceClientFactory` -instans med rätt anslutningsinställningar.

   Mer information finns i Java API-referens för [Klassen ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Kontrollera arbetsflödesinstansens status. Om statusen är annan än 2 (COMPLETE) eller 4 (TERMINATED) avslutar du instansen först genom att anropa följande metod:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Rensa arbetsflödesinstansen genom att anropa följande metod:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   The `purgeProcessInstance` tar helt bort alla data för det angivna anrops-ID:t från AEM Forms-serverdatabasen och GDS, om de är konfigurerade.

### Arbeta med överblivna uppgifter {#orphan}

Enstaka uppgifter är de uppgifter vars innehållsprocess har initierats men inte skickats ännu. i detta fall `process_instance_id` är **0** (noll). Därför kan du inte spåra användardata som lagrats för ägarlösa uppgifter med hjälp av processens instans-ID. Du kan dock spåra den med uppgifts-ID:t för en överbliven uppgift. Du kan identifiera uppgifts-ID:n från `tb_task` tabell för en användare enligt beskrivningen i [Identifiera processinstans-ID när arbetsflödesinitieraren eller deltagaren är känd](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

När du har uppgifts-ID:n gör du följande för att rensa de associerade filerna och data med en överbliven åtgärd från GDS och databasen.

1. Kör följande kommando i AEM Forms serverdatabas för att hämta ID:n för de identifierade uppgifts-ID:n.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   Frågan returnerar en lista med ID:n. För varje ID ( `fd_id`) som returneras i resultatet skapar du en lista med sträng för sessions-ID enligt följande:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Utför något av följande steg beroende på om GDS pekar på ett filsystem eller en databas:

   1. **GDS i filsystem**

      I GDS-filsystemet:

      1. Sök efter filer med följande sessions-ID-strängar som tillägg:
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      Filerna med dessa tillägg är markörfilerna. De lagras med filnamn i följande format:

      `<file_name_guid>.session<session_id_string>`

      1. Ta bort alla markörfiler och andra filer med exakt samma filnamn som `<file_name_guid>` från filsystemet.
   1. **GDS i databasen**

      Kör följande kommandon för varje sessions-ID:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. Kör följande kommandon för att ta bort data för uppgifts-ID:n från AEM Forms serverdatabas:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
