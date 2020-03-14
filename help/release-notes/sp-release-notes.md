---
title: Versionsinformation om AEM 6.5 Service Pack
description: Versionsinformation om Adobe Experience Manager 6.5 Service Pack 4.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82ded190d4fee4e4ef9849dc34372774c529844f

---


# Versionsinformation om Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | **Adobe Experience Manager 6.5** |
|---|---|
| Version | 6.5.4.0 |
| Typ | Service Pack-version |
| Date | 5 mars 2020 |
| Hämta URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), [Software Distribution(beta)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Vad ingår i Adobe Experience Manager 6.5.4.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat och prestanda, stabilitet, säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-utgåvan i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager (AEM) 6.5.

Några viktiga funktioner och förbättringar i AEM 6.5.4.0:

* AEM Assets har nu konfigurerats med en varumärkesportal via Adobe I/O Console.

* Ett nytt [genereringssteg för utskrift](../forms/using/aem-forms-workflow-step-reference.md) är nu tillgängligt för arbetsflöden i AEM Forms.

* [Flerkolumnsstöd](../forms/using/resize-using-layout-mode.md) för layoutläge för adaptiva formulär och interaktiv kommunikation.

* Stöd för [RTF](../forms/using/designing-form-template.md) i HTML5-formulär.

* Tillgänglighetsförbättringar i Assets.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.8.

En fullständig lista över funktioner, viktiga högdagrar, viktiga funktioner som introducerats i tidigare AEM 6.5-servicepaket finns i [Nyheter i Adobe Experience Manager 6.5 Service Pack 4](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* När en URL för en AEM Sites-sida innehåller ett kolon (: ) eller procentsymbol (%), svarar den underliggande webbläsaren inte och CPU-cyklerna uppvisar en topp (NPR-32369, NPR-31918).

* När en AEM Sites-sida öppnas för redigering och en komponent kopieras, är inklistringsåtgärden inte tillgänglig för vissa platshållare (NPR-32317).

* När guiden Hantera publikation öppnas visas inte ett Experience Fragment som är länkat till en Core-komponent i listorna med publicerade referenser (NPR-32233).

* Översikt över Live-kopian i Touch-gränssnittet tar mycket längre tid än det klassiska användargränssnittet att återge (NPR-32149).

* När servertid och maskintid är i olika tidszoner visar schemalagd publiceringstid servertid i Touch UI, medan datortid visas i Classic UI (NPR-32077).

* AEM Sites kan inte öppna en sida med ett suffix i URL:en (NPR-32072).

* När en användare redigerar ett innehållsfragment återställs en borttagen variant av innehållsfragmentet (NPR-32062).

* Användare kan spara ett innehållsfragment utan att lämna någon information i de obligatoriska fälten (NPR-31988).

* kernel.js och ui.js är inte i förväg ifyllda eller cachelagrade. Det leder till extra tid vid återgivning av sidor (NPR-31891).

* När PageEventAuditListener är aktiverat ökar längden på implementeringskön. Det påverkar prestandan för många verksamheter, t.ex. bulkpublicering, navigering och flyttning av bulktillgångar (NPR-31890).

* När Experience Fragments dras, observeras en hög responstid (NPR-31878).

* När du markerar alternativet Drag-komponenten här i platshållaren för ett responsivt rutnät, skickas en GET-begäran och begäran resulterar i HTTP 403-fel (NPR-31845).

* När du flyttar innehållet i samma mapp är alternativet för sidflyttning inaktiverat (NPR-31840).

* I strukturläget för redigerbara mallar visas felaktiga resultat i listan över tillåtna komponenter i layoutbehållaren. Endast komponenter med designdialogrutan visas i layoutbehållaren (NPR-31816).

* När en sida har skrivskyddad behörighet för en användare visas alternativet Öppna egenskaper i sites.html, men inte i editor.html (NPR-31770).

* När en användare klickar på knappen Skapa är sidalternativet inte tillgängligt (NPR-31756).

* Det går inte att synkronisera kampanjen i Adobe-kampanjen som innehåller OTB-designimportkomponenten (utanför rutan) (NPR-31728).

* När du försöker ändra en punktlista till en numrerad lista ändras bara de två första punkterna i listan (NPR-31636).

* När en sida inte har skapats och den underordnade noden har valts visas den inledande noden fortfarande i urvalsdialogrutan. När sidan har skapats och användaren klickar på Bläddra, dirigeras sidan om till rotnoden i stället för den redigerade noden (NPR-31618).

* Visningskonfigurationsdialogrutan fungerar inte som den ska för funktionen för anpassning av inkorgen (NPR-32503 och NPR-32492).

* Ett felmeddelande visas när arbetsflödesinformation visas med Inbox (CQ-4282168).

### Assets {#assets-6540-enhancements}

* Knappen som utlöser arbetsflödet på sidan för resurssamling är inaktiverad (NPR-32471).

* En mapp utan namn skapas i SPS (Scene7 Publishing System) när en resurs flyttas från en mapp till en annan i Experience Manager med Dynamic Media Scene7-konfiguration (NPR-32440).

* Åtgärden för att flytta alla resurser (med Markera alla och sedan flytta) till en mapp som innehåller publicerade resurser misslyckas med felet (NPR-32366).

* Återgivningsgenerering för resurser med ${extension} misslyckas (NPR-32294).

* Versionshistorik-URL:er visas under fältet Refererat av på egenskapssidan för resurser (NPR-31889).

* ZIP-filen som hämtas från DAM kan inte öppnas med WinZip (NPR-32293).

* Ursprungliga behörigheter för en mapp uppdateras när mappinställningar öppnas för att ändra mappens titel eller miniatyrbild och sedan sparas (NPR-32292).

* Kalenderikonen för den schemalagda aktiveringen visas inte i statuskolumnen (i Klassiskt användargränssnitt för DAM-tillgångslista) för resurser vars aktivering är schemalagd för ett senare datum och en senare tid (NPR-32291).

* När du skapar fragment med fragmentmallar uppstår ett fel när du söker efter samlingar när fragmentet skapas (NPR-32290).

* Flera sökfrågor utlöses när flera taggar väljs från sökfiltret (NPR-32143).

* Användargränssnittet i Experience Manager Assets visar trunkerade filnamn när resurser med fler än 50 tecken i filnamnet överförs (NPR-32054).

* Alla kryssrutor på panelen Filter avmarkeras när den första och den andra kryssrutan avmarkeras när du har markerat två kryssrutor i kryssruteträdet i Adobe Stock (NPR-31919).

* Filer- och mappsökning med Omnisearch-ansikten ger undantag (NPR-31872).

* Fältmarkering för obligatoriskt fältval i metadataredigeraren tas inte bort även efter att det obligatoriska fältet har markerats, när beroendereglerna har angetts i motsvarande metadatamatchformulär (NPR-31834).

* Fullständiga namn på taggar på lövnivå (från tagghierarkin) visas inte på egenskapssidan för resurser (NPR-31820).

* Om du använder kommandot back från objektets egenskapssida i webbläsaren Safari uppstår ett fel (NPR-31753).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Assets detail page of PDF assets does not show action buttons except To Collection and Add Rendition buttons in Experience Manager running mode on Dynamic Media Scene7 (CQ-4286705).

* Resurser större än 2 GB kan nu överföras i Dynamic Media-Scene7 (CQ-4286561).

* Resurserna tar för lång tid att bearbeta genom batchöverföringen i Scene7 (CQ-4286445).

* Knappen Spara importerar inte fjärruppsättningen när användaren inte har gjort några ändringar i Set Editor i Dynamic Media Client (CQ-4285690).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds har importerats till AEM (CQ-4283701).

* Den obearbetade statusen för visningsförinställningen för smart beskärning visas två gånger på banderolltexten bredvid förinställningsnamnet (CQ-4283517).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i 3D-visningsprogrammet visas på objektets informationssida (CQ-4283309).

* Carousel Editor öppnas inte i IE 11 i läget Dynamic Media Hybrid i Experience Manager (CQ-425590).

* Tangentbordsfokus fastnar i den nedrullningsbara menyn E-post i hämtningsdialogrutan i webbläsarna Chrome och Safari (NPR-32067).

* Kryssrutan Synkronisera allt innehåll är inte aktiverad som standard när du försöker lägga till DM-molnkonfiguration på AEM (CQ-4288533).

### Foundation UI {#foundation-ui-6540}

* Muskontrollen flyttas till föregående filterfält i stället för att finnas kvar i det befintliga filterfältet när resurser söks med hjälp av filterpanelen (NPR-32538).

* Plattformstaggning: Om du söker efter taggar genom att skriva i taggfälten visas taggar utanför rotgränserna och egenskapen för taggfält respekteras inte (NPR-31895). `rootPath`

* Plattformsgränssnitt: Webbläsaren för sökvägen bryts om en ogiltig sökväg läggs till i textfältet (NPR-31884).

* Meddelande döljs bakom en klistermeny vid sidval (NPR-31628).

### Platform {#platform-sling-6540}

* (HTL) Understrykningar ersätter kolon i sökvägsavsnittet i URL (NPR-32231).

### Projekt {#projects-6540}

* Knappen Skapa är inte synlig för användaren även om användaren har behörighet att skapa projekt i undermappen (NPR-31832).

### Projektöversättning {#projects-translation-6540}

* När ett översättningsprojekt skapas bryts gränssnittet när alternativet Trimma mellanslag aktiveras i `Apache Sling JSP Script Handler` (NPR-32154).

* Fel i användargränssnitt och Null-punktsundantag i felloggar observeras när en tagg, som ska översättas, läggs till i ett översättningsprojekt (NPR-31896).

### Integreringar {#integrations-6540}

* Generering av URL för startbibliotek baseras endast på `path` och `library_name` värden från API:t Launch och är inte baserat på `library_path` värde (NPR-31550).

* Ett felmeddelande visas när LiveFyre-relaterade objekt bearbetas (FYR-12420).

### WCM-mallredigerare {#wcm-template-editor-6540}

* I redigerbart mallstrukturläge visas inte länkknappskomponenten i listan över tillåtna komponenter i layoutbehållaren (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Det uppstod ett fel när en övertäckning skulle markeras och därefter när responsiva rutnätskomponenter skulle markeras här (CQ-4283342).

### Kampanjanpassning {#campaign-targeting-6540}

* Målmolnkonfigurationen misslyckades med felet när mbox-begäran skulle hämtas (CQ-4279880).

### Varumärkesportal {#assets-brand-portal}

* Värden för rullgardinsmenyer för metadatamatchning visas inte i resursegenskaper (CQ-4283287).

* Delschemat Metadata visar inte tabbar baserade på mimeType i resursegenskaper (CQ-4283288).

* Ett felmeddelande fylls i när metadatamatchemat avpubliceras, även om schemat tas bort vid backend.

* Förhandsvisningsbilden visas inte för en publicerad resurs (CQ-4285886).

* Användaren kan inte publicera eller avpublicera resurser som innehåller ett enkelt citattecken i namnet (CQ-4272686).

* Villkoren visas inte vid hämtning av flera resurser (CQ-4281224).

* Mindre säkerhetsluckor har åtgärdats.

### Communities {#communities}

* Formuläret Skapa medlem visas som en tom sida (NPR-31997).

* Användaren kan inte visa Analytics-rapporten för författarinstansen (NPR-30913).

### Oak-indexering och frågor {#oak-indexing-6540}

* MS Word- och MS Excel-dokument som innehåller JPEG-bilder kan inte tolkas när de tolkas med Tika-tolken, och fel som inte hittas av klassen observeras (NPR-31952).

### Formulär {#forms-6530}

>[!NOTE]
>
>AEM Service Pack innehåller inte korrigeringar för AEM Forms. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera tillägget](#install-aem-forms-add-on-package) AEM Forms och [Installera AEM Forms på JEE](#install-aem-forms-jee-installer).

* Korrespondenshantering: Bokstäverna visar extra tecken efter överföring för att bokföra processarbetsflöden (NPR-32626).

* Korrespondenshantering: Bokstäverna visar en nedrullningsbar platshållare som en textkomponent efter att de skickats in till arbetsflöden efter bearbetning (NPR-32539).

* Korrespondenshantering: Standardvärdena som definieras i brevmallen visas inte i förhandsvisningsläget (NPR-32511).

* Mobilformulär: Skicka-knappen visas som utökad när ett XDP-formulär återges i en HTML-version (NPR-32514).

* Dokumenttjänster: Problem med URL-åtkomst för brev och vissa andra sidor efter att Service Pack 2 har tillämpats (NPR-32508, NPR-32509).

* Dokumenttjänster: Om antalet transaktioner på en server överstiger en viss gräns misslyckas konverteringen från HTML till PDF och filtypsinställningarna tas bort från AEM Forms-servern (NPR-32204).

* Adaptiva former: Verktyget Webbläsartillgänglighet rapporterar fel i adaptiva formulär enligt riktlinjerna för WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Adaptiva former: Webbläsarhjälpmedelsverktyget i Chrome rapporterar ett fel med bästa praxis (NPR-32310).

* Adaptiva former: Översättningsproblem vid konfigurering av ett adaptivt formulär inbäddat på en AEM Sites-sida (NPR-32168).

* Workbench: Ett felmeddelande visas när åtgärden Hämta PDF-egenskaper används för tjänsten PDF Utilities (NPR-32150).

* Dokumentsäkerhet: En skyddad PDF-fil kan inte öppnas offline med alternativet DisableGlobalOfflineSynchronizationData inställt på True (NPR-32078).

* Designer: Om taggningsalternativet är aktiverat försvinner delformulärsramen i den genererade PDF-utdatafilen (NPR-32547, NPR-31983, NPR-31950).

* Designer: Om det finns sammanfogade celler i en tabell misslyckas hjälpmedelstestet för PDF-utdatafilen som konverterats från ett XDP-formulär med hjälp av utdatatjänsten (CQ-4285372).

* Foundation JEE: Om en AEM Forms-server är frånkopplad från ett kluster kan den inte återansluta till servern med hjälp av cachelagring (NPR-32412).

## Installera 6.5.4.0 {#install}

**Installationskrav**

* AEM 6.5.4.0 kräver AEM 6.5. Detaljerade instruktioner finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md) .
* Nedladdningen av Service Pack finns på Adobe Package Share, som du kommer åt direkt från AEM 6.5-instansen.
* På en distribution med MongoDB och flera instanser installerar du AEM 6.5.4.0 på en av Author-instanserna med hjälp av Package Manager.
* Innan du installerar Service Pack bör du kontrollera att du har en ögonblicksbild eller en ny säkerhetskopia av AEM-instansen.
* Starta om instansen innan du installerar den. Detta behövs bara när instansen fortfarande är i uppdateringsläge (och detta är fallet när instansen uppdaterades från en tidigare version), men vi rekommenderar att instansen körs under en längre period.

>[!CAUTION]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar AEM 6.5.4.0-paketet.

### Installera Service Pack via paketresurs {#install-service-pack-via-package-share}

Så här installerar du Service Pack på en befintlig AEM 6.5-instans:

1. Logga in på Package Share inifrån AEM eller direkt från webbläsaren och ladda ned [AEM 6.5.4.0-paketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0).

1. Installera det hämtade paketet med hjälp av Package Manager.

>[!NOTE]
>
>**Dialogrutan i användargränssnittet för Package Manager avslutas ibland felaktigt under installationen av 6.5.4.0**
>
>Därför rekommenderar vi att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till instansen. Användaren måste vänta på specifika loggar som rör avinstallation av uppdateringspaketet innan den kan vara säker på att installationen lyckas. Det händer vanligtvis på Safari, men kan hända i olika webbläsare.

**Automatisk installation**

Det finns två sätt att automatiskt installera AEM 6.5.4.0 i en instans som körs:

S. Placera paketet i ..*/crx-quickstart/install* -mappen när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API:t från Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - kontrollera att du använder cmd=install&amp;recursive=true - så att kapslade paket installeras.

>[!NOTE]
>
>AEM 6.5.4.0 stöder inte Bootstrap-installation.

**Validera installation**

1. På sidan Produktinformation (/system/console/ producto) visas den uppdaterade versionssträngen `Adobe Experience Manager, Version 6.5.4.0` under Installerade produkter.

1. Alla OSGi-paket är antingen **[!UICONTROL AKTIVA]** eller **[!UICONTROL FRAGMENT]** i OSGi-konsolen (använd webbkonsol: /system/console/bundles).
1. OSGI-paketet org.apache.jackrabbit.oak-core finns i version 1.10.6 eller senare (Använd webbkonsol: /system/console/bundles).

För att se vilka plattformar som är certifierade att köras med den här versionen, se de [tekniska kraven](/help/sites-deploying/technical-requirements.md).

### Installera AEM Forms-tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms. Korrigeringar i AEM Forms levereras via ett separat tilläggspaket.

>[!NOTE]
>
>AEM 6.5.4.0 innehåller en ny version av [AEM Forms-kompatibilitetspaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Om du använder en äldre version av AEM Forms-kompatibilitetspaketet och uppdaterar till AEM 6.5.4.0 installerar du den senaste versionen av AEM Forms-kompatibilitetspaketet efter installationen av Forms-tilläggspaketet.

1. Kontrollera att du har installerat AEM Service Pack.
1. Hämta motsvarande tilläggspaket för Forms som finns i [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms-tilläggspaketet enligt beskrivningen i [Installera AEM Forms-tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installera AEM Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i AEM Forms på JEE levereras via ett separat installationsprogram.

Information om hur du installerar det kumulativa installationsprogrammet för AEM Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen för korrigering 0011](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Installationsprogram för Workbench

Eftersom det är ett fullständigt installationsprogram är filstorleken större än korrigeringsversionen. Avinstallera den tidigare Workbench-versionen innan du installerar den nya.

### UberJar {#uber-jar}

UberJar för AEM 6.5.4.0 finns i [Adobe Public Maven-databasen](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

Om du vill använda UberJar i ett Maven-projekt kan du läsa artikeln [Så här använder du UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Föråldrade funktioner {#removed-deprecated-features}

I det här avsnittet listas funktioner som har markerats som borttagna i AEM 6.5.4.0. Funktioner som ska tas bort i en framtida version är först inaktuella, med ett alternativt alternativ att använda.

Kunderna rekommenderas att granska om de använder funktionen eller funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativa alternativet.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Inställningsskärmen för **[!UICONTROL AEM Cloud-tjänster]** har tagits bort. Med integreringen av AEM och Target uppdaterad i AEM 6.5 för att stödja Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera AEM-sidor för analys och personalisering, har Opt-In Wizard blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och Adobe I/O-integreringar via respektive AEM-molntjänster |

## Kända fel {#known-issues}

* Om konfigurationsguiden för **anslutna resurser** returnerar ett 404-felmeddelande efter installationen måste du manuellt installera om **cq-remotedam-client-ui-content** och **cq-remotedam-client-ui-components** -paketen med hjälp av Package Manager.
* Följande fel och varningsmeddelanden kan visas under installationen av AEM 6.5.x.x:
   * &quot;När Target-integreringen konfigureras i AEM med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källan&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källan&quot;Adobe Target Classic&quot;.
   * com.adobe.granite.Maintenance.impl.TaskScheduler: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används. CQ-4274424
   * com.adobe.granite.Maintenance.impl.TaskScheduler - Inga underhållsfönster hittades vid granit/operations/Maintenance.
   * Aktiveringspunkten i en Dynamic Media Interactive-bild syns inte när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar OSGi-paketen och innehållspaketen som ingår i AEM 6.5.4.0

Lista över OSGi-paket som ingår i AEM 6.5.4.0

[Hämta fil](assets/6540_bundles.txt)

Lista över innehållspaket som ingår i AEM 6.5.4.0

[Hämta fil](assets/6540_packages.txt)

## Begränsade platser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta kundsupport](https://daycare.day.com/public/contact.html)Mer information om hur du går till supportportalen finns i [Gå till supportportalen](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

>[!MORE SOM DET HÄR]
>
>* [Versionsinformation om AEM 6.5](/help/release-notes/release-notes.md)
>* [AEM - produktsida](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 - dokumentation](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Prenumerera på [Adobe Priority-produktuppdateringar](https://www.adobe.com/subscription/priority-product-update.html)

