---
title: Felsökning av replikering
seo-title: Troubleshooting Replication
description: I den här artikeln finns information om hur du felsöker replikeringsproblem.
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# Felsökning av replikering{#troubleshooting-replication}

Den här sidan innehåller information om hur du felsöker replikeringsproblem.

## Problem {#problem}

Replikering (icke-omvänd replikering) misslyckas av någon anledning.

## Upplösning {#resolution}

Det finns olika orsaker till att replikeringen misslyckas. I den här artikeln förklaras den metod som kan användas vid analys av dessa problem.

**Utlöses replikeringar alls när du klickar på knappen Aktivera? Om INTE, gör du följande:**

1. Gå till /crx/explorer och logga in som administratör.
1. Öppna &quot;Innehållsutforskaren&quot;
1. Se om det finns en nod/bin/replikate eller /bin/replicate.json. Om noden finns tar du bort den och sparar den.

**köas replikeringarna i replikeringsagentköerna?**

Kontrollera detta genom att gå till /etc/replication/agents.author.html och sedan klicka på replikeringsagenterna för att kontrollera.

**Om en agentkö eller ett fåtal agentköer har fastnat:**

1. Visas kön **blockerad** status? Om så är fallet, körs inte publiceringsinstansen eller svarar den inte alls? Kontrollera publiceringsinstansen för att se vad som är fel med den (d.v.s. kontrollera loggarna och se om det finns ett OutOfMemory-fel eller något annat problem. Om det sedan är långsamt tar du tråd och analyserar dem.
1. Visar köstatusen **Kön är aktiv - # väntande**? Replikeringsjobbet kan i princip fastna i en socketläsning i väntan på att publiceringsinstansen eller dispatchern ska svara. Det kan innebära att publiceringsinstansen eller dispatchern är under hög belastning eller sitter fast i ett lås. Ta tråddumpar från författaren och publicera i det här fallet.

   * Öppna trådsdumpar från författaren i en tråddumpsanalyserare, kontrollera om det visar att replikeringsagentens snedningsjobb har fastnat i en socketRead.
   * Öppna trådsdumpar från publicering i en tråddumpsanalyserare och analysera vad som kan göra att publiceringsinstansen inte svarar. Du bör se en tråd med POSTEN /bin/receive i dess namn, det vill säga den tråd som tar emot replikeringen från författaren.

**Om alla agentköer har fastnat**

1. Det är möjligt att en viss del av innehållet inte kan serialiseras under /var/replication/data på grund av att databasen är skadad eller något annat problem. Kontrollera om det finns ett relaterat fel i logs/error.log. Så här rensar du bort det felaktiga replikeringsobjektet:

   1. Gå till https://&lt;host>:&lt;port>/crx/de och logga in som admin-användare.
   1. Klicka på &quot;Verktyg&quot; i den övre menyn.
   1. Klicka på knappen för förstoringsglas.
   1. Välj &quot;XPath&quot; som Typ.
   1. I rutan Fråga anger du den här frågan /jcr:root/var/eventing/job//element(&#42;,slingevent:Job) sortera efter @slingevent:created
   1. Klicka på Sök
   1. I resultatet är de viktigaste objekten de senaste snedsättningsjobben. Klicka på var och en av dem och hitta de replikeringar som matchar det som visas högst upp i kön.

1. Det kan vara något fel med att snedställa jobbköer i utvecklingsramverket. Prova att starta om paketet org.apache.sling.event i /system/console.
1. Det kan bero på att jobbbearbetningen är helt avstängd. Det kan du kolla under Felix Console på fliken Sling Eventing. Kontrollera om den visas - Apache Sling Eventing (JOBBBEARBETNING ÄR INAKTIVERAD!)

   * Om ja, kontrollera Apache Sling Job Event Handler på fliken Konfiguration i Felix Console. Det kan bero på att kryssrutan Jobbbearbetning är aktiverad inte är markerad. Om detta är markerat och fortfarande visar att jobbbearbetning är inaktiverad, kontrollerar du om det finns någon övertäckning under /apps/system/config som inaktiverar jobbbearbetningen. Försök att skapa en osgi:config-nod för jobmanager.enabled med ett booleskt värde till true och kontrollera om aktiveringen har startat och det inte finns några fler jobb i kö.

1. Det kan också vara så att DefaultJobManager-konfigurationen försätts i ett inkonsekvent tillstånd. Detta kan inträffa när någon manuellt ändrar konfigurationen av &quot;Apache Sling Job Event Handler&quot; via OSGiconsole (t.ex. inaktiverar och återaktiverar egenskapen &quot;Jobbbearbetning aktiverad&quot; och sparar konfigurationen).

   * I det här läget försätts DefaultJobManager-konfigurationen som lagras på crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config i ett inkonsekvent läge. Och även om egenskapen &quot;Apache Sling Job Event Handler&quot; visar att &quot;Job Processing Enabled&quot; är i markerat läge, visas meddelandet &quot;Job Processing Enabled&quot; (Jobbbearbetning är inaktiverat) när man går till fliken Sling Eventing Eventing, och replikeringen fungerar inte.
   * För att lösa det här problemet måste du navigera till konfigurationssidan för OSGi-konsolen och ta bort konfigurationen Apache Sling Job Event Handler. Starta sedan om den Överordnad noden i klustret så att konfigurationen återställs till ett konsekvent tillstånd. Detta bör åtgärda problemet och replikeringen kommer att börja fungera igen.

**Skapa en replikering.log**

Ibland kan det vara praktiskt att ange att all replikeringsloggning ska läggas till i en separat loggfil på DEBUG-nivå. Så här gör du:

1. Gå till https://host:port/system/console/configMgr och logga in som administratör.
1. Hitta fabriken Apache Sling Logging Logger och skapa en instans genom att klicka på **+** till höger om fabrikskonfigurationen. Detta skapar en ny loggningslogg.
1. Ställ in konfigurationen så här:

   * Loggnivå: FELSÖKNING
   * Loggfilens sökväg: logs/replication.log
   * Kategorier: com.day.cq.replikation

1. Om du misstänker att problemet är relaterat till snedstreck/jobb på något sätt kan du även lägga till det här java-paketet under kategorier:org.apache.sling.event

## Pausar kön för replikeringsagent  {#pausing-replication-agent-queue}

Ibland kan det vara lämpligt att pausa replikeringskön för att minska belastningen på författarsystemet, utan att inaktivera den. För närvarande är detta endast möjligt om en port konfigureras tillfälligt. Från och med 5.4 kan du se pausknappen i replikeringsagentkön. Den har vissa begränsningar

1. Tillståndet är inte beständigt, vilket innebär att om du startar om en server eller ett replikeringspaket återställs det till körningsläge.
1. Pausen är inaktiv under en kortare period (OOB 1 timme efter inga aktiviteter med replikering från andra trådar) och inte under en längre tid. Eftersom det finns en funktion i sling som undviker inaktiva trådar. Kontrollera i princip om en jobbkötråd har varit oanvänd en längre tid, och i så fall startas rensningscyklerna. På grund av rensningscykeln stoppas kopplingen och därför försvinner den pausade inställningen. Eftersom jobb är beständiga initieras en ny tråd för att bearbeta kön som inte har information om den pausade konfigurationen. På grund av den här kön blir det körläge.

## Sidbehörigheter replikeras inte vid användaraktivering {#page-permissions-are-not-replicated-on-user-activation}

Sidbehörigheter replikeras inte eftersom de lagras under noderna som åtkomst beviljas till, inte med användaren.

I allmänhet bör inte sidbehörigheter replikeras från författaren till publiceringen och är inte standard. Detta beror på att åtkomsträttigheterna bör vara olika i dessa två miljöer. Därför rekommenderar vi att du konfigurerar åtkomstkontrollistor vid publicering separat från författaren.

## Replikeringskön har blockerats vid replikering av namnområdesinformation från författare till publicering {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

I vissa fall blockeras replikeringskön när du försöker replikera namnområdesinformation från författarinstansen till publiceringsinstansen. Detta beror på att replikeringsanvändaren inte har `jcr:namespaceManagement` privilegium. Undvik problemet genom att se till att:

* Replikeringsanvändaren (konfigurerad under [Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User) finns också på Publish-instansen.
* Användaren har läs- och skrivbehörighet på sökvägen där innehållet är installerat.
* Användaren har `jcr:namespaceManagement` behörighet på databasnivå. Du kan bevilja privilegiet enligt följande:

1. Logga in på CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) som administratör.
1. Klicka på **Åtkomstkontroll** -fliken.
1. Välj **Databas**.
1. Klicka **Lägg till post** (plusikonen).
1. Ange användarens namn.
1. Välj `jcr:namespaceManagement` från listan över behörigheter.
1. Klicka på OK.
