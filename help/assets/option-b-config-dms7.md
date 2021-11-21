---
title: Alternativ B - Konfigurera Dynamic Media - Scene7-läge
description: Lär dig hur du konfigurerar läget Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: b1f2a6b8fecd9ee98f345d1de8c26c6f42a44823
workflow-type: tm+mt
source-wordcount: '5787'
ht-degree: 2%

---

# Konfigurera Dynamic Media - Scene7-läge{#configuring-dynamic-media-scene-mode}

Om du använder Adobe Experience Manager för olika miljöer, som utveckling, staging och produktion, konfigurerar du Dynamic Media-Cloud Services för var och en av dessa miljöer.

## Arkitekturdiagram över Dynamic Media - Scene7-läge {#architecture-diagram-of-dynamic-media-scene-mode}

I följande arkitekturdiagram beskrivs hur läget Dynamic Media - Scene7 fungerar.

Med den nya arkitekturen ansvarar Experience Manager för de viktigaste källresurserna och synkningarna med Dynamic Media för bearbetning och publicering av mediefiler:

1. När den primära källresursen överförs till Experience Manager replikeras den till Dynamic Media. Då hanterar Dynamic Media all bearbetning och generering av resurser, till exempel videokodning och dynamiska varianter av en bild.
(I Dynamic Media - Scene7-läge är standardstorleken för överföring 2 GB eller mindre. Information om hur du aktiverar uppladdning av filstorlekar på 2 GB upp till 15 GB finns i [(Valfritt) Konfigurera Dynamic Media - Scene7-läge för överföring av resurser som är större än 2 GB](#optional-config-dms7-assets-larger-than-2gb).)
1. När återgivningarna har genererats kan Experience Manager på ett säkert sätt komma åt och förhandsgranska Dynamic Media-fjärråtergivningarna (inga binärfiler skickas tillbaka till Experience Manager-instansen).
1. När innehållet är klart att publiceras och godkännas utlöses Dynamic Media-tjänsten att skicka ut innehåll till leveransservrar och cachelagra innehåll på leveransnätverket.

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>Följande funktionslista kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager - Dynamic Media. Andra anpassade CDN stöds inte med dessa funktioner.
>
>* [Smart bildbehandling](/help/assets/imaging-faq.md)
>* [Cacheogiltigförklaring](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Hotlänksskydd](/help/assets/hotlink-protection.md)
>* [HTTP/2-leverans av innehåll](/help/assets/http2.md)
>* URL-omdirigering på CDN-nivå
>* Akamai ChinaCDN (för optimal leverans i Kina)


## Aktivera Dynamic Media i Scene7-läge {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) är inaktiverat som standard. Om du vill utnyttja Dynamic Media funktioner måste du aktivera dem.

>[!WARNING]
>
>Dynamic Media - Scene7 *Endast författarinstans i Experience Manager*. Därför måste du konfigurera `runmode=dynamicmedia_scene7` på Experience Manager Author-instansen, *not* Experience Manager Publish-instansen.

Aktivera Dynamic Media genom att starta Experience Manager med `dynamicmedia_scene7` körningsläge från kommandoraden genom att ange följande i ett terminalfönster (den exempelport som används är 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Valfritt) Migrera förinställningar och konfigurationer för Dynamic Media från 6.3 till 6.5 nolltid {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Uppgradering av Experience Manager Dynamic Media från 6.3 till 6.4 eller 6.5 innefattar nu möjligheten till driftsättning utan driftstopp. Migrera alla förinställningar och konfigurationer från `/etc` till `/conf` i CRXDE Lite, se till att du kör följande kommando.

>[!NOTE]
>
>Om du kör Experience Manager-instansen i kompatibilitetsläge, d.v.s. har kompatibilitetspaketet installerat, behöver du inte köra dessa kommandon.

För alla uppgraderingar, antingen med eller utan kompatibilitetspaketet, kan du kopiera de förinställningar för visningsprogram som ursprungligen ingick i Dynamic Media genom att köra följande kommando för Linux®-kurva:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Migrera anpassade förinställningar och konfigurationer för visningsprogram som du har skapat från `/etc` till `/conf`kör du följande Linux®-kommando:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installera funktionspaket 18912 för migrering av gruppresurser {#installing-feature-pack-for-bulk-asset-migration}

Installation av funktionspaket 18912 är *valfri*.

Med funktionspaketet 18912 kan du antingen importera resurser gruppvis via FTP eller migrera resurser från antingen Dynamic Media - hybrid- eller Dynamic Media Classic till Dynamic Media - Scene7-läge på Experience Manager. Det finns på [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Se [Installera funktionspaket 18912 för migrering av gruppresurser](/help/assets/bulk-ingest-migrate.md) för mer information.

## Skapa en Dynamic Media-konfiguration i Cloud Services {#configuring-dynamic-media-cloud-services}

**Innan du konfigurerar Dynamic Media** - När du har fått ditt e-postmeddelande med Dynamic Media-autentiseringsuppgifter måste du öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media Cloud Service har rätt autentiseringsuppgifter.

![dynamicmediaconfiguration2uppdaterad](assets/dynamicmediaconfiguration2updated.png)

**Så här skapar du en Dynamic Media-konfiguration i Cloud Services:**

1. I läget Experience Manager Author väljer du logotypen Experience Manager för att komma åt den globala navigeringskonsolen, väljer ikonen Tools och går sedan till **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** (markera inte mappikonen till vänster om **[!UICONTROL global]**) och sedan väljer **[!UICONTROL Create]**.
1. På **[!UICONTROL Create Dynamic Media Configuration]** anger du en titel, e-postadress för Dynamic Media-kontot, lösenord och väljer sedan region. Den här informationen tillhandahålls av Adobe i e-postmeddelandet om etablering. Kontakta Adobe kundsupport om du inte fått e-postmeddelandet.

   Välj **[!UICONTROL Connect to Dynamic Media]**.

   >[!NOTE]
   **RICK: BEHÅLL DIG SOM DET ÄR?** När du har fått ditt e-postmeddelande med Dynamic Media-autentiseringsuppgifter öppnar du [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media Cloud Service har rätt autentiseringsuppgifter.

1. Ange följande när anslutningen lyckas. Rubriker med asterisk (*) krävs:

   * **[!UICONTROL Company]** - namnet på Dynamic Media-kontot. Du har flera Dynamic Media-konton. Du kan till exempel ha olika undervarumärken, divisioner, mellanlagrings- eller produktionsmiljöer.

   * **[!UICONTROL Company Root Folder Path]**

   * **[!UICONTROL Publishing Assets]** - Du kan välja mellan följande tre alternativ:
      * **[!UICONTROL Immediately]** betyder att när resurser överförs, importeras resurserna och URL:en/inbäddningen anges omedelbart. Ingen användaråtgärd krävs för att publicera resurser.
      * **[!UICONTROL Upon Activation]** betyder att du måste publicera resursen explicit innan en URL/Embed-länk anges.<br><!-- CQDOC-17478, Added March 9, 2021-->Från och med Experience Manager 6.5.8 återspeglar Experience Manager Publish-instansen Dynamic Media exakta metadatavärden, som `dam:scene7Domain` och `dam:scene7FileStatus` in **[!UICONTROL Upon Activation]** endast publiceringsläget. Om du vill aktivera den här funktionen installerar du Service Pack 8 och startar sedan om Experience Manager. Gå till Sling Config Manager. Hitta konfigurationen för `Scene7ActivationJobConsumer Component` eller skapa en ny). Markera kryssrutan **[!UICONTROL Replicate Metadata after Dynamic Media publishing]** väljer **[!UICONTROL Save]**.

         ![Replikera metadata efter Dynamic Media publicering, kryssruta](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Selective Publish]** Med det här alternativet kan du styra vilka mappar som ska publiceras i Dynamic Media. Du kan använda funktioner som smart beskärning eller dynamiska återgivningar, eller avgöra vilka mappar som publiceras exklusivt i Experience Manager för förhandsgranskning. Samma tillgångar *not* som publicerats i Dynamic Media för att distribueras offentligt.<br>Du kan ange det här alternativet här i dialogrutan **[!UICONTROL Dynamic Media Cloud Configuration]** eller om du vill kan du välja att ange det här alternativet på mappnivå, i en mapps **[!UICONTROL Properties]**.<br>Se [Arbeta med selektiv publicering i Dynamic Media](/help/assets/selective-publishing.md).<br>Om du senare ändrar den här konfigurationen, eller ändrar den senare på mappnivå, påverkar ändringarna bara nya resurser som du överför från den punkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från **[!UICONTROL Quick Publish]** eller **[!UICONTROL Manage Publication]** -dialogrutan.
   * **[!UICONTROL Secure Preview Server]** - gör att du kan ange URL-sökvägen till förhandsgranskningsservern för säkra återgivningar. Det innebär att när återgivningarna har genererats kan Experience Manager på ett säkert sätt komma åt och förhandsgranska Dynamic Media-fjärråtergivningarna (inga binärfiler skickas tillbaka till Experience Manager-instansen).
Om du inte har en särskild lösning för att använda ditt företags server eller en speciell server rekommenderar Adobe att du låter den här inställningen vara angiven.

   * **[!UICONTROL Sync all content]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Markerad som standard. Avmarkera det här alternativet om du vill inkludera eller exkludera resurser från synkroniseringen till Dynamic Media. Om du avmarkerar det här alternativet kan du välja mellan följande två synkroniseringslägen för Dynamic Media:

   * **[!UICONTROL Dynamic Media sync mode]**
      * **[!UICONTROL Enabled by default]** - Konfigurationen används som standard på alla mappar såvida du inte markerar en mapp som är exkluderad. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Disabled by default]** - Konfigurationen tillämpas inte på någon mapp förrän du uttryckligen markerar en markerad mapp för synkronisering till Dynamic Media.
Om du vill markera en markerad mapp för synkronisering till Dynamic Media väljer du en resursmapp och sedan väljer du **[!UICONTROL Properties]**. På **[!UICONTROL Details]** -fliken, i **[!UICONTROL Dynamic Media sync mode]** i den nedrullningsbara listan väljer du mellan följande tre alternativ. När du är klar väljer du **[!UICONTROL Save]**. *Kom ihåg: dessa tre alternativ är inte tillgängliga om du har valt **[!UICONTROL Sync all content]**tidigare.* Se även [Arbeta med selektiv publicering på mappnivå i Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Inherited]** - Det finns inget explicit synkroniseringsvärde i mappen; I stället ärver mappen synkroniseringsvärdet från en av de överordnade mapparna eller standardläget i molnkonfigurationen. Detaljerad status för ärvda program via ett verktygstips.
         * **[!UICONTROL Enable for subfolders]** - Inkludera allt i det här underträdet för synkronisering med Dynamic Media. De mappspecifika inställningarna åsidosätter standardläget i molnkonfigurationen.
         * **[!UICONTROL Disabled for subfolders]** - Uteslut allt i det här underträdet från synkronisering till Dynamic Media.

   >[!NOTE]
   Det finns inget stöd för versionshantering i Dynamic Media - Scene7. Dessutom gäller fördröjd aktivering endast om **[!UICONTROL Publish Assets]** på sidan Redigera Dynamic Media-konfiguration är inställd på **[!UICONTROL Upon Activation]** och då endast tills resursen aktiveras första gången.
   När en mediefil har aktiverats publiceras uppdateringar direkt till S7 Delivery.

1. Välj **[!UICONTROL Save]**.
1. Om du vill förhandsgranska Dynamic Media-innehåll på ett säkert sätt innan det publiceras måste du tillåtslista författarinstansen Experience Manager för att ansluta till Dynamic Media:

   * **RICK: LÄNKA TILL NYTT PUBLICERINGSINSTÄLLNINGSÄMNE** Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto. Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kan du kontakta Adobe kundsupport.

   * Navigera till i navigeringsfältet uppe till höger på sidan **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.

   * På sidan Image Server Publish (Publicera kontext) väljer du **[!UICONTROL Test Image Serving]**.
   * För klientadressfiltret väljer du **[!UICONTROL Add]**.
   * Markera kryssrutan om du vill aktivera (aktivera) adressen. Ange IP-adressen för Experience Manager Author-instansen (inte Dispatcher IP).
   * Välj **[!UICONTROL Save]**.

Du är nu klar med den grundläggande konfigurationen; är du redo att använda Dynamic Media - Scene7.

Om du vill anpassa konfigurationen ytterligare kan du utföra alla uppgifter under [(Valfritt) Konfigurera avancerade inställningar i Dynamic Media - Scene7-läge](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Valfritt) Konfigurera avancerade inställningar i Dynamic Media - Scene7-läge {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Om du vill anpassa konfigurationen och konfigurationen av Dynamic Media - Scene7 eller optimera prestandan ytterligare kan du göra något av följande: *valfri* uppgifter:

* [(Valfritt) Konfigurera Dynamic Media - Scene7-läge för överföring av resurser som är större än 2 GB](#optional-config-dms7-assets-larger-than-2gb)

* [(Valfritt) Installation och konfiguration av Dynamic Media - inställningar för Scene7-läge](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Valfritt) Justera prestanda för Dynamic Media - Scene7-läge](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Valfritt) Filtrera resurser för replikering](#optional-filtering-assets-for-replication)

### (Valfritt) Konfigurera Dynamic Media - Scene7-läge för överföring av resurser som är större än 2 GB {#optional-config-dms7-assets-larger-than-2gb}

I Dynamic Media - Scene7-läge är standardfilstorleken för överföring av resurser 2 GB eller mindre. Du kan dock välja att konfigurera överföring av resurser som är större än 2 GB och upp till 15 GB.

Om du tänker använda den här funktionen bör du vara medveten om följande krav och punkter:

* Du måste köra Experience Manager 6.5 med Service Pack 6.5.4.0 eller senare i Dynamic Media - Scene7-läge.
* Den här stora överföringsfunktionen stöds bara för [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) kunder.
* Kontrollera att din Experience Manager-instans är konfigurerad med Amazon S3 eller Microsoft® Azure Blob Storage.

   >[!NOTE]
   Konfigurera Azure Blob-lagringen med en åtkomstnyckel och en hemlig nyckel eftersom den här stora överföringsfunktionen inte stöds med AzureSas i Blob-lagringskonfigurationen.

* Oak&#39;s [Nedladdning av direkt binär åtkomst](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) är aktiverat (eko) *Överföring av direkt binär åtkomst* är inte obligatoriskt).

   Om du vill aktivera hämtning av direkt binär åtkomst anger du egenskapen `presignedHttpDownloadURIExpirySeconds > 0` i datalagerkonfigurationen. Värdet måste vara tillräckligt långt för att ladda ned större binärfiler och eventuellt försöka igen.

* Resurser som är större än 15 GB överförs inte. (Storleksgränsen anges i steg 8 nedan.)
* När **[!UICONTROL Dynamic Media Reprocess]** arbetsflödet för resurser aktiveras för en mapp, och stora resurser som redan är synkroniserade med Dynamic Media-företaget bearbetas om. Om stora resurser ännu inte har synkroniserats i mappen överförs inte resursen. Om du vill synkronisera stora resurser i Dynamic Media kan du därför köra **[!UICONTROL Dynamic Media Reprocess]** arbetsflöde för resurser på enskilda resurser.

**Så här konfigurerar du Dynamic Media - Scene7-läge för överföring av resurser som är större än 2 GB:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och navigerar sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. Gör något av följande i fönstret CRXDE Lite:

   * Navigera till följande sökväg i den vänstra listen:

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Kopiera och klistra in banan ovanför i fältet CRXDE Lite under verktygsfältet och tryck sedan på `Enter`.

1. Högerklicka på `fileupload`väljer du **[!UICONTROL Overlay Node]**.

   ![Alternativet Täcka över nod](/help/assets/assets-dm/uploadassets15gb_a.png)

1. I dialogrutan Overlay Node väljer du **[!UICONTROL Match Node Types]** kryssruta för att aktivera (aktivera) alternativet och sedan markera **[!UICONTROL OK]**.

   ![Dialogrutan Overlay Node](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Gör något av följande i fönstret CRXDE Lite:

   * Navigera till följande nodsökväg för övertäckning i den vänstra listen:

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Kopiera och klistra in banan ovanför i fältet CRXDE Lite under verktygsfältet och tryck sedan på `Enter`.

1. I **[!UICONTROL Properties]** -fliken, under **[!UICONTROL Name]** kolumn, leta upp `sizeLimit`.
1. Till höger om `sizeLimit` namn, under **[!UICONTROL Value]** dubbelklicka på värdefältet.
1. Ange lämpligt värde i byte så att du kan öka storleksgränsen till den önskade överföringsstorleken. Om du till exempel vill öka storleken på överföringsresursen till 10 GB anger du `10737418240` i värdefältet.
Du kan ange ett värde på upp till 15 GB (`2013265920` byte). I det här fallet överförs inte överförda resurser som är större än 15 GB.

   ![Gränsvärde för storlek](/help/assets/assets-dm/uploadassets15gb_c.png)

1. I närheten av det övre vänstra hörnet av CRXDE Lite-fönstret väljer du **[!UICONTROL Save All]**.

   *Ange nu tidsgränsen för arbetsflödets hanterare för externa processer i Adobe Granite genom att göra följande:*

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen.
1. Gör något av följande:

   * Navigera till följande URL-sökväg:

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Kopiera och klistra in sökvägen ovanför i URL-fältet i webbläsaren. Se till att ersätta `localhost:4502` med din egen Experience Manager-instans.

1. I **[!UICONTROL Adobe Granite Workflow External Process Job Handler]** i **[!UICONTROL Max Timeout]** fält, ange värdet till `18000` minuter (fem timmar). Standardvärdet är 1 0800 minuter (tre timmar).

   ![Högsta timeout-värde](/help/assets/assets-dm/uploadassets15gb_d.png)

1. I dialogrutans nedre högra hörn väljer du **[!UICONTROL Save]**.

   *Ange nu tidsgränsen för Scene7 Direct Binary Upload-processen genom att göra följande:*

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen.
1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. På sidan Arbetsflödesmodeller väljer du **[!UICONTROL Dynamic Media Encode Video]**.
1. I verktygsfältet väljer du **[!UICONTROL Edit]**.
1. Dubbelklicka på arbetsflödessidan **[!UICONTROL Scene7 Direct Binary Upload]** processteg.
1. I **[!UICONTROL Step Properties]** dialogrutan, under **[!UICONTROL Common]** -fliken, under **[!UICONTROL Advanced Settings]** rubrik, i **[!UICONTROL Timeout]** fält, ange ett värde för `18000` minuter (fem timmar). Standardvärdet är `3600` minuter (en timme).
1. Välj **[!UICONTROL OK]**.
1. Välj **[!UICONTROL Sync]**.
1. Upprepa steg 14-21 för **[!UICONTROL DAM Update Asset]** arbetsflödesmodell och **[!UICONTROL Dynamic Media Reprocess]** arbetsflödesmodell.

### (Valfritt) Installation och konfiguration av Dynamic Media - inställningar för Scene7-läge {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [Konfigurera Dynamic Media Publish Setup för Image Server](/help/assets/dm-publish-settings.md)
* [Konfigurera allmänna inställningar för Dynamic Media](/help/assets/dm-general-settings.md)
* [Konfigurera färghantering](#configuring-color-management)
* [Redigera MIME-typer för format som stöds](#editing-mime-types-for-supported-formats)
* [Lägg till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats)
* [Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (klart i Dynamic Media Classic användargränssnitt)

#### Konfigurera Dynamic Media Publish Setup för Image Server {#publishing-setup-for-image-server}

På sidan Dynamic Media Publish Setup (Publiceringsinställningar) anges standardinställningar som avgör hur resurser levereras från Adobe Dynamic Media-servrar till webbplatser eller program.

Se [Konfigurera Dynamic Media Publish Setup för Image Server](/help/assets/dm-publish-settings.md).

#### Konfigurera allmänna inställningar för Dynamic Media {#configuring-application-general-settings}

Konfigurera standardfärgegenskaperna så att färgkorrigering aktiveras när bilder begärs.

Se [Konfigurera allmänna inställningar för Dynamic Media](/help/assets/dm-general-settings.md).

#### Konfigurera färghantering {#configuring-color-management}

Med Dynamic Media färghantering kan du färgkorrigera resurser. Med färgkorrigering behåller inkapslade resurser sin färgmodell (RGB, CMYK, Grå) och inbäddad färgprofil. När du begär en dynamisk återgivning korrigeras bildfärgen till målfärgrymden med hjälp av CMYK-, RGB- eller grå utdata.

Se [Konfigurera bildförinställningar](/help/assets/managing-image-presets.md).

>[!NOTE]
Som standard visas 15 renderingar när du väljer **[!UICONTROL Renditions]** och 15 visningsförinställningar när du väljer **[!UICONTROL Viewers]** i resursens detaljvy. Du kan öka den här gränsen. Se [Öka antalet bildförinställningar som visas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) eller [Öka antalet visningsförinställningar som visas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Redigera MIME-typer för format som stöds {#editing-mime-types-for-supported-formats}

Du kan definiera vilka resurstyper som bearbetas av Dynamic Media och anpassa avancerade parametrar för resurshantering. Du kan till exempel ange parametrar för tillgångsbearbetning för att göra följande:

* Konvertera en Adobe PDF till en eCatalog-resurs.
* Konvertera ett Adobe Photoshop-dokument (.PSD) till en bannermallsresurs för personalisering.
* Rastrera en Adobe Illustrator-fil (.AI) eller en Adobe Photoshop Encapsulated PostScript®-fil (.EPS).
* [Videoprofiler](/help/assets/video-profiles.md) och [Bildprofiler](/help/assets/image-profiles.md) kan användas för att definiera bearbetning av videoklipp och bilder.

Se [Överför resurser](/help/assets/manage-assets.md#uploading-assets).

**Så här redigerar du MIME-typer för de format som stöds:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och navigerar sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. Navigera till följande i den vänstra listen:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME-typer](assets/mimetypes.png)

1. Välj en mime-typ i mappen mimeTypes.
1. Till höger på CRXDE Lite-sidan i den nedre delen:

   * Dubbelklicka på **[!UICONTROL enabled]** fält. Som standard är alla resursens MIME-typer aktiverade (inställda på **[!UICONTROL true]**), vilket innebär att resurserna synkroniseras till Dynamic Media för bearbetning. Om du vill utesluta den här resursens MIME-typ från bearbetningen ändrar du den här inställningen till **[!UICONTROL false]**.

   * Dubbelknacka **[!UICONTROL jobParam]** för att öppna det tillhörande textfältet. Se [MIME-typer som stöds](/help/assets/assets-formats.md#supported-mime-types) för en lista över tillåtna värden för bearbetningsparametrar som du kan använda för en viss MIME-typ.

1. Gör något av följande:

   * Upprepa steg 3-4 för att redigera fler MIME-typer.
   * På menyraden på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.

1. I det övre vänstra hörnet på sidan väljer du **[!UICONTROL CRXDE Lite]** för att återvända till Experience Manager.

#### Lägga till MIME-typer för format som inte stöds {#adding-mime-types-for-unsupported-formats}

Du kan lägga till anpassade MIME-typer för format som inte stöds i Experience Manager Assets. Se till att alla nya noder som du lägger till i CRXDE Lite inte tas bort av Experience Manager genom att flytta MIME-typen före `image_`. Kontrollera också att dess aktiverade värde är inställt på **[!UICONTROL false]**.

**Så här lägger du till MIME-typer för format som inte stöds:**

1. Navigera från Experience Manager till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. En ny flik i webbläsaren öppnas **[!UICONTROL Adobe Experience Manager Web Console Configuration]** sida.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. På sidan bläddrar du nedåt till namnet *Adobe CQ Scene7 Asset MIME type Service* enligt följande skärmbild. Till höger om namnet väljer du **[!UICONTROL Edit the configuration values]** (pennikon).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. På **Adobe CQ Scene7 Asset MIME Type Service** väljer du en plusteckenikon &lt;+>. Platsen i tabellen där du väljer plustecknet för att lägga till den nya mime-typen är enkel.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Typ `DWG=image/vnd.dwg` i det tomma textfältet som du just lade till.

   Exemplet `DWG=image/vnd.dwg` endast för demonstrationsändamål. MIME-typen som du lägger till här kan vara ett annat format som inte stöds.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Välj **[!UICONTROL Save]**.

   Nu kan du stänga webbläsarfliken som har den öppna konfigurationssidan för Adobe Experience Manager Web Console.

1. Gå tillbaka till webbläsarfliken som har din öppna Experience Manager-konsol.
1. Navigera från Experience Manager till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Navigera till följande i den vänstra listen:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Dra MIME-typen `image_vnd.dwg` och släpp det direkt ovanför `image_` i trädet enligt följande skärmbild.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Med mime-typen `image_vnd.dwg` fortfarande markerad, från **[!UICONTROL Properties]** -fliken, i **[!UICONTROL enabled]** rad, under **[!UICONTROL Value]** kolumnrubrik, dubbeltryck på värdet för att öppna **[!UICONTROL Value]** nedrullningsbar lista.
1. Typ `false` i fältet (eller markera **[!UICONTROL false]** från listrutan).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. I närheten av det övre vänstra hörnet på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.

#### Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Använd förinställningar för gruppuppsättningar för att automatisera skapandet av bilduppsättningar eller snurra uppsättningar medan resurserna överförs till Dynamic Media.

Definiera först namnkonventionen för hur resurser grupperas i en uppsättning. Skapa sedan en förinställning för gruppuppsättning som är en unik, självständig uppsättning instruktioner. Det måste definiera hur uppsättningen ska skapas med bilder som matchar de definierade namnkonventionerna i förinställningsreceptet.

När du överför filer skapar Dynamic Media automatiskt en uppsättning med alla filer som matchar den definierade namnkonventionen i de aktiva förinställningarna.

##### Konfigurera standardnamn

Skapa en standardnamnkonvention som används i alla förinställda gruppuppsättningar. Den standardnamnkonvention som valts i definitionen av gruppuppsättningsförinställningen är troligen allt som ditt företag behöver för att gruppgenerera uppsättningar. En gruppuppsättningsförinställning skapas för att använda den standardnamnkonvention som du definierar. Du kan skapa så många gruppuppsättningsförinställningar med alternativa, anpassade namnkonventioner som behövs för en viss uppsättning innehåll om det finns ett undantag från den företagsdefinierade standardnamngivningen.

När det inte krävs någon standardnamnkonvention för att använda funktionen för gruppuppsättningsförinställningar bör du använda standardnamnkonventionen. Här kan du definiera så många element i namnkonventionen som du vill gruppera i en uppsättning så att du kan effektivisera skapandet av gruppuppsättningar.

Du kan också använda **[!UICONTROL View Code]** utan formulärfält tillgängliga. I den här vyn skapar du namnkonventionens definitioner helt med hjälp av reguljära uttryck.

Det finns två element för definition, Matcha och Basnamn. Med dessa fält kan du definiera alla element i en namnkonvention och identifiera den del av konventionen som används för att namnge den uppsättning i vilken de finns. Ett företags namnkonvention använder ofta en eller flera definitionsrader för vart och ett av dessa element. Du kan använda så många rader för din unika definition och gruppera dem i distinkta element, t.ex. för Huvudbild, Färgelement, Alternativa vyer och Färgruteelement.

**Så här konfigurerar du standardnamn:**

1. Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kan du kontakta Adobe kundsupport.

1. Navigera i navigeringsfältet nära sidans överkant till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Default Naming]**.
1. Välj **[!UICONTROL View Form]** eller **[!UICONTROL View Code]** för att ange hur du vill visa och ange information om varje element.

   Du kan välja **[!UICONTROL View Code]** om du vill visa värdeuppbyggnaden för reguljära uttryck tillsammans med dina formulärval. Du kan ange eller ändra dessa värden för att underlätta definitionen av elementen i namnkonventionen, om formulärvyn begränsar dig av någon anledning. Om dina värden inte kan tolkas i formulärvyn blir formulärfälten inaktiva.

   >[!NOTE]
   Inaktiverade formulärfält verifierar inte att reguljära uttryck är korrekta. Resultaten av det reguljära uttryck som du skapar för varje element efter resultatraden visas. Det fullständiga reguljära uttrycket visas längst ned på sidan.

1. Expandera varje element efter behov och ange de namnkonventioner som du vill använda.
1. Gör något av följande om det behövs:

   * Välj **[!UICONTROL Add]** om du vill lägga till en annan namnkonvention för ett element.
   * Välj **[!UICONTROL Remove]** om du vill ta bort en namnkonvention för ett element.

1. Gör något av följande:

   * Välj **[!UICONTROL Save As]** och ange ett namn för förinställningen.
   * Välj **[!UICONTROL Save]** om du redigerar en befintlig förinställning.

##### Skapa en förinställning för gruppuppsättning



I Dynamic Media används gruppuppsättningsförinställningar för att ordna resurser i uppsättningar med bilder (alternativa bilder, färgalternativ, 360 rotationer) för visning i visningsprogram. Förinställningarna för gruppuppsättningar körs automatiskt tillsammans med överföringsprocesserna för resurser i Dynamic Media.

Du kan skapa, redigera och hantera dina gruppuppsättningsförinställningar. Det finns två former av förinställda gruppuppsättningsdefinitioner: en för en standardnamnkonvention som du kan konfigurera och en för anpassade namnkonventioner som du skapar direkt.

Du kan antingen använda formulärfältsmetoden för att definiera en gruppuppsättningsförinställning eller kodmetoden, som gör att du kan använda reguljära uttryck. Precis som i Standardnamn kan du välja Visa kod samtidigt som du definierar i formulärvyn och använda reguljära uttryck för att skapa definitioner. Du kan också avmarkera en vy om du vill använda den ena eller den andra enbart.

**Så här skapar du en förinställning för gruppuppsättning:**

1. Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kan du kontakta Adobe kundsupport.

1. Navigera i navigeringsfältet nära sidans överkant till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Batch Set Preset]**.

   **[!UICONTROL View Form]**, som anges i det övre högra hörnet på detaljsidan, är standardvyn.

1. På panelen Förinställningslista väljer du **[!UICONTROL Add]** om du vill aktivera definitionsfälten på panelen Detaljer till höger på skärmen.
1. Skriv ett namn på förinställningen i fältet Förinställningsnamn på panelen Detaljer.
1. Välj en förinställningstyp i listrutan Gruppuppsättningstyp.
1. Gör något av följande:

   * Om du använder en standardnamnkonvention som du tidigare ställt in under **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Default Naming]**, expandera **[!UICONTROL Asset Naming Conventions]** och sedan i listrutan Namnge filer väljer du **[!UICONTROL Default]**.

   * Om du vill definiera en ny namnkonvention när du ställer in förinställningen expanderar du **[!UICONTROL Asset Naming Conventions]** och sedan i listrutan Namnge filer väljer du **[!UICONTROL Custom]**.

1. I Sekvensordning definierar du i vilken ordning bilderna ska visas efter att uppsättningen har grupperats i Dynamic Media.

   Som standard sorteras dina resurser alfanumeriskt. Du kan dock använda en kommaavgränsad lista med reguljära uttryck för att definiera ordningen.

1. Ange suffixet eller prefixet till basnamnet som du definierade i konventionen om namngivning av tillgångar för Ange namngivning och skapande. Ange också var uppsättningen ska skapas i mappstrukturen för Dynamic Media.

   Om du definierar ett stort antal uppsättningar ska uppsättningarna hållas åtskilda från de mappar som innehåller själva resurserna. Skapa till exempel en mapp för bilduppsättningar och placera genererade uppsättningar här.

1. På panelen Detaljer väljer du **[!UICONTROL Save]**.
1. Välj **[!UICONTROL Active]** bredvid den nya förinställningens namn.

   När du aktiverar förinställningen används den för att generera uppsättningen när du överför resurser till Dynamic Media.

##### Skapa en gruppuppsättningsförinställning för automatisk generering av en 2D-snurpuppsättning

Du kan använda gruppuppsättningstypen **[!UICONTROL Multi-Axis Spin Set]** för att skapa ett recept som automatiserar genereringen av tvådimensionella snurruppsättningar. Vid gruppering av bilder används reguljära uttryck för rad och kolumn så att bildresurserna justeras korrekt på motsvarande plats i den flerdimensionella arrayen. Det finns inget minsta eller högsta antal rader eller kolumner som du måste ha i en rotationsuppsättning med flera axlar.

Anta till exempel att du vill skapa en fleraxelsnurra med namnet `spin-2dspin`. Du har en uppsättning bilder med snurra uppsättningar som innehåller tre rader, med 12 bilder per rad. Bilderna får följande namn:

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

Gruppering för den delade resursnamndelen i rotationsuppsättningen läggs till i **[!UICONTROL Match]** fält (markerat). Variabeldelen av resursnamnet som innehåller raden och kolumnen läggs till i **[!UICONTROL Row]** och **[!UICONTROL Column]** fält.

När snurruppsättningen överförs och publiceras aktiverar du namnet på det tvådimensionella snurrreceptet som visas under **[!UICONTROL Batch Set Presets]** i **[!UICONTROL Upload Job Options]** -dialogrutan.

**Så här skapar du en gruppuppsättningsförinställning för automatisk generering av en 2D-snurpuppsättning:**

1. Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto.

   Dina autentiseringsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kan du kontakta Adobe kundsupport.

1. Navigera i navigeringsfältet nära sidans överkant till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Batch Set Preset]**.

   **[!UICONTROL View Form]**, som anges i det övre högra hörnet på detaljsidan, är standardvyn.

1. På panelen Förinställningslista väljer du **[!UICONTROL Add]** om du vill aktivera definitionsfälten på panelen Detaljer till höger på skärmen.
1. Skriv ett namn på förinställningen i fältet Förinställningsnamn på panelen Detaljer.
1. I listrutan Gruppuppsättningstyp väljer du **[!UICONTROL Asset Set]**.
1. I listrutan Undertyp väljer du **[!UICONTROL Multi-Axis Spin Set]**.
1. Expandera **[!UICONTROL Asset Naming Conventions]** och sedan i listrutan Namnge filer väljer du **[!UICONTROL Custom]**.
1. Använd attributen **[!UICONTROL Match]** och eventuellt **[!UICONTROL Base Name]** för att definiera ett reguljärt uttryck för namngivning av bildresurser som utgör grupperingen.

   Det reguljära uttrycket för literal Match kan till exempel se ut så här:

   `(w+)-w+-w+`

1. Expandera **[!UICONTROL Row Column Position]** och definierar sedan namnformatet för bildresursens position i 2D-rotationsmatrisen.

   Använd parentesen för att omsluta rad- eller kolumnpositionen i filnamnet.

   För en rad med ett reguljärt uttryck kan det se ut så här:

   `\w+-R([0-9]+)-\w+`

   eller

   `\w+-(\d+)-\w+`

   För det reguljära uttrycket i kolumnen kan det se ut så här:

   `\w+-\w+-C([0-9]+)`

   eller

   `\w+-\w+-C(\d+)`

   Proverna ovan är endast avsedda som exempel. Du kan skapa det reguljära uttrycket hur du vill.

   >[!NOTE]
   Om kombinationen av reguljära uttryck för rader och kolumner inte kan avgöra positionen för resursen i den flerdimensionella rotationsinställningsarrayen, läggs resursen inte till i uppsättningen. Ett fel loggas också.

1. Ange suffixet eller prefixet till basnamnet som du definierade i konventionen om namngivning av tillgångar för Ange namngivning och skapande.

   Du kan även definiera var rotationsuppsättningen skapas i mappstrukturen för Dynamic Media Classic.

   Om du definierar ett stort antal uppsättningar ska uppsättningarna hållas åtskilda från de mappar som innehåller själva resurserna. Du kan till exempel skapa en mapp för snurruppsättningar där du kan placera genererade uppsättningar här.

1. På panelen Detaljer väljer du **[!UICONTROL Save]**.
1. Välj **[!UICONTROL Active]** bredvid den nya förinställningens namn.

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

Adobe rekommenderar att du använder följande &quot;justerade&quot; jobbparametrar för PDF, PostScript® och PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Filtyp | Rekommenderade jobbparametrar |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Om du vill uppdatera någon av de här parametrarna följer du stegen i [Aktivera stöd för MIME-typbaserade resurser/Dynamic Media Classic överföringsjobbparametrar](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Uppdatera den tillfälliga arbetsflödeskön för Granite {#updating-the-granite-transient-workflow-queue}

Kön för Bevilja övergång används för **[!UICONTROL DAM Update Asset]** arbetsflöde. I Dynamic Media används den för bildhantering.

**Så här uppdaterar du den tillfälliga arbetsflödeskön för Granite:**

1. Navigera till [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) och söka efter **Kö: Bevilja tillfällig arbetsflödeskö**.

   >[!NOTE]
   En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I **[!UICONTROL Maximum Parallel Jobs]** ändrar du talet till önskat värde.

   Du kan öka **[!UICONTROL Maximum Parallel Jobs]** för att ge adekvat stöd för överföring av stora mängder filer till Dynamic Media. Det exakta värdet beror på maskinvarukapaciteten. I vissa scenarier, d.v.s. en inledande migrering eller en massöverföring som görs en gång, kan du använda ett stort värde. Tänk dock på att användning av ett stort värde (till exempel två gånger antalet kärnor) kan ha negativa effekter på andra samtidiga aktiviteter. Testa och justera värdet utifrån ditt specifika användningsfall.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Välj **[!UICONTROL Save]**.

#### Uppdatera arbetsflödeskön för Granite {#updating-the-granite-workflow-queue}

Beviljad arbetsflödeskö används för icke-tillfälliga arbetsflöden. I Dynamic Media bearbetar man video med **[!UICONTROL Dynamic Media Encode Video]** arbetsflöde.

**Så här uppdaterar du arbetsflödeskön för Granite:**

1. Navigera till `https://<server>/system/console/configMgr` och söka efter **Kö: Begränsa arbetsflödeskö**.

   >[!NOTE]
   En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I **[!UICONTROL Maximum Parallel Jobs]** ändrar du talet till önskat värde.

   Du kan öka det maximala antalet parallella jobb för att få tillräckligt stöd för överföring av filer till Dynamic Media. Det exakta värdet beror på maskinvarukapaciteten. I vissa scenarier, d.v.s. en inledande migrering eller en massöverföring som görs en gång, kan du använda ett stort värde. Tänk dock på att användning av ett stort värde (till exempel två gånger antalet kärnor) kan ha negativa effekter på andra samtidiga aktiviteter. Testa och justera värdet utifrån ditt specifika användningsfall.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Välj **[!UICONTROL Save]**.

#### Uppdatera Dynamic Media Classic överföringsanslutning {#updating-the-scene-upload-connection}

Inställningen Scene7 Upload Connection synkroniserar Experience Manager-resurser med Dynamic Media Classic-servrar.

**Så här uppdaterar du Dynamic Media Classic överföringsanslutning:**

1. Navigera till `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. I **[!UICONTROL Number of connections]** fält och/eller **[!UICONTROL Active job timeout]** ändrar du talet.

   The **[!UICONTROL Number of connections]** Inställningen styr det högsta tillåtna antalet HTTP-anslutningar för överföring från Experience Manager till Dynamic Media. vanligtvis räcker det fördefinierade värdet på tio anslutningar.

   The **[!UICONTROL Active job timeout]** inställningen avgör väntetiden för överförda Dynamic Media-resurser som ska publiceras på leveransservern. Det här värdet är som standard 2 100 sekunder eller 35 minuter.

   I de flesta fall räcker det med inställningen 2 100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Välj **[!UICONTROL Save]**.

### (Valfritt) Filtrera resurser för replikering {#optional-filtering-assets-for-replication}

I distributioner som inte är från Dynamic Media replikerar du *alla* resurser (både bilder och video) från Experience Manager-redigeringsmiljön till Experience Manager-publiceringsnoden. Det här arbetsflödet är nödvändigt eftersom publiceringsservrarna i Experience Manager också levererar resurserna.

I Dynamic Media-distributioner finns det dock inget behov av att replikera samma resurser till publiceringsnoderna i Experience Manager eftersom resurserna levereras via Cloud Servicen. Ett sådant&quot;hybridpubliceringsarbetsflöde&quot; undviker extra lagringskostnader och längre bearbetningstider för att replikera resurser. Annat innehåll, t.ex. webbplatssidor, fortsätter att hanteras från Experience Manager-publiceringsnoderna.

Med filtren kan du *exclude* resurser från att replikeras till publiceringsnoden Experience Manager.

#### Använd standardfiltren för replikering {#using-default-asset-filters-for-replication}

Om du använder Dynamic Media för bilder, video eller båda, kan du använda standardfiltren som finns i Adobe. Följande filter är aktiva som standard:

|  | Filter | Mime-typ | Återgivningar |
| --- | --- | --- | --- |
| Dynamic Media Image Delivery | filter-image<br>filteruppsättningar | Börjar med **bild/**<br> Innehåller **program/** och avsluta med **set**. | De färdiga filterbilderna (gäller för enstaka bildresurser, inklusive interaktiva bilder) och &quot;filteruppsättningar&quot; (gäller Spin Sets, Image Sets, Mixed Media Sets och Carousel Sets) kommer att<br>・ Exkludera originalbilden och statiska bildåtergivningar från replikering. |
| Dynamic Media Video Delivery | filter-video | Börjar med **video/** | &quot;Filtrera video&quot; som är färdig att användas:<br>・ Exkludera originalvideon och statiska miniatyrrenderingar från replikering. |

>[!NOTE]
Filter gäller för MIME-typer och kan inte vara sökvägsspecifika.

#### Anpassa resursfilter för replikering {#customizing-asset-filters-for-replication}

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och navigera till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. I det vänstra mappträdet navigerar du till `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` för att granska filtren.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Du definierar Mime-typen för filtret genom att leta reda på Mime-typen enligt följande:

   Expandera i den vänstra listen `content > dam > <locate_your_asset> > jcr:content > metadata`och sedan i tabellen letar du reda på `dc:format`.

   Följande bild är ett exempel på en resurs sökväg till `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observera att `dc:format` för tillgången `Fiji Red.jpg` är `image/jpeg`.

   Om du vill att det här filtret ska gälla för alla bilder, oavsett format, anger du värdet till `image/*` där `*` är ett reguljärt uttryck som används på alla bilder i alla format.

   Om du bara vill att filtret ska gälla för bilder av typen JPEG anger du värdet `image/jpeg`.

1. Definiera vilka renderingar du vill inkludera eller exkludera från replikering.

   Följande tecken kan användas för att filtrera replikering:

   | Tecken som ska användas | Så här filtrerar du resurser för replikering |
   | --- | --- |
   | * | Jokertecken |
   | + | Innehåller resurser för replikering |
   | - | Exkluderar resurser från replikering |

   Navigera till `content/dam/<locate your asset>/jcr:content/renditions`.

   Följande grafik är ett exempel på en resurs återgivningar.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   Om du bara vill replikera originalet skriver du `+original`.
