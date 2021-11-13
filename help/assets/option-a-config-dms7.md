---
title: Alternativ A - Konfigurera Dynamic Media - Scene7-läge
description: Lär dig hur du konfigurerar läget Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: b6000516b88342d6abf8072623cfece43e2ba19d
workflow-type: tm+mt
source-wordcount: '10874'
ht-degree: 1%

---

# Alternativ A - Konfigurera Dynamic Media - Scene7-läge{#configuring-dynamic-media-scene-mode}

>[!NOTE]
>
>ALTERNATIV A - DE TVÅ NYA ÄMNEN SOM JAG SKRIVER TAS BORT. MEN INNAN DU TAR BORT ÄMNENA FLYTTADES ALLT DERAS INNEHÅLL TILL DETTA ÄMNE, TILL RESPEKTIVE OMRÅDE DÄR JAG REDAN PRATAR OM ALLMÄNNA INSTÄLLNINGAR OCH PUBLICERINGSINSTÄLLNINGAR.

Om du använder Adobe Experience Manager för olika miljöer, som utveckling, staging och produktion, konfigurerar du Dynamic Media-Cloud Services för var och en av dessa miljöer.

## Arkitekturdiagram över Dynamic Media - Scene7-läge {#architecture-diagram-of-dynamic-media-scene-mode}

**RICK: BEHÅLL SOM DET ÄR**

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

**RICK: BEHÅLL SOM DET ÄR**

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) är inaktiverat som standard. Om du vill utnyttja Dynamic Media funktioner måste du aktivera dem.

>[!WARNING]
>
>Dynamic Media - Scene7 *Endast författarinstans i Experience Manager*. Därför måste du konfigurera `runmode=dynamicmedia_scene7` på Experience Manager Author-instansen, *not* Experience Manager Publish-instansen.

Om du vill aktivera Dynamic Media måste du starta Experience Manager med `dynamicmedia_scene7` körningsläge från kommandoraden genom att ange följande i ett terminalfönster (den exempelport som används är 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Valfritt) Migrera förinställningar och konfigurationer för Dynamic Media från 6.3 till 6.5 nolltid {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

**RICK: BEHÅLL SOM DET ÄR**

Uppgradering av Experience Manager Dynamic Media från 6.3 till 6.4 eller 6.5 innefattar nu möjligheten till driftsättning utan driftstopp. Migrera alla förinställningar och konfigurationer från `/etc` till `/conf` i CRXDE Lite, se till att du kör följande kommando.

>[!NOTE]
>
>Om du kör Experience Manager-instansen i kompatibilitetsläge, d.v.s. har kompatibilitetspaketet installerat, behöver du inte köra dessa kommandon.

För alla uppgraderingar, antingen med eller utan kompatibilitetspaketet, kan du kopiera de förinställningar för visningsprogram som ursprungligen ingick i Dynamic Media genom att köra följande kommando för Linux®-kurva:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Migrera anpassade förinställningar och konfigurationer för visningsprogram som du har skapat från `/etc` till `/conf`kör du följande Linux®-kommando:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installera funktionspaket 18912 för migrering av gruppresurser {#installing-feature-pack-for-bulk-asset-migration}

**RICK: BEHÅLL SOM DET ÄR**

Installation av funktionspaket 18912 är *valfri*.

Med funktionspaketet 18912 kan du antingen importera resurser gruppvis via FTP eller migrera resurser från antingen Dynamic Media - hybrid- eller Dynamic Media Classic till Dynamic Media - Scene7-läge på Experience Manager. Det finns på [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Se [Installera funktionspaket 18912 för migrering av gruppresurser](/help/assets/bulk-ingest-migrate.md) för mer information.

## Skapa en Dynamic Media-konfiguration i Cloud Services {#configuring-dynamic-media-cloud-services}

**RICK: BEHÅLL SOM DET ÄR**

**Innan du konfigurerar Dynamic Media** - När du har fått ditt e-postmeddelande med Dynamic Media-autentiseringsuppgifter måste du öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media Cloud Service har rätt autentiseringsuppgifter.

![dynamicmediaconfiguration2uppdaterad](assets/dynamicmediaconfiguration2updated.png)

**Så här skapar du en Dynamic Media-konfiguration i Cloud Services:**

1. I läget Experience Manager Author väljer du logotypen Experience Manager för att komma åt den globala navigeringskonsolen, väljer ikonen Tools och går sedan till **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** (markera inte mappikonen till vänster om **[!UICONTROL global]**) och sedan väljer **[!UICONTROL Create]**.
1. På **[!UICONTROL Create Dynamic Media Configuration]** anger du en titel, e-postadress för Dynamic Media-kontot, lösenord och väljer sedan region. Den här informationen tillhandahålls av Adobe i e-postmeddelandet om etablering. Kontakta Adobe kundsupport om du inte fått e-postmeddelandet.

   Välj **[!UICONTROL Connect to Dynamic Media]**.

   >[!NOTE]
   **RICK: BEHÅLL SOM DET ÄR?** När du har fått ditt e-postmeddelande med Dynamic Media-autentiseringsuppgifter öppnar du [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media Cloud Service har rätt autentiseringsuppgifter.

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
   Det finns inget stöd för versionshantering i DMS7. Dessutom gäller fördröjd aktivering endast om **[!UICONTROL Publish Assets]** på sidan Redigera Dynamic Media-konfiguration är inställd på **[!UICONTROL Upon Activation]** och då endast tills resursen aktiveras första gången.
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

**RICK: BEHÅLL SOM DET ÄR**

Om du vill anpassa konfigurationen och konfigurationen av Dynamic Media - Scene7 eller optimera prestandan ytterligare kan du göra något av följande: *valfri* uppgifter:

* [(Valfritt) Konfigurera Dynamic Media - Scene7-läge för överföring av resurser som är större än 2 GB](#optional-config-dms7-assets-larger-than-2gb)
* [(Valfritt) Konfigurera Dynamic Media Publish Setup](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)
   * [(Valfritt) Testa resurser innan du publicerar dem](#test-assets-before-making-public)
* [(Valfritt) Konfigurera allmänna inställningar för Dynamic Media](#configuring-application-general-settings)
* [(Valfritt) Ytterligare konfigurationsuppgifter](#additional-configuration-tasks)
* [(Valfritt) Justera prestanda för Dynamic Media - Scene7-läge](#optional-tuning-the-performance-of-dynamic-media-scene-mode)
* [(Valfritt) Filtrera resurser för replikering](#optional-filtering-assets-for-replication)

### (Valfritt) Konfigurera Dynamic Media - Scene7-läge för överföring av resurser som är större än 2 GB {#optional-config-dms7-assets-larger-than-2gb}

**RICK: BEHÅLL SOM DET ÄR**

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

### (Valfritt) Konfigurera Dynamic Media Publish Setup {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

**RICK: HELA INNEHÅLLET FRÅN DET NYA PUBLICERINGSINSTÄLLNINGSÄMNET SOM LÄGGS TILL HÄR**

>[!IMPORTANT]
Dynamic Media Publish Setup är endast tillgänglig om:
* Du kör Dynamic Media i Scene7-läge.
* Du har en *befintlig* **[!UICONTROL Dynamic Media Configuration]** (in **[!UICONTROL Cloud Services]**) i Adobe Experience Manager 6.5 eller Experience Manager as a Cloud Service.
* Du är systemadministratör för Experience Manager med administratörsbehörighet.


Inställningarna på sidan Publiceringsinställningar för Dynamic Media avgör hur resurser levereras som standard från Adobe Dynamic Media-servrar till webbplatser eller program. Om ingen inställning har angetts levererar Adobe Dynamic Media-servern en resurs enligt en standardinställning på en publiceringsinställningssida. En begäran om att leverera en bild som inte innehåller ett upplösningsattribut ger till exempel en bild med inställningen för standardobjektupplösning på sidan Bildserver.

Administratörer kan ändra standardinställningarna på sidorna Image Server, Image Renderer och Vinjettering för att skapa standardinställningar för att leverera resurser från servrar.

>[!NOTE]
Dynamic Media Publish Setup är avsedd för erfarna webbplatsutvecklare och programmerare. Adobe rekommenderar att användare som ändrar någon av dessa standardinställningar för publicering känner till Adobe Dynamic Media, HTTP-protokollets standarder och konventioner samt grundläggande bildbehandlingsteknik.

**Så här konfigurerar du Dynamic Media Publish Setup:**

1. I läget Experience Manager Author väljer du logotypen Experience Manager för att komma åt den globala navigeringskonsolen.
1. Välj ikonen Verktyg i den vänstra listen och gå sedan till **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
1. Ange din Image Server - publiceringskontext på sidan Image Server och använd sedan de fem flikarna för att konfigurera standardpubliceringsinställningarna.

   * [Bildserver](#image-server)
   * [Säkerhet](#security-tab) tab
   * [Kataloghantering](#catalog-management-tab) tab
   * [Attribut för begäran](#request-attributes-tab) tab
   * [Vanliga miniatyrattribut](#common-thumbnail-attributes-tab) tab
   * [Färghanteringsattribut](#color-management-attributes-tab) tab

   ![Dynamic Media Publish Setup page](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media Publish Setup-sidan med **[!UICONTROL Request Attributes]**har valts.*<br><br>

1. När du är klar väljer du **[!UICONTROL Save]**.

#### Bildserver {#image-server}

Sidan Image Server används för att ange standardinställningar för att leverera bilder från bildservrar. Inställningarna är tillgängliga i fem kategorier

| Publicera kontext | Beskrivning |
| --- | --- |
| Bildredigering | Anger kontext för publiceringsinställningar. |
| Testa bildvisning | Anger kontexten för testning av publiceringsinställningar.<br>Se [Testa resurser innan du gör dem offentliga](#test-assets-before-making-public). |

#### Fliken Säkerhet {#security-tab}

**[!UICONTROL Client address]** - Gör att du kan ange en eller flera IP-adresser eller IP-adressintervall. När det anges avvisas begäranden till den här bildkatalogen som kommer från en klient till en IP-adress som inte finns med i listan. Den här regeln gäller både för leverans av bilder och återgivna bilder.

#### Fliken Kataloghantering {#catalog-management-tab}

**[!UICONTROL Rule set definition file path]** - Anger filen som innehåller regeluppsättningsdefinitionerna för bildkatalogen.

Se även [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) i referenshandboken för Dynamic Media Viewer.

#### Fliken Attribut för begäran {#request-attributes-tab}

De här inställningarna gäller standardutseendet för bilder.

| Inställning | Beskrivning |
| --- | --- |
| **[!UICONTROL Reply image size limit]** | Krävs.<br>Anger den maximala svarsbildens bredd och höjd som returneras till klienten. Servern returnerar ett fel om en begäran orsakar en svarsbild vars bredd, höjd eller båda är större än den här inställningen.<br>Se även [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Request obfuscation mode]** | Aktivera om du vill att base64-kodning ska användas på giltiga begäranden.<br>Se även [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Request locking mode]** | Aktivera om du vill att ett enkelt hash-lås ska inkluderas i begäranden.<br>Se även [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default Request Attributes]** |  |
| **[!UICONTROL Default image file suffix]** | Krävs.<br>Standarddatafiltillägg som läggs till i fältvärdena katalogsökväg och MaskPath om sökvägen inte innehåller något filsuffix.<br>Se även [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default font face name]** | Anger vilket teckensnitt som ska användas om inget teckensnitt anges i en textlagerbegäran. Om du anger det måste det vara ett giltigt teckensnittsnamnvärde i teckensnittskartan för den här bildkatalogen eller i teckensnittskartan för standardkatalogen.<br>Se även [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default image]** | Tillhandahåller en standardbild som returneras som svar på en begäran där den begärda bilden inte hittas.<br>Se även [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default image mode]** | När skjutreglaget är aktiverat (skjutreglage till höger) visas **[!UICONTROL Default image]** ersätter varje lager som saknas i källbilden med standardbilden och returnerar den sammansatta bilden som vanligt. När skjutreglaget är inaktiverat (skjutreglage till vänster) ersätter standardbilden hela den sammansatta bilden, även om den saknade bilden bara är ett av flera lager.<br>Se även [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default view size]** | Krävs.<br>Servern begränsar svarsbilderna till att inte vara större än den här bredden och höjden om begäran inte uttryckligen anger visningsstorleken med `wid=`, `hei=`, eller `scl=`.<br>Se även [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default thumbnail size]** | Krävs.<br>Används i stället för attribut **[!UICONTROL Default view size]** för miniatyrbegäranden (`req=tmb`). Servern begränsar svarsbilderna så att de inte är större än den här bredden och höjden, om en miniatyrbildsbegäran (`req=tmb`) anger inte storleken explicit med `wid=`, `hei=`, eller `scl=`.<br>Se även [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default background color]** | Anger RGB som används för att fylla i områden i en svarsbild som inte innehåller verkliga bilddata.<br>Se även [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL JPEG Encoding Attributes]** |  |
| **[!UICONTROL Quality]** | Anger standardattributen för svarsbilder i JPEG. The **[!UICONTROL Quality]** -fältet definieras i intervallet 1-100.<br>Se även [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Chromatically downsampling]** | Aktivera eller inaktivera kromatisk nedsampling som används av JPEG-kodare. |
| **[!UICONTROL Default resampling mode]** | Anger de standardattribut för omsampling och interpolation som ska användas för skalning av bilddata. Använd när `resMode` har inte angetts i en begäran.<br>Se även [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) i referenshandboken för Dynamic Media Viewer. |

#### fliken Vanliga miniatyrattribut {#common-thumbnail-attributes-tab}

De här inställningarna gäller för miniatyrbildernas standardutseende och -justering.

| Inställning | Beskrivning |
| --- | --- |
| **[!UICONTROL Default background color for thumbnail]** | Anger det RGB-värde som används för att fylla i en miniatyrbilds utdataområde som inte innehåller verkliga bilddata. Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default Thumbnail Type]** inställningen är inställd på **[!UICONTROL Fit]** eller **[!UICONTROL Texture]**.<br>Se även [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Horizontal alignment]** | Anger den vågräta justeringen för miniatyrbilden i svarsbildsrektangeln som anges av `wid=` och `hei=` värden.<br>Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default Thumbnail Type]** inställningen är inställd på **[!UICONTROL Fit]**.<br>Det finns tre horisontella justeringar att välja mellan: **[!UICONTROL Center alignment]**, **[!UICONTROL Left alignment]** och **[!UICONTROL Right alignment]**.<br>Se även [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Vertical alignment]** | Anger den lodräta justeringen för miniatyrbilden i svarsbildsrektangeln som anges av `wid=` och `hei=` värden. Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default Thumbnail Type]** inställningen är inställd på **[!UICONTROL Fit]**.<br>Det finns tre lodräta justeringar att välja mellan: **[!UICONTROL Top alignment]**, **[!UICONTROL Center alignment]** och **[!UICONTROL Bottom alignment]**.<br>Se även [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default cache time to live]** | Anger ett standardutgångsintervall i timmar om en viss katalogpost inte innehåller ett giltigt värde för katalogförfallotid. Ange till `-1` för att markera som aldrig förfaller. <br>Se även [Förfaller](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default thumbnail type]** | Anger ett standardvärde för miniatyrbildstypen om en viss katalogpost inte innehåller ett giltigt katalogvärde för ThumbType. Används endast för miniatyrbildsbegäranden (`req=tmb`).<br>Det finns tre typer av miniatyrer att välja bland: **[!UICONTROL Crop]**, **[!UICONTROL Fit]** och **[!UICONTROL Texture]**.<br>Se även [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default thumbnail resolution]** | Anger ett standardvärde för upplösningen av miniatyrbildobjektet om en viss katalogpost inte innehåller ett giltigt ThumbRes-katalogvärde. Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default thumbnail type]** inställningen är inställd på **[!UICONTROL Texture]**.<br>Se även [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) i referenshandboken för Dynamic Media Viewer. |

#### Fliken Färghanteringsattribut {#color-management-attributes-tab}

De här inställningarna avgör vilka ICC-färgprofiler som används för bilder.

**Återgivningsmetod för färgkonvertering**
En färgkonverteringsåtergivningsmetod tillåter åsidosättning av standardåtergivningsmetoden för arbetsprofilerna för att bestämma hur källfärgerna justeras. Används när:

1. En av standardprofilerna för ICC är målfärgrymden för en färgkonvertering.
1. En utdataenhet (skrivare eller bildskärm) kännetecknas av den här profilen.
1. Den angivna återgivningsmetoden gäller även för den här profilen.

Olika återgivningsmetoder använder olika regler för att bestämma hur källfärgerna justeras.

Du kan till exempel ange **[!UICONTROL RGB default color space]** till **[!UICONTROL sRGB]** och **[!UICONTROL CMYK default color space]** till **[!UICONTROL WebCoated]**.

Om du gör det gör du så här:

* Aktiverar färgkorrigering för RGB och CMYK-bilder.
* RGB-bilder som inte har någon färgprofil antas finnas i *sRGB* färgrymd.
* CMYK-bilder som inte har någon färgprofil antas finnas i *WebCoated* färgrymd.
* Dynamiska återgivningar som returnerar utdata från RGB, returnerar det i dialogrutan *sRGB* färgrymd.
* Dynamiska återgivningar som returnerar CMYK-utdata och returnerar dem i *WebCoated* färgrymd.

Se även [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) i referenshandboken för Dynamic Media Viewer.

>[!NOTE]
I allmänhet är det bäst att använda standardåtergivningsmetoden för den valda färginställningen, som har testats av Adobe för att uppfylla branschstandarder. Om du t.ex. väljer en färginställning för Nordamerika eller Europa är standardåtergivningsmetoden för färgkonvertering **[!UICONTROL Relative Colormetric]**. Om du väljer en färginställning för Japan är standardåtergivningsmetoden för färgkonvertering **[!UICONTROL Perceptual]**.

| Inställning | Egenskaper |
| --- | --- |
| **[!UICONTROL CMYK default color space]** | Anger namnet på ICC-färgprofilen som ska användas som arbetsprofil för CMYK-data. If **[!UICONTROL None Specified]** väljs inaktiveras färghantering för den här bildkatalogen när det gäller CMYK-källbilder. Alla CMYK-arbetsfärgrymder är enhetsberoende, vilket innebär att de baseras på faktiska kombinationer av bläck och papper. CMYK-arbetsfärgrymderna Adobe bygger på standardtryckeriet.<br> Se även [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Gray-Scale default color space]** | Anger namnet på ICC-färgprofilen som ska användas som arbetsprofil för gråskaledata. If **[!UICONTROL None Specified]** väljs inaktiveras färghantering för den här bildkatalogen när källbilder i gråskala används.<br>Se även [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL RGB default color space]** | Anger namnet på ICC-färgprofilen som ska användas som arbetsprofil för RGB data. If **[!UICONTROL None Specified]** väljs inaktiveras färghantering för den här bildkatalogen när bilder från RGB-källor används. I allmänhet är det bäst att välja **[!UICONTROL Adobe RGB]** eller **[!UICONTROL sRGB]** i stället för profilen för en viss enhet (till exempel en bildskärmsprofil). **[!UICONTROL sRGB]** rekommenderas när du förbereder bilder för webben eller mobila enheter, eftersom färgrymden definieras för den standardbildskärm som används för att visa bilder på webben. **[!UICONTROL sRGB]** är också ett bra val när du arbetar med bilder från vanliga digitalkameror, eftersom sRGB används som standardfärgrymd i de flesta av dessa.<br>Se även [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Color conversion rendering intent]** | **[!UICONTROL Perceptual]** - Avsikten är att bevara den visuella relationen mellan färger så att de uppfattas som naturliga för det mänskliga ögat, även om färgvärdena i sig kan ändras. Den här metoden är lämplig för fotografiska bilder med många ej tryckbara färger. Den här inställningen är standardåtergivningsmetoden för den japanska tryckeribranschen. |
|  | **[!UICONTROL Relative Colorimetric]** - Jämför de extrema färgerna i källfärgrymden med målfärgrymden och anpassar färgerna. Färger utanför färgomfånget ändras till den närmast reproducerbara färgen i målfärgrymden. Med Relativa färgvärden bevaras mer av de ursprungliga färgerna i en bild än med Perceptuell. Den här inställningen är standardåtergivningsmetoden för utskrift i Nordamerika och Europa. |
|  | **[!UICONTROL Saturation]** - Försöker producera levande färger i en bild på bekostnad av färgnoggrannheten. Den här återgivningsmetoden är lämplig för affärsgrafik som diagram och diagram där klara, mättade färger är viktigare än det exakta förhållandet mellan färger. |
|  | **[!UICONTROL Absolute Colorimetric]** - Ändrar inte färger som ligger inom målfärgomfånget. Ej tryckbara färger beskärs. Ingen skalning av färger till målvitpunkten utförs. Den här metoden syftar till att bibehålla färgnoggrannheten på bekostnad av att förhållandet mellan färger bevaras och är lämplig för korrektur för att simulera utdata från en viss enhet. Den här metoden är användbar när du vill förhandsgranska hur pappersfärgen påverkar tryckta färger. |

### Testa resurser innan du gör dem offentliga {#test-assets-before-making-public}

Säker testning hjälper er att definiera en säker testmiljö och bygga en robust affärs-till-business-lösning som bygger på en konfigurerbar uppsättning IP-adresser och intervall. Med den här funktionaliteten kan ni matcha era Adobe Dynamic Media-installationer med arkitekturen i ert innehållshantering och affärssystem.

Med Säker testning kan du förhandsgranska testversionen av webbplatsen med opublicerat innehåll.

Om du vill kan du skapa en staging-miljö i stället för att göra resurserna allmänt tillgängliga av följande skäl:

* Förhandsgranska webbplatser innan den offentliga lanseringen (testwebbplatsen).
* Tjäna resurser som kräver begränsad åtkomst, till exempel e-kataloger som visar priser i B2B-webbprogram.
* Använd material bakom en brandvägg som en del av produktinformationshanteringssystemet, kundtjänstprogrammet, utbildningswebbplatsen osv.

>[!NOTE]
Säker testning påverkar inte åtkomsten till Adobe Dynamic Media Classic. Adobe Dynamic Media Classic säkerhet är konsekvent och kräver de vanliga inloggningsuppgifterna för åtkomst till Adobe Dynamic Media Classic och relaterade webbtjänster.

#### Så här fungerar säkra tester {#how-test-assets-works}

De flesta företag använder internet bakom en brandvägg. Tillgång till Internet är möjlig via vissa vägar och vanligtvis via ett begränsat antal offentliga IP-adresser.

I företagsnätverket kan du räkna ut din offentliga IP-adress med webbplatser som [https://www.whatismyip.com](https://www.whatismyip.com/) eller begär den här informationen från IT-avdelningen.

Med säker testning skapar Adobe Dynamic Media en dedikerad Image Server för testmiljöer eller interna program. Alla förfrågningar till den här servern kontrollerar den ursprungliga IP-adressen. Om den inkommande begäran inte finns i den godkända listan över IP-adresser returneras ett felsvar. Adobe Dynamic Media företagsadministratör konfigurerar den godkända listan över IP-adresser för företagets säkra testmiljö.

Eftersom platsen för den ursprungliga begäran måste bekräftas, dirigeras inte trafiken för tjänsten för säker testning via ett nätverk för innehållsdistribution, t.ex. offentlig Dynamic Media Image Server-trafik. Begäranden till tjänsten för säker testning har en något högre fördröjning än de offentliga Dynamic Media Image-servrarna.

Opublicerade resurser är omedelbart tillgängliga från tjänsterna för säker testning, utan att behöva publicera. På så sätt kan du köra en förhandsvisning innan resurser publiceras på den offentliga bildservern.

>[!NOTE]
Tjänster för säker testning använder katalogservern som är konfigurerad med en intern publiceringskontext. Om ditt företag är konfigurerat att publicera till Säker testning blir därför alla överförda resurser i Adobe Dynamic Media omedelbart tillgängliga på Säker testning. Den här funktionen är sann oavsett om resurserna har markerats för publicering vid överföring.

Tjänster för säker testning stöder för närvarande följande resurstyper och funktioner:

* Bilder.
* Vinjetter (renderingsserverbegäranden).
* Rendera serverförfrågningar (stöds, men måste begäras uttryckligen av kunden).
* Uppsättningar, inklusive bilduppsättningar, eCatalog, renderingsuppsättningar och medieuppsättningar.
* Adobe Dynamic Media multimedievisningsprogram som standard.
* Adobe Dynamic Media OnDemand JSP pages.
* Statiskt innehåll, till exempel PDF-filer och progressivt levererade videor.
* HTTP-videoströmning.
* Progressiv videoströmning.

Följande tillgångstyper och funktioner stöds för närvarande inte:

* Adobe Dynamic Media Classic Info- eller eCatalog-sökning
* RTMP-videoströmning
* Webb-till-tryck
* UGC-tjänster (användargenererat innehåll)

>[!IMPORTANT]
Stöd för nya eller befintliga UGC-vektorbildresurser i Adobe Dynamic Media upphörde den 30 september 2021.

#### Testa tjänsten för säker testning {#test-secure-testing-service}

Så här ser du till att tjänsten Secure Testing fungerar som förväntat:

##### Förbered ditt konto

1. Kontakta Adobe kundtjänst och begär att de aktiverar säker testning på ditt konto.
1. I Adobe Experience Manager väljer du **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
1. På sidan Image Server finns **[!UICONTROL Publish Context]** nedrullningsbar lista, välja **[!UICONTROL Test Image Serving]**.
1. Välj **[!UICONTROL Security]** -fliken.
1. För **[!UICONTROL Client address]** filter, markera **[!UICONTROL Add]**.
1. I **[!UICONTROL IP Address]** anger du en IP-adress.
1. I **[!UICONTROL Mask]** skriver du en nätmask.

   >[!NOTE]
   Om du lägger till mer än en IP-adress och nätmask tillåts *alla* IP-adresser för att göra tillgångsanrop, och de visas alla.

1. Gör något av följande:

   * Om du vill lägga till fler IP-adresser upprepar du de tre föregående stegen.
   * Fortsätt till nästa steg.

1. I det övre högra hörnet på sidan Image Server väljer du **[!UICONTROL Save]**.
1. Ladda upp bilderna till ditt Adobe Dynamic Media-konto.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Se till att vissa bilder är markerade för publicering och att andra är omarkerade och skicka sedan publiceringsjobbet.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Bestäm namnet på tjänsten för säker testning genom att gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media General Setting]**.
1. På **[!UICONTROL Server]** sidan, hitta servernamnet till höger om **[!UICONTROL Published Server Name]**.

Kontakta Adobe Care om servernamnet saknas eller om URL:en till inte fungerar.

##### Förbered webbplatsvarianter

Du behöver två varianter av en webbplats som länkar de publicerade och opublicerade resurserna:

* Offentlig version - Länka resurser med den traditionella URL-syntaxen för Adobe Dynamic Media.
* Mellanlagringsversion - Länka resurser med samma syntax men med namnet på platsen för säker testning.

##### Kör testerna

Utför följande tester:

1. Kontrollera om resurser är synliga inifrån företagets nätverk.

   I företagsnätverket som identifieras av det tidigare definierade IP-adressintervallet visar mellanlagringsversionen av webbplatsen alla bilder, oavsett om de är markerade för publicering eller inte. Därför kan du testa utan att oavsiktligt göra bilder tillgängliga innan du förhandsgranskar eller startar produkten.

   Bekräfta att den offentliga versionen av din webbplats visar publicerade resurser så som de har varit med Adobe Dynamic Media tidigare.

1. Verifiera att icke-publicerade resurser (dvs. omärkta för publicering) är skyddade från åtkomst från tredje part utanför företagets nätverk.

   Få åtkomst till nätverket från utsidan (till exempel från din hemdator eller via en 4G/5G-anslutning) och kontrollera sedan att den offentliga versionen av webbplatsen visar alla publicerade resurser, men inget av det opublicerade innehållet.

   Bekräfta att mellanlagringsversionen inte visar någon resurs eftersom du använder tjänsten för säker testning från en ej godkänd IP-adress.

### Konfigurera allmänna inställningar för Dynamic Media {#configuring-application-general-settings}

>[!IMPORTANT]
Allmänna inställningar för Dynamic Media är endast tillgängliga om:
* Du kör Dynamic Media i Scene7-läge.
* Du har en *befintlig* **[!UICONTROL Dynamic Media Configuration]** (in **[!UICONTROL Cloud Services]**) i Adobe Experience Manager 6.5 eller Experience Manager as a Cloud Service.
* Du är systemadministratör för Experience Manager med administratörsbehörighet.


När du skapar ett konto tillhandahåller Adobe Dynamic Media automatiskt de tilldelade servrarna för ditt företag. De här servrarna används för att skapa URL-strängar för din webbplats och dina program. Dessa URL-anrop är specifika för ditt konto.

Se även [Testa tjänsten Secure Testing](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**Så här konfigurerar du den allmänna inställningen för Dynamic Media:**

1. I läget Experience Manager Author väljer du logotypen Experience Manager för att komma åt den globala navigeringskonsolen.
1. Välj ikonen Verktyg i den vänstra listen och gå sedan till **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media General Setting]**.
1. Ange din **[!UICONTROL Published Server Name]** och **[!UICONTROL Origin Server Name]** och använd sedan de fem flikarna för att konfigurera standardinställningar för publicering.

   * [Server](#server-general-setting)
   * [Överför till program](#upload-to-application)
   * [Bildredigering](#image-editing-tab) tab
   * [PostScript](#postscript-tab) tab
   * [Photoshop](#photoshop-tab) tab
   * [PDF](#pdf-tab) tab
   * [Illustrator](#illustrator-tab) tab

   ![Dynamic Media General Settings page](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media General Settings page, with the **[!UICONTROL Image Editing]**har valts.*<br><br>

1. När du är klar väljer du **[!UICONTROL Save]**.

#### Server {#server-general-setting}

När du skapar ett konto tillhandahåller Adobe Dynamic Media automatiskt de tilldelade servrarna för ditt företag. De här servrarna används för att skapa URL-strängar för din webbplats och dina program. Dessa URL-anrop är specifika för ditt konto.

| Alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Published Server Name]** | Krävs.<br>Den här servern är den CDN-server (Content Deliver Network) som används i alla systemgenererade URL-anrop som är specifika för ditt konto. Ändra inte det här servernamnet om du inte har fått instruktioner om att göra det av Adobe tekniska support. Namnet måste använda `https://` i banan. |
| **[!UICONTROL Origin Server Name]** | Krävs.<br>Den här servern används endast för kvalitetstestning. Ändra inte det här servernamnet om du inte har fått instruktioner om att göra det från Adobe tekniska support. |

#### Överför till program {#upload-to-application}

* **[!UICONTROL Overwrite Images]**

   Adobe Dynamic Media tillåter inte att två filer har samma namn. Varje objekts Adobe Dynamic Media-ID (bildnamn minus filnamnstillägg) måste vara unikt. På grund av den här regeln **[!UICONTROL Upload to Application]** har en överskrivning. Den exakta effekten av det här alternativet beror på det angivna alternativet Skriv över bilder som du har valt. De här alternativen anger hur ersättningsbilder överförs: om de ersätter originalbilderna eller blir dubblettbilder. Namnet på duplicerade bilder ändras med ett `-1`. Till exempel: `chair.tif` har bytt namn `chair-1.tif`. De här alternativen påverkar bilder som har överförts till en annan mapp än den ursprungliga eller bilder med ett annat filnamnstillägg än den ursprungliga, till exempel JPG, TIF eller PNG.

   | Skriv över bilder, alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Overwrite in current folder, same base name/extension]** | Standard.<br>Det här alternativet är den striktaste regeln för ersättning. Det kräver att du överför ersättningsbilden till samma mapp som originalbilden och att ersättningsbilden har samma filnamnstillägg som originalbilden. Om dessa krav inte uppfylls skapas en dubblett. |
   | **[!UICONTROL Overwrite in current folder, same base name regardless of extension]** | Kräver att du överför ersättningsbilden till samma mapp som originalet, men filnamnstillägget kan skilja sig från originalet. Till exempel ersätter stol.tif stol.jpg. |
   | **[!UICONTROL Overwrite in any folder, same base asset name/extension]** | Kräver att ersättningsbilden har samma filnamnstillägg som den ursprungliga bilden (t.ex. måste stol.jpg ersätta stol.jpg, inte stol.tif). Du kan dock överföra ersättningsbilden till en annan mapp än den ursprungliga. Den uppdaterade bilden finns i den nya mappen; filen inte längre kan hittas på sin ursprungliga plats. |
   | **[!UICONTROL Overwrite in any folder, same base asset name regardless of extension]** | Det här alternativet är den mest omfattande ersättningsregeln. Du kan överföra en ersättningsbild till en annan mapp än den ursprungliga, överföra en fil med ett annat filnamnstillägg och ersätta den ursprungliga filen. Om originalfilen finns i en annan mapp finns ersättningsbilden i den nya mappen som den överfördes till. |

* **[!UICONTROL Preserve Crop]**

   Kontrollerar bevarande av befintliga manuella beskärningsdefinitioner.

   Se även `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) och [ÅterbearbetaResurserJobb](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), båda i referenshandboken för Dynamic Media Viewer.

#### Standardalternativ för överföring {#default-upload-options}

##### Fliken Bildredigering {#image-editing-tab}

Med det här filtret kan du finjustera en skärpefiltereffekt på den slutliga nedsamplade bilden. Det hjälper dig att styra intensiteten i effekten, radien för effekten (mätt i pixlar) och ett tröskelvärde för kontrast som ignoreras.

För effekten Oskarp mask används samma alternativ som för filtret Oskarp mask i Photoshop. Till skillnad från vad namnet antyder är Oskarp mask ett skärpefilter.

| Oskarp mask, alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Amount]** | Krävs.<br>Styr mängden kontrast som används på kantpixlar.<br>Tänk på det som intensiteten i effekten. Den största skillnaden mellan mängdvärdena för Oskarp mask i Adobe Dynamic Media och mängdvärdena i Adobe Photoshop är att Photoshop har ett intervall på 1 till 500 %. I Adobe Dynamic Media är värdeintervallet `0.0` till `5.0`. Värdet 5.0 i Adobe Dynamic Media motsvarar 500 % i Photoshop. värdet 0,9 motsvarar 90 % och så vidare. |
| **[!UICONTROL Radius]** | Krävs.<br>Styr radien för effekten.<br>Värdeintervallet är `0` till `250`. Effekten körs på alla pixlar i en bild och strålar ut från alla pixlar i alla riktningar. Radien mäts i pixlar. Om du till exempel vill få en liknande skärpeeffekt för en bild på 2 000 x 2 000 pixlar och en bild på 500 x 500 pixlar anger du en radie på två pixlar för bilden på 2 000 x 2 000 pixlar. Ange sedan radien 1 pixel på bilden med 500 x 500 pixlar. Ett större värde används för en bild som har fler pixlar. |
| **[!UICONTROL Threshold]** | Krävs.<br>Tröskelvärde är ett kontrastintervall som ignoreras när filtret Oskarp mask används. Den här effekten är viktig så att inget &quot;brus&quot; uppstår i en bild när filtret används. Värdeintervallet är `0` - `255`, vilket är antalet steg för intensitet i en gråskalebild. `0`=svart, `128`=50% grå och `255`=vitt.<br>Ett tröskelvärde på `12` ignorerar små variationer i hudtonens ljusstyrka för att undvika att lägga till brus, men ändå ger kantkontrast till kontrastrika områden som där ögonfransar möter hud.<br>Om du har ett foto av någon annans ansikte påverkar Oskarp mask de kontrastrika delarna av bilden. Till exempel där ögonfransar och hud möts för att skapa ett tydligt kontrastområde och den utjämnade huden. Även den jämnaste huden uppvisar subtila förändringar i intensitetsvärden. Om du inte använder ett tröskelvärde framhäver filtret dessa subtila ändringar i hudpixlar. I sin tur skapas en högljudd och oönskad effekt medan kontrasten på ögonfransarna ökar, vilket ökar skärpan.<br>För att undvika det här problemet introduceras ett tröskelvärde som instruerar filtret att ignorera pixlar som inte förändrar kontrasten dramatiskt, som mjuk hud.<br>Lägg märke till texturen bredvid dragkedjan i zippargrafiken som visades tidigare. Bildbrus visas eftersom tröskelvärdena var för låga för att undertrycka bruset. |
| **[!UICONTROL Monochrome]** | Markera för att få bildintensiteten oskarp mask (intensitet).<br>Avmarkera alternativet om du vill skapa en oskarp mask för varje färgkomponent separat. |

Se även [Öka skärpan i bilder i Adobe Dynamic Media och på Image Server](/help/assets/assets/sharpening_images.pdf).

##### PostScript-flik {#postscript-tab}

Du kan rastrera Adobe PostScript®-filer, behålla genomskinliga bakgrunder, välja en upplösning och välja en färgrymd.

Du kan använda Adobe PostScript®-filer (EPS) i Adobe Dynamic Media. I Adobe Dynamic Media finns kommandon för att konfigurera de här filerna när du överför dem.

När du överför PostScript-bildfiler (EPS) kan du formatera dem på olika sätt. Du kan rastrera filerna, behålla den genomskinliga bakgrunden, välja en upplösning och välja en färgrymd.

| PostScript, alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Processing]** | Välj Rastrera om du vill konvertera vektorgrafik i filen till bitmappsformat. |
| **[!UICONTROL Maintain transparent background in rendered images]** | Bevarar filens genomskinlighet i bakgrunden. |
| **[!UICONTROL Resolution (pixel/inch)]** | Anger upplösningsinställningen. Den här inställningen avgör hur många pixlar som visas per tum i filen. |
| **[!UICONTROL Color space]** | ・ **[!UICONTROL Detect automatically]** - Behåller filens färgrymd.<br>・ **[!UICONTROL Force as RGB]** - Konverterar till färgmodellen RGB.<br>・ **[!UICONTROL Force as CMYK]** - Konverterar till CMYK-färgmodellen.<br>・ **[!UICONTROL Force as Grayscale]** - Konverterar till färgmodellen Gråskala. |

##### Fliken Photoshop {#photoshop-tab}

Du kan skapa mallar från Adobe® Photoshop®-filer, behålla lager, ange hur lager ska namnges, extrahera text och ange hur bilder ska förankras i mallar.

| Photoshop | Beskrivning |
| --- | --- |
| **[!UICONTROL Maintain layers]** | Rippar lagren i PSD, om det finns några, till enskilda resurser. Resurslagren förblir kopplade till PSD. Du kan visa dem genom att öppna filen PSD i detaljvyn och välja lagerpanelen. Se Visa och redigera lager i en PSD-fil. |
| **[!UICONTROL Create template]** | Skapar en mall från lagren i filen PSD. |
| **[!UICONTROL Extract text]** | Extraherar texten så att användare kan söka efter text i ett visningsprogram. |
| **[!UICONTROL Extend layers to background size]** | Utökar storleken på överlappade bildlager till storleken på bakgrundslagret. |
| **[!UICONTROL Layer naming]** | Utökar storleken på överlappade bildlager till storleken på bakgrundslagret.<br>・ **[!UICONTROL Layer name]** - Namnger bilderna efter deras lagernamn i filen PSD. Ett lager med namnet Price Tag i den ursprungliga PSD-filen blir till exempel en bild med namnet Price Tag. Om lagernamnen i filen PSD är Photoshop standardlagernamn (Bakgrund, Lager 1, Lager 2 och så vidare) får bilderna namn efter sina lagernummer i filen PSD. <br>・ **[!UICONTROL Photoshop and layer number]** - Namnger bilderna efter deras lagernummer i filen PSD och ignorerar de ursprungliga lagernamnen. Bilderna får samma namn som Photoshop-filnamnet och ett nummer i det tillagda lagret. Det andra lagret i en fil med namnet `Spring Ad.psd` är namngiven `Spring Ad_2` även om det har ett icke-standardnamn i Photoshop.<br>・ **[!UICONTROL Photoshop and layer name]** - Namnger bilderna efter PSD-filen följt av lagernamnet eller lagernumret. Lagernumret används om lagernamnen i filen PSD är Photoshop standardlagernamn. Ett lager med namnet `Price Tag` i en PSD-fil med namnet `SpringAd` är namngiven `Spring Ad_Price Tag`. Ett lager med standardnamnet Lager2 anropas `Spring Ad_2`. |
| **[!UICONTROL Anchor]** | Ange hur bilder ska förankras i mallar som genereras från lagerkompositionen som skapas från filen PSD. Som standard är ankarpunkten i mitten. Med en central ankarpunkt kan ersättningsbilder bäst fylla samma område, oavsett ersättningsbildens proportioner. Bilder med en annan aspekt som ersätter den här bilden upptar i själva verket samma utrymme när de refererar till mallen och använder parameterersättning. Ändra till en annan inställning om ditt program kräver att ersättningsbilderna fyller ut det tilldelade utrymmet i mallen. |

##### PDF, flik {#pdf-tab}

Du kan välja att rastrera filerna, extrahera sökord och länkar, ange upplösning och välja en färgrymd.

| PDF, alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Processing]** | ・ **[!UICONTROL None]** - Ingen bearbetning av PDF görs.<br>・ **[!UICONTROL Thumbnail]** - Rippar varje sida i filen PDF och konverterar den till en miniatyrbild.<br> ・ **[!UICONTROL Rasterize]** - Rippar sidorna i PDF-filen och konverterar vektorgrafik till bitmappsbilder. Välj det här alternativet om du vill skapa en e-katalog. |
| **[!UICONTROL Extract]** | ・ **[!UICONTROL None]** - Inga sökord eller länkar extraheras från PDF.<br>・ **[!UICONTROL Search words]** - Extraherar sökord från PDF-filen så att filen kan genomsökas efter nyckelord i en eCatalog Viewer.<br>・ **[!UICONTROL Links]** - Extraherar länkar från PDF-filerna och konverterar dem till Image Maps som används i en eCatalog Viewer.<br>・ **[!UICONTROL Search words and links]** - Extraherar både sökord och länkar för användning i ett eCatalog-visningsprogram. |
| **[!UICONTROL Resolution (pixel/inch)]** | Anger upplösningsinställningen. Den här inställningen avgör hur många pixlar som visas per tum i filen PDF. Standardvärdet är 150. |
| **[!UICONTROL Color space]** | ・ **[!UICONTROL Detect automatically]** - Behåller färgrymden för PDF-filen.<br>・ **[!UICONTROL Force as RGB]** - Konverterar till färgmodellen RGB.<br>・ **[!UICONTROL Force as CMYK]** - Konverterar till CMYK-färgmodellen.<br>・ **[!UICONTROL Force as Grayscale]** - Konverterar till färgmodellen Gråskala. |

##### Fliken Illustrator {#illustrator-tab}

Du kan rastrera Adobe Illustrator®-filer, behålla genomskinliga bakgrunder, välja en upplösning och välja en färgrymd.

Du kan använda Adobe® Illustrator®-filer (AI) i Adobe Dynamic Media. I Adobe Dynamic Media finns kommandon för att konfigurera de här filerna när du överför dem.

När du överför Illustrator-bildfiler (AI) kan du formatera dem på olika sätt. Du kan rastrera filerna, behålla den genomskinliga bakgrunden, välja en upplösning och välja en färgrymd. Formateringsalternativ för PostScript- och Illustrator-filer finns på överföringsskärmen under PostScript-alternativ och Illustrator-alternativ i rutan Överför jobbalternativ.


| Illustrator | Beskrivning |
| --- | --- |
| **[!UICONTROL Processing]** | Välj Rastrera om du vill konvertera vektorgrafik i filen till bitmappsformat. |
| **[!UICONTROL Maintain transparent background in rendered images]** | Bevarar filens genomskinlighet i bakgrunden. |
| **[!UICONTROL Resolution (pixel/inch)]** | Anger upplösningsinställningen. Den här inställningen avgör hur många pixlar som visas per tum i filen. |
| **[!UICONTROL Color space]** | ・ **[!UICONTROL Detect automatically]** - Behåller filens färgrymd.<br>・ **[!UICONTROL Force as RGB]** - Konverterar till färgmodellen RGB.<br>・ **[!UICONTROL Force as CMYK]** - Konverterar till CMYK-färgmodellen.<br>・ **[!UICONTROL Force as Grayscale]** - Konverterar till färgmodellen Gråskala. |


**[!UICONTROL Default Color Profiles]** - Se [Konfigurera färghantering](#configuring-color-management) för ytterligare information.

>[!NOTE]
Som standard visas 15 återgivningar när du väljer **[!UICONTROL Renditions]** och 15 visningsförinställningar när du väljer **[!UICONTROL Viewers]** i resursens detaljvy. Du kan öka den här gränsen. Se [Öka antalet bildförinställningar som visas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) eller [Öka antalet visningsförinställningar som visas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

### (Valfritt) Ytterligare konfigurationsuppgifter {#additional-configuration-tasks}

Tillvalsuppgifter för konfiguration och konfiguration omfattar följande:

* [Redigera MIME-typer för format som stöds](#editing-mime-types-for-supported-formats) **RICK: BEHÅLL?**
* [Lägg till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats) **RICK: BEHÅLL?**
* [Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) **RICK: BEHÅLL?**

* **[!UICONTROL Compatibility Attributes]** - **RICK: BEHÖVER DU FORTFARANDE? VAR I KLASSISK** Med den här inställningen kan inledande och avslutande stycken i textlager hanteras som i version 3.6 för bakåtkompatibilitet.
* **[!UICONTROL Localization Support]** - **RICK: BEHÖVER DU FORTFARANDE? VAR I KLASSISK** Med de här inställningarna kan du hantera flera språkattribut. Här kan du också ange en sträng för språkområdeskarta så att du kan definiera vilka språk du vill ha stöd för de olika verktygstipsen i visningsprogram. Mer information om konfiguration **[Lokaliseringsstöd]**, se [Att tänka på när lokalisering av resurser konfigureras](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Redigera MIME-typer för format som stöds {#editing-mime-types-for-supported-formats}

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

Använd förinställningar för gruppuppsättningar för att automatisera skapandet av bilduppsättningar eller snurra uppsättningar medan resurserna överförs till Dynamic Media.

Definiera först namnkonventionen för hur resurser grupperas i en uppsättning. Skapa sedan en förinställning för gruppuppsättning som är en unik, självständig uppsättning instruktioner. Det måste definiera hur uppsättningen ska skapas med bilder som matchar de definierade namnkonventionerna i förinställningsreceptet.

När du överför filer skapar Dynamic Media automatiskt en uppsättning med alla filer som matchar den definierade namnkonventionen i de aktiva förinställningarna.

##### Konfigurera standardnamn

Skapa en standardnamnkonvention som används i alla förinställda gruppuppsättningar. Den standardnamnkonvention som valts i definitionen av gruppuppsättningsförinställningen är troligen allt som ditt företag behöver för att gruppgenerera uppsättningar. En gruppuppsättningsförinställning skapas för att använda den standardnamnkonvention som du definierar. Du kan skapa så många gruppuppsättningsförinställningar med alternativa, anpassade namnkonventioner som behövs för en viss uppsättning innehåll om det finns ett undantag från den företagsdefinierade standardnamngivningen.

När det inte krävs någon standardnamnkonvention för att använda funktionen för gruppuppsättningsförinställningar bör du använda standardnamnkonventionen. Här kan du definiera så många element i namnkonventionen som du vill gruppera i en uppsättning så att du kan effektivisera skapandet av gruppuppsättningar.

Du kan också använda **[!UICONTROL View Code]** utan formulärfält tillgängliga. I den här vyn skapar du namnkonventionens definitioner helt med hjälp av reguljära uttryck.

Det finns två element för definition, Matcha och Basnamn. Med dessa fält kan du definiera alla element i en namnkonvention och identifiera den del av konventionen som används för att namnge den uppsättning i vilken de finns. Ett företags namnkonvention använder ofta en eller flera definitionsrader för vart och ett av dessa element. Du kan använda så många rader för din unika definition och gruppera dem i distinkta element, t.ex. för Huvudbild, Färgelement, Alternativa vyer och Färgruteelement.

**Så här konfigurerar du standardnamn:**

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

Adobe rekommenderar följande finjusteringstips för synkroniseringsprestanda/skalbarhet för att Dynamic Media - Scene7-läget ska fungera smidigt:

* Uppdaterar de fördefinierade jobbparametrarna för bearbetning av olika filformat.
* Uppdaterar de fördefinierade arbetstrådarna för Granite-arbetsflödet (videoresurser).
* Uppdaterar det fördefinierade tillfälliga Granite-arbetsflödet (bilder och icke-videomaterial) för köarbetstrådar.
* Uppdaterar de maximala överföringsanslutningarna till Dynamic Media Classic-servern.

#### Uppdatera de fördefinierade jobbparametrarna för bearbetning av olika filformat

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR?**

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

**RICK: BEHÅLL SOM DET ÄR**

I distributioner som inte är från Dynamic Media replikerar du *alla* resurser (både bilder och video) från Experience Manager-redigeringsmiljön till Experience Manager-publiceringsnoden. Det här arbetsflödet är nödvändigt eftersom publiceringsservrarna i Experience Manager också levererar resurserna.

I Dynamic Media-distributioner finns det dock inget behov av att replikera samma resurser till publiceringsnoderna i Experience Manager eftersom resurserna levereras via Cloud Servicen. Ett sådant&quot;hybridpubliceringsarbetsflöde&quot; undviker extra lagringskostnader och längre bearbetningstider för att replikera resurser. Annat innehåll, t.ex. webbplatssidor, fortsätter att hanteras från Experience Manager-publiceringsnoderna.

Med filtren kan du *exclude* resurser från att replikeras till publiceringsnoden Experience Manager.

#### Använd standardfiltren för replikering {#using-default-asset-filters-for-replication}

**RICK: BEHÅLL SOM DET ÄR**

Om du använder Dynamic Media för bilder, video eller båda, kan du använda standardfiltren som finns i Adobe. Följande filter är aktiva som standard:

|  | Filter | Mime-typ | Återgivningar |
| --- | --- | --- | --- |
| Dynamic Media Image Delivery | filter-image<br>filteruppsättningar | Börjar med **bild/**<br> Innehåller **program/** och avsluta med **set**. | De färdiga filterbilderna (gäller för enstaka bildresurser, inklusive interaktiva bilder) och &quot;filteruppsättningar&quot; (gäller Spin Sets, Image Sets, Mixed Media Sets och Carousel Sets) kommer att<br>・ Exkludera originalbilden och statiska bildåtergivningar från replikering. |
| Dynamic Media Video Delivery | filter-video | Börjar med **video/** | &quot;Filtrera video&quot; som är färdig att användas:<br>・ Exkludera originalvideon och statiska miniatyrrenderingar från replikering. |

>[!NOTE]
Filter gäller för MIME-typer och kan inte vara sökvägsspecifika.

#### Anpassa resursfilter för replikering {#customizing-asset-filters-for-replication}

**RICK: BEHÅLL SOM DET ÄR**

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
