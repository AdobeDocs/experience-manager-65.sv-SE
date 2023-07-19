---
title: Skapa och konfigurera roller
seo-title: Creating and configuring roles
description: Lär dig hur du associerar användare och grupper med roller som redan ingår i databasen för användarhantering. Du kan också skapa, redigera och ta bort roller.
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2525'
ht-degree: 0%

---

# Skapa och konfigurera roller{#creating-and-configuring-roles}

På webbsidorna för användarhantering kan du koppla användare och grupper till roller som redan ingår i databasen för användarhantering. Du kan också skapa, redigera och ta bort roller.

Användarhantering har två typer av roller:

**Muterbara roller:** Den här typen av roll kan redigeras och tas bort och rollbehörigheter kan läggas till och tas bort från de här rolltyperna. Alla roller som du skapar betraktas som ändringsbara. Du kan lägga till eller ta bort användare och grupper som tilldelats till ändringsbara roller.

**Oföränderliga roller:** Standardrollerna som ingår i användarhantering är oföränderliga roller. Dessa roller kan inte redigeras eller tas bort. Du kan dock lägga till eller ta bort användare och grupper som tilldelats oföränderliga roller.

Både ändringsbara och oföränderliga roller kan också skapas via API:er för AEM formulär.

## Standardroller {#default-roles}

Följande standardroller ingår i databasen för användarhantering.

**användare i administrationskonsolen:** Kan komma åt administrationskonsolen.

**Programadministratör:** Kan använda alla Workbench-funktioner. Kan använda sidorna för program och tjänster i administrationskonsolen för att konfigurera egenskaper, slutpunkter och säkerhet för tjänstens körtid.

**AEM formuläradministratör:** Kan utföra alla åtgärder för alla installerade tjänster.

**Säkerhetsadministratör:** Styr inställningarna för användarhantering och hanterar användare och grupper som är associerade med en användarhanterardomän

**Tjänstanvändare:** Kan visa och anropa vilken tjänst som helst

**Superadministratör:** Har tillgång till alla administrativa funktioner i systemet, inklusive tjänster

**Förtroendeadministratör:** Kan hantera PKI-förtroendeinställningar och PKI-autentiseringsuppgifter som hanteras från sidan Hantering av förtroendearkivet i administrationskonsolen

### Ytterligare standardroller {#additional-default-roles}

Följande extra standardroller kan inkluderas, beroende på vilka AEM du har installerat

**Användare av program för dokumentöverföring:** Kan överföra dokument med Flex Remoting.

**Forms Administrator:** Kan visa och ändra inställningar från Forms-sidan i administrationskonsolen

**AEM Contentspace Administrator:** Kan visa och ändra inställningar från sidan Innehållstjänster (inaktuellt) i administrationskonsolen

**AEM Contentspace User:** Kan logga in på webbsidor i innehållsområdet (borttaget)

**Documentum Connector Administrator:** Kan visa och ändra inställningar från sidan Connector for EMC Documentum i administrationskonsolen

**AEM formulär FileNet Connector Administrator:** Kan visa och ändra inställningar från Connector for IBM FileNet-sidan i administrationskonsolen

**AEM formulär IBM CM Connector Administrator:** Kan visa och ändra inställningar från Connector for IBM Content Manager-sidan i administrationskonsolen

**Rights Management Administrator:** Utför alla åtgärder som krävs för alla serverkonfigurationer på de relevanta Rights Management-sidorna

**Rights Management-slutanvändare:** Kan komma åt Rights Management:s webbsidor

**Rights Management Invite User:** Kan bjuda in användare

**Rights Management Hantera inbjudna och lokala användare:** Kan utföra åtgärder som krävs för att hantera alla inbjudna och lokala användare på relevanta Rights Management-sidor

**Administratör för principuppsättning i Rights Management:** Utför alla uppgifter som krävs för alla principuppsättningar på de relevanta Rights Management-sidorna

**Rights Management Super Administrator:** Utför alla åtgärder som krävs från Rights Management-sidan

**AEM Workspace Administrator:** Kan visa och ändra inställningar från sidan Arbetsyta i administrationskonsolen

***anteckning **: Flex Workspace är föråldrat för AEM formulärreleaser.*

**Arbetsytans användare:** Kan logga in på slutanvändarprogrammet för arbetsytan

**Utdataadministratör:** Kan visa och ändra inställningar från utdatasidan i administrationskonsolen

**PDFG-administratör:** Kan visa och ändra inställningar från PDF Generator-sidan i administrationskonsolen

**PDFG-användare:** Har tillgång till alla icke-administrativa funktioner för PDF Generator

**Acrobat Reader DC Extensions Web Application:** Kan använda webbprogrammet Acrobat Reader DC Extensions

>[!NOTE]
>
>Användare med vissa typer av administratörsbehörighet kan av säkerhetsskäl inte komma åt arbetsytans slutanvändarsidor. Eftersom dessa sidor kan finnas utanför en brandvägg kan ett tillstånd för åtgärder på administrationsnivå utgöra en säkerhetsrisk. Endast användare som har AEM Workspace Administrator eller AEM form Workspace User kan komma åt Workspace-slutanvändarens webbsidor.

>[!NOTE]
>
>Flex Workspace är föråldrat för AEM formulärreleaser.

## Skapa en roll {#create-a-role}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Ny roll.
1. I rutan Rollnamn skriver du ett namn för rollen och, om du vill, skriver en beskrivning av rollen och klickar sedan på Nästa.

   >[!NOTE]
   >
   >När du använder MySQL kan du inte skapa två roller som har samma namn men som skiljer sig åt när det gäller användningen av utökade tecken. Om du till exempel försöker skapa en roll med namnet abcde när det redan finns en roll med namnet âbcdè uppstår ett fel.

1. Klicka på Sök behörigheter och välj de behörigheter som ska läggas till i rollen.
1. Klicka på OK och sedan på Nästa.
1. Tilldela den här rollen till användare och grupper:

   * Klicka på Sök efter användare/grupper.
   * Ange sökvillkoren i rutan Sök.
   * Välj Namn, E-post eller Användar-ID och välj sedan Användare, Grupper eller Användare och grupper.
   * Markera domänen, välj antalet resultat som ska visas och klicka på Sök.
   * Markera kryssrutorna för de användare och grupper som rollen ska tilldelas till och klicka på OK.

1. Markera enheten om du vill visa användar- och gruppinformation.
1. Klicka på OK och sedan på Slutför.

## Redigera en roll {#edit-a-role}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Rollnamn.

   Som standard visas alla roller i databasen för användarhantering på sidan Rollhantering. Om listan med roller är stor använder du sökområdet högst upp på sidan för att söka efter ett specifikt rollnamn.

1. Klicka på rollen för att redigera, redigera de allmänna inställningarna och klicka på Spara.
1. Om du vill redigera rollbehörigheter klickar du på fliken Behörigheter och gör följande:

   * Om du vill lägga till nya behörigheter klickar du på Sök behörigheter, markerar kryssrutorna för de behörigheter som ska läggas till, klickar på OK och sedan på Spara.
   * Om du vill ta bort en behörighet från rollen markerar du kryssrutan för behörigheten, klickar på Ta bort och klickar sedan på Spara.

1. Om du vill hantera vem rollen är tilldelad klickar du på fliken Rollanvändare och gör följande:

   * Om du vill tilldela rollen till nya användare och grupper klickar du på Sök efter användare/grupper och fyller i sökinformationen. Markera kryssrutan för varje användare och grupp som rollen ska tilldelas till, klicka på OK och sedan på Spara.
   * Om du vill ta bort rollen markerar du kryssrutan för användarna eller gruppen, klickar på Ta bort tilldelning och klickar sedan på Spara.

## Ta bort en roll {#delete-a-role}

Du kan ta bort alla roller som du har skapat, men inte standardrollerna AEM formulär som ingår i produkten.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Rollnamn.

   Som standard visas alla roller i databasen för användarhantering på sidan Rollhantering. Om listan med roller är stor använder du sökområdet högst upp på sidan för att söka efter ett specifikt rollnamn.

1. Markera kryssrutan för rollen som ska tas bort, klicka på Ta bort och klicka sedan på OK.

## Tilldela användare och grupper en roll {#assign-a-role-to-users-and-groups}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Användare och grupper.
1. Ange information om du vill begränsa sökningen och klicka på Sök. Sökresultaten visas längst ned på sidan. Du kan sortera listan genom att klicka på någon av kolumnrubrikerna.
1. Markera kryssrutorna bredvid de användare och grupper som ska associeras med en roll och klicka på Tilldela roll.
1. Välj den roll som ska tilldelas användaren eller gruppen och klicka på OK.

Du kan också tilldela roller via sidan Rollhantering.

## Bestämma vem som har tilldelats till en roll {#determine-who-is-assigned-to-a-role}

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Rollnamn.

   Som standard visas alla roller i databasen för användarhantering på sidan Rollhantering. Om listan med roller är stor använder du sökområdet högst upp på sidan för att söka efter ett specifikt rollnamn.

1. Klicka på fliken Rollanvändare på sidan Rollinformation. En lista över användare och grupper som är direkt kopplade till rollen visas.

## Ändra rollbehörigheter {#change-role-permissions}

Du kan ändra behörigheterna för alla roller som du har skapat. Du kan inte ändra behörigheten för standardrollerna AEM formulär som ingår i produkten.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Rollnamn.

   Som standard visas alla roller i databasen för användarhantering på sidan Rollhantering. Om listan med roller är stor använder du sökområdet högst upp på sidan för att söka efter ett specifikt rollnamn.

1. Markera rollen som du vill visa behörigheter för och klicka på fliken Behörigheter.
1. Om du vill ändra dessa behörigheter klickar du på Sök behörigheter, markerar kryssrutorna för de behörigheter som ska läggas till i rollen, klickar på OK och sedan på Spara.
1. Om du vill ta bort en behörighet markerar du den, klickar på Ta bort och klickar sedan på Spara.

### AEM formulärbehörigheter {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Lägga till, ta bort och ändra slutpunkter för en tjänst

**Inloggning från Admin Console:** Visa administrationskonsolen

**Certifikatändring:** Ändra pålitlighetsinställningarna för alla certifikat i förtroendearkivet

**Certifikatet har lästs:** Läs alla certifikat i Trust Store

**Certifikatskrivning:** Lägg till ett certifikat i förtroendearkivet

**Lägg till komponent:** Installera en ny komponent i systemet

**Ta bort komponent:** Ta bort alla komponenter i systemet

**Komponenten har lästs:** Läs alla komponenter i systemet

**ContentSpace Administrator:** Behörighet för ContentSpace-administratör (borttagen)

**Konsolinloggning för Contentspace:** Behörighet för Console-inloggning (borttagen)

**Styrning av kärninställningar:** Hantera inställningarna på sidan Core System Settings i administrationskonsolen

**CREATE_VERSION_PERM:** Skapa en ny version av en tjänst

**Ändra autentiseringsuppgifter:** Ändra eventuella signeringsreferenser i Trust Store

**Läs autentiseringsuppgifter:** Läs alla autentiseringsuppgifter för signering i Trust Store

**Skrivning av autentiseringsuppgifter:** Lägg till en signeringsreferens i Trust Store

**CRL-ändring:** Ändra en lista över återkallade certifikat (Certificate Revocation List) i pålitlighetsarkivet

**CRL-läsning:** Läs alla listor över återkallade certifikat i Trust Store

**CRL-skrivning:** Lägg till en CRL i Trust Store

**Delegat:** Ange en åtkomstkontrollista för en resurs

**DELETE_VERSION_PERM:** Ta bort en version av en tjänst

**Dokumentöverföring:** Överför dokument i AEM formulär

**Domänkontroll:** Skapa, ta bort eller ändra inställningar för alla användarhanteringsdomäner, inklusive autentisering och katalogproviders

**Redigera händelsetyp:** Redigera till händelsetyper

**Identity Impersonation Control:** Personifiera identitet i användarhanteraren

**INVOKE_PERM:** Anropa alla åtgärder för en tjänst

**Kontroll av LCDS-datamodell:** Läs och distribuera datamodeller i datatjänster

**Uppdatering av License Manager:** Uppdatera licensinformation

**MODIFY_CONFIG_PERM:** Ändra konfigurationen för en tjänst

**TERM** Ändra versionen av en tjänst

**PDFGAdminBehörighet:** PDFG-administratör

**PDFGUserPermission:** PDFG-användare

**PERM_DCTM_ADMIN:** Documentum Connector-administratör

**PERM_FILENET_ADMIN:** FileNet Connector-administratör

**PERM_FORMS_ADMIN:** Forms-administratör

**PERM_IBMCM_ADMIN:** Administratör för IBM CM Connector

**PERM_OUTPUT_ADMIN:** Utdataadministratör

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Använda webbprogrammet Acrobat Reader DC-tillägg

**PERM_SP_ADMIN:** Hantera inställningar för SharePoint Connector

**PERM_WORKSPACE_ADMIN:** Hantera arbetsyteinställningar

**PERM_WORKSPACE_USER:** Logga in i slutanvändarprogrammet för arbetsytan

**Huvudkontroll:** Hantera användare och grupper för alla domäner och hantera rolltilldelningar för alla användare och grupper i alla domäner

**Läs/ta bort processinspelning:** Visa och hämta arbetsflödesgranskningsinstanser

**PROCESS_OWNER_PERM:** Visa trenddata och utföra administrativa åtgärder för en tjänst som skapats från en process

**Läs:** Läs innehållet i en resurs

**READ_PERM:** Läsa eller visa en tjänst

**Förnya försäkran:** Förnya bekräftelser i användarhantering

**Databasdelegat:** Ange en åtkomstkontrollista för en resurs

**Databasläsning:** Läs innehållet i en resurs

**Databasgenomgång:** Inkludera en resurs i en resursbegäran i en lista eller läs metadata för en resurs

**Databasskrivning:** Skriv databasmetadata och -innehåll

**Ägare av ändringsprofil för Rights Management:** Ändra principägare

**Inloggning på Rights Management slutanvändarkonsol:** Logga in på användargränssnittet i Rights Management

**Konfiguration för hantering av Rights Management:** Hantera serverkonfiguration

**Rights Management Hantera inbjudna och lokala användare:** Hantera inbjudna och lokala användare

**Hantera principuppsättningar i Rights Management:** Hantera alla profiler och dokument i alla principuppsättningar

**Lägg till koordinator för Rights Management-principuppsättning:** Lägga till, ta bort och ändra behörigheter för koordinatorer för principuppsättningar

**Skapa princip för Rights Management-principuppsättning:** Skapa en ny princip för en principuppsättning

**Ta bort princip för uppsättningsuppsättning för Rights Management-princip:** Ta bort en profil från en principuppsättning

**Redigera princip för Rights Management-principuppsättning:** Redigera en profil i en principuppsättning

**Rights Management Policy Set Manage Document Publisher (Hantera dokumentutgivare):** När du skapar principuppsättningar tilldelar du användare rollen som dokumentutgivare. Dokumentets utgivare är den användare som skyddar dokumentet med en profil.

**Ta bort koordinator för Rights Management-principuppsättning:** Ta bort en koordinator för principuppsättning från en principuppsättning

**Rights Management Policy Set Refoke Document:** Återkalla åtkomst till dokument i en principuppsättning

**Byteprincip för Rights Management-principuppsättning:** Byta profil för ett dokument

**Rights Management-principuppsättning Avåterkalla dokument:** Återkalla ett dokument

**Vyhändelse för Rights Management Policy Set:** Visa policy- och dokumenthändelser för alla profiler eller dokument i en principuppsättning

**Serverhändelser för Rights Management View:** Söka efter och visa alla granskningshändelser

**Rollkontroll:** Skapa, ta bort och ändra roller i Användarhantering

**Aktivera tjänst:** Starta en tjänst och göra den tillgänglig för anrop

**Tjänsttillägg:** Distribuera en ny tjänst till tjänstregistret. Detta innefattar att lägga till nya processer och processvarianter

**Inaktivering av tjänst:** Stoppa alla tjänster i systemet

**Radera tjänst:** Ta bort alla tjänster i systemet, inklusive processer och processvarianter

**Anropa tjänst:** Anropa alla tjänster i tjänstregistret som är tillgängliga vid körning

**Tjänständring:** Ändra konfigurationsegenskaperna för alla tjänster i systemet. Detta inkluderar låsning och upplåsning av en tjänst i utvecklingsmiljön samt tillägg eller borttagning av slutpunkter från en tjänst

**Tjänstläsning:** Läs alla tjänster i systemet. Detta inkluderar alla processer och processvarianter

**SERVICE_AGENT_PERM:** Visa data och interagera med processinstanser för en tjänst som skapats från en process

**SERVICE_MANAGER_PERM:** Utför belastningsutjämning och andra administrativa åtgärder för en tjänst som skapats från en process

**START_STOP_PERM:** Starta eller stoppa en tjänst

**SUPERVISOR_PERM:** Visa processinstansdata för en tjänst som skapats från en process

**Bläddra:** Inkludera en resurs i en resursbegäran i en lista eller läs metadata för en resurs

**Skriv:** Skriv databasmetadata och -innehåll

**Öppna filer i Workbench**

Om du vill visa innehållet i resursvyn i Workbench och öppna filer för visning, måste användaren ha följande behörigheter:

* Databasläsning
* Databasgenomgång
* Anropa tjänst
* Tjänstläsning

## Ta bort en användare eller grupp från en roll {#remove-a-user-or-group-from-a-role}

Använd sidan Rollhantering för att ta bort användare och grupper från en viss roll. Om användaren eller gruppen ärver rolltilldelningen kan du inte ta bort rollen på användar- eller gruppnivå. Ta antingen bort användaren eller gruppen från arvsträdet eller ta bort rollen från den överordnade.

1. I administrationskonsolen klickar du på Inställningar > Användarhantering > Rollhantering och sedan på Rollnamn.

   Som standard visas alla roller i databasen för användarhantering på sidan Rollhantering. Om listan med roller är stor använder du sökområdet högst upp på sidan för att söka efter ett specifikt rollnamn.

1. Klicka på namnet på rollen som ska uppdateras i listan över roller och klicka sedan på fliken Rollanvändare. En lista över användare och grupper som är associerade med rollen visas.
1. Markera kryssrutorna för de användare och grupper som ska tas bort från rollen och klicka på Ta bort tilldelning.
1. Klicka på Spara och sedan på OK.
