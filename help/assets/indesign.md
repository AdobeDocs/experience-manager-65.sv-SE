---
title: Integrera [!DNL Assets] med [!DNL InDesign Server]
description: Integrera [!DNL Adobe Experience Manager Assets] med [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---

# Integrera [!DNL Adobe Experience Manager Assets] med [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] använder:

* En proxy som distribuerar inläsningen av vissa bearbetningsuppgifter. En proxy är en [!DNL Experience Manager] instans som kommunicerar med en proxyarbetare för att utföra en viss uppgift, och andra [!DNL Experience Manager] -instanser för att leverera resultaten.
* En proxyarbetare som definierar och hanterar en viss uppgift.
Dessa kan omfatta en mängd olika uppgifter, till exempel med hjälp av en [!DNL InDesign Server] för att bearbeta filer.

Så här överför du filer till [!DNL Experience Manager Assets] som du har skapat med [!DNL Adobe InDesign] en proxy används. Detta använder en proxyarbetare för att kommunicera med [!DNL Adobe InDesign Server], där [skript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) körs för att extrahera metadata och generera olika renderingar för [!DNL Experience Manager Assets]. Proxyarbetaren möjliggör tvåvägskommunikation mellan [!DNL InDesign Server] och [!DNL Experience Manager] instanser i en molnkonfiguration.

>[!NOTE]
>
>[!DNL Adobe InDesign] erbjuds som två separata erbjudanden. [Adobe InDesign](https://www.adobe.com/products/indesign.html) datorprogram som används för att utforma sidlayouter för tryck och digital distribution. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) gör att du kan skapa automatiska dokument baserat på vad du har skapat med [!DNL InDesign]. Den fungerar som en tjänst som erbjuder ett gränssnitt till dess [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Skripten skrivs i [!DNL ExtendScript], som liknar [!DNL JavaScript]. Mer information om [!DNL InDesign] skript se [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Hur extraheringen fungerar {#how-the-extraction-works}

The [!DNL Adobe InDesign Server] kan integreras med [!DNL Experience Manager Assets] så att INDD-filer skapas med [!DNL InDesign] kan överföras, återgivningar genereras, alla media extraheras (till exempel video) och lagras som resurser:

>[!NOTE]
>
>Tidigare versioner av [!DNL Experience Manager] kunde extrahera XMP och miniatyrbilden, nu kan alla media extraheras.

1. Överför INDD-filen till [!DNL Experience Manager Assets].
1. Ett ramverk skickar kommandoskript till [!DNL InDesign Server] via SOAP (Simple Object Access Protocol)
Detta kommandoskript kommer att:

   * Hämta INDD-filen.
   * Kör [!DNL InDesign Server] kommandon:

      * Strukturen, texten och eventuella mediefiler extraheras.
      * PDF och JPG genereras.
      * HTML och IDML-renderingar genereras.

   * Lägg tillbaka de resulterande filerna i [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML är ett XML-baserat format som återger allt innehåll i [!DNL InDesign] -fil. Det lagras som ett komprimerat paket med [ZIP](https://www.techterms.com/definition/zip) komprimering. Mer information finns i [InDesign Interchange Formats INX and IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Om [!DNL InDesign Server] är inte installerat eller inte konfigurerat kan du ändå överföra en INDD-fil till [!DNL Experience Manager]. De återgivningar som skapas är dock begränsade till PNG och JPEG. Du kommer inte att kunna generera HTML, IDML eller sidåtergivningarna.

1. Efter extraheringen och renderingen:

   * Strukturen replikeras till en `cq:Page` (typ av återgivning).
   * Den extraherade texten och filerna lagras i [!DNL Experience Manager Assets].
   * Alla återgivningar lagras i [!DNL Experience Manager Assets], i själva tillgången.

## Integrera [!DNL InDesign Server] med Experience Manager {#integrating-the-indesign-server-with-aem}

Integrera [!DNL InDesign Server] för användning med [!DNL Experience Manager Assets] När du har konfigurerat proxyn måste du:

1. [Installera InDesignen Server](#installing-the-indesign-server).
1. Vid behov, [konfigurera Experience Manager Assets Workflow](#configuring-the-aem-assets-workflow).
Detta är bara nödvändigt om standardvärdena inte passar för din instans.
1. Konfigurera en [proxyarbetare för InDesignen Server](#configuring-the-proxy-worker-for-indesign-server).

### Installera [!DNL InDesign Server] {#installing-the-indesign-server}

Installera och starta [!DNL InDesign Server] för användning med [!DNL Experience Manager]:

1. Hämta och installera [!DNL InDesign Server].

1. Om det behövs kan du anpassa konfigurationen av [!DNL InDesign Server] -instans.

1. Starta servern från kommandoraden:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Detta startar servern med SOAP-pluginprogrammet som lyssnar på port 8080. Alla loggmeddelanden och utdata skrivs direkt till kommandofönstret.

   >[!NOTE]
   >
   >Om du vill spara utdatameddelandena i en fil använder du omdirigering, till exempel under Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Konfigurera [!DNL Experience Manager Assets] arbetsflöde {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] har ett förkonfigurerat arbetsflöde **[!UICONTROL DAM Update Asset]**, som har flera steg specifikt för [!DNL InDesign]:

* [Medieextrahering](#media-extraction)
* [Sidextrahering](#page-extraction)

Det här arbetsflödet är konfigurerat med standardvärden som kan anpassas för dina inställningar för de olika författarinstanserna (det här är ett standardarbetsflöde, så mer information finns under [Redigera ett arbetsflöde](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Om du använder standardvärdena (inklusive SOAP-porten) behövs ingen konfiguration.

Överför efter installationen [!DNL InDesign] filer i [!DNL Experience Manager Assets] (med någon av de vanliga metoderna) utlöser arbetsflödet för att bearbeta resursen och förbereda de olika återgivningarna. Testa konfigurationen genom att överföra en INDD-fil till [!DNL Experience Manager Assets] för att bekräfta att du ser de olika renderingar som har skapats av IDS under `<*your_asset*>.indd/Renditions`

#### Medieextrahering {#media-extraction}

Det här steget styr extraheringen av media från INDD-filen.

Om du vill anpassa kan du redigera **[!UICONTROL Arguments]** -fliken i **[!UICONTROL Media Extraction]** steg.

![Medieextraheringsargument och skriptsökvägar](assets/media_extraction_arguments_scripts.png)

Medieextraheringsargument och skriptsökvägar

* **ExtendScript-bibliotek**: Detta är ett enkelt http get/post-metodbibliotek som krävs av de andra skripten.

* **Utöka skript**: Du kan ange olika skriptkombinationer här. Om du vill att dina egna skript ska köras på [!DNL InDesign Server], spara skripten på `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Ändra inte ExtendScript-biblioteket. Det här biblioteket innehåller de HTTP-funktioner som krävs för att kommunicera med Sling. Den här inställningen anger vilket bibliotek som ska skickas till [!DNL InDesign Server] för användning där.

The `ThumbnailExport.jsx` skript som körs i arbetsflödessteget för medieextrahering genererar en miniatyrrendering i JPG-format. Den här återgivningen används i arbetsflödessteget Bearbeta miniatyrbilder för att generera de statiska återgivningar som krävs av [!DNL Experience Manager].

Du kan konfigurera arbetsflödessteget Bearbeta miniatyrbilder för att generera statiska återgivningar i olika storlekar. Se till att du inte tar bort standardinställningarna eftersom de krävs av [!DNL Experience Manager Assets] gränssnitt. Arbetsflödet för att ta bort återgivning för förhandsvisning av bilder tar slutligen bort återgivningen av miniatyrbilder i JPG eftersom den inte längre behövs.

#### Sidextrahering {#page-extraction}

Detta skapar en [!DNL Experience Manager] sida från de extraherade elementen. En extraheringshanterare används för att extrahera data från en återgivning (för närvarande HTML eller IDML). Dessa data används sedan för att skapa en sida med PageBuilder.

Om du vill anpassa kan du redigera **[!UICONTROL Arguments]** -fliken i **[!UICONTROL Page Extraction]** steg.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Extraheringshanterare**: Välj den hanterare som du vill använda i popup-listan. En extraheringshanterare fungerar på en viss återgivning, som väljs av en relaterad `RenditionPicker` (se `ExtractionHandler` API). I en standard [!DNL Experience Manager] installation av följande finns:
   * Extraheringshandtag för IDML-export: Fungerar på `IDML` återgivning genererad i MediaExtract-steget.

* **Sidnamn**: Ange det namn som du vill ska tilldelas till den resulterande sidan. Om det lämnas tomt är namnet&quot;page&quot; (eller ett derivat om&quot;page&quot; redan finns).

* **Sidrubrik**: Ange den titel som du vill tilldela den resulterande sidan.

* **Sidrotsökväg**: Sökvägen till rotplatsen för den resulterande sidan. Om den lämnas tom används noden med resursens återgivningar.

* **Sidmall**: Den mall som ska användas när den resulterande sidan genereras.

* **Siddesign**: Den siddesign som ska användas när den resulterande sidan genereras.

### Konfigurera proxyarbetaren för [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Arbetaren finns på proxyinstansen.

1. Expandera i verktygskonsolen **[!UICONTROL Cloud Services Configurations]** i den vänstra rutan. Expandera **[!UICONTROL Cloud Proxy Configuration]**.

1. Dubbelklicka på **[!UICONTROL IDS worker]** för att öppna för konfiguration.

1. Klicka **[!UICONTROL Edit]** för att öppna konfigurationsdialogrutan och definiera de nödvändiga inställningarna:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS-pool**
SOAP-slutpunkterna som ska användas för kommunikation med [!DNL InDesign Server]. Du kan lägga till, ta bort och beställa objekt.

1. Spara genom att klicka på OK.

### Konfigurera Dag CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Om [!DNL InDesign Server] och [!DNL Experience Manager] finns på olika värdar eller ett eller båda av dessa program fungerar inte på standardportar, konfigurera [!UICONTROL Day CQ Link Externalizer] för att ange värdnamn, port och innehållssökväg för [!DNL InDesign Server].

1. Gå till webbkonsolen på `https://[aem_server]:[port]/system/console/configMgr`.
1. Leta reda på konfigurationen **[!UICONTROL Day CQ Link Externalizer]**. Klicka **[!UICONTROL Edit]** att öppna.
1. Inställningarna för länkutjämnaren hjälper dig att skapa absoluta URL:er för [!DNL Experience Manager] driftsättning och [!DNL InDesign Server]. Använd **[!UICONTROL Domains]** fält för att ange värdnamnet för [!DNL Adobe InDesign Server]. Klicka **Spara**.

   Använd i absoluta URL:er `localhost` som värdnamn för den lokala (författare) instansen och värdnamn eller IP-adress för publiceringsinstansen enligt följande bild.

   ![Inställning för extern länkning](assets/link-externalizer-config.png)

### Aktivera parallell jobbbearbetning för [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Nu kan du aktivera parallell jobbbearbetning för IDS. Bestäm det maximala antalet parallella jobb (`x`) och [!DNL InDesign Server] kan bearbeta:

* På en multiprocessordator är det maximala antalet parallella jobb (`x`) som [!DNL InDesign Server] kan bearbeta är ett mindre än antalet processorer som kör IDS.
* När du kör IDS på flera datorer måste du räkna antalet tillgängliga processorer (t.ex. på alla datorer) och sedan subtrahera det totala antalet datorer.

Så här konfigurerar du antalet parallella IDS-jobb:

1. Öppna **[!UICONTROL Configurations]** fliken Felix Console, till exempel: `https://[aem_server]:[port]/system/console/configMgr`.

1. Välj IDS-bearbetningskön under `Apache Sling Job Queue Configuration`.

1. Uppsättning:

   * **Typ** - `Parallel`
   * **Maximalt antal parallella jobb** - `<*x*>` (enligt beräkning ovan)

1. Spara dessa ändringar.
1. Om du vill aktivera stöd för flera sessioner i Adobe CS6 och senare bör du kontrollera `enable.multisession.name` kryssruta, under `com.day.cq.dam.ids.impl.IDSJobProcessor.name` konfiguration.
1. Skapa en [pool med `x` IDS-arbetare genom att lägga till SOAP-slutpunkter i IDS Worker-konfigurationen](#configuring-the-proxy-worker-for-indesign-server).

   Om flera datorer körs [!DNL InDesign Server]lägger du till SOAP-slutpunkter (antal processorer per dator -1) för varje dator.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>När du arbetar med en grupp arbetare kan du aktivera blockeringslista för IDS-arbetare.
>
>Aktivera **[!UICONTROL enable.retry.name]** kryssruta, under `com.day.cq.dam.ids.impl.IDSJobProcessor.name` konfiguration, vilket möjliggör omprövningar av IDS-jobb.
>
>Under `com.day.cq.dam.ids.impl.IDSPoolImpl.name` konfiguration, ange ett positivt värde för `max.errors.to.blacklist` parameter som bestämmer antalet jobbomprövningar innan ett ID tas bort från jobbarbetslistan.
>
>Som standard, efter den konfigurerbara`retry.interval.to.whitelist.name`) tid i minuter som IDS-arbetaren valideras. Om arbetaren hittas online tas den bort från blockeringslista.

## Aktivera stöd för [!DNL InDesign Server] 10.0 eller senare {#enabling-support-for-indesign-server-or-later}

För [!DNL InDesign Server] 10.0 eller senare utför du följande steg för att aktivera stöd för flera sessioner.

1. Öppna Configuration Manager från din [!DNL Experience Manager Assets] instance `https://[aem_server]:[port]/system/console/configMgr`.
1. Redigera konfigurationen `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Välj **[!UICONTROL ids.cc.enable]** och klicka på **[!UICONTROL Save]**.

>[!NOTE]
>
>För [!DNL InDesign Server] integrering med [!DNL Experience Manager Assets]använder du en flerkärnig processor eftersom den sessionsstödfunktion som krävs för integreringen inte stöds på enskilda kärnsystem.

## Konfigurera [!DNL Experience Manager] autentiseringsuppgifter {#configure-aem-credentials}

Du kan ändra administratörens standardautentiseringsuppgifter (användarnamn och lösenord) för att komma åt [!DNL InDesign Server] från [!DNL Experience Manager] utan att bryta integreringen med [!DNL InDesign Server].

1. Gå till `/etc/cloudservices/proxy.html`.
1. Ange det nya användarnamnet och lösenordet i dialogrutan.
1. Spara inloggningsuppgifterna.

>[!MORELIKETHIS]
>
>* [Om Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
