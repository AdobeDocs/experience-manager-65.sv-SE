---
title: Konfigurera Dynamic Media - Scene7-läge
description: Information om hur du konfigurerar läget Dynamic Media - Scene7.
uuid: ce43c589-d415-4611-9266-b4e8887e4cdc
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 492730a1-b29c-42db-ba6b-8a48cf8ce0f2
docset: aem65
translation-type: tm+mt
source-git-commit: d357b5832a3bd95c372c26fd7553eba70583eb6f
workflow-type: tm+mt
source-wordcount: '5591'
ht-degree: 6%

---


# Konfigurera Dynamic Media - Scene7-läge{#configuring-dynamic-media-scene-mode}

Om du använder Adobe Experience Manager för olika miljöer, till exempel en för utveckling, en för staging och en för liveproduktion, måste du konfigurera Dynamic Media-Cloud Servicens för var och en av dessa miljöer.

## Arkitektur för Dynamic Media - Scene7-läge {#architecture-diagram-of-dynamic-media-scene-mode}

I följande arkitekturdiagram beskrivs hur läget Dynamic Media - Scene7 fungerar.

Med den nya arkitekturen ansvarar AEM för primära källresurser och synkronisering med Dynamic Media för bearbetning och publicering av resurser:

1. När den primära källresursen överförs till AEM replikeras den till Dynamic Media. I det läget hanterar Dynamic Media all materialbearbetning och återgivningsgenerering, till exempel videokodning och dynamiska varianter av en bild. <!-- (In Dynamic Media - Scene7 mode, be aware that you can only upload assets whose file sizes are 2 GB or less.) Jira ticket CQ-4286561 fixed this issue. DM-S7 NOW SUPPORTS THE UPLOAD OF ASSETS LARGER THAN 2 GB. -->
1. När återgivningarna har genererats kan AEM på ett säkert sätt få åtkomst till och förhandsgranska de dynamiska fjärråtergivningarna (inga binärfiler skickas tillbaka till AEM).
1. När innehållet är klart att publiceras och godkännas utlöses Dynamic Media-tjänsten att skicka ut innehållet till leveransservrar och cachelagra innehållet vid CDN.

![chlimage_1-550](assets/chlimage_1-550.png)

## Aktivera Dynamic Media i Scene7-läge {#enabling-dynamic-media-in-scene-mode}

[Dynamiska medier](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) är inaktiverade som standard. Om du vill utnyttja funktionerna för dynamiska medier måste du aktivera dem.

>[!NOTE]
>
>Dynamic Media - Scene7-läget är endast till för AEM Author-instansen. Därför måste du konfigurera `runmode=dynamicmedia_scene7` på AEM Author-instansen, *inte* AEM Publish-instansen.

Om du vill aktivera dynamiska medier måste du starta AEM med `dynamicmedia_scene7` körningsläget från kommandoraden genom att ange följande i ett terminalfönster (exempelporten som används är 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Valfritt) Migrera förinställningar och konfigurationer för dynamiska media från 6.3 till 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Om du uppgraderar AEM Dynamic Media från 6.3 till 6.4 eller 6.5 (som nu innehåller möjligheten till noll driftsättningar under driftstopp), måste du köra följande kommando för att migrera alla förinställningar och konfigurationer från `/etc` till `/conf` CRXDE Lite.

>[!NOTE]
>
>Om du kör AEM i kompatibilitetsläge, d.v.s. har kompatibilitetspaketet installerat, behöver du inte köra dessa kommandon.

För alla uppgraderingar, antingen med eller utan kompatibilitetspaketet, kan du kopiera de förinställda visningsprogrammen som ursprungligen levererades med Dynamic Media genom att köra följande kommando för Linux-vändning:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Om du vill migrera anpassade förinställningar och konfigurationer för visningsprogram som du har skapat från `/etc` till `/conf`kör du följande kommando för Linux-kontroll:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installerar funktionspaket 18912 för migrering av gruppresurser {#installing-feature-pack-for-bulk-asset-migration}

Installation av funktionspaket 18912 är *valfritt*.

Med funktionspaketet 18912 kan du antingen importera resurser gruppvis via FTP eller migrera resurser från antingen Dynamic Media - hybrid-läge eller Dynamic Media Classic till Dynamic Media - Scene7-läge AEM. Den kan fås från [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Mer information finns i [Installera funktionspaket 18912 för migrering](/help/assets/bulk-ingest-migrate.md) av gruppresurser.

## Skapa en dynamisk mediekonfiguration i Cloud Services {#configuring-dynamic-media-cloud-services}

**Innan du konfigurerar Dynamic Media**: När du har fått ditt e-postmeddelande med inloggningsuppgifter för Dynamic Media måste du [logga in](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) på Dynamic Media Classic för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att Dynamic Media Cloud Service har rätt autentiseringsuppgifter.

![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**Skapa en dynamisk mediekonfiguration i Cloud Services**

1. I AEM trycker du på den AEM logotypen för att komma åt den globala navigeringskonsolen, trycker på verktygsikonen och sedan på **[!UICONTROL Cloud Services > Dynamic Media Configuration.]**
1. På sidan Läsare för Dynamic Media-konfiguration trycker du i den vänstra rutan på **[!UICONTROL global]** (tryck inte på och välj inte mappikonen till vänster om **[!UICONTROL global]**) och sedan trycker du på **[!UICONTROL Create.]**
1. På **[!UICONTROL Create Dynamic Media Configuration]** sidan anger du en titel, e-postadress för Dynamic Media-kontot, lösenord och väljer sedan region. Dessa tillhandahålls av Adobe i e-postmeddelandet om etablering. Kontakta supporten om du inte fått detta.

   Klicka på **[!UICONTROL Connect to Dynamic Media.]**

   >[!NOTE]
   >
   >När du har fått ditt e-postmeddelande med inloggningsuppgifter för Dynamic Media loggar du [in på](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) Dynamic Media Classic för att ändra ditt lösenord. Lösenordet som anges i e-postmeddelandet om etablering genereras av systemet och är endast avsett som ett tillfälligt lösenord. Det är viktigt att du uppdaterar lösenordet så att molntjänsten Dynamic Media är konfigurerad med rätt autentiseringsuppgifter.

1. Ange följande när anslutningen lyckas. Rubriker med asterisk (*) krävs:

   * **[!UICONTROL Company]** - namnet på Dynamic Media-kontot. Det är möjligt att du har flera Dynamic Media-konton för olika undervarumärken, divisioner eller olika miljöer för staging/produktion.

   * **[!UICONTROL Company Root Folder Path]**

   * **[!UICONTROL Publishing Assets]** - Du kan välja mellan följande tre alternativ:
      * **[!UICONTROL Immediately]** betyder att när resurser överförs, importeras resurserna och URL:en/inbäddningen anges omedelbart. Ingen användaråtgärd krävs för att publicera resurser.
      * **[!UICONTROL Upon Activation]** betyder att du måste publicera resursen explicit innan en URL/Embed-länk anges.
      * **[!UICONTROL Selective Publish]** Med det här alternativet kan du styra vilka mappar som publiceras i Dynamic Media så att du kan använda funktioner som Smart beskärning eller dynamiska återgivningar, eller vilka mappar som publiceras exklusivt i AEM för förhandsgranskning. samma resurs *inte* publiceras i Dynamic Media för att distribueras i den offentliga domänen.<br>Du kan ange det här alternativet här i **[!UICONTROL Dynamic Media Cloud Configuration]** eller om du vill kan du välja att ställa in det här alternativet på mappnivå i en mapps **[!UICONTROL Properties]**.<br>Se [Arbeta med selektiv publicering i dynamiska media.](/help/assets/selective-publishing.md)<br>Observera att om du senare ändrar den här konfigurationen, eller ändrar den senare på mappnivå, påverkar dessa ändringar bara nya resurser som du överför från den punkten och framåt. Publiceringsläget för befintliga resurser i mappen ändras inte förrän du ändrar dem manuellt från antingen **[!UICONTROL Quick Publish]** eller **[!UICONTROL Manage Publication]** dialogrutan.
   * **[!UICONTROL Secure Preview Server]** - gör att du kan ange URL-sökvägen till förhandsgranskningsservern för säkra återgivningar. Det innebär att när renderingar har genererats kan AEM på ett säkert sätt komma åt och förhandsgranska de dynamiska fjärrrenderingarna (inga binärfiler skickas tillbaka till AEM).
Om du inte har ett särskilt arrangemang för att använda ditt företags server eller en speciell server rekommenderar Adobe Systems att du låter den här inställningen vara kvar som den har angetts.

   * **[!UICONTROL Sync all content]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Markerat som standard. Avmarkera det här alternativet om du vill inkludera eller exkludera resurser från synkroniseringen till dynamiska media. Om du avmarkerar det här alternativet kan du välja mellan följande två synkroniseringslägen för dynamiska media:

   * **[!UICONTROL Dynamic Media sync mode]**
      * **[!UICONTROL Enabled by default]** - Konfigurationen används som standard på alla mappar såvida du inte markerar en mapp som är exkluderad. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Disabled by default]** - Konfigurationen tillämpas inte på någon mapp förrän du uttryckligen markerar en vald mapp för synkronisering till Dynamic Media.
Om du vill markera en markerad mapp för synkronisering till dynamiska media markerar du en resursmapp och klickar sedan på **[!UICONTROL Properties.]** På **[!UICONTROL Details]** -fliken i **[!UICONTROL Dynamic Media sync mode]** listrutan på följande tre alternativ. När du är klar trycker du på **[!UICONTROL Save.]** *Kom ihåg: Dessa tre alternativ är inte tillgängliga om du valde **Synkronisera allt innehåll**tidigare.* Se även [Arbeta med selektiv publicering på mappnivå i Dynamic Media.](/help/assets/selective-publishing.md)
         * **[!UICONTROL Inherited]** - Det finns inget explicit synkroniseringsvärde i mappen; I stället ärver mappen synkroniseringsvärdet från någon av dess överordnade mappar eller standardläget i molnkonfigurationen. Detaljerad status för ärvda program genom ett verktygstips.
         * **[!UICONTROL Enable for sub-folders]** - Inkludera allt i det här underträdet för synkronisering till Dynamic Media. De mappspecifika inställningarna åsidosätter standardläget i molnkonfigurationen.
         * **[!UICONTROL Disabled for sub-folders]** - Uteslut allt i det här underträdet från synkronisering till Dynamic Media.

   >[!NOTE]
   >
   >Det finns inget stöd för versionshantering i DMS7. Dessutom gäller fördröjd aktivering endast om **[!UICONTROL Publish Assets]** på sidan Redigera Dynamic Media-konfiguration är inställd på **[!UICONTROL Upon Activation]** och då endast tills resursen aktiveras första gången.
   >
   >
   >När en mediefil har aktiverats publiceras uppdateringar direkt till S7 Delivery.

1. Tryck på **[!UICONTROL Save.]**
1. Om du vill förhandsgranska dynamiskt mediematerial på ett säkert sätt innan det publiceras måste du &quot;tillåtslista&quot; den AEM författarinstansen för att ansluta till Dynamic Media:

   * Logga in på ditt konto för Dynamic Media Classic: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html). Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.
   * Klicka på i navigeringsfältet uppe till höger på sidan **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server.]**

   * På sidan Image Server Publish (Publicera kontext) väljer du **[!UICONTROL Test Image Serving.]**
   * Tryck på för klientadressfiltret **[!UICONTROL Add.]**
   * Markera kryssrutan för att aktivera (aktivera) adressen och ange sedan IP-adressen för AEM Author-instansen (inte Dispatcher IP).
   * Klicka på **[!UICONTROL Save.]**

Du är nu klar med den grundläggande konfigurationen; är du redo att använda läget Dynamic Media - Scene7.

Om du vill anpassa konfigurationen ytterligare kan du utföra alla åtgärder under [(Valfritt) Konfigurera avancerade inställningar i läget](#optionalconfigurationofadvancedsettingindynamicmediascene7mode)Dynamic Media - Scene7.

## (Valfritt) Konfigurera avancerade inställningar i Dynamic Media - Scene7-läge {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Om du vill anpassa konfigurationen och konfigurationen av läget Dynamic Media - Scene7 ytterligare, eller optimera prestandan, kan du utföra en eller flera av följande *valfria* uppgifter:

* [(Valfritt) Installation och konfiguration av Dynamic Media - Scene7-lägesinställningar](#optionalsetupandconfigurationofdynamicmediascene7modesettings)

* [(Valfritt) Justera prestanda för Dynamic Media - Scene7-läge](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Valfritt) Filtrera resurser för replikering](#optional-filtering-assets-for-replication)

### (Valfritt) Installation och konfiguration av Dynamic Media - Scene7-lägesinställningar</p> {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings-p}

När du är i körläge `dynamicmedia_scene7`använder du användargränssnittet för Dynamic Media Classic (Scene7) för att göra ändringar i inställningarna för Dynamic Media.

Vissa av ovanstående uppgifter kräver att du loggar in på Dynamic Media Classic (Scene7) här: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

Installations- och konfigureringsuppgifter omfattar följande:

* [Publiceringskonfiguration för Image Server](#publishing-setup-for-image-server)
* [Konfigurera allmänna inställningar för programmet](#configuring-application-general-settings)
* [Konfigurera färghantering](#configuring-color-management)
* [Konfigurera bearbetning av resurser](#configuring-asset-processing)
* [Lägga till anpassade MIME-typer för format som inte stöds](#adding-custom-mime-types-for-unsupported-formats)
* [Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Publiceringskonfiguration för Image Server {#publishing-setup-for-image-server}

Publiceringsinställningarna avgör hur resurser levereras som standard från Dynamic Media. Om ingen inställning anges levererar Dynamic Media en resurs enligt standardinställningarna som definierats i Publiceringsinställningar. En begäran om att leverera en bild som inte innehåller ett upplösningsattribut ger till exempel en bild med inställningen för standardobjektupplösning.

Så här konfigurerar du publiceringsinställningar: i Dynamic Media Classic klickar du på **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server.]**

Bildserverskärmen anger standardinställningar för att leverera bilder. I gränssnittsskärmen finns en beskrivning av varje inställning.

* **[!UICONTROL Request Attributes]** - De här inställningarna begränsar antalet bilder som kan levereras från servern.
* **[!UICONTROL Default Request Attributes]** - De här inställningarna gäller standardutseendet för bilder.
* **[!UICONTROL Common Thumbnail Attributes]** - De här inställningarna gäller för miniatyrbildernas standardutseende.
* **[!UICONTROL Defaults for Catalog Fields]**- De här inställningarna gäller bildernas upplösning och standardtyp av miniatyrbilder.
* **[!UICONTROL Color Management Attributes]** - De här inställningarna avgör vilka ICC-färgprofiler som används.
* **[!UICONTROL Compatibility Attributes]** - Den här inställningen gör att inledande och avslutande stycken i textlager kan hanteras som de var i version 3.6 för bakåtkompatibilitet.
* **[!UICONTROL Localization Support]** - Med de här inställningarna kan du hantera flera språkattribut. Här kan du också ange en sträng för språkområdeskarta så att du kan definiera vilka språk du vill ha stöd för de olika verktygstipsen i visningsprogram. Mer information om hur du konfigurerar **[lokaliseringsstöd]** finns i [Saker att tänka på när du konfigurerar lokalisering av resurser](https://help.adobe.com/en_US/scene7/using/WS997f1dc4cb0179f034e07dc31412799d19a-8000.html).

#### Konfigurera allmänna inställningar för programmet {#configuring-application-general-settings}

Öppna sidan Allmänna inställningar för programmet genom att klicka på i fältet Global navigering i Dynamic Media Classic **[!UICONTROL Setup > Application Setup > General Settings.]**

**Servrar - **On account provisioning, ger Dynamic Media automatiskt de servrar som är tilldelade ditt företag. De här servrarna används för att skapa URL-strängar för din webbplats och dina program. Dessa URL-anrop är specifika för ditt konto. Ändra inte något av servernamnen om du inte uttryckligen har fått instruktioner om att göra det av AEM.

**[!UICONTROL Overwrite Images]** - Dynamic Media tillåter inte att två filer har samma namn. Varje objekts URL-ID (filnamnet minus filtillägget) måste vara unikt. De här alternativen anger hur ersättningsresurser överförs: om de ersätter originalet eller blir dubbletter. Duplicerade resurser får ett nytt namn med namnet&quot;-1&quot; (till exempel heter stol.tif stol-1.tif). Dessa alternativ påverkar resurser som överförts till en annan mapp än den ursprungliga eller resurser med ett annat filnamnstillägg än den ursprungliga (till exempel JPG, TIF eller PNG).

* **[!UICONTROL Overwrite in current folder, same base image name/extension]** - Det här alternativet är den striktaste regeln för ersättning. Det kräver att du överför ersättningsbilden till samma mapp som originalbilden och att ersättningsbilden har samma filnamnstillägg som originalbilden. Om dessa krav inte uppfylls skapas en dubblett.

>[!NOTE]
>
>Välj alltid den här inställningen om du vill att AEM ska vara konsekvent: **Skriv över i den aktuella mappen, samma basbildens namn/tillägg**

* **[!UICONTROL Overwrite in any folder, same base asset name/extension]** - Kräver att ersättningsbilden har samma filnamnstillägg som originalbilden (t.ex. måste stol.jpg ersätta stol.jpg, inte stol.tif). Du kan dock överföra ersättningsbilden till en annan mapp än den ursprungliga. Den uppdaterade bilden finns i den nya mappen; filen inte längre kan hittas på sin ursprungliga plats
* **[!UICONTROL Overwrite in any folder, same base asset name regardless of extension]** - Det här alternativet är den mest omfattande ersättningsregeln. Du kan överföra en ersättningsbild till en annan mapp än den ursprungliga, överföra en fil med ett annat filnamnstillägg och ersätta den ursprungliga filen. Om originalfilen finns i en annan mapp finns ersättningsbilden i den nya mappen som den överfördes till.

**[!UICONTROL Default Color Profiles]** - Mer information finns i [Konfigurera färghantering](#configuring-color-management) .

>[!NOTE]
>
>Som standard visas 15 återgivningar när du väljer **[!UICONTROL Renditions]** och 15 visningsförinställningar när du väljer **[!UICONTROL Viewers]** i resursens detaljvy. Du kan öka den här gränsen. See [Increasing the number of image presets that display](/help/assets/managing-image-presets.md#increasingthenumberofimagepresetsthatdisplay) or [Increasing the number of viewer presets that display](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).


#### Konfigurera färghantering {#configuring-color-management}

Med dynamisk mediefärghantering kan du färgkorrigera resurser. Med färgkorrigering behåller inkapslade resurser sin färgmodell (RGB, CMYK, Grå) och inbäddad färgprofil. När du begär en dynamisk återgivning korrigeras bildfärgen till målfärgrymden med hjälp av CMYK-, RGB- eller grå utdata. Se [Konfigurera bildförinställningar](/help/assets/managing-image-presets.md).

Så här konfigurerar du standardfärgegenskaperna så att färgkorrigering aktiveras när du begär bilder:

1. [Logga in på Dynamic Media Classic](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) med de autentiseringsuppgifter som angavs under etableringen. Navigera till **[!UICONTROL Setup > Application Setup.]**
1. Expandera **[!UICONTROL Publish Setup]** området och välj **[!UICONTROL Image Server.]** Ange **[!UICONTROL Publish Context]** till **[!UICONTROL Image Serving]** när du anger standardvärden för publiceringsinstanser.
1. Bläddra till den egenskap som du behöver ändra, till exempel en egenskap i **[!UICONTROL Color Management Attributes]** området.

   Du kan ange följande egenskaper för färgkorrigering:

   * **[!UICONTROL CMYK Default Color Space]** - Namn på CMYK-standardfärgprofil
   * **[!UICONTROL Gray-Scale Default Color Space]** - Namn på standardfärgprofilen för gråskala
   * **[!UICONTROL RGB Default Color Space]** - Namn på standardfärgprofilen för RGB
   * **[!UICONTROL Color Conversion Rendering Intent]** - Anger återgivningsmetod. Godtagbara värden är: **[!UICONTROL perceptual]**, **[!UICONTROL relative colometric]**, **[!UICONTROL saturation]**, **[!UICONTROL absolute colometric.]** Adobe rekommenderar **[!UICONTROL relative]** som standard.

1. Tryck på **[!UICONTROL Save.]**

Du kan till exempel ställa in **[!UICONTROL RGB Default Color Space]** på *sRGB* och **[!UICONTROL CMYK Default Color Space]** på *WebCoated*.

Om du gör det gör du så här:

* Aktiverar färgkorrigering för RGB- och CMYK-bilder.
* RGB-bilder som inte har någon färgprofil antas finnas i *färgrymden sRGB* .
* CMYK-bilder som inte har någon färgprofil antas finnas i *WebCoated* -färgmodellen.
* Dynamiska renderingar som returnerar RGB-utdata returnerar den i färgrymden *sRGB *.
* Dynamiska återgivningar som returnerar CMYK-utdata returnerar det i *WebCoated* -färgrymden.

#### Konfigurera bearbetning av resurser {#configuring-asset-processing}

Du kan definiera vilka resurstyper som ska bearbetas av Dynamic Media och anpassa avancerade parametrar för resurshantering. Du kan till exempel ange parametrar för tillgångsbearbetning för att göra följande:

* Konvertera en Adobe PDF till en eCatalog-resurs.
* Konvertera ett Adobe Photoshop-dokument (.PSD) till en bannermallsresurs för personalisering.
* Rastrera en Adobe Illustrator-fil (.AI) eller en Adobe Photoshop Encapsulated Postscript-fil (.EPS).
* Obs! Videoprofiler och bildprofiler kan användas för att definiera bearbetning av videoklipp och bilder.

Se [Överföra resurser](/help/assets/managing-assets-touch-ui.md#uploading-assets).

**Så här konfigurerar du bearbetning av resurser**

1. In AEM, click the AEM logo to access the global navigation console, then click **[!UICONTROL Tools > General > CRXDE Lite.]**
1. Navigera till följande i den vänstra listen:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![mimetypes](assets/mimetypes.png)

1. Välj en mime-typ i mappen mimeTypes.
1. Till höger på CRXDE Lite-sidan i den nedre delen:

   * dubbelklicka på **[!UICONTROL enabled]** fältet. Som standard är alla resursens MIME-typer aktiverade (inställda på **[!UICONTROL true]**), vilket innebär att resurserna synkroniseras till Dynamic Media för bearbetning. Om du vill utesluta den här resursens MIME-typ från bearbetningen ändrar du den här inställningen till **[!UICONTROL false.]**

   * dubbelklicka **[!UICONTROL jobParam]** för att öppna det tillhörande textfältet. Se [Mime-typer](/help/assets/assets-formats.md#supported-mime-types) som stöds för en lista över tillåtna värden för processparametrar som du kan använda för en viss MIME-typ.

1. Gör något av följande:

   * Upprepa steg 3-4 om du vill redigera ytterligare MIME-typer.
   * På menyraden på CRXDE Lite-sidan klickar du på **[!UICONTROL Save All.]**

1. Tryck för **[!UICONTROL CRXDE Lite]** att gå tillbaka till AEM i det övre vänstra hörnet på sidan.

#### Lägga till anpassade MIME-typer för format som inte stöds {#adding-custom-mime-types-for-unsupported-formats}

Du kan lägga till anpassade MIME-typer för format som inte stöds i AEM Assets. För att säkerställa att nya noder som du lägger till i CRXDE Lite inte tas bort av AEM måste du se till att du placerar MIME-typen före `image_` och att dess aktiverade värde är inställt på **[!UICONTROL false.]**

**Lägga till anpassade MIME-typer för format som inte stöds**

1. Från AEM, tryck **[!UICONTROL Tools > Operations > Web Console.]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. En ny flik i webbläsaren öppnas på **[!UICONTROL Adobe Experience Manager Web Console Configuration]** sidan.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. På sidan bläddrar du nedåt till namnet *Adobe CQ Scene7 Asset MIME type Service* enligt följande skärmbild. Tryck på **[!UICONTROL Edit the configuration values]** (pennikonen) till höger om namnet.

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. På sidan för **Adobe CQ Scene7 Asset MIME-typtjänst** klickar du på en plusteckenikon &lt;+>. Platsen i tabellen där du klickar på plustecknet för att lägga till den nya mime-typen är enkel.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Skriv `DWG=image/vnd.dwg` i det tomma textfältet som du just lade till.

   Observera att exemplet bara `DWG=image/vnd.dwg` är för illustrationsändamål. MIME-typen som du lägger till här kan vara ett annat format som inte stöds.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. In the lower-right corner of the page, tap **[!UICONTROL Save.]**

   Nu kan du stänga webbläsarfliken som har den öppna konfigurationssidan för Adobe Experience Manager Web Console.

1. Gå tillbaka till webbläsarfliken som har din öppna AEM.
1. Från AEM, tryck **[!UICONTROL Tools > General > CRXDE Lite.]**

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Navigera till följande i den vänstra listen:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Dra MIME-typen `image_vnd.dwg` och släpp den direkt ovanför `image_` i trädet så som visas på skärmbilden nedan.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Med mime-typen `image_vnd.dwg` markerad dubbelklickar du på värdet på fliken **[!UICONTROL Properties]**, på raden **[!UICONTROL enabled]**, under kolumnrubriken **[!UICONTROL Value]**, för att öppna listrutan **[!UICONTROL Value]**.
1. Skriv `false` i fältet (eller välj **[!UICONTROL false]** från listrutan).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Near the upper-left corner of the CRXDE Lite page, click **[!UICONTROL Save All.]**

#### Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurpuppsättningar {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Använd förinställningar för gruppuppsättningar för att automatisera skapandet av bilduppsättningar eller snurruppsättningar medan resurser överförs till Dynamic Media.

Definiera först namnkonventionen för hur resurser ska grupperas tillsammans i en uppsättning. Du kan sedan skapa en gruppuppsättningsförinställning som är en unik, självständig uppsättning instruktioner som definierar hur uppsättningen ska skapas med bilder som matchar de definierade namnkonventionerna i förinställningsreceptet.

När du överför filer skapar Dynamic Media automatiskt en uppsättning med alla filer som matchar den definierade namnkonventionen i de aktiva förinställningarna.

**Konfigurerar standardnamngivning**

Skapa en standardnamnkonvention som används i alla förinställda gruppuppsättningar. Den standardnamnkonvention som valts i förinställningsdefinitionen för gruppuppsättning kan vara allt ditt företag behöver för att gruppgenerera uppsättningar. En gruppuppsättningsförinställning skapas för att använda den standardnamnkonvention som du definierar. Du kan skapa så många gruppuppsättningsförinställningar med alternativa, anpassade namnkonventioner som behövs för en viss uppsättning innehåll om det finns ett undantag från den företagsdefinierade standardnamngivningen.

När det inte krävs någon standardnamnkonvention för att använda funktionen för gruppuppsättningsförinställningar rekommenderar vi att du använder standardnamnkonventionen för att definiera så många element i namnkonventionen som du vill gruppera i en uppsättning så att du kan effektivisera skapandet av gruppuppsättningar.

Observera också att du kan använda **[!UICONTROL View Code]** utan formulärfält. I den här vyn skapar du namnkonventionens definitioner helt med hjälp av reguljära uttryck.

Det finns två element för definition, Matcha och Basnamn. Med dessa fält kan du definiera alla element i en namnkonvention och identifiera den del av konventionen som används för att namnge den uppsättning i vilken de finns. Ett företags personliga namnkonvention kan använda en eller flera definitionsrader för vart och ett av dessa element. Du kan använda så många rader för din unika definition och gruppera dem i distinkta element, t.ex. för Huvudbild, Färgelement, Alternativa vyer och Färgruteelement.

**Konfigurera standardnamn**

1. Logga in på ditt konto för Dynamic Media Classic (Scene7): [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Tryck på **[!UICONTROL Setup > Application Setup > Batch Set Presets > Default Naming.]**
1. Välj **[!UICONTROL View Form]** eller **[!UICONTROL View Code]** för att ange hur du vill visa och ange information om varje element.

   Du kan markera kryssrutan om du vill visa värdeuppbyggnaden för det reguljära uttrycket tillsammans med dina formulärval. **[!UICONTROL View Code]** Du kan ange eller ändra dessa värden för att underlätta definitionen av elementen i namnkonventionen, om formulärvyn begränsar dig av någon anledning. Om dina värden inte kan tolkas i formulärvyn blir formulärfälten inaktiva.

   >[!NOTE]
   >
   >Inaktiverade formulärfält verifierar inte att reguljära uttryck är korrekta. Resultaten av det reguljära uttryck som du skapar för varje element efter resultatraden visas. Det fullständiga reguljära uttrycket visas längst ned på sidan.

1. Expandera varje element efter behov och ange de namnkonventioner som du vill använda.
1. Gör något av följande om det behövs:

   * Tryck för **[!UICONTROL Add]** att lägga till en annan namnkonvention för ett element.
   * Tryck för **[!UICONTROL Remove]** att ta bort en namnkonvention för ett element.

1. Gör något av följande:

   * Tryck **[!UICONTROL Save As]** och skriv ett namn för förinställningen.
   * Tryck **[!UICONTROL Save]** om du redigerar en befintlig förinställning.

**Skapa en förinställning för gruppuppsättning**

I Dynamic Media används gruppuppsättningsförinställningar för att ordna resurser i uppsättningar med bilder (alternativa bilder, färgalternativ, 360-rotation) för visning i visningsprogram. Förinställningarna för gruppuppsättningar körs automatiskt tillsammans med överföringsprocesserna för resurser i Dynamic Media.

Du kan skapa, redigera och hantera dina gruppuppsättningsförinställningar. Det finns två former av förinställda gruppuppsättningsdefinitioner: en för en standardnamnkonvention som du kan ha konfigurerat och en för anpassade namnkonventioner som du skapar direkt.

Du kan antingen använda formulärfältsmetoden för att definiera en gruppuppsättningsförinställning eller kodmetoden, som gör att du kan använda reguljära uttryck. Precis som i Standardnamn kan du välja Visa kod samtidigt som du definierar i formulärvyn och använda reguljära uttryck för att skapa definitioner. Du kan också avmarkera en vy om du vill använda den ena eller den andra enbart.

**Skapa en förinställning för gruppuppsättning**

1. Logga in på ditt konto för Dynamic Media Classic (Scene7): [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Tryck på **[!UICONTROL Setup > Application Setup > Batch Set Presets > Batch Set Preset.]**

   Observera att **[!UICONTROL View Form]** standardvyn är inställd i det övre högra hörnet på detaljsidan.

1. Tryck på panelen Förinställningslista för **[!UICONTROL Add]** att aktivera definitionsfälten på panelen Detaljer till höger på skärmen.
1. Skriv ett namn på förinställningen i fältet Förinställningsnamn på panelen Detaljer.
1. Välj en förinställningstyp i listrutan Gruppuppsättningstyp.
1. Gör något av följande:

   * Om du använder en standardnamnkonvention som du tidigare har konfigurerat under **[!UICONTROL Application Setup > Batch Set Presets > Default Naming]** expanderar du **[!UICONTROL Asset Naming Conventions]** och trycker sedan på **[!UICONTROL Default.]**

   * To define a new naming convention as you set up the preset, expand **[!UICONTROL Asset Naming Conventions]**, and then in the File Naming drop-down list, click **[!UICONTROL Custom.]**

1. I Sekvensordning definierar du i vilken ordning bilderna ska visas efter att uppsättningen har grupperats tillsammans i Dynamic Media.

   Som standard sorteras dina resurser alfanumeriskt. Du kan dock använda en kommaavgränsad lista med reguljära uttryck för att definiera ordningen.

1. Ange suffixet eller prefixet till basnamnet som du definierade i konventionen om namngivning av tillgångar för Ange namngivning och skapande. Definiera också var uppsättningen ska skapas i mappstrukturen Dynamic Media.

   Om du definierar ett stort antal uppsättningar kanske du föredrar att hålla dessa åtskilda från de mappar som innehåller själva resurserna. Du kan till exempel skapa en mapp för bilduppsättningar och placera genererade uppsättningar här.

1. Tryck på **[!UICONTROL Save.]**
1. Tryck **[!UICONTROL Active]** bredvid den nya förinställningens namn.

   När du aktiverar förinställningen används den för att generera uppsättningen när du överför resurser till dynamiska media.

**Skapa en gruppuppsättningsförinställning för automatisk generering av en 2D-snurpuppsättning**

Du kan använda gruppuppsättningstypen **[!UICONTROL Multi-Axis Spin Set]** för att skapa ett recept som automatiserar genereringen av 2D-snurpuppsättningar. Vid gruppering av bilder används reguljära uttryck för rad och kolumn så att bildresurserna justeras korrekt på motsvarande plats i den flerdimensionella arrayen. Det finns inget minsta eller högsta antal rader eller kolumner som du måste ha i en rotationsuppsättning med flera axlar.

Anta till exempel att du vill skapa en fleraxelsnurvuppsättning med namnet `spin-2dspin`. Du har en uppsättning bilder med snurra uppsättningar som innehåller tre rader, med 12 bilder per rad. Bilderna får följande namn:

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Med den här informationen kan ditt recept för gruppuppsättningstyp skapas på följande sätt:

![chlimage_1-560](assets/chlimage_1-560.png)

Gruppering för den delade resursnamnsdelen av rotationsuppsättningen läggs till i fältet **Matcha** (markerat). Variabeldelen av resursnamnet som innehåller raden och kolumnen läggs till i fälten **Rad** och **Kolumn**.

När rotationsuppsättningen har överförts och publicerats aktiverar du namnet på det 2D-rotationsuppsättningsrecept som visas under **Förinställningar för gruppuppsättning** i dialogrutan **Alternativ för överföringsjobb**.

**Skapa en gruppuppsättningsförinställning för automatisk generering av en 2D-snurpuppsättning**

1. Logga in på ditt konto för Dynamic Media Classic (Scene7): [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. I navigeringsfältet nära sidans överkant klickar du på **[!UICONTROL Setup]>[!UICONTROL Application Setup]>[!UICONTROL Batch Set Presets]>[!UICONTROL Batch Set Preset]**.

   Observera att **[!UICONTROL View Form]** standardvyn är inställd i det övre högra hörnet på detaljsidan.

1. Klicka på panelen Förinställningslista för **[!UICONTROL Add]** att aktivera definitionsfälten på panelen Detaljer till höger på skärmen.
1. Skriv ett namn på förinställningen i fältet Förinställningsnamn på panelen Detaljer.
1. I listrutan Gruppuppsättningstyp väljer du **[!UICONTROL Asset Set.]**
1. I listrutan Undertyp väljer du **[!UICONTROL Multi-Axis Spin Set.]**
1. Expandera **[!UICONTROL Asset Naming Conventions]** och klicka sedan på i listrutan Namnge fil **[!UICONTROL Custom.]**
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

   Kom ihåg att detta bara är exempel. Du kan skapa det reguljära uttrycket hur du vill.

   >[!NOTE]
   >
   >Om kombinationen av reguljära uttryck för rader och kolumner inte kan avgöra positionen för resursen i den flerdimensionella spinset-arrayen, läggs resursen inte till i uppsättningen och ett fel loggas.

1. Ange suffixet eller prefixet till basnamnet som du definierade i konventionen om namngivning av tillgångar för Ange namngivning och skapande.

   Definiera också var rotationsuppsättningen ska skapas i mappstrukturen Dynamic Media Classic.

   Om du definierar ett stort antal uppsättningar kanske du föredrar att hålla dessa åtskilda från de mappar som innehåller själva resurserna. Du kan till exempel skapa en mapp för snurruppsättningar där du kan placera genererade uppsättningar här.

1. Klicka på panelen Detaljer **[!UICONTROL Save.]**
1. Klicka **[!UICONTROL Active]** bredvid den nya förinställningens namn.

   När du aktiverar förinställningen används den för att generera uppsättningen när du överför resurser till dynamiska media.

### (Valfritt) Justera prestanda för Dynamic Media - Scene7-läge {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

För att Dynamic Media - Scene7-läget ska fungera smidigt rekommenderar Adobe följande finjusteringstips för synkroniseringsprestanda/skalbarhet:

* Uppdaterar de fördefinierade jobbparametrarna för bearbetning av olika filformat.
* Uppdaterar de fördefinierade arbetstrådarna för Granite-arbetsflödet (videoresurser).
* Uppdaterar det fördefinierade tillfälliga Granite-arbetsflödet (bilder och icke-videomaterial) för köarbetstrådar.
* Uppdaterar de maximala överföringsanslutningarna till Dynamic Media Classic-servern.

#### Uppdatera de fördefinierade jobbparametrarna för bearbetning av olika filformat

Du kan justera jobbparametrar för snabbare bearbetning när du överför filer. Om du till exempel överför PSD-filer, men inte vill bearbeta dem som mallar, kan du ange att lagerextraheringen ska vara false (av). I så fall visas den justerade jobbparametern som `process=None&createTemplate=false`.

Adobe rekommenderar att du använder följande&quot;justerade&quot; jobbparametrar för PDF-, PostScript- och PSD-filer:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Filtyp | Rekommenderade jobbparametrar |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| Postscript | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

Om du vill uppdatera någon av de här parametrarna följer du stegen i [Aktivera stöd](#enabling-mime-type-based-assets-scene-upload-job-parameter-support)för MIME-typbaserade resurser/Dynamic Media Classic-överföringsjobbparametrar.

#### Uppdatera den tillfälliga arbetsflödeskön för Granite {#updating-the-granite-transient-workflow-queue}

Kön för Bevilja överföring av arbetsflöde används för **[!UICONTROL DAM Update Asset]** arbetsflödet. I Dynamic Media används den för bildinläsning och bearbetning.

**Så här uppdaterar du den tillfälliga arbetsflödeskön för Granite**

1. Gå till [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) och sök efter **kö: Bevilja en tillfällig arbetsflödeskö**.

   >[!NOTE]
   >
   >En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I **[!UICONTROL Maximum Parallel Jobs]** fältet ändrar du talet till önskat värde.

   Som standard beror det maximala antalet parallella jobb på antalet tillgängliga processorkärnor. På en server med fyra kärnor tilldelas till exempel två arbetstrådar. (Ett värde mellan 0,0 och 1,0 är baserat på förhållandet, eller alla tal som är större än 1 tilldelar antalet arbetstrådar.)

   Adobe rekommenderar att 32 **[!UICONTROL Maximum Parallel Jobs]** är konfigurerat för att ge tillräckligt stöd för överföring av filer till Dynamic Media Classic (Scene7).

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Tryck på **[!UICONTROL Save.]**

#### Uppdaterar arbetsflödeskön Granite {#updating-the-granite-workflow-queue}

Beviljad arbetsflödeskö används för icke-tillfälliga arbetsflöden. I Dynamic Media brukade det bearbeta video med **[!UICONTROL Dynamic Media Encode Video]** arbetsflödet.

**Så här uppdaterar du arbetsflödeskön för Granite**

1. Navigera till `https://<server>/system/console/configMgr` och sök efter **kö: Begränsa arbetsflödeskö**.

   >[!NOTE]
   >
   >En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I **[!UICONTROL Maximum Parallel Jobs]** fältet ändrar du talet till önskat värde.

   Som standard beror det maximala antalet parallella jobb på antalet tillgängliga processorkärnor. På en server med fyra kärnor tilldelas till exempel två arbetstrådar. (Ett värde mellan 0,0 och 1,0 är baserat på förhållandet, eller alla tal som är större än 1 tilldelar antalet arbetstrådar.)

   I de flesta fall räcker standardinställningen 0,5.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Tryck på **[!UICONTROL Save.]**

#### Uppdaterar anslutningen för Dynamic Media Classic-överföring {#updating-the-scene-upload-connection}

Inställningen Scene7 Upload Connection synkroniserar AEM till Dynamic Media Classic-servrar.

**Så här uppdaterar du den dynamiska Media Classic-överföringsanslutningen**

1. Navigera till `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. I **[!UICONTROL Number of connections]** fältet och/eller i **[!UICONTROL Active job timeout]** fältet ändrar du numret.

   Inställningen styr det maximala antalet HTTP-anslutningar som tillåts för AEM till Dynamic Media-överföring. **[!UICONTROL Number of connections]** vanligtvis räcker det fördefinierade värdet på 10 anslutningar.

   Inställningen avgör **[!UICONTROL Active job timeout]** väntetiden för när överförda dynamiska medieresurser ska publiceras på leveransservern. Det här värdet är som standard 2 100 sekunder eller 35 minuter.

   I de flesta fall räcker det med inställningen 2 100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Tryck på **[!UICONTROL Save.]**

### (Valfritt) Filtrera resurser för replikering {#optional-filtering-assets-for-replication}

I distributioner av icke-dynamiska media replikerar du *alla* resurser (både bilder och video) från AEM redigeringsmiljö till AEM publiceringsnod. Det här arbetsflödet är nödvändigt eftersom AEM publiceringsservrar också levererar resurserna.

I Dynamic Media-distributioner behöver du dock inte replikera samma resurser till publiceringsnoder eftersom resurserna levereras via molntjänsten AEM. Ett sådant&quot;hybridpubliceringsarbetsflöde&quot; undviker extra lagringskostnader och längre bearbetningstider för att replikera resurser. Annat innehåll, t.ex. webbplatssidor, fortsätter att hanteras från de AEM publiceringsnoderna.

Med filtren kan du *utesluta* resurser från replikering till AEM publiceringsnod.

#### Använda standardresursfilter för replikering {#using-default-asset-filters-for-replication}

Om du använder Dynamic Media för bild och/eller video kan du använda de standardfilter som vi tillhandahåller i befintligt skick. Följande filter är aktiva som standard:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>MimeterType</strong></td>
   <td><strong>Återgivningar</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filterbilder</p> <p>filteruppsättningar</p> <p> </p> </td>
   <td><p>Börjar med <strong>bild/</strong></p> <p>Innehåller <strong>program/</strong> och slutar med <strong>en uppsättning</strong>.</p> </td>
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
>
>Filter gäller för MIME-typer och kan inte vara sökvägsspecifika.

#### Anpassa resursfilter för replikering {#customizing-asset-filters-for-replication}

1. In AEM, tap the AEM logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite.]**
1. Navigera till det vänstra mappträdet för `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` att granska filtren.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Du definierar Mime-typen för filtret genom att leta reda på Mime-typen enligt följande:

   I den vänstra listen expanderar du `content > dam > <locate_your_asset> > jcr:content > metadata`och letar upp `dc:format`.

   Följande bild är ett exempel på en resurs sökväg till `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observera att `dc:format` för tillgången `Fiji Red.jpg` är `image/jpeg`.

   Om du vill att det här filtret ska gälla för alla bilder, oavsett format, anger du värdet `image/*` där `*` är ett reguljärt uttryck som ska användas för alla bilder i alla format.

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
   <td>Jokertecken<br /> </td>
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

