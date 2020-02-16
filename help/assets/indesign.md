---
title: Integrera AEM-material med Adobe InDesign Server
description: Lär dig hur du integrerar AEM Assets med Adobe InDesign Server.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# Integrera AEM-material med Adobe InDesign Server {#integrating-aem-assets-with-indesign-server}

Adobe Experience Manager (AEM) Assets använder:

* En proxy som distribuerar inläsningen av vissa bearbetningsuppgifter. En proxy är en AEM-instans som kommunicerar med en proxyarbetare för att utföra en viss uppgift och andra AEM-instanser för att leverera resultaten.
* En proxyarbetare som definierar och hanterar en viss uppgift.
Dessa kan omfatta en mängd olika arbetsuppgifter. till exempel använda en InDesign Server för att bearbeta filer.

För att överföra filer till AEM Resurser som du har skapat med Adobe InDesign används en proxy. Detta använder en proxyarbetare för att kommunicera med Adobe InDesign Server, där [skript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) körs för att extrahera metadata och generera olika renderingar för AEM Assets. Proxyarbetaren möjliggör tvåvägskommunikation mellan InDesign Server och AEM-instansen/instanserna i en molnkonfiguration.

>[!NOTE]
>
>Adobe InDesign finns som två produkter:
>
>* [InDesign](https://www.adobe.com/products/indesign.html)
   >  På så sätt kan du designa sidlayouter för tryck och/eller digital distribution.
   >
   >
* [InDesign Server](https://www.adobe.com/products/indesignserver.html)
   >  Med den här motorn kan du programmässigt skapa automatiserade dokument baserat på vad du har skapat med InDesign. Den fungerar som en tjänst som erbjuder ett gränssnitt till sin [ExtendScript](https://www.adobe.com/devnet/scripting.html) -motor.
   >  Skripten skrivs i ExtendScript, som påminner om javascript. Mer information om InDesign-skript finns på [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).


## Hur extraheringen fungerar {#how-the-extraction-works}

Adobe InDesign Server kan integreras med AEM Assets så att INDD-filer som skapats med InDesign kan laddas upp, återgivningar genereras, alla media kan extraheras (till exempel video) och lagras som resurser:

>[!NOTE]
>
>Tidigare versioner av AEM kunde extrahera XMP och miniatyrbilden, nu kan alla media extraheras.

1. Överför din INDD-fil till AEM Resurser.
1. Ett ramverk skickar kommandoskript till InDesign Server via SOAP (Simple Object Access Protocol).
Detta kommandoskript kommer att:

   * Hämta INDD-filen.
   * Kör InDesign Server-kommandon:

      * Strukturen, texten och eventuella mediefiler extraheras.
      * PDF- och JPG-renderingar genereras.
      * HTML- och IDML-renderingar genereras.
   * Lägg tillbaka de resulterande filerna i AEM Resurser.
   >[!NOTE]
   >
   >IDML är ett XML-baserat format som återger allt innehåll i InDesign-filen. Den lagras som ett komprimerat paket med [ZIP](https://www.techterms.com/definition/zip) -komprimering. Mer information finns i [InDesign Interchange Formats INX och IDML](http://www.peachpit.com/articles/article.aspx?p=1381880&seqNum=8).

   >[!CAUTION]
   >
   >Om InDesign Server inte är installerad eller inte konfigurerad kan du ändå överföra en INDD-fil till AEM. De återgivningar som genereras är dock begränsade till PNG och JPEG. Du kommer inte att kunna generera HTML-, IDML- eller sidåtergivningar.

1. Efter extraheringen och renderingen:

   * Strukturen replikeras till en `cq:Page` (typ av återgivning).
   * Den extraherade texten och filerna lagras i AEM Resurser.
   * Alla återgivningar lagras i AEM Resurser, i själva resursen.

## Integrera InDesign Server med AEM {#integrating-the-indesign-server-with-aem}

Om du vill integrera InDesign Server för användning med AEM Assets och efter att du har konfigurerat din proxy måste du:

1. [Installera InDesign Server](#installing-the-indesign-server).
1. Om det behövs [konfigurerar du arbetsflödet](#configuring-the-aem-assets-workflow)för AEM Resurser.
Detta är bara nödvändigt om standardvärdena inte passar för din instans.
1. Konfigurera en [proxyarbetare för InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Installera InDesign Server {#installing-the-indesign-server}

Så här installerar och startar du InDesign Server för användning med AEM:

1. Hämta och installera Adobe InDesign Server.

1. Om det behövs kan du anpassa konfigurationen för InDesign Server-instansen.

1. Starta servern från kommandoraden:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Detta startar servern med SOAP-pluginprogrammet som lyssnar på port 8080. Alla loggmeddelanden och utdata skrivs direkt till kommandofönstret.

   >[!NOTE]
   >
   >Om du vill spara utdatameddelandena i en fil använder du omdirigering; under Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Konfigurera arbetsflödet för AEM Resurser {#configuring-the-aem-assets-workflow}

AEM Assets har ett förkonfigurerat arbetsflöde för **[!UICONTROL DAM Update Asset]**, som innehåller flera processsteg specifikt för InDesign:

* [Medieextrahering](#media-extraction)
* [Sidextrahering](#page-extraction)

Det här arbetsflödet är konfigurerat med standardvärden som kan anpassas för dina inställningar för de olika författarinstanserna (det här är ett standardarbetsflöde, så mer information finns under [Redigera ett arbetsflöde](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Om du använder standardvärdena (inklusive SOAP-porten) behövs ingen konfiguration.

Efter installationen utlöses det arbetsflöde som krävs för att bearbeta resursen och de olika återgivningarna när InDesign-filerna överförs till AEM Resurser (på något av de vanliga sätten). Testa konfigurationen genom att överföra en INDD-fil till AEM Resurser för att bekräfta att du ser de olika renderingar som skapas av IDS under `<*your_asset*>.indd/Renditions`

#### Medieextrahering {#media-extraction}

Det här steget styr extraheringen av media från INDD-filen.

Om du vill anpassa kan du redigera fliken **[!UICONTROL Argument]** i steget **[!UICONTROL Medieextrahering]** .

![Medieextraheringsargument och skriptsökvägar](assets/media_extraction_arguments_scripts.png)

Medieextraheringsargument och skriptsökvägar

* **ExtendScript library**: Detta är ett enkelt http get/post-metodbibliotek som krävs av de andra skripten.

* **Utöka skript**: Här kan du ange olika skriptkombinationer. Om du vill att dina egna skript ska köras på InDesign Server sparar du skripten på `/apps/settings/dam/indesign/scripts`.

Mer information om InDesign-skript finns i [dokumentationen för InDesign-utvecklare](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>Ändra inte ExtendScript-biblioteket. Det här biblioteket innehåller de HTTP-funktioner som krävs för att kommunicera med Sling. Den här inställningen anger vilket bibliotek som ska skickas till InDesign Server för användning där.

Skriptet som körs av arbetsflödessteget för medieextrahering genererar en miniatyrrendering i .jpg-format. `ThumbnailExport.jsx` Den här återgivningen används i arbetsflödet Bearbeta miniatyrbilder för att generera de statiska återgivningar som krävs av AEM.

Du kan konfigurera arbetsflödessteget Bearbeta miniatyrbilder för att generera statiska återgivningar i olika storlekar. Se till att du inte tar bort standardvärdena eftersom de krävs av användargränssnittet för AEM Resurser. Arbetsflödessteget Ta bort återgivning av bildförhandsvisning tar bort återgivningen av .jpg-miniatyrer eftersom den inte längre behövs.

#### Sidextrahering {#page-extraction}

Då skapas en AEM-sida av de extraherade elementen. En extraheringshanterare används för att extrahera data från en återgivning (för närvarande HTML eller IDML). Dessa data används sedan för att skapa en sida med PageBuilder.

Om du vill anpassa kan du redigera fliken **[!UICONTROL Argument]** i steget **[!UICONTROL Sidextrahering]** .

![chlimage_1-96](assets/chlimage_1-289.png)

* **Extraheringshanterare** för sida: Välj den hanterare som du vill använda i popup-listan. En extraheringshanterare fungerar på en viss återgivning som väljs av en relaterad `RenditionPicker` (se `ExtractionHandler` API:t). I en standard-AEM-installation är följande tillgängligt:
   * Extraheringshandtag för IDML-export: Används för den `IDML` återgivning som genereras i MediaExtract-steget.

* **Sidnamn**: Ange det namn som du vill tilldela den resulterande sidan. Om det lämnas tomt är namnet&quot;page&quot; (eller ett derivat om&quot;page&quot; redan finns).

* **Sidrubrik**: Ange den titel som du vill tilldela den resulterande sidan.

* **Sidrotsökväg**: Sökvägen till rotplatsen för den resulterande sidan. Om den lämnas tom används den nod som innehåller resursens återgivningar.

* **Sidmall**: Den mall som ska användas när den resulterande sidan genereras.

* **Siddesign**: Den siddesign som ska användas när den resulterande sidan genereras.

### Konfigurera proxyarbetaren för InDesign Server {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Arbetaren finns på proxyinstansen.

1. Expandera **[!UICONTROL Cloud Services Configurations]** i den vänstra rutan i verktygskonsolen. Expandera sedan **[!UICONTROL Cloud Proxy Configuration]**.

1. Dubbelklicka på den **[!UICONTROL IDS-arbetare]** som ska öppnas för konfiguration.

1. Klicka på **[!UICONTROL Redigera]** för att öppna konfigurationsdialogrutan och definiera de nödvändiga inställningarna:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS-pool** SOAP-slutpunkter som ska användas för kommunikation med InDesign Server. Du kan lägga till, ta bort och beställa objekt.

1. Spara genom att klicka på OK.

### Konfigurera Dag CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Om InDesign-servern och AEM körs på olika värdar eller något eller båda programmen inte körs på standardportar, konfigurerar du [!UICONTROL Day CQ Link Externalizer] för att ange värdnamn, port och innehållssökväg för InDesign-servern.

1. Gå till webbkonsolen på `https://[aem_server]:[port]/system/console/configMgr`.
1. Leta upp CQ Link Externalizer **[!UICONTROL för]** konfigurationsdagen och öppna den genom att trycka på **[!UICONTROL Redigera]** .
1. Ange värdnamnet och kontextsökvägen för InDesign-servern och klicka på **Spara**.

   ![chlimage_1-97](assets/chlimage_1-290.png)

### Aktivera parallell jobbbearbetning för InDesign-servrar {#enabling-parallel-job-processing-for-indesign-server-s}

Nu kan du aktivera parallell jobbbearbetning för IDS. Bestäm det maximala antalet parallella jobb (`x`) som en InDesign Server kan bearbeta:

* På en enda multiprocessordator är det maximala antalet parallella jobb (`x`) som en InDesign Server kan bearbeta ett mindre än antalet processorer som kör IDS.
* När du kör IDS på flera datorer måste du räkna antalet tillgängliga processorer (t.ex. på alla datorer) och sedan subtrahera det totala antalet datorer.

Så här konfigurerar du antalet parallella IDS-jobb:

1. Öppna fliken **[!UICONTROL Konfigurationer]** i Felix Console; till exempel: `https://[aem_server]:[port]/system/console/configMgr`.

1. Välj IDS-bearbetningskön under `Apache Sling Job Queue Configuration`.

1. Uppsättning:

   * **Typ** - `Parallel`
   * **Maximalt antal parallella jobb** - `<*x*>` (enligt beräkning ovan)

1. Spara dessa ändringar.
1. Om du vill aktivera stöd för flera sessioner för Adobe CS6 och senare markerar du `enable.multisession.name` kryssrutan under `com.day.cq.dam.ids.impl.IDSJobProcessor.name` konfiguration.
1. Skapa en [pool med `x` IDS-arbetare genom att lägga till SOAP-slutpunkter i IDS Worker-konfigurationen](#configuring-the-proxy-worker-for-indesign-server).

   Om det finns flera datorer som kör InDesign-servrar lägger du till SOAP-slutpunkter (antal processorer per dator -1) för varje dator.

   >[!NOTE]
   >
   >Du kan välja att aktivera svartlistning av IDS-arbetare när du arbetar med en grupp arbetare.
   >
   >
   >Om du vill göra det aktiverar du kryssrutan **[!UICONTROL enable.retry.name]** under `com.day.cq.dam.ids.impl.IDSJobProcessor.name` konfigurationen, vilket aktiverar omprövningar av IDS-jobb.
   >
   >
   >Under `com.day.cq.dam.ids.impl.IDSPoolImpl.name` konfigurationen anger du också ett positivt värde för `max.errors.to.blacklist` parameter som avgör antalet jobbomprövningar innan du tar bort ett ID från jobbhanterarlistan.
   >
   >
   >Som standard valideras IDS-arbetaren efter den konfigurerbara tiden (retry.interval.to.whitelist.name) i minuter. Om arbetaren hittas online tas den bort från svartlistan.

## Aktivera stöd för InDesign Server 10.0 eller senare {#enabling-support-for-indesign-server-or-later}

För InDesign Server 10.0 eller senare utför du följande steg för att aktivera stöd för flera sessioner.

1. Öppna Configuration Manager från din AEM Resurser-instans `https://[aem_server]:[port]/system/console/configMgr`.
1. Redigera konfigurationen `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Välj **[!UICONTROL alternativet ids.cc.enable]** och klicka på **[!UICONTROL Spara]**.

>[!NOTE]
>
>För InDesign Server-integrering med AEM Assets kan du använda en processor med flera kärnor eftersom den sessionsstödfunktion som krävs för integreringen inte stöds på enskilda kärnsystem.

## Konfigurera AEM-autentiseringsuppgifter {#configure-aem-credentials}

Du kan ändra administratörens standardautentiseringsuppgifter (användarnamn och lösenord) för att komma åt InDesign-servern från din AEM-instans utan att integreringen med InDesign-servern avbryts.

1. Gå till `/etc/cloudservices/proxy.html`.
1. Ange det nya användarnamnet och lösenordet i dialogrutan.
1. Spara inloggningsuppgifterna.

>[!MORELIKETHIS]
>
>* [Om Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

