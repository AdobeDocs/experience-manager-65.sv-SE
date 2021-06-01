---
title: Konfigurera Dynamic Media - Scene7-läge
description: Lär dig hur du konfigurerar läget Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Konfiguration,Scene7-läge
source-git-commit: 485464350f391fca327207b78b165897fdacc2d3
workflow-type: tm+mt
source-wordcount: '5793'
ht-degree: 4%

---

# Konfigurera Dynamic Media - Scene7-läge{#configuring-dynamic-media-scene-mode}

Om du använder Adobe Experience Manager för olika miljöer, som utveckling, staging och produktion, konfigurerar du Dynamic Media-Cloud Services för var och en av dessa miljöer.

## Arkitekturdiagram över Dynamic Media - Scene7-läge {#architecture-diagram-of-dynamic-media-scene-mode}

I följande arkitekturdiagram beskrivs hur läget Dynamic Media - Scene7 fungerar.

Med den nya arkitekturen ansvarar Experience Manager för de viktigaste källresurserna och synkningarna med Dynamic Media för bearbetning och publicering av mediefiler:

1. När den primära källresursen överförs till Experience Manager replikeras den till Dynamic Media. Då hanterar Dynamic Media all bearbetning och generering av resurser, till exempel videokodning och dynamiska varianter av en bild. <!-- (In Dynamic Media - Scene7 mode, be aware that you can only upload assets whose file sizes are 2 GB or less.) Jira ticket CQ-4286561 fixed this issue. DM-S7 NOW SUPPORTS THE UPLOAD OF ASSETS LARGER THAN 2 GB. -->
1. När återgivningarna har genererats kan Experience Manager på ett säkert sätt komma åt och förhandsgranska Dynamic Media-fjärråtergivningarna (inga binärfiler skickas tillbaka till Experience Manager-instansen).
1. När innehållet är klart att publiceras och godkännas utlöses Dynamic Media-tjänsten att skicka ut innehåll till leveransservrar och cachelagra innehåll på leveransnätverket.

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>Följande funktionslista kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager - Dynamic Media. Andra anpassade CDN stöds inte med dessa funktioner.
>
>* [Smart bildbehandling](/help/assets/imaging-faq.md)
* [Cacheogiltigförklaring](/help/assets/invalidate-cdn-cache-dynamic-media.md)
* [Hotlänksskydd](/help/assets/hotlink-protection.md)
* [HTTP/2-leverans av innehåll](/help/assets/http2.md)
* URL-omdirigering på CDN-nivå
* Akamai ChinaCDN (för optimal leverans i Kina)


## Aktivera Dynamic Media i Scene7-läge {#enabling-dynamic-media-in-scene-mode}

[Dynamic ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) Mediais är inaktiverat som standard. Om du vill utnyttja Dynamic Media funktioner måste du aktivera dem.

>[!WARNING]
Dynamic Media - Scene7-läget är endast för *författarinstansen av Experience Manager*. Därför måste du konfigurera `runmode=dynamicmedia_scene7` på Experience Manager Author-instansen *inte* Experience Manager Publish-instansen.

Om du vill aktivera Dynamic Media måste du starta Experience Manager med körningsläget `dynamicmedia_scene7` från kommandoraden genom att ange följande i ett terminalfönster (exempelporten som används är 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Valfritt) Migrera förinställningar och konfigurationer för Dynamic Media från 6.3 till 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Uppgradering av Experience Manager Dynamic Media från 6.3 till 6.4 eller 6.5 innefattar nu möjligheten till driftsättning utan driftstopp. Om du vill migrera alla förinställningar och konfigurationer från `/etc` till `/conf` i CRXDE Lite ska du köra följande kommando.

>[!NOTE]
Om du kör Experience Manager-instansen i kompatibilitetsläge, d.v.s. har kompatibilitetspaketet installerat, behöver du inte köra dessa kommandon.

För alla uppgraderingar, antingen med eller utan kompatibilitetspaketet, kan du kopiera de förinställningar för visningsprogram som ursprungligen ingick i Dynamic Media genom att köra följande kommando för Linux®-kurva:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Om du vill migrera anpassade förinställningar och konfigurationer för visningsprogram som du har skapat från `/etc` till `/conf` kör du följande kommando för Linux®-kontroll:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installerar funktionspaket 18912 för migrering av gruppresurser {#installing-feature-pack-for-bulk-asset-migration}

Installationen av funktionspaket 18912 är *valfri*.

Med funktionspaketet 18912 kan du antingen importera resurser gruppvis via FTP eller migrera resurser från antingen Dynamic Media - hybrid- eller Dynamic Media Classic till Dynamic Media - Scene7-läge på Experience Manager. Den är tillgänglig från [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Mer information finns i [Installera funktionspaket 18912 för migrering av gruppresurser](/help/assets/bulk-ingest-migrate.md).

## Skapa en Dynamic Media-konfiguration i Cloud Servicens {#configuring-dynamic-media-cloud-services}

**Innan du konfigurerar Dynamic Media** - När du har fått ditt e-postmeddelande med Dynamic Media-inloggningsuppgifter måste du öppna  [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och sedan logga in på ditt konto för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media Cloud Service har rätt autentiseringsuppgifter.

![dynamicmediaconfiguration2uppdaterad](assets/dynamicmediaconfiguration2updated.png)

**Så här skapar du en Dynamic Media-konfiguration i Cloud Services:**

1. I läget Experience Manager Author trycker du på Experience Manager-logotypen för att komma åt den globala navigeringskonsolen och sedan på verktygsikonen och sedan på **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Läsare för Dynamic Media-konfiguration trycker du i den vänstra rutan på **[!UICONTROL global]** (tryck inte på och välj inte mappikonen till vänster om **[!UICONTROL global]**) och sedan trycker du på **[!UICONTROL Create]**.
1. På sidan **[!UICONTROL Create Dynamic Media Configuration]** anger du en titel, e-postadress för Dynamic Media-konto, lösenord och väljer sedan region. Den här informationen tillhandahålls av Adobe i e-postmeddelandet om etablering. Kontakta Adobe kundtjänst om du inte har fått e-postmeddelandet.

   Tryck på **[!UICONTROL Connect to Dynamic Media]**.

   >[!NOTE]
   När du har fått ditt e-postmeddelande med Dynamic Media-inloggningsuppgifter öppnar du [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och loggar sedan in på ditt konto för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media-Cloud Servicen har rätt autentiseringsuppgifter.

1. Ange följande när anslutningen lyckas. Rubriker med asterisk (*) krävs:

   * **[!UICONTROL Company]** - namnet på Dynamic Media-kontot. Du har flera Dynamic Media-konton. Du kan till exempel ha olika undervarumärken, divisioner, mellanlagrings- eller produktionsmiljöer.

   * **[!UICONTROL Company Root Folder Path]**

   * **[!UICONTROL Publishing Assets]** - Du kan välja mellan följande tre alternativ:
      * **[!UICONTROL Immediately]** betyder att när resurser överförs, importeras resurserna och URL:en/inbäddningen anges omedelbart. Ingen användaråtgärd krävs för att publicera resurser.
      * **[!UICONTROL Upon Activation]** betyder att du måste publicera resursen explicit innan en URL/Embed-länk anges.<br><!-- CQDOC-17478, Added March 9, 2021-->Från och med Experience Manager 6.5.8 återspeglar Experience Manager Publish-instansen korrekta Dynamic Media-metadatavärden, till exempel  `dam:scene7Domain` och  `dam:scene7FileStatus` i  **[!UICONTROL Upon Activation]** publiceringsläge. Om du vill aktivera den här funktionen installerar du Service Pack 8 och startar sedan om Experience Manager. Gå till Sling Config Manager. Hitta konfigurationen för `Scene7ActivationJobConsumer Component` eller skapa en ny). Markera kryssrutan **[!UICONTROL Replicate Metadata after Dynamic Media publishing]** och tryck sedan på **[!UICONTROL Save]**.

         ![Replikera metadata efter Dynamic Media publicering, kryssruta](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Selective Publish]** Med det här alternativet kan du styra vilka mappar som ska publiceras i Dynamic Media. Du kan använda funktioner som smart beskärning eller dynamiska återgivningar, eller avgöra vilka mappar som publiceras exklusivt i Experience Manager för förhandsgranskning. Samma resurser är *inte* publicerade i Dynamic Media för att levereras i den offentliga domänen.<br>Du kan ange det här alternativet här i  **[!UICONTROL Dynamic Media Cloud Configuration]** eller, om du vill, du kan välja att ange det här alternativet på mappnivå, i en mapps  **[!UICONTROL Properties]**.<br>Se  [Arbeta med selektiv publicering i Dynamic Media.](/help/assets/selective-publishing.md)<br>Om du senare ändrar den här konfigurationen, eller ändrar den senare på mappnivå, påverkar ändringarna bara nya resurser som du överför från den punkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från antingen **[!UICONTROL Quick Publish]** eller **[!UICONTROL Manage Publication]**-dialogrutan.
   * **[!UICONTROL Secure Preview Server]** - gör att du kan ange URL-sökvägen till förhandsgranskningsservern för säkra återgivningar. Det innebär att när återgivningarna har genererats kan Experience Manager på ett säkert sätt komma åt och förhandsgranska Dynamic Media-fjärråtergivningarna (inga binärfiler skickas tillbaka till Experience Manager-instansen).
Om du inte har en särskild lösning för att använda ditt företags server eller en speciell server rekommenderar Adobe att du låter den här inställningen vara angiven.

   * **[!UICONTROL Sync all content]** -  <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Markerat som standard. Avmarkera det här alternativet om du vill inkludera eller exkludera resurser från synkroniseringen till Dynamic Media. Om du avmarkerar det här alternativet kan du välja mellan följande två synkroniseringslägen för Dynamic Media:

   * **[!UICONTROL Dynamic Media sync mode]**
      * **[!UICONTROL Enabled by default]** - Konfigurationen används som standard på alla mappar såvida du inte markerar en mapp som är exkluderad.  <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Disabled by default]** - Konfigurationen tillämpas inte på någon mapp förrän du uttryckligen markerar en markerad mapp för synkronisering till Dynamic Media.
Om du vill markera en markerad mapp för synkronisering till Dynamic Media väljer du en resursmapp och trycker sedan på **[!UICONTROL Properties]** i verktygsfältet. Välj bland följande tre alternativ i listrutan **[!UICONTROL Dynamic Media sync mode]** på fliken **[!UICONTROL Details]**. När du är klar trycker du på **[!UICONTROL Save]**. *Kom ihåg: Dessa tre alternativ är inte tillgängliga om du valde **Synkronisera allt**innehåll tidigare.* Se även  [Arbeta med selektiv publicering på mappnivå i Dynamic Media.](/help/assets/selective-publishing.md)
         * **[!UICONTROL Inherited]** - Det finns inget explicit synkroniseringsvärde i mappen; I stället ärver mappen synkroniseringsvärdet från en av de överordnade mapparna eller standardläget i molnkonfigurationen. Detaljerad status för ärvda program via ett verktygstips.
         * **[!UICONTROL Enable for subfolders]** - Inkludera allt i det här underträdet för synkronisering med Dynamic Media. De mappspecifika inställningarna åsidosätter standardläget i molnkonfigurationen.
         * **[!UICONTROL Disabled for subfolders]** - Uteslut allt i det här underträdet från synkronisering till Dynamic Media.

   >[!NOTE]
   Det finns inget stöd för versionshantering i DMS7. Dessutom gäller fördröjd aktivering endast om **[!UICONTROL Publish Assets]** på sidan Redigera Dynamic Media-konfiguration är inställd på **[!UICONTROL Upon Activation]** och då endast tills resursen aktiveras första gången.
   När en mediefil har aktiverats publiceras uppdateringar direkt till S7 Delivery.

1. Tryck på **[!UICONTROL Save]**.
1. Om du vill förhandsgranska Dynamic Media-innehåll på ett säkert sätt innan det publiceras måste du tillåtslista författarinstansen Experience Manager för att ansluta till Dynamic Media:

   * Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och logga sedan in på ditt konto. Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

   * Tryck på **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]** i navigeringsfältet uppe till höger på sidan.

   * Välj **[!UICONTROL Test Image Serving]** i listrutan Publiceringskontext på sidan Image Server Publish.
   * Tryck på **[!UICONTROL Add]** för klientadressfiltret.
   * Markera kryssrutan om du vill aktivera (aktivera) adressen. Ange IP-adressen för Experience Manager Author-instansen (inte Dispatcher IP).
   * Tryck på **[!UICONTROL Save]**.

Du är nu klar med den grundläggande konfigurationen; är du redo att använda Dynamic Media - Scene7.

Om du vill anpassa konfigurationen ytterligare kan du utföra alla åtgärder under [(Valfritt) Konfigurera avancerade inställningar i Dynamic Media - Scene7-läge](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Valfritt) Konfigurera avancerade inställningar i Dynamic Media - Scene7-läge {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Om du vill anpassa konfigurationen och konfigurationen av Dynamic Media - Scene7 eller optimera prestandan ytterligare kan du utföra en eller flera av följande *valfria* uppgifter:

* [(Valfritt) Installation och konfiguration av Dynamic Media - inställningar för Scene7-läge](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Valfritt) Justera prestanda för Dynamic Media - Scene7-läge](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Valfritt) Filtrera resurser för replikering](#optional-filtering-assets-for-replication)

### (Valfritt) Installation och konfiguration av Dynamic Media - Inställningar för Scene7-läge {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

När du är i körläge `dynamicmedia_scene7` använder du användargränssnittet i Dynamic Media Classic för att ändra dina Dynamic Media-inställningar.

Vissa av ovanstående uppgifter kräver att du öppnar [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och sedan loggar in på ditt konto.

Installations- och konfigureringsuppgifter omfattar följande:

* [Publiceringskonfiguration för Image Server](#publishing-setup-for-image-server)
* [Konfigurera allmänna inställningar för programmet](#configuring-application-general-settings)
* [Konfigurera färghantering](#configuring-color-management)
* [Redigera MIME-typer för format som stöds](#editing-mime-types-for-supported-formats)
* [Lägga till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats)
* [Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Publiceringsinställningar för Image Server {#publishing-setup-for-image-server}

Publiceringsinställningarna avgör hur resurser levereras som standard från Dynamic Media. Om ingen inställning anges levererar Dynamic Media en resurs enligt standardinställningarna som definierats i Publiceringsinställningar. En begäran om att leverera en bild som inte innehåller ett upplösningsattribut ger till exempel en bild med inställningen för standardobjektupplösning.

Så här konfigurerar du publiceringsinställningar: i Dynamic Media Classic: tryck på **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**.

Bildserverskärmen anger standardinställningar för att leverera bilder. I gränssnittsskärmen finns en beskrivning av varje inställning.

* **[!UICONTROL Request Attributes]** - De här inställningarna begränsar antalet bilder som kan levereras från servern.
* **[!UICONTROL Default Request Attributes]** - De här inställningarna gäller standardutseendet för bilder.
* **[!UICONTROL Common Thumbnail Attributes]** - De här inställningarna gäller för miniatyrbildernas standardutseende.
* **[!UICONTROL Defaults for Catalog Fields]**- De här inställningarna gäller bildernas upplösning och standardtyp av miniatyrbilder.
* **[!UICONTROL Color Management Attributes]** - De här inställningarna avgör vilka ICC-färgprofiler som används.
* **[!UICONTROL Compatibility Attributes]** - Den här inställningen gör att inledande och avslutande stycken i textlager kan hanteras som de var i version 3.6 för bakåtkompatibilitet.
* **[!UICONTROL Localization Support]** - Med de här inställningarna kan du hantera flera språkattribut. Här kan du också ange en sträng för språkområdeskarta så att du kan definiera vilka språk du vill ha stöd för de olika verktygstipsen i visningsprogram. Mer information om hur du konfigurerar **[lokaliseringsstöd]** finns i [Att tänka på när du konfigurerar lokalisering av resurser](https://help.adobe.com/en_US/scene7/using/WS997f1dc4cb0179f034e07dc31412799d19a-8000.html).

#### Konfigurerar allmänna inställningar för programmet {#configuring-application-general-settings}

Öppna sidan Allmänna inställningar för programmet genom att trycka på **[!UICONTROL Setup > Application Setup > General Settings]** i det globala navigeringsfältet i Dynamic Media Classic.

**[!UICONTROL Servers]** - Vid kontoetablering tillhandahåller Dynamic Media automatiskt de tilldelade servrarna för ditt företag. De här servrarna används för att skapa URL-strängar för din webbplats och dina program. Dessa URL-anrop är specifika för ditt konto. Ändra inte något av servernamnen om du inte uttryckligen har fått instruktioner från Adobe kundtjänst om att göra det.

**[!UICONTROL Overwrite Images]** - Dynamic Media tillåter inte att två filer har samma namn. Varje objekts URL-ID (filnamnet minus filtillägget) måste vara unikt. De här alternativen anger hur ersättningsresurser överförs: om de ersätter originalet eller blir dubbletter. Duplicerade resurser får ett nytt namn med namnet&quot;-1&quot; (till exempel heter stol.tif stol-1.tif). Dessa alternativ påverkar resurser som överförts till en annan mapp än den ursprungliga eller resurser med ett annat filnamnstillägg än den ursprungliga (till exempel JPG, TIF eller PNG).

* **[!UICONTROL Overwrite in current folder, same base image name/extension]** - Det här alternativet är den striktaste regeln för ersättning. Det kräver att du överför ersättningsbilden till samma mapp som originalbilden och att ersättningsbilden har samma filnamnstillägg som originalbilden. Om dessa krav inte uppfylls skapas en dubblett.

>[!NOTE]
Välj alltid den här inställningen om du vill att den ska vara konsekvent med Experience Manager: **Skriv över i den aktuella mappen, samma basbildnamn/tillägg**

* **[!UICONTROL Overwrite in any folder, same base asset name/extension]** - Kräver att ersättningsbilden har samma filnamnstillägg som originalbilden (t.ex. måste stol.jpg ersätta stol.jpg, inte stol.tif). Du kan dock överföra ersättningsbilden till en annan mapp än den ursprungliga. Den uppdaterade bilden finns i den nya mappen; filen inte längre kan hittas på sin ursprungliga plats
* **[!UICONTROL Overwrite in any folder, same base asset name regardless of extension]** - Det här alternativet är den mest omfattande ersättningsregeln. Du kan överföra en ersättningsbild till en annan mapp än den ursprungliga, överföra en fil med ett annat filnamnstillägg och ersätta den ursprungliga filen. Om originalfilen finns i en annan mapp finns ersättningsbilden i den nya mappen som den överfördes till.

**[!UICONTROL Default Color Profiles]** - Mer information finns i  [Konfigurera ](#configuring-color-management) färghantering.

>[!NOTE]
Som standard visas 15 återgivningar när du väljer **[!UICONTROL Renditions]** och 15 visningsförinställningar när du väljer **[!UICONTROL Viewers]** i resursens detaljvy. Du kan öka den här gränsen. Se [Öka antalet bildförinställningar som visas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) eller [Öka antalet visningsförinställningar som visas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).


#### Konfigurerar färghantering {#configuring-color-management}

Med dynamisk mediefärghantering kan du färgkorrigera resurser. Med färgkorrigering behåller inkapslade resurser sin färgmodell (RGB, CMYK, Grå) och inbäddad färgprofil. När du begär en dynamisk återgivning korrigeras bildfärgen till målfärgrymden med hjälp av CMYK-, RGB- eller grå utdata. Se [Konfigurera bildförinställningar](/help/assets/managing-image-presets.md).

Så här konfigurerar du standardfärgegenskaperna så att färgkorrigering aktiveras när bilder begärs:

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och logga sedan in på ditt konto med de autentiseringsuppgifter som anges under etableringen.
1. Navigera till **[!UICONTROL Setup > Application Setup]**.
1. Expandera området **[!UICONTROL Publish Setup]** och markera **[!UICONTROL Image Server]**. Ange **[!UICONTROL Publish Context]** som **[!UICONTROL Image Serving]** när du anger standardvärden för publiceringsinstanser.
1. Bläddra till den egenskap som du vill ändra. En egenskap i området **[!UICONTROL Color Management Attributes]**.

   Du kan ange följande egenskaper för färgkorrigering:

   * **[!UICONTROL CMYK Default Color Space]** - Namn på CMYK-standardfärgprofil
   * **[!UICONTROL Gray-Scale Default Color Space]** - Namn på standardfärgprofilen för gråskala
   * **[!UICONTROL RGB Default Color Space]** - Namn på standardfärgprofilen för RGB
   * **[!UICONTROL Color Conversion Rendering Intent]** - Anger återgivningsmetod. Godtagbara värden är: **[!UICONTROL perceptual]**, **[!UICONTROL relative colometric]**, **[!UICONTROL saturation]**, **[!UICONTROL absolute colometric]**. Adobe rekommenderar **[!UICONTROL relative]** som standard.

1. Tryck på **[!UICONTROL Save]**.

Du kan till exempel ställa in **[!UICONTROL RGB Default Color Space]** på *sRGB* och **[!UICONTROL CMYK Default Color Space]** på *WebCoated*.

Om du gör det gör du så här:

* Aktiverar färgkorrigering för RGB- och CMYK-bilder.
* RGB-bilder som inte har någon färgprofil antas finnas i färgrymden *sRGB*.
* CMYK-bilder som inte har någon färgprofil antas finnas i färgrymden *WebCoated*.
* Dynamiska återgivningar som returnerar RGB-utdata returnerar det i färgrymden *sRGB*.
* Dynamiska återgivningar som returnerar CMYK-utdata returnerar det i färgrymden *WebCoated*.

#### Redigera MIME-typer för format som stöds {#editing-mime-types-for-supported-formats}

Du kan definiera vilka resurstyper som bearbetas av Dynamic Media och anpassa avancerade parametrar för resurshantering. Du kan till exempel ange parametrar för tillgångsbearbetning för att göra följande:

* Konvertera en Adobe PDF till en eCatalog-resurs.
* Konvertera ett Adobe Photoshop-dokument (.PSD) till en bannermallsresurs för personalisering.
* Rastrera en Adobe Illustrator-fil (.AI) eller en Adobe Photoshop Encapsulated PostScript®-fil (.EPS).
* [Videoprofiler ](/help/assets/video-profiles.md) och  [bildprofiler ](/help/assets/image-profiles.md) kan användas för att definiera bearbetning av videoklipp och bilder.

Se [Överför resurser](/help/assets/manage-assets.md#uploading-assets).

**Så här redigerar du MIME-typer för de format som stöds:**

1. Tryck på Experience Manager-logotypen i Experience Manager för att komma åt den globala navigeringskonsolen och tryck sedan på **[!UICONTROL Tools > General > CRXDE Lite]**.
1. Navigera till följande i den vänstra listen:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME-typer](assets/mimetypes.png)

1. Välj en mime-typ i mappen mimeTypes.
1. Till höger på CRXDE Lite-sidan i den nedre delen:

   * dubbelklicka på fältet **[!UICONTROL enabled]**. Som standard är alla resursens MIME-typer aktiverade (inställda på **[!UICONTROL true]**), vilket innebär att resurserna synkroniseras till Dynamic Media för bearbetning. Om du vill utesluta den här resursens MIME-typ från bearbetningen ändrar du den här inställningen till **[!UICONTROL false]**.

   * dubbeltryck på **[!UICONTROL jobParam]** för att öppna det tillhörande textfältet. Se [MIME-typer som stöds](/help/assets/assets-formats.md#supported-mime-types) för en lista över tillåtna värden för processparametrar som du kan använda för en viss MIME-typ.

1. Gör något av följande:

   * Upprepa steg 3-4 för att redigera fler MIME-typer.
   * Tryck på **[!UICONTROL Save All]** på menyraden på CRXDE Lite-sidan.

1. Tryck på **[!UICONTROL CRXDE Lite]** längst upp till vänster på sidan för att gå tillbaka till Experience Manager.

#### Lägger till MIME-typer för format som inte stöds {#adding-mime-types-for-unsupported-formats}

Du kan lägga till anpassade MIME-typer för format som inte stöds i Experience Manager Assets. Kontrollera att alla nya noder som du lägger till i CRXDE Lite inte tas bort av Experience Manager genom att flytta MIME-typen före `image_`. Kontrollera också att dess aktiverade värde är **[!UICONTROL false]**.

**Så här lägger du till MIME-typer för format som inte stöds:**

1. Tryck på **[!UICONTROL Tools > Operations > Web Console]** från Experience Manager.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. En ny flik i webbläsaren öppnas på sidan **[!UICONTROL Adobe Experience Manager Web Console Configuration]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. På sidan bläddrar du nedåt till namnet *Adobe CQ Scene7 Asset MIME type Service* enligt följande skärmbild. Tryck på **[!UICONTROL Edit the configuration values]** (pennikonen) till höger om namnet.

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. På sidan **Adobe CQ Scene7 Asset MIME type Service** trycker du på en plusteckenikon &lt;+>. Platsen i tabellen där du trycker på plustecknet för att lägga till den nya mime-typen är enkel.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Skriv `DWG=image/vnd.dwg` i det tomma textfältet som du just lade till.

   Exemplet `DWG=image/vnd.dwg` är endast för illustrationsändamål. MIME-typen som du lägger till här kan vara ett annat format som inte stöds.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Tryck på **[!UICONTROL Save]** längst ned till höger på sidan.

   Nu kan du stänga webbläsarfliken som har den öppna konfigurationssidan för Adobe Experience Manager Web Console.

1. Gå tillbaka till webbläsarfliken som har din öppna Experience Manager-konsol.
1. Tryck på **[!UICONTROL Tools > General > CRXDE Lite]** från Experience Manager.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Navigera till följande i den vänstra listen:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Dra MIME-typen `image_vnd.dwg` och släpp den direkt ovanför `image_` i trädet så som visas på följande skärmbild.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Med mime-typen `image_vnd.dwg` fortfarande markerad dubbeltrycker du på värdet på fliken **[!UICONTROL Properties]** på raden **[!UICONTROL enabled]** under kolumnrubriken **[!UICONTROL Value]** för att öppna listrutan **[!UICONTROL Value]**.
1. Skriv `false` i fältet (eller välj **[!UICONTROL false]** i listrutan).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. I närheten av det övre vänstra hörnet på CRXDE Lite-sidan trycker du på **[!UICONTROL Save All]**.

#### Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Använd förinställningar för gruppuppsättningar för att automatisera skapandet av bilduppsättningar eller snurra uppsättningar medan resurserna överförs till Dynamic Media.

Definiera först namnkonventionen för hur resurser grupperas i en uppsättning. Skapa sedan en förinställning för gruppuppsättning som är en unik, självständig uppsättning instruktioner. Det måste definiera hur uppsättningen ska skapas med bilder som matchar de definierade namnkonventionerna i förinställningsreceptet.

När du överför filer skapar Dynamic Media automatiskt en uppsättning med alla filer som matchar den definierade namnkonventionen i de aktiva förinställningarna.

**Konfigurerar standardnamngivning**

Skapa en standardnamnkonvention som används i alla förinställda gruppuppsättningar. Den standardnamnkonvention som valts i definitionen av gruppuppsättningsförinställningen är troligen allt som ditt företag behöver för att gruppgenerera uppsättningar. En gruppuppsättningsförinställning skapas för att använda den standardnamnkonvention som du definierar. Du kan skapa så många gruppuppsättningsförinställningar med alternativa, anpassade namnkonventioner som behövs för en viss uppsättning innehåll om det finns ett undantag från den företagsdefinierade standardnamngivningen.

När det inte krävs någon standardnamnkonvention för att använda funktionen för gruppuppsättningsförinställningar bör du använda standardnamnkonventionen. Här kan du definiera så många element i namnkonventionen som du vill gruppera i en uppsättning så att du kan effektivisera skapandet av gruppuppsättningar.

Alternativt kan du använda **[!UICONTROL View Code]** utan några formulärfält tillgängliga. I den här vyn skapar du namnkonventionens definitioner helt med hjälp av reguljära uttryck.

Det finns två element för definition, Matcha och Basnamn. Med dessa fält kan du definiera alla element i en namnkonvention och identifiera den del av konventionen som används för att namnge den uppsättning i vilken de finns. Ett företags namnkonvention använder ofta en eller flera definitionsrader för vart och ett av dessa element. Du kan använda så många rader för din unika definition och gruppera dem i distinkta element, t.ex. för Huvudbild, Färgelement, Alternativa vyer och Färgruteelement.

**Så här konfigurerar du standardnamn:**

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Tryck på **[!UICONTROL Setup > Application Setup > Batch Set Presets > Default Naming]** i navigeringsfältet uppe på sidan.
1. Välj **[!UICONTROL View Form]** eller **[!UICONTROL View Code]** för att ange hur du vill visa och ange information om varje element.

   Du kan markera kryssrutan **[!UICONTROL View Code]** om du vill visa värdeuppbyggnaden för det reguljära uttrycket tillsammans med dina formulärval. Du kan ange eller ändra dessa värden för att underlätta definitionen av elementen i namnkonventionen, om formulärvyn begränsar dig av någon anledning. Om dina värden inte kan tolkas i formulärvyn blir formulärfälten inaktiva.

   >[!NOTE]
   Inaktiverade formulärfält verifierar inte att reguljära uttryck är korrekta. Resultaten av det reguljära uttryck som du skapar för varje element efter resultatraden visas. Det fullständiga reguljära uttrycket visas längst ned på sidan.

1. Expandera varje element efter behov och ange de namnkonventioner som du vill använda.
1. Gör något av följande om det behövs:

   * Tryck på **[!UICONTROL Add]** om du vill lägga till en annan namnkonvention för ett element.
   * Tryck på **[!UICONTROL Remove]** om du vill ta bort en namnkonvention för ett element.

1. Gör något av följande:

   * Tryck på **[!UICONTROL Save As]** och ange ett namn för förinställningen.
   * Tryck på **[!UICONTROL Save]** om du redigerar en befintlig förinställning.

**Skapa en förinställning för gruppuppsättning**

I Dynamic Media används gruppuppsättningsförinställningar för att ordna resurser i uppsättningar med bilder (alternativa bilder, färgalternativ, 360 rotationer) för visning i visningsprogram. Förinställningarna för gruppuppsättningar körs automatiskt tillsammans med överföringsprocesserna för resurser i Dynamic Media.

Du kan skapa, redigera och hantera dina gruppuppsättningsförinställningar. Det finns två former av förinställda gruppuppsättningsdefinitioner: en för en standardnamnkonvention som du kan konfigurera och en för anpassade namnkonventioner som du skapar direkt.

Du kan antingen använda formulärfältsmetoden för att definiera en gruppuppsättningsförinställning eller kodmetoden, som gör att du kan använda reguljära uttryck. Precis som i Standardnamn kan du välja Visa kod samtidigt som du definierar i formulärvyn och använda reguljära uttryck för att skapa definitioner. Du kan också avmarkera en vy om du vill använda den ena eller den andra enbart.

**Så här skapar du en förinställning för gruppuppsättning:**

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Tryck på **[!UICONTROL Setup > Application Setup > Batch Set Presets > Batch Set Preset]** i navigeringsfältet uppe på sidan.

   **[!UICONTROL View Form]**, som anges i det övre högra hörnet på detaljsidan, är standardvyn.

1. Tryck på **[!UICONTROL Add]** på panelen Förinställningslista för att aktivera definitionsfälten på panelen Detaljer till höger på skärmen.
1. Skriv ett namn på förinställningen i fältet Förinställningsnamn på panelen Detaljer.
1. Välj en förinställningstyp i listrutan Gruppuppsättningstyp.
1. Gör något av följande:

   * Om du använder en standardnamnkonvention som du tidigare konfigurerat under **[!UICONTROL Application Setup > Batch Set Presets > Default Naming]** expanderar du **[!UICONTROL Asset Naming Conventions]** och trycker sedan på **[!UICONTROL Default]** i listrutan Namnge fil.

   * Om du vill definiera en ny namnkonvention när du konfigurerar förinställningen expanderar du **[!UICONTROL Asset Naming Conventions]** och trycker sedan på **[!UICONTROL Custom]** i listrutan Filnamngivning.

1. I Sekvensordning definierar du i vilken ordning bilderna ska visas efter att uppsättningen har grupperats i Dynamic Media.

   Som standard sorteras dina resurser alfanumeriskt. Du kan dock använda en kommaavgränsad lista med reguljära uttryck för att definiera ordningen.

1. Ange suffixet eller prefixet till basnamnet som du definierade i konventionen om namngivning av tillgångar för Ange namngivning och skapande. Ange också var uppsättningen ska skapas i mappstrukturen för Dynamic Media.

   Om du definierar ett stort antal uppsättningar ska uppsättningarna hållas åtskilda från de mappar som innehåller själva resurserna. Skapa till exempel en mapp för bilduppsättningar och placera genererade uppsättningar här.

1. Tryck på **[!UICONTROL Save]** på panelen Detaljer.
1. Tryck på **[!UICONTROL Active]** bredvid den nya förinställningens namn.

   När du aktiverar förinställningen används den för att generera uppsättningen när du överför resurser till Dynamic Media.

**Skapa en gruppuppsättningsförinställning för automatisk generering av en 2D-snurpuppsättning**

Du kan använda gruppuppsättningstypen **[!UICONTROL Multi-Axis Spin Set]** för att skapa ett recept som automatiserar genereringen av 2D-snurruppsättningar. Vid gruppering av bilder används reguljära uttryck för rad och kolumn så att bildresurserna justeras korrekt på motsvarande plats i den flerdimensionella arrayen. Det finns inget minsta eller högsta antal rader eller kolumner som du måste ha i en rotationsuppsättning med flera axlar.

Anta till exempel att du vill skapa en fleraxelssnurra med namnet `spin-2dspin`. Du har en uppsättning bilder med snurra uppsättningar som innehåller tre rader, med 12 bilder per rad. Bilderna får följande namn:

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Med den här informationen kan du skapa ditt recept för gruppuppsättningstyp enligt följande:

![chlimage_1-560](assets/chlimage_1-560.png)

Gruppering för den delade resursnamndelen i rotationsuppsättningen läggs till i fältet **Matcha** (markerat). Variabeldelen av resursnamnet som innehåller raden och kolumnen läggs till i fälten **Rad** och **Kolumn**.

När rotationsuppsättningen har överförts och publicerats aktiverar du namnet på det 2D-rotationsuppsättningsrecept som visas under **Förinställningar för gruppuppsättning** i dialogrutan **Alternativ för överföringsjobb**.

**Så här skapar du en gruppuppsättningsförinställning för automatisk generering av en 2D-snurpuppsättning:**

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Tryck på **[!UICONTROL Setup]> [!UICONTROL Application Setup] > [!UICONTROL Batch Set Presets] >[!UICONTROL Batch Set Preset]** på navigeringsfältet nära sidans överkant.

   **[!UICONTROL View Form]**, som anges i det övre högra hörnet på detaljsidan, är standardvyn.

1. Tryck på **[!UICONTROL Add]** på panelen Förinställningslista för att aktivera definitionsfälten på panelen Detaljer till höger på skärmen.
1. Skriv ett namn på förinställningen i fältet Förinställningsnamn på panelen Detaljer.
1. I listrutan Gruppuppsättningstyp väljer du **[!UICONTROL Asset Set]**.
1. Välj **[!UICONTROL Multi-Axis Spin Set]** i listrutan Undertyp.
1. Expandera **[!UICONTROL Asset Naming Conventions]** och tryck sedan på **[!UICONTROL Custom]** i listrutan Namnge fil.
1. Använd attributen **[!UICONTROL Match]** och eventuellt **[!UICONTROL Base Name]** för att definiera ett reguljärt uttryck för namngivning av bildresurser som utgör grupperingen.

   Det reguljära uttrycket för literal Match kan till exempel se ut så här:

   `(w+)-w+-w+`

1. Expandera **[!UICONTROL Row Column Position]** och definiera sedan namnformatet för bildresursens position i 2D-rotationsmatrisen.

   Använd parentesen för att omsluta rad- eller kolumnpositionen i filnamnet.

   För en rad med ett reguljärt uttryck kan det se ut så här:

   `\w+-R([0-9]+)-\w+`

   eller

   `\w+-(\d+)-\w+`

   För det reguljära uttrycket i kolumnen kan det se ut så här:

   `\w+-\w+-C([0-9]+)`

   eller

   `\w+-\w+-C(\d+)`

   Proven ovan är endast avsedda som illustrationer. Du kan skapa det reguljära uttrycket hur du vill.

   >[!NOTE]
   Om kombinationen av reguljära uttryck för rader och kolumner inte kan avgöra positionen för resursen i den flerdimensionella rotationsinställningsarrayen, läggs resursen inte till i uppsättningen. Ett fel loggas också.

1. Ange suffixet eller prefixet till basnamnet som du definierade i konventionen om namngivning av tillgångar för Ange namngivning och skapande.

   Ange också var rotationsuppsättningen ska skapas i mappstrukturen för Dynamic Media Classic.

   Om du definierar ett stort antal uppsättningar ska uppsättningarna hållas åtskilda från de mappar som innehåller själva resurserna. Du kan till exempel skapa en mapp för snurruppsättningar där du kan placera genererade uppsättningar här.

1. Tryck på **[!UICONTROL Save]** på panelen Detaljer.
1. Tryck på **[!UICONTROL Active]** bredvid den nya förinställningens namn.

   När du aktiverar förinställningen används den för att generera uppsättningen när du överför resurser till Dynamic Media.

### (Valfritt) Justera prestanda för Dynamic Media - Scene7-läge {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Adobe rekommenderar följande finjusteringstips för synkroniseringsprestanda/skalbarhet för att Dynamic Media - Scene7-läget ska fungera smidigt:

* Uppdaterar de fördefinierade jobbparametrarna för bearbetning av olika filformat.
* Uppdaterar de fördefinierade arbetstrådarna för Granite-arbetsflödet (videoresurser).
* Uppdaterar det fördefinierade tillfälliga Granite-arbetsflödet (bilder och icke-videomaterial) för köarbetstrådar.
* Uppdaterar de maximala överföringsanslutningarna till Dynamic Media Classic-servern.

#### Uppdatera de fördefinierade jobbparametrarna för bearbetning av olika filformat

Du kan justera jobbparametrar för snabbare bearbetning när du överför filer. Om du till exempel överför PSD-filer, men inte vill bearbeta dem som mallar, kan du ange att lagerextraheringen ska vara false (av). I så fall visas den justerade jobbparametern enligt följande: `process=None&createTemplate=false`.

Om du vill aktivera mallskapande använder du följande parametrar: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe rekommenderar att du använder följande&quot;justerade&quot; jobbparametrar för PDF-, PostScript®- och PSD-filer:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Filtyp | Rekommenderade jobbparametrar |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Om du vill uppdatera någon av de här parametrarna följer du stegen i [Aktivera stöd för MIME-typbaserade resurser/Dynamic Media Classic-överföringsjobbparametrar](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Uppdaterar den tillfälliga arbetsflödeskön för Granite {#updating-the-granite-transient-workflow-queue}

Kön för Bevilja överföring av arbetsflöde används för **[!UICONTROL DAM Update Asset]**-arbetsflödet. I Dynamic Media används den för bildhantering.

**Så här uppdaterar du den tillfälliga arbetsflödeskön för Granite:**

1. Gå till [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) och sök efter **kö: Bevilja övergångsarbetsflödeskö**.

   >[!NOTE]
   En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I fältet **[!UICONTROL Maximum Parallel Jobs]** ändrar du talet till önskat värde.

   Du kan öka **[!UICONTROL Maximum Parallel Jobs]** för att få tillräckligt stöd för överföring av filer till Dynamic Media. Det exakta värdet beror på maskinvarukapaciteten. I vissa scenarier, d.v.s. en inledande migrering eller en massöverföring som görs en gång, kan du använda ett stort värde. Tänk dock på att användning av ett stort värde (till exempel två gånger antalet kärnor) kan ha negativa effekter på andra samtidiga aktiviteter. Testa och justera värdet utifrån ditt specifika användningsfall.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Tryck på **[!UICONTROL Save]**.

#### Uppdaterar arbetsflödeskön för Granite {#updating-the-granite-workflow-queue}

Beviljad arbetsflödeskö används för icke-tillfälliga arbetsflöden. I Dynamic Media bearbetades video med arbetsflödet **[!UICONTROL Dynamic Media Encode Video]**.

**Så här uppdaterar du arbetsflödeskön för Granite:**

1. Navigera till `https://<server>/system/console/configMgr` och sök efter **Kö: Begränsa arbetsflödeskö**.

   >[!NOTE]
   En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I fältet **[!UICONTROL Maximum Parallel Jobs]** ändrar du talet till önskat värde.

   Du kan öka det maximala antalet parallella jobb för att få tillräckligt stöd för överföring av filer till Dynamic Media. Det exakta värdet beror på maskinvarukapaciteten. I vissa scenarier, d.v.s. en inledande migrering eller en massöverföring som görs en gång, kan du använda ett stort värde. Tänk dock på att användning av ett stort värde (till exempel två gånger antalet kärnor) kan ha negativa effekter på andra samtidiga aktiviteter. Testa och justera värdet utifrån ditt specifika användningsfall.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Tryck på **[!UICONTROL Save]**.

#### Uppdaterar Dynamic Media Classic-överföringsanslutningen {#updating-the-scene-upload-connection}

Inställningen Scene7 Upload Connection synkroniserar Experience Manager-resurser till Dynamic Media Classic-servrar.

**Så här uppdaterar du uppladdningsanslutningen för Dynamic Media Classic:**

1. Navigera till `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. I fältet **[!UICONTROL Number of connections]** och/eller fältet **[!UICONTROL Active job timeout]** ändrar du talet efter behov.

   Inställningen **[!UICONTROL Number of connections]** styr det maximala antalet HTTP-anslutningar som tillåts för överföring från Experience Manager till Dynamic Media. vanligtvis räcker det fördefinierade värdet på tio anslutningar.

   Inställningen **[!UICONTROL Active job timeout]** avgör väntetiden för överförda Dynamic Media-resurser som ska publiceras på leveransservern. Det här värdet är som standard 2 100 sekunder eller 35 minuter.

   I de flesta fall räcker det med inställningen 2 100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Tryck på **[!UICONTROL Save]**.

### (Valfritt) Filtrera resurser för replikering {#optional-filtering-assets-for-replication}

I andra distributioner än Dynamic Media replikerar du *alla*-resurser (både bilder och video) från Experience Manager-redigeringsmiljön till publiceringsnoden i Experience Manager. Det här arbetsflödet är nödvändigt eftersom publiceringsservrarna i Experience Manager också levererar resurserna.

I Dynamic Media-distributioner finns det dock inget behov av att replikera samma resurser till publiceringsnoderna i Experience Manager eftersom resurserna levereras via Cloud Servicen. Ett sådant&quot;hybridpubliceringsarbetsflöde&quot; undviker extra lagringskostnader och längre bearbetningstider för att replikera resurser. Annat innehåll, t.ex. webbplatssidor, fortsätter att hanteras från Experience Manager-publiceringsnoderna.

Med filtren kan du *utesluta*-resurser från replikering till publiceringsnoden i Experience Manager.

#### Använda standardresursfilter för replikering {#using-default-asset-filters-for-replication}

Om du använder Dynamic Media för bilder, video eller båda, kan du använda standardfiltren som finns i Adobe. Följande filter är aktiva som standard:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mime-typ</strong></td>
   <td><strong>Återgivningar</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filterbilder</p> <p>filteruppsättningar</p> <p> </p> </td>
   <td><p>Börjar med <strong>image/</strong></p> <p>Innehåller <strong>program/</strong> och avslutas med <strong>uppsättning</strong>.</p> </td>
   <td>De färdiga filterbilderna (gäller för enstaka bildresurser, inklusive interaktiva bilder) och "filteruppsättningar" (gäller Spin Sets, Image Sets, Mixed Media Sets och Carousel Sets) kommer att
    <ul>
     <li>Uteslut den ursprungliga bilden och statiska bildåtergivningar från replikering.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Börjar med <strong>video/</strong></td>
   <td>"filter-video" som är klar att användas:
    <ul>
     <li>Undanta återgivningar av originalvideo och statiska miniatyrer från replikering.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Filter gäller för MIME-typer och kan inte vara sökvägsspecifika.

#### Anpassa resursfilter för replikering {#customizing-asset-filters-for-replication}

1. Tryck på Experience Manager-logotypen i Experience Manager för att komma åt den globala navigeringskonsolen och tryck på **[!UICONTROL Tools > General > CRXDE Lite]**.
1. Navigera till `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` i det vänstra mappträdet för att granska filtren.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Du definierar Mime-typen för filtret genom att leta reda på Mime-typen enligt följande:

   Expandera `content > dam > <locate_your_asset> > jcr:content > metadata` i den vänstra listen och gå sedan till `dc:format` i tabellen.

   Följande bild är ett exempel på en resurs sökväg till `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observera att `dc:format` för resursen `Fiji Red.jpg` är `image/jpeg`.

   Om du vill att det här filtret ska gälla för alla bilder, oavsett format, anger du värdet `image/*` där `*` är ett reguljärt uttryck som används för alla bilder i alla format.

   Om du bara vill att filtret ska gälla för bilder av typen JPEG anger du värdet `image/jpeg`.

1. Definiera vilka renderingar du vill inkludera eller exkludera från replikering.

   Följande tecken kan användas för att filtrera replikering:

<table>
 <tbody>
  <tr>
   <td><strong>Tecken som ska användas</strong></td>
   <td><strong>Så här filtrerar du resurser för replikering</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Jokertecken</td>
  </tr>
  <tr>
   <td>+</td>
   <td>Innehåller resurser för replikering.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Exkluderar resurser från replikering.</td>
  </tr>
 </tbody>
</table>

Navigera till `content/dam/<locate your asset>/jcr:content/renditions`.

Följande grafik är ett exempel på en resurs återgivningar.

![chlimage_1-4](assets/chlimage_1-4.png)

Om du bara vill replikera originalet skriver du `+original`.
