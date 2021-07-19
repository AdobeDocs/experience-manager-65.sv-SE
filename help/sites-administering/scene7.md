---
title: Integrera Adobe Experience Manager med Dynamic Media Classic
description: Lär dig hur du integrerar Adobe Experience Manager med Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '5295'
ht-degree: 1%

---

# Integrera Adobe Experience Manager med Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic är en värdbaserad lösning för att hantera, förbättra, publicera och distribuera multimediematerial för webben, mobiler, e-post och internetanslutna skärmar och för tryck.

Om du vill använda Dynamic Media Classic måste du konfigurera molnkonfigurationen så att Dynamic Media Classic och Adobe Experience Manager Assets kan samverka med varandra. I det här dokumentet beskrivs hur du konfigurerar Experience Manager och Dynamic Media Classic.

Information om hur du använder alla Dynamic Media Classic-komponenter på en sida och arbetar med video finns i [Använd Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* Dynamic Media Classic&#39;s DHTML viewer Platform nåddes officiellt den 31 januari 2014. Mer information finns i [Vanliga frågor och svar om DHTML-visningsprogrammet](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Innan du konfigurerar Dynamic Media Classic att arbeta med Experience Manager bör du läsa [Bästa praxis](#best-practices-for-integrating-scene-with-aem) för integrering av Dynamic Media Classic med Experience Manager.
>* Om du använder Dynamic Media Classic med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i Experience Manager använder 3.x-API:erna och andra använder 4.x-API:erna. 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) och 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).

>



## Integrering med Experience Manager/Dynamic Media Classic jämfört med Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Experience Manager-användare kan välja mellan två lösningar för Dynamic Media. Du kan använda något av följande:

* Integrera din instans av Experience Manager med Dynamic Media Classic.
* Använd Dynamic Media som är integrerat i Experience Manager.

Använd följande kriterier för att avgöra vilken lösning du ska välja:

* Är du **befintlig** Dynamic Media Classic-kund vars resurser finns i Dynamic Media Classic för publicering och leverans, men du vill integrera dessa resurser med hjälp av webbplatsutveckling (WCM), Experience Manager Assets eller båda? Om så är fallet använder du [Experience Manager/Dynamic Media Classic point-to-point integration](#aem-scene-point-to-point-integration) som beskrivs i det här dokumentet.

* Om du är **ny**-Experience Manager-kund och har behov av multimedieleverans väljer du alternativet [Dynamic Media](#aem-dynamic-media). Det här alternativet är bäst om du inte har något befintligt S7-konto och många resurser lagrade i det systemet.

* Använd båda lösningarna i vissa fall. I [scenariot med dubbla användningsområden](/help/sites-administering/scene7.md#dual-use-scenario) beskrivs det scenariot.

### Experience Manager/Dynamic Media Classic point-to-point-integrering {#aem-scene-point-to-point-integration}

När du arbetar med resurser i den här lösningen gör du något av följande:

* Ladda upp material direkt till Dynamic Media Classic och gå sedan till via **Dynamic Media Classic**-webbläsaren för att skapa sidor eller
* Överför till Experience Manager Assets och aktivera sedan automatisk publicering till Dynamic Media Classic. du kommer åt via **Resurser** i webbläsaren för att skapa sidor

Komponenterna som du använder för den här integreringen finns i **Dynamic Media Classic**-komponentområdet i [Designläge](/help/sites-authoring/author-environment-tools.md#page-modes).

### Experience Manager Dynamic Media {#aem-dynamic-media}

Experience Manager Dynamic Media förenar Dynamic Media Classic-funktionerna direkt i Experience Manager.

När du arbetar med resurser i den här lösningen följer du det här arbetsflödet:

1. Ladda upp enstaka bild- och videomaterial direkt till Experience Manager.
1. Koda videofilmer direkt i Experience Manager.
1. Bygg bildbaserade uppsättningar direkt i Experience Manager.
1. Lägg till interaktivitet i bilder eller videoklipp om tillämpligt.

Komponenterna som du använder för Dynamic Media finns i **[!UICONTROL Dynamic Media]**-komponentområdet i [designläge](/help/sites-authoring/author-environment-tools.md#page-modes). De innehåller följande:

* **[!UICONTROL Dynamic Media]** -  **[!UICONTROL Dynamic Media]** Komponenten är smart - beroende på om du lägger till en bild eller en video har du olika alternativ. Komponenten har stöd för bildförinställningar, bildbaserade visningsprogram som bilduppsättningar, snurra, blandade medieuppsättningar och video. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

* **[!UICONTROL Interactive Media]** -  **[!UICONTROL Interactive Media]** Komponenten är för material som karusellbanderoller, interaktiva bilder och interaktiv video. Sådana resurser har interaktivitet i dem, till exempel hotspot-områden eller bildscheman. Den här komponenten är smart. Det betyder att du kan välja mellan olika alternativ, beroende på om du lägger till en bild eller en video. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

### Scenario med dubbla användningsområden {#dual-use-scenario}

Du kan använda både Dynamic Media och Dynamic Media Classic-integreringsfunktionerna i Experience Manager samtidigt. I följande exempeltabell beskrivs när du aktiverar och inaktiverar vissa områden.

Så här använder du Dynamic Media och Dynamic Media Classic samtidigt:

1. Konfigurera [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) i Cloud Services.
1. Följ de specifika instruktionerna för ditt användningsfall:

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic-integrering</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>Om du är ...</strong></td>
    <td><strong>Arbetsflöde för användningsfall</strong></td>
    <td><strong>Bild/video</strong></td>
    <td><strong>Dynamic Media Component</strong></td>
    <td><strong>S7 Content Browser and Components</strong></td>
    <td><strong>Automatisk överföring från resurser till S7</strong></td>
    </tr>
    <tr>
    <td>Nyheter i Sites och Dynamic Media</td>
    <td>Överför resurser till Experience Manager och använd Experience Manager Dynamic Media-komponenten för att skapa resurser på Sites-sidor</td>
    <td><p>På</p> <p>(Se steg 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">På</a></td>
    <td>Av</td>
    <td>Av</td>
    </tr>
    <tr>
    <td>Inom detaljhandeln och nytt för Sites och Dynamic Media</td>
    <td>Överför icke-produktresurser till Experience Manager för hantering och leverans. Ladda upp produktmaterial till Dynamic Media Classic och använd Dynamic Media Classic Content Browser i Experience Manager och komponent för att skapa produktinformationssidor på webbplatser.</td>
    <td><p>På</p> <p>(Se steg 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">På</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">På</a></td>
    <td>Av</td>
    </tr>
    <tr>
    <td>Nyheter i Assets och Dynamic Media</td>
    <td>Överför resurser till Experience Manager Assets och använd publicerad URL/inbäddningskod från Dynamic Media</td>
    <td><p>På</p> <p>(Se steg 3)</p> </td>
    <td>Av</td>
    <td>Av</td>
    <td>Av</td>
    </tr>
    <tr>
    <td>Nyheter i Dynamic Media och mallar</td>
    <td>Använd Dynamic Media för bild och video. Skapa bildmallar i Dynamic Media Classic och använd Dynamic Media Classic Content Finder för att inkludera mallar på webbplatssidor.</td>
    <td><p>På</p> <p>(Se steg 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">På</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">På</a></td>
    <td>Av</td>
    </tr>
    <tr>
    <td>En befintlig Dynamic Media Classic-kund och är ny på Sites</td>
    <td>Överför resurser till Dynamic Media Classic och använd Experience Manager Dynamic Media Classic-innehållsläsaren för att söka efter och redigera resurser på webbplatssidor</td>
    <td>Av</td>
    <td>Av</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">På</a></td>
    <td>Av</td>
    </tr>
    <tr>
    <td>En befintlig Dynamic Media Classic-kund och är ny i Sites and Assets</td>
    <td>Ladda upp material till DAM och publicera automatiskt till Dynamic Media Classic för leverans. Använd Experience Manager Dynamic Media Classic-webbläsare för att söka efter och redigera resurser på webbplatssidor.</td>
    <td>Av</td>
    <td>Av</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">På</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">På</a></p> <p>(Se steg 4)</p> </td>
    </tr>
    <tr>
    <td>Befintlig Dynamic Media Classic-kund och nybörjare på Assets</td>
    <td><p>Ladda upp material till Experience Manager och använd Dynamic Media för att generera renderingar för nedladdning/delning. Publicera automatiskt Experience Manager-material till Dynamic Media Classic för leverans.</p> <p><strong>Viktigt:</strong> Inkräktar på dubblettbearbetningen och renderingar som genererats i Experience Manager inte synkroniseras med Dynamic Media Classic</p> </td>
    <td><p>På</p> <p>(Se steg 3)</p> </td>
    <td>Av</td>
    <td>Av</td>
    <td><p><a href="#configuringautouploadingfromaemassets">På</a></p> <p>(Se steg 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Valfritt) (se falltabell) - Konfigurera molnkonfigurationen [Dynamic Media](/help/assets/config-dynamic.md) och [aktivera Dynamic Media-servern](/help/assets/config-dynamic.md).
1. (Valfritt) (se falltabell) - Om du väljer att aktivera automatisk överföring från resurser till Dynamic Media Classic måste du lägga till följande:

   1. Konfigurera automatisk överföring till Dynamic Media Classic.
   1. Lägg till steget **Dynamic Media Classic upload** efter alla steg i Dynamic Media arbetsflöde *i slutet av* **arbetsflödet för Dam Update Asset** ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Valfritt) Begränsa uppladdning av Dynamic Media Classic-resurser med MIME-typ i [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). MIME-typer för resurser som inte finns i den här listan överförs inte till Dynamic Media Classic-servern.
   1. (Valfritt) Konfigurera video i Dynamic Media Classic-konfigurationen. Du kan aktivera videokodning för båda eller för både Dynamic Media och Dynamic Media Classic samtidigt. Dynamiska återgivningar används för att förhandsgranska och spela upp lokalt i Experience Manager, medan Dynamic Media Classic-videoåtergivningar genereras och lagras på Dynamic Media Classic-servrar. När du konfigurerar videokodningstjänster för både Dynamic Media och Dynamic Media Classic ska du använda en [videobearbetningsprofil](/help/assets/video-profiles.md) i resursmappen för Dynamic Media Classic.
   1. (Valfritt) [Konfigurera säker förhandsvisning i Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Begränsningar {#limitations}

När både Dynamic Media Classic och Dynamic Media är aktiverade finns följande begränsningar:

* Manuell överföring till Dynamic Media Classic genom att markera en resurs och dra den till en Dynamic Media Classic-komponent på en Experience Manager-sida fungerar inte.
* Även om synkroniserade resurser från Experience Manager till Dynamic Media Classic uppdateras automatiskt till Dynamic Media Classic när resursen redigeras i Assets, utlöser en återställningsåtgärd ingen ny överföring. Därför får Dynamic Media Classic inte den senaste versionen omedelbart efter en återställning. Du kan lösa problemet genom att redigera igen när återställningen är klar.
* Är det nödvändigt att du använder Dynamic Media för ett användningsfall och Dynamic Media Classic-integrering för ett annat så att Dynamic Media-material inte interagerar med Dynamic Media Classic-systemet? I så fall ska du inte använda Dynamic Media Classic-konfigurationen i Dynamic Media-mappen. Använd inte heller Dynamic Media-konfigurationen (bearbetningsprofilen) för en Dynamic Media Classic-mapp.

## Bästa tillvägagångssätt för att integrera Dynamic Media Classic med Experience Manager {#best-practices-for-integrating-scene-with-aem}

När du integrerar Dynamic Media Classic med Experience Manager finns det några viktiga tips som måste följas inom följande områden:

* Testa integreringen
* Överför resurser direkt från Dynamic Media Classic rekommenderas för vissa scenarier

Se [kända begränsningar](#known-limitations-and-design-implications).

### Testkör integreringen {#test-driving-your-integration}

Adobe rekommenderar att du testkör integreringen genom att låta rotmappen peka mot en undermapp i stället för ett helt företag.

>[!CAUTION]
>
>Det kan ta lång tid att importera resurser från ett befintligt Dynamic Media Classic-företagskonto och visa dem i Experience Manager. Se till att du anger en mapp i Dynamic Media Classic som inte har för många resurser (rotmappen har till exempel ofta för många resurser och kan krascha systemet).

### Överför resurser från Experience Manager Assets jämfört med Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Du kan överföra resurser antingen med hjälp av funktionen Resurser (digital resurshantering) eller genom att gå till Dynamic Media Classic direkt i Experience Manager via innehållsläsaren i Dynamic Media Classic. Vilken du väljer beror på följande faktorer:

* Dynamic Media Classic-resurstyper som Experience Manager Assets ännu inte stöder måste läggas till på en Experience Manager-webbplats direkt från Dynamic Media Classic via Dynamic Media Classic-innehållsläsaren. Exempel: bildmallar.
* För resurstyper som stöds av både Experience Manager Assets och Dynamic Media Classic beror överföringssättet på följande:

   * Var tillgångarna finns idag OCH
   * Hur viktigt det är att hantera dem i en gemensam databas

Anta att resurserna redan finns i Dynamic Media Classic och att det inte är viktigt att hantera dem i en gemensam databas. Om så är fallet är det inte längre nödvändigt att exportera resurserna till Experience Manager Assets så att du bara kan synkronisera dem till Dynamic Media Classic för leverans. Adobe rekommenderar att du sparar resurser i en enda databas och synkroniserar till Dynamic Media Classic för leverans.

## Konfigurera integrering med Dynamic Media Classic {#configuring-scene-integration}

Du kan konfigurera Experience Manager att överföra resurser till Dynamic Media Classic. Resurser från en CQ-målmapp kan överföras (automatiskt eller manuellt) från Experience Manager till ett Dynamic Media Classic-företagskonto.

>[!NOTE]
>
>Adobe rekommenderar att du endast använder den angivna målmappen för import av Dynamic Media Classic-resurser. Digitala resurser som ligger utanför målmappen kan bara användas i Dynamic Media Classic-komponenter på sidor där Dynamic Media Classic-konfigurationen har aktiverats. Dessutom placeras de i en on-demand-mapp i Dynamic Media Classic. Mappen on-demand är inte synkroniserad med Experience Manager (resurser kan identifieras i Dynamic Media Classic-webbläsaren).

**Så här konfigurerar du Dynamic Media Classic för integrering med Experience Manager:**

1. [Definiera en molnkonfiguration](#creating-a-cloud-configuration-for-scene)  - Definierar mappningen mellan en Dynamic Media Classic-mapp och en Assets-mapp. Slutför det här steget även om du bara vill synkronisera Experience Manager-resurser till Dynamic Media Classic) åt gången.
1. [Aktivera  **Adobe CQ s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener)  - klar i  [!UICONTROL OSGi] konsolen.
1. Om du vill att Experience Manager Assets automatiskt ska överföras till Dynamic Media Classic måste du aktivera det alternativet och lägga till Dynamic Media Classic i arbetsflödet [!UICONTROL DAM Update Asset]. Du kan också överföra resurser manuellt.
1. Lägga till Dynamic Media Classic-komponenter i sidosparken. Med den här funktionen kan användare använda Dynamic Media Classic-komponenter på sina Experience Manager-sidor.
1. [Mappa konfigurationen till sidan i Experience Manager](#enabling-scene-for-wcm)  - Det här steget krävs för att visa alla förinställningar för video som du har skapat i Dynamic Media Classic. Det är också nödvändigt om du måste publicera en resurs utanför CQ-målmappen till Dynamic Media Classic.

I det här avsnittet beskrivs hur du utför alla dessa steg och en lista med viktiga begränsningar.

### Hur synkronisering mellan Dynamic Media Classic och Experience Manager Assets fungerar {#how-synchronization-between-scene-and-aem-assets-works}

När du konfigurerar Experience Manager Assets och Dynamic Media Classic-synkronisering är det viktigt att du förstår följande:

#### Överför till Dynamic Media Classic från Experience Manager Assets {#uploading-to-scene-from-aem-assets}

* Det finns en angiven synkroniseringsmapp i Experience Manager för Dynamic Media Classic-överföringar.
* Överföringar till Dynamic Media Classic kan automatiseras om de digitala resurserna placeras i den angivna synkroniseringsmappen.
* Mappen och undermappsstrukturen i Experience Manager replikeras i Dynamic Media Classic.

>[!NOTE]
>
>Experience Manager bäddar in alla metadata som XMP innan de överförs till Dynamic Media Classic, så alla egenskaper på metadatanoden är tillgängliga i Dynamic Media Classic som XMP.

#### Kända begränsningar och designkonsekvenser {#known-limitations-and-design-implications}

I och med synkroniseringen mellan Experience Manager Assets och Dynamic Media Classic finns det för närvarande följande begränsningar/designkonsekvenser:

<table>
 <tbody>
  <tr>
   <td><strong>Begränsningar/konstruktionsdetaljer</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>En avsedd synkroniseringsmapp (målmapp)</td>
   <td>Du kan bara ha en mapp per företag i Experience Manager för Dynamic Media Classic-överföringar. Du kan skapa flera konfigurationer om du måste ha tillgång till mer än ett företagskonto i Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Mappstruktur</td>
   <td>Om du tar bort en synkroniserad mapp med resurser tas alla Dynamic Media Classic-fjärrresurser bort, men mappen finns kvar.</td>
  </tr>
  <tr>
   <td>On demand-mapp</td>
   <td>Resurser som finns utanför målmappen och som överförs manuellt till Dynamic Media Classic i WCM placeras automatiskt i en separat on-demand-mapp i Dynamic Media Classic. Du konfigurerar den här mappen i molnkonfigurationen i Experience Manager.</td>
  </tr>
  <tr>
   <td>Blandat media</td>
   <td>Blandade medieuppsättningar visas i Experience Manager, men stöds inte i Experience Manager.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Genererade PDF-filer från e-kataloger i Dynamic Media Classic importeras till CQ-målmappen.</td>
  </tr>
  <tr>
   <td>Gränssnittsuppdatering</td>
   <td>När du synkroniserar mellan Experience Manager och Dynamic Media Classic måste du uppdatera användargränssnittet så att ändringarna visas. </td>
  </tr>
  <tr>
   <td>Videominiatyrer</td>
   <td>Om du överför en video till Experience Manager Assets för kodning via Dynamic Media Classic kan det ta en stund innan videominiatyrbilderna och de kodade videoklippen är tillgängliga i Experience Manager Assets, beroende på hur lång videobearbetningstiden är.</td>
  </tr>
  <tr>
   <td>Målundermappar</td>
   <td><p>Om du använder undermappar i målmappen måste du antingen använda unika namn för varje resurs (oavsett plats). Se även till att du konfigurerar Dynamic Media Classic (under Konfigurera) så att resurser inte skrivs över, oavsett var de finns.</p> <p>Annars överförs resurser med samma namn som överförs till en Dynamic Media Classic-målundermapp, men resursen med samma namn i målmappen tas bort. </p> </td>
  </tr>
 </tbody>
</table>

### Konfigurera Dynamic Media Classic-servrar {#configuring-scene-servers}

Om du kör Experience Manager bakom en proxy eller har speciella brandväggsinställningar måste du uttryckligen aktivera värdarna för de olika regionerna. Servrar hanteras i innehåll i `/etc/cloudservices/scene7/endpoints` och kan anpassas efter behov. Markera en URL-adress och redigera sedan om det behövs för att ändra URL-adressen. I tidigare versioner av Experience Manager var dessa värden hårdkodade.

Om du navigerar till `/etc/cloudservices/scene7/endpoints.html` ser du de servrar som visas (och kan redigera dem genom att trycka på URL-adressen):

![chlimage_1-296](assets/chlimage_1-296.png)

### Skapa en molnkonfiguration för Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

En molnkonfiguration definierar mappningen mellan en Dynamic Media Classic-mapp och en Experience Manager Assets-mapp. Den måste vara konfigurerad för att synkronisera Experience Manager-resurser med Dynamic Media Classic. Mer information finns i Så här fungerar synkroniseringen.

>[!CAUTION]
>
>Det kan ta lång tid att importera resurser från ett befintligt Dynamic Media Classic-företagskonto och visa dem i Experience Manager. Se till att du anger en mapp i Dynamic Media Classic som inte har för många resurser. Rotmappen har till exempel ofta för många resurser.
>
>Om du vill testa och köra integreringen ska rotmappen bara peka på en undermapp, i stället för på hela företaget.

>[!NOTE]
>
>Du kan ha flera konfigurationer: en molnkonfiguration representerar en användare på ett Dynamic Media Classic-företag. Om du vill få åtkomst till andra Dynamic Media Classic-företag eller -användare måste du skapa flera konfigurationer.

**Så här skapar du en molnkonfiguration för Dynamic Media Classic:**

1. Markera ikonen Experience Manager och gå till **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]** så att du kan komma åt Adobe Dynamic Media Classic.

1. Välj **[!UICONTROL Configure now]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. Ange lämplig information i fältet **[!UICONTROL Title]** och eventuellt i fältet **[!UICONTROL Name]**. Välj **[!UICONTROL Create]**.

   >[!NOTE]
   >
   >När du skapar fler konfigurationer visas fältet **[!UICONTROL parent configuration]**.
   >
   >Ändra inte den överordnade konfigurationen genom att **inte**. Om du ändrar den överordnade konfigurationen kan integreringen brytas.

1. Ange e-postadress, lösenord och region för ditt Dynamic Media Classic-konto och välj **[!UICONTROL Connect to Dynamic Media Classic]**. Du är ansluten till Dynamic Media Classic-servern och dialogrutan utökas med fler alternativ.

1. Ange **[!UICONTROL Company]**-namnet och **[!UICONTROL Root Path]**. Den här informationen är namnet på den publicerade servern tillsammans med sökvägen som du vill ange. Om du inte känner till det publicerade servernamnet går du till **[!UICONTROL Setup > Application Setup]** i Dynamic Media Classic).

   >[!NOTE]
   >
   >Dynamic Media Classic-rotsökvägen är den Dynamic Media Classic-mapp som Experience Manager ansluter till. Den kan begränsas till en viss mapp.

   >[!CAUTION]
   >
   >Beroende på storleken på Dynamic Media Classic-mappen kan det ta lång tid att importera en rotmapp. Dessutom kan Dynamic Media Classic-data överskrida lagringsutrymmet i Experience Manager. Kontrollera att du importerar rätt mapp. Om du importerar för mycket data kan det stoppa systemet.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Välj **[!UICONTROL OK]**. Experience Manager sparar konfigurationen.

>[!NOTE]
>
>Om du återansluter:
>
>* När du återansluter till Dynamic Media Classic vid publicering fungerar inte lösenordet vid publicering eller återanslutning (inte ett problem i Author-instansen).
>* Om du ändrar värden som region, företagsnamn måste du ansluta till Dynamic Media Classic igen. Om konfigurationsalternativen har ändrats men inte sparats visar Experience Manager felaktigt att konfigurationen är giltig. Var noga med att återansluta.

>



### Aktivera Adobe CQ Dynamic Media Classic Dam Listener {#enabling-the-adobe-cq-scene-dam-listener}

Aktivera Adobe CQ Dynamic Media Classic Dam Listener, som är inaktiverat som standard.

**Så här aktiverar du Adobe CQ Dynamic Media Classic Dam Listener:**

1. Välj ikonen [!UICONTROL Tools] och navigera sedan till **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Gå till **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** i webbkonsolen och markera kryssrutan **[!UICONTROL Enabled]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Välj **[!UICONTROL Save]**.

### Lägg till konfigurerbar tidsgräns i arbetsflödet för Dynamic Media Classic Upload {#adding-configurable-timeout-to-scene-upload-workflow}

När en Experience Manager-instans har konfigurerats för att hantera videokodning via Dynamic Media Classic finns som standard en 35-minuters timeout för alla överföringsjobb. Du kan konfigurera den här inställningen om du vill att videokodningsjobb som kan vara längre ska kunna användas.

1. Navigera till **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Ändra talet som du vill i fältet **[!UICONTROL Active job timeout]**. Ett icke-negativt tal accepteras med måttenheten i sekunder. Som standard är det här talet 2100.

   >[!NOTE]
   >
   >Bästa praxis: De flesta resurser är kapslade inom några minuter (till exempel bilder). Men i vissa fall - till exempel större videofilmer - ökar du timeoutvärdet till 7 200 sekunder (två timmar) för att få plats med lång bearbetningstid. Annars markeras det här Dynamic Media Classic-överföringsjobbet som **[!UICONTROL UploadFailed]** i JCR-metadata (Java™ Content Repository).

1. Välj **[!UICONTROL Save]**.

### Automatisk uppladdning från Experience Manager Assets {#autouploading-from-aem-assets}

Från och med Experience Manager 6.3.2 är Experience Manager Assets konfigurerat så att alla överförda digitala resurser uppdateras till Dynamic Media Classic, om resurserna finns i en CQ-målmapp.

När en resurs läggs till i Experience Manager Assets överförs den automatiskt och publiceras i Dynamic Media Classic.

>[!NOTE]
>
>Den största filstorleken för automatisk överföring från Experience Manager Assets till Dynamic Media Classic är 500 MB.

**Så här skickar du filer från Experience Manager Assets:**

1. Markera ikonen Experience Manager och gå till **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Under rubriken Dynamic Media, under Tillgängliga konfigurationer, väljer du **[!UICONTROL dms7 (Dynamic Media]**).
1. Markera fliken **[!UICONTROL Advanced]**, markera kryssrutan **[!UICONTROL Enable Automatic Upload]** och välj sedan **[!UICONTROL OK]**. Du måste nu konfigurera arbetsflödet för DAM-resurser så att det omfattar överföring till Dynamic Media Classic.

   >[!NOTE]
   >
   >Se [Konfigurera tillståndet (publicerad/opublicerad) för resurser som skickats till Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) för information om hur du överför resurser till Dynamic Media Classic i ett opublicerat läge.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Gå tillbaka till välkomstsidan för Experience Manager och välj **[!UICONTROL Workflows]**. Dubbelklicka på arbetsflödet **DAM Update Asset** så att det öppnas.
1. I sidosparken navigerar du till **[!UICONTROL Workflow]**-komponenterna och väljer **[!UICONTROL Dynamic Media Classic]**. Dra **[!UICONTROL Dynamic Media Classic]** till arbetsflödet och välj **[!UICONTROL Save]**. Resurser som har lagts till i Experience Manager Resurser i målmappen överförs automatiskt till Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* När du lägger till resurser efter automatisering och de inte placeras i CQ-målmappen, överförs de inte till Dynamic Media Classic.
   >* Experience Manager bäddar in alla metadata som XMP innan de överförs till Dynamic Media Classic, så alla egenskaper på metadatanoden är tillgängliga i Dynamic Media Classic som XMP.


### Konfigurera status (publicerad/opublicerad) för resurser som skickats till Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Om du flyttar resurser från Experience Manager Assets till Dynamic Media Classic kan du antingen publicera dem automatiskt (standardbeteende) eller överföra dem till Dynamic Media Classic i ett opublicerat läge.

Du kanske inte vill publicera resurser direkt på Dynamic Media Classic om du vill testa dem i en staging-miljö innan du publicerar dem. Du kan använda Experience Manager med Dynamic Media Classic&#39;s Secure Test-miljö för att överföra resurser direkt från Assets till Dynamic Media Classic i ett opublicerat läge.

Dynamic Media Classic-resurser är fortfarande tillgängliga via säker förhandsvisning. Det är bara när resurser publiceras i Experience Manager som Dynamic Media Classic också publiceras live i produktionen.

Om du vill publicera resurser direkt när du överför dem till Dynamic Media Classic behöver du inte konfigurera några alternativ. Den här funktionen är standardbeteendet.

Om du inte vill att resurser som skickas till Dynamic Media Classic ska publiceras automatiskt beskrivs hur du konfigurerar Experience Manager och Dynamic Media Classic att utföra den här funktionen i det här avsnittet.

#### Krav för att överföra resurser till Dynamic Media Classic som inte publicerats {#prerequisites-to-push-assets-to-scene-unpublished}

Innan du kan överföra resurser till Dynamic Media Classic utan att publicera dem måste du konfigurera följande:

1. [Använd Admin Console för att skapa ett supportärende](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). I ditt supportärende begär du att du aktiverar säker förhandsvisning för ditt Dynamic Media Classic-konto.
1. [Konfigurera säker förhandsgranskning för ditt Dynamic Media Classic-konto](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en).

Detta är samma steg som du följer för att skapa säkra testinställningar i Dynamic Media Classic.

>[!NOTE]
>
>Om installationsmiljön är ett 64-bitars UNIX®-operativsystem kan du läsa [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) om andra konfigurationsalternativ som du måste ange.

#### Kända begränsningar för att överföra resurser i opublicerat läge  {#known-limitations-for-pushing-assets-in-unpublished-state}

Om du använder den här funktionen bör du tänka på följande begränsningar:

* Versionskontroll stöds inte.
* Om en mediefil redan har publicerats i Experience Manager och en senare version skapas, publiceras den nya versionen omedelbart direkt i produktion. Publicera vid aktivering fungerar endast med den initiala publiceringen av en mediefil.

>[!NOTE]
>
>Om du vill publicera resurser direkt är det bäst att behålla **[!UICONTROL Enable Secure Preview]** inställt på **[!UICONTROL Immediately]** och använda funktionen **[!UICONTROL Enable Automatic Upload]**.

### Ange status för resurser som skickats till Dynamic Media Classic som opublicerade {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Om en användare publicerar resursen i Experience Manager utlöses S7-resursen automatiskt till produktions-/liveresursen (resursen är inte längre i säker förhandsvisning/avpublicerad).

**Så här anger du status för resurser som skickats till Dynamic Media Classic som opublicerade:**

1. Markera ikonen Experience Manager och gå till **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Välj **[!UICONTROL Dynamic Media Classic]**.
1. Välj din konfiguration i Dynamic Media Classic.
1. Välj fliken **[!UICONTROL Advanced]**.
1. I listrutan **[!UICONTROL Enable Secure View]** väljer du **[!UICONTROL Upon AEM Publish Activation]** om du vill skicka resurser till Dynamic Media Classic utan publicering. (Som standard är det här värdet **[!UICONTROL Immediately]**, där Dynamic Media Classic-resurser publiceras direkt.)

   Mer information om hur du testar resurser innan du publicerar dem finns i [Dynamic Media Classic-dokumentationen](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html).

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Välj **[!UICONTROL OK]**.

Om du aktiverar Säker förhandsvisning innebär det att dina resurser skickas till den säkra förhandsgranskningsservern som inte har publicerats.

Om du vill se om **[!UICONTROL Secure Preview]** är aktiverat går du till en Dynamic Media Classic-komponent på en sida i Experience Manager. Välj **[!UICONTROL Edit]**. Resursen har den säkra förhandsvisningsservern som anges i URL:en. När du har publicerat i Experience Manager uppdateras serverdomänen i filreferensen från förhandsgransknings-URL:en till produktions-URL:en.

### Aktivera Dynamic Media Classic för WCM {#enabling-scene-for-wcm}

Du måste aktivera Dynamic Media Classic för WCM av två anledningar:

* Det aktiverar listrutan med universella videoprofiler för framtagning av sidor. Utan den här listan är listrutan **[!UICONTROL Universal Video Preset]** tom och kan inte anges.
* Om en digital resurs inte finns i målmappen kan du överföra resursen till Dynamic Media Classic om du aktiverar Dynamic Media Classic för den sidan i sidegenskaperna. Dra och släpp sedan resursen på en Dynamic Media Classic-komponent. Normala arvsregler gäller (vilket innebär att underordnade sidor ärver konfigurationen från den överordnade sidan).

När du aktiverar Dynamic Media Classic för WCM gäller arvsregler, precis som för andra konfigurationer. Du kan aktivera Dynamic Media Classic för WCM i det pekoptimerade eller klassiska användargränssnittet.

#### Aktivera Dynamic Media Classic för WCM i det pekoptimerade användargränssnittet {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. Markera ikonen Experience Manager och navigera till **[!UICONTROL Sites]** och sedan till rotsidan på din webbplats (inte språkspecifik).

1. Välj ikonen [!UICONTROL settings] i verktygsfältet och välj **[!UICONTROL Open Properties]**.

1. Välj **[!UICONTROL Cloud Services]**, välj **[!UICONTROL Add Configuration]** och välj **[!UICONTROL Dynamic Media Classic]**.
1. Välj önskad konfiguration i listrutan **[!UICONTROL Adobe Dynamic Media Classic]** och välj **[!UICONTROL OK]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   Videoförinställningar från den konfigurationen av Dynamic Media Classic är tillgängliga för användning i Experience Manager med Dynamic Media Classic-videokomponenten på den sidan och underordnade sidor.

#### Aktivera Dynamic Media Classic för WCM i det klassiska användargränssnittet {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. I Experience Manager väljer du **[!UICONTROL Websites]** och navigerar till rotsidan på din webbplats (inte språkspecifik).

1. I sidosparken väljer du ikonen **[!UICONTROL Page]** och väljer **[!UICONTROL Page Properties]**.

1. Välj **[!UICONTROL Cloud Services]** > **[!UICONTROL Add services]** > **[!UICONTROL Dynamic Media Classic]**.
1. Välj önskad konfiguration i listrutan **[!UICONTROL Adobe Dynamic Media Classic]** och välj **[!UICONTROL OK]**.

   Videoförinställningar från den konfigurationen av Dynamic Media Classic är tillgängliga för användning i Experience Manager med Dynamic Media Classic-videokomponenten på den sidan och underordnade sidor.

### Konfigurera en standardkonfiguration {#configuring-a-default-configuration}

Om du har flera Dynamic Media Classic-konfigurationer kan du ange en av dem som standard för Dynamic Media Classic-innehållsläsaren.

Endast en Dynamic Media Classic-konfiguration kan markeras som standard vid en viss tidpunkt. Standardkonfigurationen är de företagsresurser som visas som standard i Dynamic Media Classic Content Browser.

**Så här konfigurerar du en standardkonfiguration:**

1. Markera ikonen Experience Manager och gå till **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Välj **[!UICONTROL Dynamic Media Classic]**.
1. Välj din konfiguration i Dynamic Media Classic.
1. Om du vill öppna konfigurationen väljer du **[!UICONTROL Edit]**.

1. Markera kryssrutan **[!UICONTROL Default Configuration]** på fliken **[!UICONTROL General]** för att göra den till standardföretag och rotsökväg som visas i Dynamic Media Classic-innehållsläsaren.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Om det bara finns en konfiguration har markeringen **[!UICONTROL Default Configuration]** ingen effekt.

### Konfigurera Ad-hoc-mappen {#configuring-the-ad-hoc-folder}

Du kan konfigurera den on demand-mapp som resurser överförs till i Dynamic Media Classic när resursen inte finns i CQ-målmappen. Se Publicera resurser utanför CQ-målmappen.

**Så här konfigurerar du Ad-hoc-mappen:**

1. Markera ikonen Experience Manager och gå till **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Välj **[!UICONTROL Dynamic Media Classic]**.
1. Välj din konfiguration i Dynamic Media Classic.
1. Om du vill öppna konfigurationen väljer du **[!UICONTROL Edit]**.

1. Välj fliken **[!UICONTROL Advanced]**. I fältet **[!UICONTROL Ad-hoc Folder]** kan du ändra mappen **Ad-hoc**. Som standard är det **namnet_på_företaget/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Konfigurera universella videoförinställningar {#configuring-universal-presets}

Information om hur du konfigurerar universella videoförinställningar för videokomponenten finns i [Video](/help/assets/s7-video.md).

## Aktivera stöd för MIME-typbaserade resurser/Dynamic Media Classic-överföringsjobbparametrar {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Du kan aktivera konfigurerbara parametrar för Dynamic Media Classic-överföringsjobb som utlöses av synkroniseringen av Digital Asset Manager/Dynamic Media Classic-resurser.

Du konfigurerar det godkända filformatet efter MIME-typ i OSGi-området (Open Service Gateway-initiativ) på Experience Manager Web Console Configuration-panelen. Sedan kan du anpassa de individuella parametrarna för överföringsjobb som används för varje MIME-typ i JCR (Java™ Content Repository).

**Så här aktiverar du MIME-typbaserade resurser:**

1. Markera ikonen Experience Manager och gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. På Adobe Experience Manager Web Console Configuration-panelen väljer du **[!UICONTROL OSGi]** på menyn **[!UICONTROL Configuration]**.
1. Under kolumnen Namn söker du efter och väljer **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** för att redigera konfigurationen.
1. I området Mime Type Mapping väljer du ett plustecken (+) för att lägga till en MIME-typ.

   Se [MIME-typer som stöds](/help/assets/assets-formats.md#supported-mime-types).

1. Skriv det nya MIME-typnamnet i textfältet.

   Du kan till exempel skriva `<file_extension>=<mime_type>` som i `EPS=application/postscript` ELLER `PSD=image/vnd.adobe.photoshop`.

1. Välj **[!UICONTROL Save]** längst ned till höger i konfigurationsfönstret.
1. Gå tillbaka till Experience Manager och välj **[!UICONTROL CRXDE Lite]** i den vänstra listen.
1. På CRXDE Lite-sidan navigerar du till `/etc/cloudservices/scene7/<environment>` (ersätt `<environment>` som det faktiska namnet) i den vänstra listen.
1. Expandera `<environment>` (ersätt `<environment>` för det faktiska namnet) för att visa noden `mimeTypes`.
1. Välj den mimeType som du nyss lade till.

   Till exempel `mimeTypes > application_postscript` ELLER `mimeTypes > image_vnd.adobe.photoshop`.

1. Till höger på CRXDE Lite-sidan väljer du fliken **[!UICONTROL Properties]**.
1. Ange en Dynamic Media Classic-parameter för överföringsjobb i värdefältet **[!UICONTROL jobParam]**.

   Till exempel, `psprocess="rasterize"&psresolution=120` .

   Se [Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) för fler överföringsjobbparametrar som du kan använda.

   >[!NOTE]
   >
   >Om du överför PSD-filer, och vill bearbeta dem som mallar med lagerextraheringar, anger du följande i fältet **[!UICONTROL jobParam]**-värde:
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >Kontrollera att PSD-filen innehåller &quot;lager&quot;. Om det bara är en bild eller en bild med mask, bearbetas den som en bild eftersom det inte finns några lager att bearbeta.

1. I det övre vänstra hörnet på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.

## Felsöka integreringen mellan Dynamic Media Classic och Experience Manager {#troubleshooting-scene-and-aem-integration}

Om du har problem med att integrera Experience Manager med Dynamic Media Classic kan du hitta lösningar i följande scenarier.

**Om det inte går att publicera digitalt material till Dynamic Media Classic:**

* Kontrollera att resursen du överför finns i mappen **[!UICONTROL CQ target]** (du anger den här mappen i molnkonfigurationen för Dynamic Media Classic).
* Om det inte är det måste du konfigurera molnkonfigurationen i **[!UICONTROL Page Properties]** för den sidan så att överföring till mappen **[!UICONTROL CQ ad hoc]** tillåts.

* Mer information finns i loggarna.

**Om dina videoförinställningar inte visas:**

* Kontrollera att du har konfigurerat molnkonfigurationen för den sidan via **[!UICONTROL Page Properties]**. Videoförinställningar är tillgängliga i videokomponenten i Dynamic Media Classic.

**Om videomaterialet inte spelas upp i Experience Manager:**

* Kontrollera att du har använt rätt videokomponent. Dynamic Media Classic-videokomponenten skiljer sig från den grundläggande videokomponenten. Se [Foundation Video Component jämfört med Dynamic Media Classic Video Component](/help/assets/s7-video.md).

**Om nya eller ändrade resurser i Experience Manager inte automatiskt överförs till Dynamic Media Classic:**

* Kontrollera att resurserna finns i CQ-målmappen. Endast resurser som finns i CQ-målmappen uppdateras automatiskt (förutsatt att du har konfigurerat Experience Manager Assets att överföra resurser automatiskt).
* Kontrollera att du har konfigurerat Cloud Servicens så att Automatisk överföring aktiveras och att du har uppdaterat och sparat arbetsflödet DAM-resurs så att det omfattar Dynamic Media Classic-överföring.
* Gör något av följande när du överför en bild till en undermapp till målmappen för Dynamic Media Classic:

   * Se till att namnen på alla resurser oavsett plats är unika. Annars tas resursen i huvudmålmappen bort och bara resursen i undermappen finns kvar.
   * Ändra hur Dynamic Media Classic skriver över resurser under Konfigurera i Dynamic Media Classic-kontot. Ange inte att Dynamic Media Classic ska ska skriva över resurser oavsett plats om du använder resurser med samma namn i undermappar.

**Om de borttagna resurserna eller mapparna inte är synkroniserade mellan Dynamic Media Classic och Experience Manager:**

* Resurser och mappar som tas bort i Experience Manager Resurser visas fortfarande i den synkroniserade mappen i Dynamic Media Classic. Ta bort dem manuellt.

**Om videouppladdningen misslyckas:**

* Om videouppladdningen misslyckas och du använder Experience Manager för att koda video via Dynamic Media Classic-integreringen, se [Lägg till konfigurerbar tidsgräns i arbetsflödet för Dynamic Media Classic Upload](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>Det kan ta lång tid att importera resurser från ett befintligt Dynamic Media Classic-företagskonto och visa dem i Experience Manager. Se till att du anger en mapp i Dynamic Media Classic som inte har för många resurser. Rotmappen har till exempel ofta för många resurser.
>
>Om du vill testa integreringen ska rotmappen bara peka på en undermapp, i stället för på hela företaget.
