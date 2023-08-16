---
title: Konfigurerar OSGi
seo-title: Configuring OSGi
description: OSGi är en grundläggande del i Adobe Experience Manager (AEM) teknikstack. Det används för att styra de sammansatta AEM och deras konfiguration. I den här artikeln beskrivs hur du kan hantera konfigurationsinställningarna för sådana paket.
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Konfigurerar OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) är en grundläggande del i Adobe Experience Manager (AEM) teknikstack. Det används för att styra de sammansatta AEM och deras konfiguration.

OSGi &quot;*innehåller standardmallar som gör det möjligt att konstruera program utifrån små, återanvändbara och samverkansbaserade komponenter. Dessa komponenter kan sammanställas i ett program och distribueras*&quot;.

På så sätt blir det enkelt att hantera paket när de kan stoppas, installeras och startas individuellt. De inbördes beroendena hanteras automatiskt. Varje OSGi-komponent (se [OSGi-specifikation](https://docs.osgi.org/specification/)) finns i ett av de olika paketen.

Du kan hantera konfigurationsinställningarna för sådana paket genom att antingen:

* med [Adobe CQ webbkonsol](#osgi-configuration-with-the-web-console)
* använda [konfigurationsfiler](#osgi-configuration-with-configuration-files)
* konfigurera [content-nodes ( `sling:OsgiConfig`) i databasen](#osgi-configuration-in-the-repository)

Båda metoderna kan användas trots att det finns små skillnader, främst i relation till [Körningslägen](/help/sites-deploying/configure-runmodes.md):

* [Adobe CQ webbkonsol](#osgi-configuration-with-the-web-console)

   * Webbkonsolen är standardgränssnittet för OSGi-konfiguration. Det innehåller ett användargränssnitt för redigering av de olika egenskaperna, där möjliga värden kan väljas från fördefinierade listor.

     Det är därför den enklaste metoden.

   * Alla konfigurationer som görs med webbkonsolen tillämpas omedelbart och tillämpas på den aktuella instansen, oavsett aktuellt körningsläge eller eventuella efterföljande ändringar av körningsläget.

* [konfigurationsfiler](#osgi-configuration-with-configuration-files)

   * Innehåller inställningar som är definierade i webbkonsolen.
   * Kan inkluderas i innehållspaket för användning i andra instanser.

* [content-nodes (sling:osgiConfig) i databasen](#osgi-configuration-in-the-repository)

   * Kräver manuell konfiguration med CRXDE Lite.
   * På grund av namngivningskonventionerna för `sling:OsgiConfig` -noder kan du koppla konfigurationen till en viss [körningsläge](/help/sites-deploying/configure-runmodes.md). Du kan även spara konfigurationer för mer än ett körningsläge i samma databas.
   * Alla lämpliga konfigurationer används omedelbart (beroende på körningsläget).

Alla dessa konfigurationsmetoder, oavsett vilken metod du använder:

* Kontrollera att identiska konfigurationer återskapas när du kopierar eller replikerar databasinnehållet.
* Gör att du kan checka ut konfigurationer till FileVault eller Subversion, antingen av säkerhetsskäl eller för ytterligare uppdateringar.
* Kan sparas i paket som kan användas när du konfigurerar andra instanser.
* Gör att du kan utföra konfigurationsimplementeringar med skript för att sprida konfigurationsinformationen.

>[!NOTE]
>
>Information om vissa viktiga inställningar finns i listan under [Konfigurationsinställningar för OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## OSGi-konfiguration med webbkonsolen {#osgi-configuration-with-the-web-console}

The [Webbkonsol](/help/sites-deploying/web-console.md) i AEM tillhandahåller ett standardiserat gränssnitt för att konfigurera paketen. The **Konfiguration** -fliken används för att konfigurera OSGi-paket och är därför den underliggande mekanismen för att konfigurera AEM systemparametrar.

Alla ändringar som görs tillämpas omedelbart på den aktuella OSGi-konfigurationen, ingen omstart krävs.

>[!NOTE]
>
>Ändringar som görs i webbkonsolen sparas i databasen som [konfigurationsfiler](#osgi-configuration-with-configuration-files). Dessa filer kan inkluderas i innehållspaket för återanvändning i andra installationer.

>[!NOTE]
>
>På webbkonsolen gäller alla beskrivningar som anger standardinställningar för Sling.
>
>Adobe Experience Manager har sina egna standardinställningar, så de standardvärden som är angivna kan skilja sig från standardvärdena som är dokumenterade på konsolen.

Så här uppdaterar du en konfiguration med webbkonsolen:

1. Öppna **Konfiguration** fliken Web Console av antingen:

   * Öppna webbkonsolen från länken på panelen **Verktyg -> Åtgärder** -menyn. När du har loggat in på konsolen kan du använda den nedrullningsbara menyn i:

     **OSGi >**

   * Den direkta URL:en, till exempel:

     `http://localhost:4502/system/console/configMgr`

   En lista visas.

1. Välj det paket som du vill konfigurera av:

   * klicka på **Redigera** ikon för paketet
   * klicka på **Namn** i paketet

1. En dialogruta öppnas. Här kan du redigera efter behov. Ange till exempel **Loggnivå** till `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Uppdateringar sparas i databasen som [konfigurationsfiler](#osgi-configuration-with-configuration-files). Om du vill söka efter de här filerna efteråt och inkludera dem i ett innehållspaket för användning i en annan instans, till exempel, ska du göra en anteckning om den beständiga identiteten ( `PID`).

1. Klicka **Spara**.

   Ändringarna tillämpas omedelbart på den aktuella OSGi-konfigurationen för det system som körs, ingen omstart krävs.

   >[!NOTE]
   >
   >Du kan nu hitta den relaterade [konfigurationsfiler](#osgi-configuration-with-configuration-files). Om du till exempel vill inkludera innehåll i ett innehållspaket som ska användas på en annan instans.

## OSGi-konfiguration med konfigurationsfiler {#osgi-configuration-with-configuration-files}

Konfigurationsändringar som görs med webbkonsolen sparas i databasen som konfigurationsfiler ( `.config`) under:

`/apps`

Dessa filer kan inkluderas i innehållspaket och återanvändas i andra instanser.

>[!NOTE]
>
>Konfigurationsfilernas format är specifikt - se Sling Apache-dokumentationen för:
>* fullständig information om [Apache Sling Provisioning Model och Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* självstudiekurser och exempel [Hämta resurser och egenskaper i Sling](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>Därför rekommenderar vi att du skapar och underhåller konfigurationsfilen genom att göra faktiska ändringar i webbkonsolen.

Webbkonsolen visar ingen indikation på var i databasen dina ändringar har sparats, men de kan enkelt hittas:

1. Skapa konfigurationsfilen genom att [göra en första ändring i webbkonsolen](#osgi-configuration-with-the-web-console).
1. Öppna CRXDE Lite.
1. I **verktyg** meny, välja **Fråga ...** .
1. Om du vill söka efter PID för konfigurationen som du har uppdaterat skickar du en fråga till **Typ** `SQL`.

   Till exempel: **Apache Felix OSGi Management Console** har den beständiga identiteten (PID) för:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Så SQL-frågan kan vara:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Konfigurationsfilsnoden visas.

   I exemplet ovan:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Du kan öppna den här filen om du vill visa ändringarna, men för att undvika att skriva fel rekommenderar vi att du gör faktiska ändringar i konsolen.

1. Du kan nu skapa ett innehållspaket som innehåller den här noden och använda det som behövs på dina andra instanser.

## OSGi-konfiguration i databasen {#osgi-configuration-in-the-repository}

Förutom att använda webbkonsolen kan du även definiera konfigurationsinformation i databasen. På så sätt kan du enkelt konfigurera olika körningslägen.

Dessa konfigurationer skapas genom att skapa `sling:OsgiConfig` noder i databasen som systemet ska referera till. De här noderna speglar OSGi-konfigurationerna och ett användargränssnitt har skapats för dem. Om du vill uppdatera konfigurationsdata uppdaterar du nodegenskaperna.

Om du ändrar konfigurationsdata i databasen tillämpas ändringarna omedelbart på den aktuella OSGi-konfigurationen. Det är som om ändringarna gjorts med webbkonsolen, med lämplig validering och konsekvenskontroll. Det här arbetsflödet gäller även kopiering av en konfiguration från `/libs/` till `/apps/`.

Eftersom samma konfigurationsparameter finns på flera ställen:

* söker efter alla noder av typen `sling:OsgiConfig`
* filter efter tjänstnamn
* filter enligt körningsläge

>[!NOTE]
>
>Läs även [definiera en databasbaserad konfiguration för en specifik instans](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=en).

### Lägga till en ny konfiguration i databasen {#adding-a-new-configuration-to-the-repository}

#### Vad du behöver veta {#what-you-need-to-know}

Om du vill lägga till en konfiguration i databasen måste du känna till följande:

1. The **Beständig identitet** (PID) för tjänsten.

   Referera till **Konfigurationer** i webbkonsolen. Namnet visas inom parentes efter paketnamnet (eller i **Konfigurationsinformation** längst ned på sidan).

   Skapa till exempel en nod `com.day.cq.wcm.core.impl.VersionManagerImpl.` konfigurera **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Är en specifik [körningsläge](/help/sites-deploying/configure-runmodes.md) krävs? Skapa mappen:

   * `config` - för alla körningslägen
   * `config.author` - för redigeringsmiljön
   * `config.publish` - för publiceringsmiljön
   * `config.<run-mode>` - i förekommande fall

1. Är en **Konfiguration** eller **Fabrikskonfiguration** är nödvändigt?
1. De enskilda parametrar som ska konfigureras, inklusive befintliga parameterdefinitioner som måste återskapas.

   Referera till det enskilda parameterfältet i webbkonsolen. Namnet visas inom hakparenteser för varje parameter.

   Skapa till exempel en egenskap
   `versionmanager.createVersionOnActivation` konfigurera **Skapa version vid aktivering**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Finns det en konfiguration i `/libs`? Använd kommandot **Fråga** i CRXDE Lite för att skicka följande SQL-fråga:

   `select * from sling:OsgiConfig`

   I så fall kan konfigurationen kopieras till ` /apps/<yourProject>/`och sedan anpassats på den nya platsen.

#### Skapa konfigurationen i databasen {#creating-the-configuration-in-the-repository}

Så här lägger du till den nya konfigurationen i databasen:

1. Använd CRXDE Lite för att navigera till:

   ` /apps/<yourProject>`

1. Om den inte finns skapar du `config` mapp ( `sling:Folder`):

   * `config` - gäller för alla körlägen
   * `config.<run-mode>` - specifikt för ett visst körläge

1. Skapa en nod under den här mappen:

   * Typ: `sling:OsgiConfig`
   * Namn: den beständiga identiteten (PID).

     till exempel AEM WCM Version Manager använder `com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >När du skapar ett fabrikskonfiguration `-<identifier>` till namnet.
   >
   >Som i: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Plats `<identifier>` ersätts med fri text som du (måste) anger för att identifiera instansen (du kan inte utelämna den här informationen), till exempel:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Skapa en egenskap på den här noden för varje parameter som du vill konfigurera:

   * Namn: parameternamnet som visas i webbkonsolen. Namnet visas inom hakparenteser i slutet av fältbeskrivningen. Till exempel `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * Typ: efter behov.
   * Värde: efter behov.

   Du behöver bara skapa egenskaper för de parametrar som du vill konfigurera, medan andra fortfarande använder standardvärdena enligt AEM.

1. Spara alla ändringar.

   Ändringarna tillämpas när noden uppdateras genom att tjänsten startas om (som med ändringarna i webbkonsolen).

>[!CAUTION]
>
>Ändra ingenting i dialogrutan `/libs` bana.

>[!CAUTION]
>
>Den fullständiga sökvägen till en konfiguration måste vara korrekt för att den ska kunna läsas vid start.

## Konfigurationsinformation {#configuration-details}

### Upplösningsordning vid start {#resolution-order-at-startup}

Följande prioritetsordning används:

1. Databasnoder under `/apps/*/config...`antingen med text `sling:OsgiConfig` eller egenskapsfiler.

1. Databasnoder med typ `sling:OsgiConfig` under `/libs/*/config...`. (färdiga definitioner).

1. Alla `.config` filer från `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. i det lokala filsystemet.

En allmän konfiguration i `/libs` kan maskeras av en projektspecifik konfiguration i `/apps`.

### Upplösningsordning vid körning {#resolution-order-at-runtime}

Konfigurationsändringar som görs medan systemet körs utlöser en omladdning med den ändrade konfigurationen.

Sedan gäller följande prioritetsordning:

1. När du ändrar en konfiguration i webbkonsolen börjar det gälla direkt när det gäller körning.
1. Ändra en konfiguration i `/apps` börjar gälla omedelbart.
1. Ändra en konfiguration i `/libs` börjar gälla omedelbart, såvida det inte maskeras av en konfiguration i `/apps`.

### Upplösning för flera körningslägen {#resolution-of-multiple-run-modes}

För körningslägesspecifika konfigurationer kan flera körningslägen kombineras. Du kan till exempel skapa konfigurationsmappar med följande format:

`/apps/*/config.<runmode1>.<runmode2>/`

Konfigurationer i sådana mappar används om alla körningslägen matchar ett körningsläge som har definierats vid start.

Om en instans till exempel startades med körningslägena `author,dev,emea`, konfigurationsnoder i `/apps/*/config.emea`, `/apps/*/config.author.dev/`och `/apps/*/config.author.emea.dev/` används, medan konfigurationsnoder i `/apps/*/config.author.asean/` och `/config/author.dev.emea.noldap/` används inte.

Om flera konfigurationer för samma PID kan användas, används konfigurationen med det högsta antalet matchande körningslägen.

Om en instans till exempel startades med körningslägena `author,dev,emea`och både `/apps/*/config.author/` och `/apps/*/config.emea.author/` definiera en konfiguration för
`com.day.cq.wcm.core.impl.VersionManagerImpl`, konfigurationen i `/apps/*/config.emea.author/` används.

Regelns granularitet är på PID-nivå.
Du kan inte definiera vissa egenskaper för samma PID i `/apps/*/config.author/` och mer specifika `/apps/*/config.emea.author/` för samma PID.
Konfigurationen med det högsta antalet matchande körningslägen gäller för hela PID.

### Standardkonfigurationer {#standard-configurations}

I följande lista visas ett litet urval av de konfigurationer som är tillgängliga (i en standardinstallation) i databasen:

* Författare - AEM WCM-filter:

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publicera - AEM WCM-filter:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publicera - AEM WCM-sidstatistik:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>När dessa konfigurationer finns i `/libs` de får inte redigeras direkt, utan kopieras till programområdet ( `/apps`) före anpassning.

Använd knappen **Fråga** i CRXDE Lite för att skicka följande SQL-fråga:

`select * from sling:OsgiConfig`

### Konfigurationsbeständighet {#configuration-persistence}

* Om du ändrar en konfiguration via webbkonsolen skrivs den (vanligtvis) in i databasen på:

  `/apps/{somewhere}`

   * Som standard `{somewhere}` är `system/config` så att konfigurationen skrivs till

     `/apps/system/config`

   * Om du redigerar en konfiguration som ursprungligen kom från en annan plats i databasen: till exempel:

     /libs/foo/config/someconfig

     Den uppdaterade konfigurationen skrivs sedan under den ursprungliga platsen, till exempel:

     `/apps/foo/config/someconfig`

* Inställningar som ändrats av `admin` sparas i `*.config` filer under:

  ```
     /crx-quickstart/launchpad/config
  ```

   * Det här området är privata data för OSGi-konfigurationsadministratören och innehåller all konfigurationsinformation som anges av `admin`, oavsett hur de gick in i systemet.
   * Det här området är en implementeringsdetalj och du får aldrig redigera den här katalogen direkt.
   * Det är emellertid användbart att veta var dessa konfigurationsfiler finns så att kopior kan tas för säkerhetskopiering, eller för flera installationer, eller både och:

      * Apache Felix OSGi Management Console

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling Client Repository

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Redigera aldrig mappar eller filer under:
>
>`/crx-quickstart/launchpad/config`
