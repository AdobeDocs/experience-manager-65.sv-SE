---
title: Användarsynkronisering för Communities
description: Läs om hur användarsynkronisering fungerar i Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 0%

---

# Användarsynkronisering för Communities {#communities-user-synchronization}

## Introduktion {#introduction}

I Adobe Experience Manager (AEM) Communities, från Publish-miljön (beroende på vilka behörigheter som har konfigurerats), kan *webbplatsbesökare* bli *medlemmar*, skapa *användargrupper* och redigera deras *medlemsprofil* .

*Användardata* refererar till *användare*, *användarprofiler* och *användargrupper*.

*Medlemmar* refererar till *användare* som är registrerade i Publish-miljön, till skillnad från användare som är registrerade i författarmiljön.

Mer information om användardata finns på [Hantera användare och användargrupper](/help/communities/users.md).

## Synkronisera användare i en Publish-servergrupp {#synchronizing-users-across-a-publish-farm}

Användardata som skapats i Publish-miljön visas inte i redigeringsmiljön.

De flesta användardata som skapas i redigeringsmiljön är avsedda att finnas kvar i redigeringsmiljön och är inte synkroniserade eller replikerade till Publish-instanser.

När [topologin](/help/communities/topologies.md) är en [publiceringsgrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm) måste registrering och ändringar som görs i en Publish-instans synkroniseras med andra Publish-instanser. Medlemmar måste kunna logga in och se sina data på valfri Publish-nod.

När användarsynkronisering är aktiverat synkroniseras användardata automatiskt mellan Publish-instanser i servergruppen.

### Instruktioner för användarsynkronisering {#user-sync-setup-instructions}

Detaljerade stegvisa instruktioner om hur du aktiverar synkronisering i en publiceringsgrupp finns i [Användarsynkronisering](/help/sites-administering/sync.md).

## Användarsynkronisering i bakgrunden {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **VLT-paket**

  Det är en zip-fil med alla ändringar som görs i en utgivare, som måste distribueras mellan olika utgivare. Ändringar på en utgivare genererar händelser som plockas av händelseavlyssnaren för ändring. Detta skapar ett virtuellt paket som innehåller alla ändringar.

* **distributionspaket**

  Det innehåller distributionsinformation för Sling. Det är information om var innehållet ska distribueras och när det senast distribuerades.

## Vad händer när ... {#what-happens-when}

### Publish Site från webbgruppskonsolen {#publish-site-from-communities-sites-console}

När en communitywebbplats publiceras från konsolen [Webbplatser för grupper](/help/communities/sites-console.md) på författaren är effekten att [replikera](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) de associerade sidorna och Sling distribuerar de dynamiskt skapade användargrupperna, inklusive deras medlemskap.

### Användaren är skapad eller redigerar profilen i Publish {#user-is-created-or-edits-profile-on-publish}

Användare och profiler som skapats i Publish-miljön (t.ex. genom självregistrering, social inloggning eller LDAP-autentisering) visas inte i redigeringsmiljön.

När topologin är en [publiceringsgrupp](/help/communities/topologies.md) och användarsynkroniseringen har konfigurerats korrekt, synkroniseras *användar* och *användarprofilen* över hela publiceringsgruppen med Sling-distribution.

### Ny community-grupp skapas på Publish {#new-community-group-is-created-on-publish}

Även om det initieras från en Publish-instans skapas communitygrupper, vilket resulterar i nya webbplatssidor och en ny användargrupp, i själva verket på Author-instansen.

Som en del av processen replikeras de nya webbplatssidorna till alla Publish-instanser. Den dynamiskt skapade användargruppen och dess medlemskap distribueras till alla Publish-instanser.

### Användare eller användargrupper skapas med säkerhetskonsolen {#users-or-user-groups-are-created-using-security-console}

Användardata som skapats i publiceringsmiljön visas inte i redigeringsmiljön och omvänt.

När konsolen [Användaradministration och säkerhet](/help/sites-administering/security.md) används för att lägga till nya användare i publiceringsmiljön synkroniserar användarsynkroniseringen de nya användarna och deras gruppmedlemskap med andra publiceringsinstanser, om det behövs. Användarsynkronisering synkroniserar även användargrupper som skapats via säkerhetskonsolen.

### Användare publicerar innehåll på Publish {#user-posts-content-on-publish}

För användargenererat innehåll (UGC) nås data som anges i en publiceringsinstans via den [konfigurerade SRP](/help/communities/srp-config.md).

## God praxis {#bestpractices}

Som standard är användarsynkroniseringen **inaktiverad**. När du aktiverar användarsynkronisering måste du ändra *befintliga* OSGi-konfigurationer. Inga nya konfigurationer ska läggas till som ett resultat av aktivering av användarsynkronisering.

Användarsynkronisering förlitar sig på redigeringsmiljön för att hantera distributionen av användardata, även om användardata inte skapas på författaren.

**Förutsättningar**

1. Om användare och användargrupper redan har skapats på en utgivare bör du [manuellt synkronisera](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) användardata till alla utgivare innan du konfigurerar och aktiverar användarsynkronisering.

   När användarsynkronisering har aktiverats synkroniseras endast nyskapade användare och grupper.

1. Kontrollera att den senaste koden har installerats:

   * [AEM plattformsuppdateringar](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities-uppdateringar](/help/communities/deploy-communities.md#latestfeaturepack)

Följande konfigurationer krävs för att aktivera användarsynkronisering på AEM Communities. Kontrollera att dessa konfigurationer är korrekta för att förhindra att distribution av säljinnehåll misslyckas.

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

Den här konfigurationen hämtar innehållet som ska synkroniseras mellan utgivarna. Konfigurationen är på Author-instansen. Författaren måste hålla reda på alla utgivare som finns där och var all information ska synkroniseras.

Standardvärdena i konfigurationen är för en enda publiceringsinstans. När användarsynkronisering är användbart för att synkronisera flera publiceringsinstanser, till exempel för en publiceringsgrupp, måste ytterligare publiceringsinstanser läggas till i konfigurationen.

**Hur synkroniseras innehållet?**

Författarinstans skickar utgivarens slutpunkt. När en användare skapas eller uppdateras på specifika utgivare (n) hämtar författaren innehållet från deras exportslutpunkter och [överför innehållet](/help/communities/sync.md#main-pars-image-1413756164) till andra utgivare (n-1, dvs. inte de utgivare som innehållet hämtas från).

Så här konfigurerar du synkroniseringsagenter för Apache Sling:

1. Logga in med administratörsbehörighet på din AEM författarinstans.
1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md). Exempel: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Hitta **Apache Sling Distribution Agent - Sync Agents Factory**.

   * Välj den befintliga konfiguration som ska öppnas för redigering (pennikon).

     Verifiera namn: **social pubsync.**

   * Markera kryssrutan **Aktiverad**.
   * Välj **Använd flera köer.**
   * Ange **Exporter-slutpunkter** och **Import-slutpunkter** (du kan lägga till fler export- och importslutpunkter).

     Dessa slutpunkter definierar var du vill hämta innehållet från och var du vill skicka innehållet. Författaren hämtar innehållet från den angivna exporterarens slutpunkt och skickar innehållet till utgivaren (utom den utgivare som innehållet hämtades från).

   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite-distribution - krypterad lösenordsleverantör {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Det gör att författaren kan identifiera den behöriga användaren som har behörighet att synkronisera användardata från författaren till publiceringen.

Den [behöriga användaren skapade](/help/sites-administering/sync.md#createauthuser) på alla publiceringsinstanser hjälper utgivaren att ansluta till författaren och konfigurera Sling-distributionen på författaren. Den här auktoriserade användaren har alla nödvändiga [ACL](/help/sites-administering/sync.md#howtoaddacl).

När data ska installeras på eller hämtas från utgivare ansluter författaren till utgivare med de autentiseringsuppgifter (användarnamn och lösenord) som anges i den här konfigurationen.

Så här ansluter du författare till utgivare med hjälp av auktoriserade användare:

1. Logga in med administratörsbehörighet på din AEM författarinstans.
1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md).

   Exempel: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Leta upp **Adobe Granite-distribution - krypterad lösenordstransporthemlighetsprovider.**
1. Välj den befintliga konfiguration som ska öppnas för redigering (pennikon).

   Verifiera egenskapen **social pubsync** - **publishUser.**

1. Ange användarnamn och lösenord för den [behöriga användaren](/help/sites-administering/sync.md#createauthorizeduser).

   Till exempel **usersync - admin**

![granite-password-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

Den här konfigurationen används för att konfigurera data som du vill synkronisera mellan utgivare. När data skapas/uppdateras i sökvägar som anges i **Tillåtna rötter** aktiveras &quot;var/community/distribution/diff&quot; och den skapade replikatorn hämtar data från en utgivare och installerar dem på andra utgivare.

Så här konfigurerar du data (nodsökvägar) att synkronisera:

1. Logga in med administratörsbehörighet för din publiceringsinstans.
1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md).

   Exempel: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Hitta **Apache Sling Distribution Agent - köagentfabrik**.
1. Välj den befintliga konfiguration som ska öppnas för redigering (pennikon).

   Verifiera namn: **social pubsync -reverse**

1. Markera kryssrutan **Aktiverad** och spara.
1. Ange de nodsökvägar som ska replikeras i **Tillåtna rötter**.
1. Upprepa för varje **publish**-instans.

   ![queue-agent-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

Den här konfigurationen synkroniserar gruppmedlemskap mellan utgivare.
Om medlemskapet för en grupp i en utgivare inte uppdateras av andra utgivare måste du se till att **ref:members** läggs till i **utsökta egenskapsnamn**.

Så här ser du till att medlemskapet synkroniseras:

1. Logga in med administratörsbehörighet för din publiceringsinstans.
1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md).

   Exempel: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Leta reda på **Adobe Granite Distribution - Diff Observer Factory**.
1. Välj den befintliga konfiguration som ska öppnas för redigering (pennikon).

   Verifiera **agentnamn: socialpubsync -reverse**.

1. Markera kryssrutan **Aktiverad**.
1. Ange **rep:members** som beskrivning för propertyName i **sökta egenskapsnamn** och Spara.

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Factory för schemalagda utlösare {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Med den här konfigurationen kan du konfigurera avsökningsintervallet (efter vilket utgivare pingas och ändringar hämtas av författaren) så att ändringarna synkroniseras mellan utgivare.

Författaren avfrågar utgivare var 30:e sekund (standard). Om det finns paket i mappen `/var/sling/distribution/packages/  socialpubsync -  vlt /shared` hämtar den paketen och installerar dem på andra utgivare.

Så här ändrar du avsökningsintervallet:

1. Logga in med administratörsbehörighet på din AEM författarinstans.
1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md), till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Leta upp **utlösare för Apache Sling Distribution - Factory för schemalagda utlösare**

   * Välj den befintliga konfiguration som ska öppnas för redigering (pennikon).

     Verifiera **social pubsync-edul-trigger**

   * Ange intervallet i sekunder till önskat intervall och spara.

   ![schemalagd-trigger](assets/scheduled-trigger.png)

### AEM Communities Sync Listener {#aem-communities-user-sync-listener}

För problem i Sling-distributionen där det finns en diskrepans i prenumerationer och följande kontrollerar du om följande egenskaper i **AEM Communities User Sync Listener** -konfigurationer är inställda:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* Distribuerade mappar

Så här synkroniserar du prenumerationer:

I varje AEM publiceringsinstans:

1. Logga in med administratörsbehörighet.
1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md). Exempel: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Leta reda på **AEM Communities-lyssnaren för användarsynkronisering**.
1. Välj den befintliga konfiguration som ska öppnas för redigering (pennikon)

   Verifiera namn: **social pubsync-edul-trigger**

1. Ange följande **NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   De nodtyper som anges i den här egenskapen synkroniseras och meddelandeinformationen (bloggar och konfigurationer som följs) synkroniseras mellan olika utgivare.

1. Lägg till alla mappar som ska synkroniseras i **DistributedFolders**. Exempel:

   `segments/scoring`

   `social/relationships`

   `activities`

1. Ange **ignorablenodes** till:

   `.tokens`

   `system`

   `rep:cache` (eftersom klibbiga sessioner används behöver du inte synkronisera den här noden till olika utgivare).

   ![user-sync-listner](assets/user-sync-listner.png)

### Unikt försäljnings-ID {#unique-sling-id}

AEM författarinstans använder Sling ID för att identifiera varifrån data kommer och till vilka utgivare de behöver (eller inte behöver) skicka tillbaka paketet till.

Se till att alla utgivare i en publiceringsgrupp har ett unikt Sling ID. Om Sling ID är samma för flera publiceringsinstanser i en publiceringsgrupp misslyckas användarsynkroniseringen. Eftersom författaren inte vet var paketet ska hämtas och var paketet ska installeras.

För att säkerställa ett unikt Sling-ID för utgivaren i publiceringsgruppen, på varje Publish-instans:

1. Bläddra till [https://_host:port_/system/console/status-slingssettings](https://localhost:4503/system/console/status-slingsettings).
1. Kontrollera värdet för **Sling ID**.

   ![slingid](assets/slingid.png)

   Om Sling ID för en Publish-instans matchar Sling ID för någon annan Publish-instans:

1. Stoppa en av Publish-instanserna som har ett matchande Sling ID.
1. I katalogen `crx-quickstart/launchpad/felix` söker du efter och tar bort filen *sling.id.file.*

   På ett Linux-system:

   `rm -i $(find . -type f -name sling.id.file)`

   På ett Windows-system:

   Använd Utforskaren i Windows och sök efter `sling.id.file`

1. Starta Publish-instansen. Vid start tilldelas den ett nytt Sling ID.
1. Verifiera att **Sling ID** nu är unikt.

Upprepa dessa steg tills alla Publish-instanser har ett unikt Sling ID.

### Vault Package Builder Factory {#vault-package-builder-factory}

För att uppdateringar ska kunna synkroniseras på rätt sätt måste du ändra valvpaketets byggare för användarsynkronisering.
I `/home/users` skapas en `*/rep:cache`-nod. Det är ett cacheminne som används för att hitta att om vi frågar efter en nods huvudnamn kan det här cacheminnet användas direkt.

Användarsynkroniseringen kan avbrytas om `rep :cache` noder synkroniseras mellan utgivare.

Så här ser du till att uppdateringarna synkroniseras korrekt mellan olika utgivare, i varje AEM Publish-instans:

1. Åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

   Exempel: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Leta reda på **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   Builder name: social pubsync-vlt.

1. Välj redigeringsikonen.
1. Lägg till två paketnodsfilter:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Hantering av profiler
   * Om du vill skriva över befintliga rep:policy-noder med nya lägger du till ett tredje paketfilter: `/home/users|+.*/rep:policy`
   * Ange `Acl Handling: IGNORE` om du vill förhindra att profiler distribueras

   ![Vaultpaketbyggare, fabrik](assets/vault-package-builder-factory.png)

## Felsöka Sling-distribution i AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Om Sling-distributionen misslyckas provar du följande felsökningssteg:

1. **Sök efter [felaktigt tillagda konfigurationer](/help/sites-administering/sync.md#improperconfig)**

   Se till att flera konfigurationer inte läggs till eller redigeras, i stället bör de befintliga standardkonfigurationerna redigeras.
1. **Kontrollera konfigurationer**

   Se till att alla [konfigurationer](/help/communities/sync.md#bestpractices) har angetts korrekt i AEM Author-instansen, vilket anges i [Bästa praxis](/help/communities/sync.md#main-pars-header-863110628).

1. **Kontrollera behörigheter**

   Om paketen inte är korrekt installerade kontrollerar du att den [behöriga användaren](/help/sites-administering/sync.md#createauthuser) som skapades i den första Publish-instansen har rätt åtkomstkontrollistor.

   Om du vill validera detta ändrar du i stället för den [skapade auktoriserade användaren](/help/sites-administering/sync.md#createauthuser) konfigurationen [Adobe Granite Distribution - Krypterad lösenordstransportprovider](/help/sites-administering/sync.md#adobegraniteencpasswrd) på författarinstansen så att administratörens användarautentiseringsuppgifter används. Försök sedan installera paketen igen. Om användarsynkroniseringen fungerar bra med administratörsautentiseringsuppgifter innebär det att den skapade publiceringsanvändaren inte har rätt åtkomstkontrollistor.

1. **Kontrollera konfigurationen för Diff-observationsfabriken**

   Om bara specifika noder inte synkroniseras över hela publiceringsgruppen, till exempel, synkroniseras inte gruppmedlemmar, kontrollerar du att konfigurationen [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) är aktiverad och att **rep: members** är inställda i **sökta egenskapsnamn**.

1. **Kontrollera AEM Communities användarsynkroniseringens lyssnarkonfiguration.** Om de skapade användarna är synkroniserade men prenumerationer och följningar inte fungerar kontrollerar du att konfigurationen för AEM Communities användarsynkroniseringsavlyssnare har:

   * Nodtyper - inställda på **rep:User, nt:undefined**, **nt:resource**, **rep:ACL**, **sling:Folder** och **sling:OrderedFolder**.
   * Ignorerbara noder - inställt på **.tokens**, **system** och **rep:cache**.
   * Distribuerade mappar - Ange de mappar som du vill distribuera.

1. **Kontrollera loggar som genereras när användare skapas i Publish-instansen**

   Om ovanstående konfigurationer är korrekt inställda men användarsynkroniseringen inte fungerar kontrollerar du loggarna som genereras när användaren skapas.

   Kontrollera om ordningen på loggarna är densamma enligt följande:

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

Felsök:

1. Inaktivera användarsynkronisering:
1. Logga in AEM författarinstansen med administratörsbehörighet.

   1. Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md). Exempel: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Leta reda på konfigurationen **Apache Sling Distribution Agent - Sync Agents Factory**.
   1. Avmarkera kryssrutan **Aktiverad**.

      När användarsynkroniseringen inaktiveras för Author-instansen (exporteraren och importören) inaktiveras slutpunkterna och Author-instansen är statisk. Paketen **vlt** har inte fästs eller hämtats av författaren.

      Om en användare nu skapas på en publiceringsinstans skapas paketet **vlt** i noden */var/sling/distribution/packages/ social pubsync - vlt /data* . Och om de här paketen skickas av författaren till en annan tjänst. Du kan hämta och extrahera dessa data för att kontrollera vilka egenskaper som skickas till andra tjänster.

1. Gå till en utgivare och skapa en användare på utgivaren. Därför skapas händelser.
1. Kontrollera [ordningen för loggar](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities) som skapas när användare skapas.
1. Kontrollera om ett **vlt**-paket har skapats på **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Aktivera nu användarsynkronisering på AEM Author-instansen.
1. På utgivaren ändrar du export- eller importslutpunkterna i **Apache Sling Distribution Agent - Sync Agents Factory**.
Vi kan hämta och extrahera paketdata för att kontrollera vilka egenskaper som skickas till andra utgivare och vilka data som går förlorade.
