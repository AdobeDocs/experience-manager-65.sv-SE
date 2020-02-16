---
title: Importera och hantera arkiv
seo-title: Importera och hantera arkiv
description: Lär dig hur du importerar och hanterar arkiv.
seo-description: Lär dig hur du importerar och hanterar arkiv.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importera och hantera arkiv {#import-and-manage-archives}

Använd fliken Arkiv för att importera och hantera LCA:er som har skapats i Workbench.

## Importera ett arkiv {#import-an-archive}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Programhantering och sedan på fliken Aktiviteter.
1. Klicka på Importera.
1. Klicka på Bläddra för att leta reda på arkivet som ska importeras och klicka sedan på Förhandsgranska.
1. Granska listan över resurser och objekt som ska installeras med arkivet. Kontrollera att det inte finns några konflikter med befintliga resurser, objekt och tjänstkonfigurationer eftersom det inte finns någon ångra-funktion tillgänglig.

   Om du väljer att importera tjänstkonfigurationerna importerar AEM-formulär alla processkonfigurationsfiler (slutpunkter, säkerhetsprofiler och tjänstkonfigurationsparametrar) som används av processerna i LCA.

1. Klicka på Importera.
1. Granska importresultaten och klicka antingen på Hoppa över konfiguration för att slutföra importprocessen eller klicka på Konfigurera för att konfigurera arkivet.

   >[!NOTE]
   >
   >Om du klickar på Hoppa över konfiguration kan du konfigurera arkivet senare.

1. Om du klickar på Konfigurera visas sidan Konfigurera slutpunkter där du kan göra de ändringar du behöver:

   * Om du vill byta namn på en slutpunkt eller redigera dess beskrivning klickar du på den.
   * Om du vill lägga till en Task Manager-slutpunkt klickar du på Lägg till TaskManager. Mer information om inställningar för Task Manager finns i [Konfigurera slutpunkter](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)för Task Manager.
   * Om du vill lägga till en bevakad mappslutpunkt klickar du på Lägg till bevakad mapp. Mer information om inställningarna för bevakad mapp finns i [Inställningar](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)för bevakad mapp.
   * Om du vill lägga till en e-postslutpunkt klickar du på Lägg till e-post. Mer information om e-postinställningarna finns i Inställningar för [e-postslutpunkt](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Om du vill lägga till en EJB-slutpunkt klickar du på Lägg till EJB och anger ett namn och en beskrivning för slutpunkten.
   * Om du vill lägga till en SOAP-slutpunkt klickar du på Lägg till SOAP och anger ett namn och en beskrivning för slutpunkten.
   * Om du vill lägga till en fjärrslutpunkt klickar du på Lägg till fjärranslutning. Mer information om fjärrinställningar finns i [Fjärrinställningar för slutpunkter](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Om du vill lägga till en REST-slutpunkt klickar du på Lägg till REST och anger ett namn och en beskrivning för slutpunkten. Anteckna den URL för REST-anrop som visas på sidan Lägg till REST-slutpunkt.
   * Om du vill ta bort en slutpunkt markerar du kryssrutan bredvid den och klickar på Ta bort.

1. Klicka på Nästa.
1. Om en process eller tjänst i LCA har konfigurationsparametrar visas sidan Konfigurera parametrar där du konfigurerar tjänstparametrarna och klickar på Nästa.
1. Gör de ändringar du behöver på sidan Konfigurera säkerhetsprofil:

   * **** Kräv att anropare autentiserar: Den här inställningen anger om tjänsten kan anropas med eller utan autentiseringsuppgifter.

      Om *uppringare för närvarande krävs för att autentisera* visas, måste uppringaren autentiseras och uppringarens huvudnamn måste ha behörighet att anropa tjänsten. I annat fall avvisas anropsförsöket. Klicka på Tillåt oautentiserade anropare för att ta bort behovet av autentisering.

      Om *anropare inte behöver autentisera* visas behöver anroparen inte autentiseras. Anropet av tjänsten lyckas alltid eftersom det inte finns någon auktoriseringskontroll. Klicka på Kräv att anropare autentiserar för att begära autentisering.

   * **** Kör som: Anger den körningsidentitet som används av en tjänst efter att den har anropats. Klicka på Ändra om du vill ändra det här alternativet. Välj bland följande alternativ:

      **** Ospecificerad: Standardbeteendet används.

      **** Anropare: Använder samma identitet som användaren som anropade tjänsten.

      **** System: Kör tjänsten med fullständig behörighet. Det här är standardinställningen för långvariga processer.

      **** Namngiven användare: Gör att du kan köra tjänsten som en specifik användare. Det här är standardinställningen för kortlivade processer. När du väljer det här alternativet klickar du på Välj användare för att visa sidan Välj huvudnamn, där du kan söka efter och välja användaren.

   * Om du vill lägga till ett huvudnamn i säkerhetsprofilen klickar du på Lägg till huvudnamn och väljer den användare eller grupp som ska läggas till som huvudnamn. Klicka på Nästa och välj sedan de behörigheter du vill tilldela detta huvudkonto:

      **** INVOKE_PERM: Så här anropar du alla åtgärder på tjänsten

      **** MODIFY_CONFIG_PERM: Ändra konfigurationen för en tjänst

      **** SUPERVISOR_PERM: Så här visar du processinstansdata för en tjänst som skapats från en process

      **** START_STOP_PERM: Starta och stoppa en tjänst

      **** ADD_REMOVE_ENDPOINTS_PERM: Lägga till, ta bort och ändra slutpunkter för en tjänst

      **** CREATE_VERSION_PERM: Skapa en ny version av tjänsten

      **** DELETE_VERSION_PERM: Så här tar du bort en version av tjänsten

      **** MODIFY_VERSION_PERM: Ändra en version av tjänsten

      **** READ_PERM: Så här visar du tjänsten

      Klicka på Slutför för att lägga till säkerhetsobjektet i säkerhetsprofilen.

1. Klicka på Slutför för att slutföra konfigurationen.

## Konfigurera de AEM-formulär som ingår i en arkivfil {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Programhantering och sedan på fliken Aktiviteter.
1. På sidan Arkivhantering väljer du den arkivfil som ska konfigureras.
1. På sidan Visa arkiv väljer du den markerade arkivresursen.
1. Konfigurera den importerade processarkivfilen.

## Använd konfigurationsguiden för att konfigurera AEM-formulär som ingår i en arkivfil {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Programhantering och sedan på fliken Aktiviteter.
1. Klicka på Konfigurera bredvid den arkivfil som ska konfigureras.
1. Sidan Konfigurera slutpunkter visas där du kan göra de ändringar du behöver:

   * Om du vill byta namn på en slutpunkt eller redigera dess beskrivning klickar du på den.
   * Om du vill lägga till en Task Manager-slutpunkt klickar du på Lägg till TaskManager. Mer information om inställningar för Task Manager finns i [Konfigurera slutpunkter](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)för Task Manager.
   * Om du vill lägga till en bevakad mappslutpunkt klickar du på Lägg till bevakad mapp. Mer information om inställningarna för bevakad mapp finns i [Inställningar](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)för bevakad mapp.
   * Om du vill lägga till en e-postslutpunkt klickar du på Lägg till e-post. Mer information om e-postinställningarna finns i Inställningar för [e-postslutpunkt](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Om du vill lägga till en EJB-slutpunkt klickar du på Lägg till EJB och anger ett namn och en beskrivning för slutpunkten.
   * Om du vill lägga till en SOAP-slutpunkt klickar du på Lägg till SOAP och anger ett namn och en beskrivning för slutpunkten.
   * Om du vill lägga till en fjärrslutpunkt klickar du på Lägg till fjärranslutning. Mer information om fjärrinställningar finns i [Fjärrinställningar för slutpunkter](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Om du vill lägga till en REST-slutpunkt klickar du på Lägg till REST och anger ett namn och en beskrivning för slutpunkten. Anteckna den URL för REST-anrop som visas på sidan Lägg till REST-slutpunkt.
   * Om du vill ta bort en slutpunkt markerar du kryssrutan bredvid den och klickar på Ta bort.

1. Klicka på Nästa.
1. Om en process eller tjänst i LCA har konfigurationsparametrar visas sidan Konfigurera parametrar där du konfigurerar tjänstparametrarna och klickar på Nästa.
1. På sidan Konfigurera säkerhetsprofil kan du göra de ändringar du behöver:

   * **** Kräv att anropare autentiserar: Den här inställningen anger om tjänsten kan anropas med eller utan autentiseringsuppgifter.

      Om *uppringare för närvarande krävs för att autentisera* visas, måste uppringaren autentiseras och uppringarens huvudnamn måste ha behörighet att anropa tjänsten. I annat fall avvisas anropsförsöket. Klicka på Tillåt oautentiserade anropare för att ta bort behovet av autentisering.

      Om *anropare inte behöver autentisera* visas kan anroparen av tjänsten vara autentiserad eller ej. Anropet av tjänsten lyckas alltid eftersom det inte finns någon auktoriseringskontroll. Klicka på Kräv att anropare autentiserar för att begära autentisering.

   * **** Kör som: Anger den körningsidentitet som används av en tjänst efter att den har anropats. Klicka på Ändra om du vill ändra det här alternativet. Välj bland följande alternativ:

      **** Ospecificerad: Standardbeteendet används.

      **** Anropare: Använder samma identitet som användaren som anropade tjänsten.

      **** System: Kör tjänsten med fullständig behörighet. Det här är standardinställningen för långvariga processer.

      **** Namngiven användare: Gör att du kan köra tjänsten som en specifik användare. Det här är standardinställningen för kortlivade processer. När du väljer det här alternativet klickar du på Välj användare för att visa sidan Välj huvudnamn, där du kan söka efter och välja användaren.

   * Om du vill lägga till ett huvudnamn i säkerhetsprofilen klickar du på Lägg till huvudnamn och väljer den användare eller grupp som ska läggas till som huvudnamn. Klicka på Nästa och välj sedan de behörigheter du vill tilldela detta huvudkonto:

      **** INVOKE_PERM: Så här anropar du alla åtgärder på tjänsten

      **** MODIFY_CONFIG_PERM: Ändra konfigurationen för en tjänst

      **** SUPERVISOR_PERM: Så här visar du processinstansdata för en tjänst som skapats från en process

      **** START_STOP_PERM: Starta och stoppa en tjänst

      **** ADD_REMOVE_ENDPOINTS_PERM: Lägga till, ta bort och ändra slutpunkter för en tjänst

      **** CREATE_VERSION_PERM: Skapa en ny version av tjänsten

      **** DELETE_VERSION_PERM: Så här tar du bort en version av tjänsten

      **** MODIFY_VERSION_PERM: Ändra en version av tjänsten

      **** READ_PERM: Så här visar du tjänsten

      Klicka på Slutför för att lägga till säkerhetsobjektet i säkerhetsprofilen.

## Ta bort ett arkiv {#remove-an-archive}

>[!NOTE]
>
>Om du vill ta bort ett arkiv som innehåller resurser som lagras i en tredjepartsdatabas (EMC Documentum Content Server, IBM FileNet Content Manager eller IBM Content Manager) måste du även ta bort resursfilerna från databasen med Workbench.

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Arkivhantering.
1. Markera kryssrutan för arkivet som ska tas bort på sidan Arkivhantering och klicka på Ta bort.

