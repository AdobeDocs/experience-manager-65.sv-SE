---
title: Användarsynkronisering
seo-title: Användarsynkronisering
description: Läs om användarsynkronisering i AEM.
seo-description: Läs om användarsynkronisering i AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Användarsynkronisering{#user-synchronization}

## Introduktion {#introduction}

När distributionen är en [publiceringsgrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm)måste medlemmarna kunna logga in och se sina data på valfri publiceringsnod.

Användare och användargrupper (användardata) som har skapats i publiceringsmiljön behövs inte i författarmiljön.

De flesta användardata som skapas i redigeringsmiljön är avsedda att finnas kvar i redigeringsmiljön och inte kopieras till publiceringsinstanser.

Registrering och ändringar som görs på en publiceringsinstans måste synkroniseras med andra publiceringsinstanser för att de ska ha tillgång till samma användardata.

Från och med AEM 6.1 synkroniseras användardata automatiskt mellan publiceringsinstanserna i servergruppen när användarsynkronisering är aktiverad och skapas inte på författaren.

## Sling Distribution {#sling-distribution}

Användardata, tillsammans med deras [åtkomstkontrollistor](/help/sites-administering/security.md), lagras i [Oak Core](/help/sites-deploying/platform.md), lagret nedanför Oak JCR, och du får åtkomst till dem via [Oak API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Med ovanliga uppdateringar är det rimligt att användardata synkroniseras med andra publiceringsinstanser via [Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (Sling-distribution).

Fördelarna med användarsynkronisering med Sling-distribution jämfört med traditionell replikering är:

* *användare*, *användarprofiler* och *användargrupper* som skapas vid publicering skapas inte för författaren

* Sling distribution anger egenskaper i jcr-händelser, vilket gör det möjligt att agera i händelseavlyssnare på publiceringssidan utan att bekymra sig om oändliga replikeringsslingor
* Sling-distribution skickar endast användardata till icke-ursprungliga publiceringsinstanser, vilket eliminerar onödig trafik
* [Åtkomstkontrollistorna](/help/sites-administering/security.md) i användarnoden ingår i synkroniseringen

>[!NOTE]
>
>Om sessioner krävs rekommenderar vi att du antingen använder en SSO-lösning eller använder en klisteristisk session, och att kunderna loggar in om de byter till en annan utgivare.

>[!CAUTION]
>
>Synkronisering av ***administratörsgruppen*** stöds inte, även om användarsynkronisering är aktiverat. I stället loggas ett fel att &quot;importera diff&quot; i felloggen.
>
>Om en användare läggs till i eller tas bort från gruppen ***administratörer** måste ändringen därför göras manuellt för varje publiceringsinstans när distributionen är en publiceringsgrupp.

## Aktivera användarsynkronisering {#enable-user-sync}

>[!NOTE]
>
>Som standard är användarsynkronisering `disabled`.
>
>Att aktivera användarsynkronisering innebär att ändra *befintliga* OSGi-konfigurationer.
>
>Inga nya konfigurationer ska läggas till som ett resultat av aktivering av användarsynkronisering.

Användarsynkronisering förlitar sig på redigeringsmiljön för att hantera distributionen av användardata, även om användardata inte skapas på författaren. Mycket, men inte allt, av konfigurationen sker i författarmiljön och varje steg identifierar tydligt om den ska utföras på författaren eller publiceringen.

Följande steg är nödvändiga för att aktivera användarsynkronisering, följt av ett [felsökningsavsnitt](#troubleshooting) :

### Förutsättningar {#prerequisites}

1. Om användare och användargrupper redan har skapats på en utgivare bör du synkronisera [användardata](#manually-syncing-users-and-user-groups) manuellt med alla utgivare innan du konfigurerar och aktiverar användarsynkronisering.

När användarsynkroniseringen är aktiverad synkroniseras endast nyskapade användare och grupper.

1. Kontrollera att den senaste koden har installerats:

* [Uppdateringar om AEM-plattformar](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
* [Uppdateringar för AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

**Aktivera användarsynkronisering**

* **on author**

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * leta `Apache Sling Distribution Agent - Sync Agents Factory`

      * välj den befintliga konfiguration som ska öppnas för redigering (pennikonen)Verifiera `name`: **`socialpubsync`**

      * markera `Enabled` kryssrutan
      * select `Save`


![](assets/chlimage_1-20.png)

### 2. Skapa auktoriserad användare {#createauthuser}

**Konfigurera behörigheter** Den här behöriga användaren kommer att användas i steg 3 för att konfigurera Sling-distributionen på författaren.

* **på varje publiceringsinstans**

   * logga in med administratörsbehörighet
   * åtkomst till [säkerhetskonsolen](/help/sites-administering/security.md)

      * till exempel [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * skapa en ny användare

      * for example, `usersync-admin`
   * lägg till den här användaren i **`administrators`** användargruppen
   * [lägg till ACL för den här användaren i /home](#howtoaddacl)

      * `Allow jcr:all` med begränsning `rep:glob=*/activities/*`



>[!CAUTION]
>
>En ny användare måste skapas.
>
>* Standardanvändaren som är tilldelad är **`admin`**.
>* Använd inte `communities-user-admin user.`
>



#### Lägga till ACL {#addacls}

* åtkomst till CRXDE Lite

   * till exempel [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* välj `/home` nod
* i den högra rutan väljer du `Access Control` fliken
* markera knappen för att lägga till en ACL-post `+`

   * **Huvudkonto**: *sök efter användare som har skapats för användarsynkronisering*
   * **Typ**: `Allow`
   * **Behörigheter**: `jcr:all`
   * **Restrictions** rep:glob: `*/activities/*`
   * välj **OK**

* välj **Spara alla**

![](assets/chlimage_1-21.png)

Se även

* [Behörighetshantering](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Felsökningsavsnittet [Ändra åtgärdsundantag under](#modify-operation-exception-during-response-processing)svarsbearbetning.

### 3. Transportreferenser för Apache Sling Distribution - Användarreferenser baserade DistributionTransportSecretProvider {#adobegraniteencpasswrd}

**Konfigurera behörigheter**

När en auktoriserad användare, som är medlem i **`administrators`**användargruppen, har skapats på alla publiceringsinstanser måste den auktoriserade användaren identifieras som behörig användare av författaren med behörighet att synkronisera användardata från författaren till publiceringen.

* **on author**

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * leta `Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider`
   * välj den befintliga konfiguration som ska öppnas för redigering (pennikonen)Verifiera `property name`: **`socialpubsync-publishUser`**

   * ange användarnamn och lösenord till den [behöriga användare](#createauthorizeduser) som skapades vid publicering i steg 2

      * for example, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

**Aktivera användarsynkronisering**

* **vid publicering**:

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * till exempel [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * leta `Apache Sling Distribution Agent - Queue Agents Factory`

      * välj den befintliga konfiguration som ska öppnas för redigering (pennikonen)Verifiera `Name`: `socialpubsync-reverse`

      * markera `Enabled` kryssrutan
      * select `Save`
   * **repeat **for each publish instance



![](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Factory {#diffobserver}

**Aktivera gruppsynkronisering**

* **för varje publiceringsinstans**:

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * till exempel [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * leta **`Adobe Social Sync - Diff Observer Factory`**

      * välj den befintliga konfiguration som ska öppnas för redigering (pennikon)

         Verify `agent name`: `socialpubsync-reverse`

      * markera `Enabled` kryssrutan
      * select `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution Trigger - Factory för schemalagda utlösare {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Valfritt) Ändra avsökningsintervall**

Som standard kommer författaren att söka efter ändringar var 30:e sekund. Så här ändrar du intervallet:

* **on author**

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * leta `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * välj den befintliga konfiguration som ska öppnas för redigering (pennikon)

         * Verify `Name`: `socialpubsync-scheduled-trigger`
      * ange `Interval in Seconds` till önskat intervall
      * select `Save`



![](assets/chlimage_1-24.png)

## Konfigurera för flera publiceringsinstanser {#configure-for-multiple-publish-instances}

Standardkonfigurationen är för en enda publiceringsinstans. Eftersom orsaken till aktiveringen av användarsynkronisering är att synkronisera flera publiceringsinstanser, t.ex. för en publiceringsgrupp, måste de ytterligare publiceringsinstanserna läggas till i Sync Agents Factory.

### 7. Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory-1}

**Lägg till publiceringsinstanser:**

* **on author**

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * leta `Apache Sling Distribution Agent - Sync Agents Factory`

      * välj den befintliga konfiguration som ska öppnas för redigering (pennikonen)Verifiera `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **Exporterarslutpunkter** Det ska finnas en exportörslutpunkt för varje utgivare. Om det till exempel finns två utgivare, localhost:4503 och 4504, ska det finnas två poster:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Importerarslutpunkter** Det ska finnas en importerarslutpunkt för varje utgivare. Om det till exempel finns två utgivare, localhost:4503 och 4504, ska det finnas två poster:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* select `Save`

### 8. AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

**(Valfritt) Synkronisera ytterligare JCR-noder**

Om det finns anpassade data som ska synkroniseras över flera publiceringsinstanser:

* **för varje publiceringsinstans**:

   * logga in med administratörsbehörighet
   * åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

      * for example, `https://localhost:4503/system/console/configMgr`
   * leta `AEM Communities User Sync Listener`
   * välj den befintliga konfiguration som ska öppnas för redigering (pennikonen)Verifiera `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **Nodtyper**Det här är listan över nodtyper som ska synkroniseras. Alla andra nodtyper än sling:Mappen måste listas här (sling:folder hanteras separat).
Standardlista över nodtyper som ska synkroniseras:

   * rep:User
   * nt:ostrukturerad
   * nt:resurs

* **Ignorerbara egenskaper**Det här är listan över egenskaper som kommer att ignoreras om några ändringar identifieras. Ändringar av de här egenskaperna kan synkroniseras som en sidoeffekt av andra ändringar (eftersom synkronisering alltid finns på nodnivå), men ändringar av de här egenskaperna utlöser inte själva synkroniseringen.
Standardegenskap som ska ignoreras:

   * cq:lastModified

* **Ignorerbara noder**-undersökvägar som helt ignoreras under synkroniseringen. Inget under dessa delsökvägar kommer att synkroniseras när som helst.
Standardnoder som ska ignoreras:

   * .tokens
   * system

* **Distribuerade mappar**Mest sling:Mappar ignoreras eftersom synkronisering inte behövs. Här listas de få undantagen.
Standardmappar att synkronisera

   * segment/poäng
   * sociala medier/relationer
   * verksamhet

### 9. Unikt försäljnings-ID {#unique-sling-id}

>[!CAUTION]
>
>Om Sling ID matchar mellan två eller flera publiceringsinstanser misslyckas synkroniseringen av användargruppen.

Om Sling ID är samma för flera publiceringsinstanser i en publiceringsgrupp synkroniseras inte användargrupperna.

Så här validerar du att alla värden för Sling ID skiljer sig åt för varje publiceringsinstans:

1. gå till [https://*host:port*/system/console/status-slingssettings](https://localhost:4503/system/console/status-slingsettings)
1. kontrollera värdet för **Sling ID**

![](assets/chlimage_1-27.png)

Om Sling ID för en publiceringsinstans matchar Sling ID för någon annan publiceringsinstans:

1. stoppa en av publiceringsinstanserna som har ett matchande Sling ID
1. i katalogen crx-quickstart/launchpad/felix

   * söka efter och ta bort filen med namnet *sling.id.file*

      * i ett Linux-system:
         `rm -i $(find . -type f -name sling.id.file)`

      * i ett Windows-system:
         `use windows explorer and search for *sling.id.file*`

1. starta publiceringsinstansen

   * vid start tilldelas det ett nytt Sling ID

1. validera att **Sling ID** nu är unikt

Upprepa dessa steg tills alla publiceringsinstanser har ett unikt Sling ID.

## Vault Package Builder Factory {#vault-package-builder-factory}

För att uppdateringarna ska kunna synkroniseras på rätt sätt måste du ändra valvpaketets byggare för användarsynkronisering:

* på varje AEM-publiceringsinstans
* åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

   * till exempel [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* leta upp `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* markera redigeringsikonen
* lägg till två `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* principhantering:

   * om du vill skriva över befintliga rep:principnoder med nya lägger du till ett tredje paketfilter:

      * `/home/users|+.*/rep:policy`
   * för att förhindra att profiler distribueras, ange

      * `Acl Handling:` `IGNORE`


![Vault Package Builder Factory](assets/vault-package-builder-factory.png)

## Vad händer när ... {#what-happens-when}

### Självregister för användare eller redigeringsprofil vid publicering {#user-self-registers-or-edits-profile-on-publish}

Användare och profiler som skapats i publiceringsmiljön (självregistrering) visas inte i författarmiljön.

När topologin är en [publiceringsgrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm) och användarsynkroniseringen har konfigurerats korrekt, synkroniseras *användare *och *användarprofil* över hela publiceringsgruppen med Sling-distribution.

### Användare eller användargrupper skapas med säkerhetskonsolen {#users-or-user-groups-are-created-using-security-console}

Användardata som skapats i publiceringsmiljön visas inte som avsett i redigeringsmiljön och vice versa.

När konsolen [Användaradministration och -säkerhet](/help/sites-administering/security.md) används för att lägga till nya användare i publiceringsmiljön synkroniserar användarsynkroniseringen de nya användarna och deras gruppmedlemskap med andra publiceringsinstanser, om det behövs. Användarsynkronisering synkroniserar även användargrupper som skapats via säkerhetskonsolen.

## Felsökning {#troubleshooting}

### Använda användarsynkronisering offline {#how-to-take-user-sync-offline}

Distributionskön måste vara tom och tyst om du vill inaktivera användarsynkronisering för att [ta bort en utgivare](#how-to-remove-a-publisher) eller [manuellt synkronisera data](#manually-syncing-users-and-user-groups).

Så här kontrollerar du status för distributionskön:

* on author:

   * med [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * sök efter poster i `/var/sling/distribution/packages`

         * mappnoder namngivna med mönstret `distrpackage_*`
   * med [Package Manager](/help/sites-administering/package-manager.md)

      * söka efter väntande paket (ännu inte installerat)

         * namngiven med mönstret `socialpubsync-vlt*`
         * skapad av `communities-user-admin`


Inaktivera användarsynkronisering när distributionskön är tom:

* on author

   * *uncheck * `Enabled` kryssrutan för [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

Så här återaktiverar du användarsynkronisering när åtgärderna har slutförts:

* on author

   * markera kryssrutan för `Enabled` [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnostik för användarsynkronisering {#user-sync-diagnostics}

Diagnostik för användarsynkronisering är ett verktyg som kontrollerar konfigurationen och försöker identifiera eventuella problem.

Gå bara från huvudkonsolen via **Verktyg, Åtgärder, Diagnostik och Diagnostik för användarsynkronisering.**

Om du bara anger användarsynkroniseringskonsolen visas resultatet.

Detta visas när användarsynkronisering inte har aktiverats:

![](assets/chlimage_1-28.png)

#### Så här kör du diagnostik för utgivare {#how-to-run-diagnostics-for-publishers}

När diagnostiken körs från redigeringsmiljön kommer resultatet att inkludera ett [INFO] -avsnitt som visar listan med konfigurerade publiceringsinstanser som kan bekräftas.

I listan finns en URL för varje publiceringsinstans som kör diagnostiken för den instansen. URL-parametern `syncUser` läggs till i diagnostikwebbadressen med dess värde inställt på den *auktoriserade synkroniseringsanvändaren* som skapades i [steg 2](/help/sites-administering/sync.md#2createauthorizeduser).

**Obs**: Innan du startar URL:en måste den *auktoriserade synkroniseringsanvändaren* redan vara inloggad på den publiceringsinstansen.

![](assets/chlimage_1-29.png)

### Felaktig konfiguration {#configuration-improperly-added}

När användarsynkroniseringen inte fungerar är det vanligaste problemet att ytterligare konfigurationer har *lagts till*. I stället borde den befintliga *standardkonfigurationen ha *redigerats*.

Här följer några vyer över hur den redigerade bilden visas standardkonfigurationer i webbkonsolen. Om fler än en instans visas bör den tillagda konfigurationen tas bort.

#### (författare) En Apache Sling Distribution Agent - Sync Agents Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### (author) One Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### (publicera) One Apache Sling Distribution Agent - Queue Agents Factory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### (publicera) En Adobe Social Sync - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (författare) One Apache Sling Distribution Trigger - Factory för schemalagda utlösare {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### Ändra åtgärdsundantag under svarsbearbetning {#modify-operation-exception-during-response-processing}

Om följande syns i loggen:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

Kontrollera sedan att avsnitt [2. Skapa behörig användare](/help/sites-administering/sync.md#createauthuser) följdes korrekt.

I det här avsnittet beskrivs hur du skapar en behörig användare, som finns i alla publiceringsinstanser, och identifierar dem i OSGi-konfigurationen för den hemliga providern. By default, the user is `admin`.

Den behöriga användaren bör göras medlem i **`administrators`** användargruppen och behörigheterna för den gruppen bör inte ändras.

Den behöriga användaren bör uttryckligen ha följande behörigheter och begränsningar för alla publiceringsinstanser:

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */aktiviteter/* |
| /home/users | X | */aktiviteter/* |
| /home/groups | X | */aktiviteter/* |

Som medlem i `administrators` gruppen bör den auktoriserade användaren ha följande behörigheter för alla publiceringsinstanser:

| **path** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Synkronisering av användargrupp misslyckades {#user-group-sync-failed}

Om Sling ID matchar mellan två eller flera publiceringsinstanser misslyckas synkroniseringen av användargruppen.

Se avsnitt [9. Unikt försäljnings-ID](#unique-sling-id)

### Synkronisera användare och användargrupper manuellt {#manually-syncing-users-and-user-groups}

* på utgivaren där användare och användargrupper finns:

   * [om det är aktiverat, inaktivera användarsynkronisering](#how-to-take-user-sync-offline)
   * [skapa ett paket](/help/sites-administering/package-manager.md#creating-a-new-package) med `/home`

      * när du redigerar paketet

         * Fliken Filter: Lägg till filter:Rotsökväg: `/home`
         * Fliken Avancerat: AC-hantering: `Overwrite`
   * [exportera paketet](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* på andra publiceringsinstanser:

   * [importera paketet](/help/sites-administering/package-manager.md#installing-packages)

Om du vill konfigurera eller aktivera användarsynkronisering går du till steg 1: Agenten för [Apache Sling Distribution - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

### När en utgivare blir otillgänglig {#when-a-publisher-becomes-unavailable}

När en publiceringsinstans blir otillgänglig bör den inte tas bort om den kommer att vara online igen i framtiden. Ändringarna köas för utgivaren och när den är online igen behandlas ändringarna.

Om publiceringsinstansen aldrig kommer att vara online igen, om den är permanent offline, måste den tas bort eftersom köbygget kommer att resultera i märkbart diskutrymme i författarmiljön.

När en utgivare inte är tillgänglig har författarloggen undantag som liknar:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Så här tar du bort en utgivare {#how-to-remove-a-publisher}

Om du vill ta bort en utgivare från [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)måste distributionskön vara tom och tyst.

* on author:

   * [Ta användarsynkronisering offline](#how-to-take-user-sync-offline)
   * följ [steg 7](#apache-sling-distribution-agent-sync-agents-factory) för att ta bort utgivaren från båda serverlistorna:

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * återaktivera användarsynkronisering

      * markera kryssrutan för `Enabled` [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)
