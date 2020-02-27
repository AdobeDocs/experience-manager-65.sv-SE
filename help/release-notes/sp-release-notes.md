---
title: Versionsinformation om AEM 6.5 Service Pack
description: Versionsinformation om Adobe Experience Manager 6.5 Service Pack 3.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: fdcd9173b02347a7a9527b292635d63e8aa9ce19

---


# Versionsinformation om Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | **Adobe Experience Manager 6.5** |
|---|---|
| Version | 6.5.3.0 |
| Typ | Service Pack-version |
| Date | 12 december 2019 |
| Hämta URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0), [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aem.html#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.3.zip) |

## Vad ingår i Adobe Experience Manager 6.5.3.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet och viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av version 6.5 i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager (AEM) 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.6.

* Experience Manager Assets har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate 64.

* Ny kolumn för skapat datum, som är sorterbar, har lagts till i DAM-listvyn och i resurssökningsresultat i listvyn.

* Resurssortering baserad på namnkolumnen har aktiverats i listvyn.

* Dynamic Media har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video medan bildrutan flyttas för att följa scenens fokuspunkt.

* Dynamic Media har stöd för Smart Imaging.

* Möjlighet att [ange inställningar för frånvaro](../forms/using/configure-out-of-office-settings.md) i AEM-arbetsflöden.

* Möjlighet att [dela inkorgs- eller inkorgsobjekt](../forms/using/configure-shared-queues-osgi.md) med andra användare i AEM-arbetsflöden.

* Möjlighet att [generera interaktiv kommunikation i batchläge](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* Uppdaterad version av jQuery som paketerats i ContextHub till 3.4.1.

### Ändringslista {#list-of-changes}

#### Assets {#assets-6530-enhancements}

**Produktförbättringar**

* Experience Manager Assets har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate 64 (NPR-27573).

* Ny kolumn för skapat datum, som är sorterbar, har lagts till i DAM-listvyn och i resurssökningsresultat i listvyn (NPR-31312).

* Resurssortering baserat på namnkolumnen är tillåtet i listvyn (NPR-31299).

* Resursfilerna GLB, GLTF, OBJ och STL har stöd för förhandsgranskning av resurser på sidan Resursinformation i DAM (CQ-4282277).

* ReplicationOnModifyListener-händelsen utlöses för segmentnoder under segmentöverföring i Dynamic Media (CQ-4281279).

* Dynamic Media har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video samtidigt som bildrutan flyttas för att följa scenens fokuspunkt (CQ-4278995).

* Dynamic Media stöder Smart Imaging (CQ-422249).

* Vyn Sök/bläddra har angetts som standardvy i Foundation-väljaren om frågeparametrar skickas i begäran (NPR-31601).

**Korrigeringar**

* Metadata för vissa PDF-dokument uppdateras inte och sparas i PDF-filen när titeln ändras (NPR-31629).

* Resursdelning fungerar inte för resurser som har plustecknet + i sina namn (NPR-31547).

* Redigeringar i standardsökformuläret Resurser Admin * Search Rail fungerar inte som förväntat (NPR-31502).

* Förslag visas inte när du använder Omnissearch on assets view för att söka efter resurser (NPR-31496).

* Resursreferenser i samlingar uppdateras inte när de refererade resurserna flyttas till en annan plats, om samma resurser refereras till av olika samlingar av olika användare (NPR-31486).

* Duplicerade IPTC-taggar läggs till i metadata för resurser (NPR-31328).

* Antalet sökresultat i det övre högra hörnet uppdateras inte korrekt när sökningen utlöses från filterfältet (NPR-31316).

* Alla kryssrutor är avmarkerade när kryssrutorna på den andra nivån avmarkeras i filtypsfiltret, och texten i sökfältet är inte synkroniserad med de valda/omarkerade egenskaperna (NPR-31287).

* Det går inte att ta bort alla medlemmar (användare/grupper) från en mapps medlemsdel. När användaren försöker ta bort alla användare läggs den inloggade användaren till i listan (NPR-31171).

* Resurser med plustecken (+) i filnamnet kan inte tas bort (NPR-31162).

* Menyn Skapa, som visas på den övre menyn när du väljer en mapp, visar inte &quot;Mapp&quot; som ett alternativ för att skapa (NPR-30877).

* Mappval Skapa > FileUpload-åtgärdsobjekt saknas när ACL för Deny jcr:removeChildNodes och jcr:removeNode på sökväg tillämpas för en användare (NPR-30840).

* DAM-arbetsflöden försätts i viloläge när vissa mp4-resurser överförs, vilket gör att alla återstående arbetsflöden försätts i viloläge (NPR-30662).

* Slut på minne uppstår när stora PDF-filer (av flera gigabyte) överförs till DAM och dess underresurser bearbetas (NPR-30614).

* Massförflyttning av resurser misslyckas och ett varningsmeddelande visas (NPR-30610).

* Resursnamn ändras till gemener när resurser flyttas från en mapp till en annan i AEM som körs i körläget Dynamic Media Scene 7 (NPR-31630).

* Ett fel uppstod när en fjärrbilduppsättning redigerades för bilden som finns i mappen som heter same som namnet på Scene 7-företaget (NPR-31340).

* Dynamiska medieresurser som innehåller referenser publiceras inte (NPR-31180).

* Överföringar från AEM Dynamic Media - Scene 7-miljön till Scene 7 tar för lång tid att slutföra (NPR-31048).

* Aktiveringspunkten som läggs till i en bildresurs är inte synlig via Interactive Image Viewer på sidan med resursinformation (NPR-30979).

* Enorma snedningsjobb skapas och Bearbetningsbanderollen visas igen när åtgärder som utförs på resurser i AEM Assets skickas till Scene 7 (NPR-30947).

* En konflikt inträffar när en språkkopia av resurser skapas och resurser inte överförs till Scene 7 (NPR-30932).

* Dynamiska återgivningar som hämtats från AEM som körs i läget Dynamic Media Hybrid är brutna (de är av texttyp med innehållet&quot;det går inte att hitta bilden&quot; i stället för bildinnehållstypen) (NPR-30876).

* Arbetsflödet för Dynamic Media Encode Video misslyckas med att generera miniatyrbilder för videon som migreras från Scene 7 till Dynamic Media - körningsläget Scene 7 (CQ-4282011).

* IpsApiException observerades när resurser migrerades från en instans till en annan med olika företags-ID:n för Scene 7 (CQ-4280548).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds har importerats till AEM (CQ-4283701).

* Rullningsknappar visas i visningsprogrammet om en 3D-resurs har få kameravinklar (CQ-4283322).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i DimensionalViewer på sidan Resursinformation (CQ-4283309).

* Videor kan inte spelas upp med SmartCropVideoViewer i Internet Explorer 11 och Safari (CQ-4281422).

* Användning av flyttningsknappen för att flytta flera resurser, från en mapp till en annan, misslyckas i AEM-körning på dynamiska media - scen7-körningsläge (CQ-4280384).

* Förvrängd video visas i resursinformation när MIME-typen är en annan än MP4 (CQ-4279704).

* Videoklipp som nyligen har infogats i mappar med en videoprofil är fortfarande i bearbetningstillstånd även när kodens procenttal har slutförts till 100 % (CQ-4279389).

* När du flyttar resurser från en mapp skapas ett stort antal snedstreck (API-anrop för Scene 7) än vad som helst krävs (CQ-4278664).

* Namn på bilduppsättningen ändras till gemener i Scen 7 när bilduppsättning (eller mediaset) skapas och namnges med lämplig namnkonvention i DAM (CQ-428112).

* Scene 7 Migrator anger felaktigt publiceringstillstånd (CQ-4263492).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition i innehållsfragment (CQ-4282898).

* PDF-filer är inte indexerade och innehållet i dem är inte sökbart (CQ-4278916).

* Felmeddelandet&quot;Grupp visas inte av användarväljaren: false förväntas vara lika med true&quot; visas när en stängd användargrupp läggs till med ett annat värde `principalName` och `authorizableId` (CQ-4278177).

* Resursens gränssnittskolumnvy visar alla sökvägar oavsett vilken sökväg en klientorganisation har (CQ-4278175).

* Resursväljarens sökning fungerar inte som förväntat (CQ-4275886).

* Återgivningsarbetsflöden misslyckas (CQ-4271928).

* DAM-händelserensning tar bort den senaste (maxSavedActivities) händelseinformationen och lagrar data som skapats tidigare (NPR-31336).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Åtgärdsfältet och antalet resurser uppdateras inte när du markerar alla och sedan avmarkerar vissa objekt (mappar/enskilda resurser) i Touch UI (NPR-3118).

* Ett undantag visas i AEM vid avsökning efter jobbinformation för en resurs (CQ-4283569).

* XSS-sårbarhet i DAM (NPR-31654).

#### Sites {#sites}

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy (NPR-30980).
* Om antalet poster är fler än 40 visas bara de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna (NPR-31182).
* När en användare lägger till japanska eller koreanska tecken i egenskapen description på en meny, visas förvrängda tecken för japansk och koreansk text på menyn. (NPR-31331).
* Det går inte att infoga en inbäddad tabell som listobjekt (NPR-30879) i RTF-redigeraren.
* När du har gjort en avskalning av RTF-redigerare (Rich Text Editor). använder textbunden teckensnittsstorlek för element, oväntat (NPR-31284).
* När en användare fokuserar på fält med vänster stödlinje och använder ett kortkommando för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från de vänstra fältspåren (NPR-31172).
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden (NPR-30882).
* API:t ResponsiveGridExporter returnerar inte gränssnittet com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Paketet com.day.cq.wcm.foundation.model.impl deklareras som ett privat paket (NPR-31398).
* När en sida som innehåller vissa ExperienceFragments öppnas i icke-redigerarläge (antingen i Författare utan prefixet och `editor.html` `wcmmode=disabled`, eller i Utgivare), avslutas begäran med HTTP-statusfelkoden 500 (NPR-30743).
* Användare kan inte ändra sitt lösenord och komma åt sin profilsida (NPR-31161).
* En JavaScript-fil med användardata genereras på serversidan (NPR-30822).
* AEM-redigeringsgränssnittet tillåter nätfiske med externt innehåll (NPR-29745).
* Sårbarhet vid språkinjektion i metadataredigeraren för AEM 6.5 (NPR-31017).

#### Sök- och användargränssnitt {#search-ui-interface}

* När du växlar från kortvyn till listvyn på en sökresultatsida uppstår en fördröjning innan sidan kan rullas (NPR-31286).

* Kryssrutan Markera alla är dold i listvyn i användargränssnittet för webbplatser (NPR-31614).

* Antalet Markera alla på en sökresultatsida är felaktigt (NPR-31120).

* I metadataredigeraren visas taggar som inte finns (NPR-31119).

#### Översättning {#translation}

* Två popup-fönster visas när du väljer alternativet Förfallodatum i ett översättningsjobb (NPR-31270).

#### Platform {#platform}

* Alternativet Mime-typ i webbkonsolen fungerar inte (NPR-31108).

* Klientcertifikatet accepteras inte när enkel inloggning konfigureras (NPR-31165).

* Uppdateringar i buffertstorlekskonfigurationen för Jetty-baserad HTTP-tjänst sparas inte (NPR-30925).

* QueryBuilder har nu stöd för orderby ``fn:name()`` i XPath-frågor (NPR-31322).

* Dubblettaktiveringsträdet skapas vid uppgradering från AEM 6.3 (NPR-31513).

* Vidarebefordrade begäranden bevarar inte svarshuvuden som ställs in vid slingautentisering (NPR-30013).

* Det går inte att söka i väljarkomponenterna (NPR-31692).

* Ett fel visas när en ZIP-fil bifogas till ett AEM Communities-inlägg på grund av olika versioner av Apache POI- och Apache Tika-paketet (NPR-31018).

* Paketet är dolt i konfigurationshanteraren och är därför inte tillgängligt för anpassade paket (NPR-31720). ``org.apache.sling.distribution.api``

#### Projekt {#projects}

* Det går inte att växla kalendervyer (NPR-31271).

#### Varumärkesportal {#assets-brand-portal}

**Produktförbättringar**

* Arbetsflödet för import av mediekällor i AEM Resurser ändras så att endast de nyskapade resurserna från Brand Portal hämtas till AEM, och de resurser som redan finns i mappen NEW hoppas över för att undvika replikering (CQ-4278527).

**Korrigeringar**

* En felaktig ikon visas när en ny Contribute-mapp skapas i funktionen Resurser (CQ-4282825).
* När du skapar en ny Contribute-mapp visas inte en eller båda undermapparna (NYTT och DELAT) i Contribute-mappen (CQ-4282424).
* Systemet genererar ett undantag om användaren försöker publicera om Contribute-mappen från AEM till Brand Portal efter att ha tagit emot nya resurser i Contribute-mappen från Brand Portal end (CQ-4279740).
* Det är inte tillåtet att skapa en Contribute-mapp i en Contribute-mapp (kapslad mapp) för att undvika komplexitet (CQ-4278391).
* Systemet genererar ett undantag när användarlistan för varumärkesportalen (.csv-fil) som importeras från AEM Admin Console överförs. Endast fälten Email, FirstName och LastName i CSV-filen är obligatoriska (CQ-4278390).

#### Communities {#communities}

**Korrigeringar**

* Snabblänkar för att hantera grupper (Öppna/Redigera/Publicera/Ta bort grupper) är inte synliga för communityadministratörer (Gruppadministratör/Webbplatsadministratör) (NPR-31627).
* En inskickad blogg visas bara om sidan uppdateras/läses in manuellt (NPR-31599).
* JCR-frågan som används av funktionen &quot;Mentions&quot; är skiftlägeskänslig och tar för lång tid att returnera resultaten (NPR-31475).
* AEM 6.5 UberJar-filen genererar ett undantag, paket saknas i AEM 6.5 UberJar-filen (NPR-31186). `cq-social-translation`
* Jackson Database-bibliotek uppdaterade till version 2.9.9.3 för att åtgärda nya säkerhetsluckor (NPR-30967).
* Aktiviteter och meddelandetitlar är inkonsekventa (NPR-30941).
* Sidindelningen fungerar inte korrekt i webbgruppsbloggar (NPR-30914).
* Analysrapporter fylls inte i i AEM-redigeringsmiljön. En tom sida visas (NPR-30913).

#### Oak {#oak}

* Uppdateringar av Lucene-index gör att författarservern sinkas (NPR-31548).

#### Formulär {#forms-6530}

>[!NOTE]
>
>AEM Service Pack innehåller inte korrigeringar för AEM Forms. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera tillägget](#install-aem-forms-add-on-package) AEM Forms och [Installera AEM Forms på JEE](#install-aem-forms-jee-installer).

##### Formulärtilläggspaket {#forms-add-on-package-6530}

**Adaptiva former**

* Strängar innehåller ordlistenyckeln när adaptiva former lokaliseras (NPR-31110).

**Interaktiv kommunikation**

* **MissingNode.toString()** returnerar felaktiga resultat efter uppgradering av Jackson-bibliotek till 2.10.0 (NPR-31549).

* Textredigeraren tar slumpmässigt bort blankstegstecken från text som kopieras från Microsoft Word (NPR-31113).

**Korrespondenshantering**

* Bildtexter och verktygstips visas inte när bokstäver migreras från LiveCycle ES4SP1 till AEM 6.5 (NPR-31615).

* **Textflödesformatering stöds** inte längre i felmeddelanden när bokstäver sparas som utkast (NPR-30463).

**Arbetsflöde**

* OSGi-arbetsflödet misslyckas på grund av 100 % processoranvändning (NPR-31233).

**HTML5-formulär**

* När du genererar HTML5-förhandsgranskning av ett XDP-formulär visas ett flimmer när instanser av ett delformulär läggs till (NPR-30909).

##### Formulär i JEE-installationsprogram {#forms-jee-installer-6530}

**Formulär - dokumenttjänster**

* SOAP-webbtjänst som använder MTOM i ett .NET-projekt visar undantag för AssemblerServiceClient-anrop och HTMLToPDF2-metoder (NPR-4281771).

**Foundation JEE**

* Åtgärdskonfigurationen läser inte in processnamnen för åtgärden Anropa ett formulärarbetsflöde för att skicka (NPR-31478).
* AEM Forms för JEE-användare stöter på fel som liknar de här när .lca-filer importeras eller LDAP konfigureras i Admin Console:

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


### Funktionspaket ingår {#feature-packs-included-6530}

>[!NOTE]
>
>För AEM Forms-kunder är det viktigt att installera AEM Forms-tilläggspaket efter installation av AEM Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Formulär - Foundation JEE {#forms-foundation-jee-feature}

* Stöd för AEM Forms i Oracle 18c (NPR-29155).

## Installera 6.5.3.0 {#install}

**Installationskrav**

* AEM 6.5.3.0 kräver AEM 6.5. Detaljerade instruktioner finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md) .
* Nedladdningen av Service Pack finns på Adobe Package Share, som du kommer åt direkt från AEM 6.5-instansen.
* På en distribution med MongoDB och flera instanser installerar du AEM 6.5.3.0 på en av Author-instanserna med hjälp av Package Manager.
* Innan du installerar Service Pack bör du kontrollera att du har en ögonblicksbild eller en ny säkerhetskopia av AEM-instansen.
* Starta om instansen innan du installerar den. Detta behövs bara när instansen fortfarande är i uppdateringsläge (och detta är fallet när instansen uppdaterades från en tidigare version), men vi rekommenderar att instansen körs under en längre period.

>[!CAUTION]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar AEM 6.5.3.0-paketet.

### Installera Service Pack via paketresurs {#install-service-pack-via-package-share}

Så här installerar du Service Pack på en befintlig AEM 6.5-instans:

1. Logga in på Package Share inifrån AEM eller direkt från webbläsaren och ladda ned [AEM 6.5.3.0-paketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. Installera det hämtade paketet med hjälp av Package Manager.

>[!NOTE]
>
>**Dialogrutan i användargränssnittet för Package Manager avslutas ibland felaktigt under installationen av 6.5.3.0**
>
>Därför rekommenderar vi att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till instansen. Användaren måste vänta på specifika loggar som rör avinstallation av uppdateringspaketet innan den kan vara säker på att installationen lyckas. Det händer vanligtvis på Safari, men kan hända i olika webbläsare.

**Automatisk installation**

Det finns två sätt att automatiskt installera AEM 6.5.3.0 i en instans som körs:

S. Placera paketet i ..*/crx-quickstart/install* -mappen när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API:t från Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - kontrollera att du använder cmd=install&amp;recursive=true - så att kapslade paket installeras.

>[!NOTE]
>
>AEM 6.5.3.0 stöder inte Bootstrap-installation.

**Validera installation**

1. På sidan Produktinformation (/system/console/ producto) visas den uppdaterade versionssträngen `Adobe Experience Manager, Version 6.5.3.0` under Installerade produkter.

1. Alla OSGi-paket är antingen **[!UICONTROL AKTIVA]** eller **[!UICONTROL FRAGMENT]** i OSGi-konsolen (använd webbkonsol: /system/console/bundles).
1. OSGI-paketet org.apache.jackrabbit.oak-core finns i version 1.10.6 eller senare (Använd webbkonsol: /system/console/bundles).

För att se vilka plattformar som är certifierade att köras med den här versionen, se de [tekniska kraven](/help/sites-deploying/technical-requirements.md).

### Installera AEM Forms-tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms. Korrigeringar i AEM Forms levereras via ett separat tilläggspaket.

>[!NOTE]
>
>AEM 6.5.3.0 innehåller en ny version av [AEM Forms-kompatibilitetspaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Om du använder en äldre version av AEM Forms-kompatibilitetspaketet och uppdaterar till AEM 6.5.3.0 installerar du den senaste versionen av AEM Forms-kompatibilitetspaketet efter installationen av Forms-tilläggspaketet.

1. Kontrollera att du har installerat AEM Service Pack.
1. Hämta motsvarande tilläggspaket för Forms som finns i [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms-tilläggspaketet enligt beskrivningen i [Installera AEM Forms-tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installera AEM Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i AEM Forms på JEE levereras via ett separat installationsprogram.

Information om hur du installerar det kumulativa installationsprogrammet för AEM Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen för patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Installationsprogram för Workbench

Eftersom det är ett fullständigt installationsprogram är filstorleken större än korrigeringsversionen. Avinstallera den tidigare Workbench-versionen innan du installerar den nya.

## UberJar {#uber-jar}

UberJar för AEM 6.5.3.0 finns i [Adobe Public Maven-databasen](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

Om du vill använda UberJar i ett Maven-projekt kan du läsa artikeln [Så här använder du UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Föråldrade funktioner {#removed-deprecated-features}

I det här avsnittet listas funktioner som har markerats som borttagna i AEM 6.5.3.0. Funktioner som ska tas bort i en framtida version är först inaktuella, med ett alternativt alternativ att använda.

Kunder uppmanas att granska om de använder funktionen eller funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativa alternativet.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Inställningsskärmen för **[!UICONTROL AEM Cloud-tjänster]** har tagits bort. Med integreringen av AEM och Target uppdaterad i AEM 6.5 för att stödja Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera AEM-sidor för analys och personalisering, har Opt-In Wizard blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och Adobe I/O-integreringar via respektive AEM-molntjänster |

## Kända fel {#known-issues}

* Om konfigurationsguiden för **anslutna resurser** returnerar ett 404-felmeddelande efter installationen av AEM 6.5.3.0 måste du installera om **cq-remotedam-client-ui-content** och **cq-remotedam-client-ui-components** -paketen manuellt med hjälp av Package Manager.
* Följande fel och varningsmeddelanden kan visas under installationen av AEM 6.5.x.x:
   * &quot;När Target-integreringen konfigureras i AEM med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källan&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källan&quot;Adobe Target Classic&quot;.
   * com.adobe.granite.Maintenance.impl.TaskScheduler: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används. CQ-4274424
   * com.adobe.granite.Maintenance.impl.TaskScheduler - Inga underhållsfönster hittades vid granit/operations/Maintenance.
   * Aktiveringspunkten i en Dynamic Media Interactive-bild syns inte när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i AEM 6.5.3.0

Lista över OSGi-paket som ingår i AEM 6.5.3.0

[Hämta fil](assets/6530_bundles.txt)

Lista över innehållspaket som ingår i AEM 6.5.3.0

[Hämta fil](assets/sp_6530_packages.txt)

## Användbara resurser {#helpful-resources}

* [Versionsinformation om AEM 6.5](/help/release-notes/release-notes.md)
* [AEM - produktsida](https://www.adobe.com/solutions/web-experience-management.html)
* [Stöd för AEM-utvecklare](https://docs.adobe.com/content/ddc/en.html)
* [AEM 6.5 - dokumentation](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Prenumerera på [Adobe Priority-produktuppdateringar](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## Begränsade platser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta kundsupport](https://daycare.day.com/public/contact.html)Mer information om hur du går till supportportalen finns i [Gå till supportportalen](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).
