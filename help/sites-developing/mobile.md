---
title: Skapa platser för mobila enheter
description: Att skapa en mobilwebbplats liknar att skapa en standardwebbplats, eftersom det även handlar om att skapa mallar och komponenter
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3722'
ht-degree: 0%

---

# Skapa platser för mobila enheter{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Att skapa en mobilwebbplats liknar att skapa en standardwebbplats, eftersom det även handlar om att skapa mallar och komponenter. Mer information om hur du skapar mallar och komponenter finns på följande sidor: [Mallar](/help/sites-developing/templates.md), [Komponenter](/help/sites-developing/components.md)och [Komma igång med att utveckla AEM Sites](/help/sites-developing/getting-started.md). Den största skillnaden är att aktivera de inbyggda mobilfunktionerna i Adobe Experience Manager (AEM) på webbplatsen. Detta uppnås genom att skapa en mall som är beroende av mobilsidkomponenten.

Överväg att använda [responsiv design](/help/sites-developing/responsive.md), skapar en enda plats för flera skärmstorlekar.

Om du vill komma igång kan du titta på **Webbplats för mobil demo inom detaljhandeln** som finns i AEM.

Så här skapar du en mobilwebbplats:

1. Skapa sidkomponenten:

   * Ange `sling:resourceSuperType` egenskap till `wcm/mobile/components/page`
På så sätt är komponenten beroende av den mobila sidkomponenten.

   * Skapa `body.jsp` med projektspecifik logik.

1. Skapa sidmallen:

   * Ange `sling:resourceType` till den nya sidkomponenten.
   * Ange `allowedPaths` -egenskap.

1. Skapa designsidan för webbplatsen.
1. Skapa webbplatsens rotsida nedanför `/content` nod:

   * Ange `cq:allowedTemplates` -egenskap.
   * Ange `cq:designPath` -egenskap.

1. I sidegenskaperna för platsens rotsida anger du enhetsgrupperna i **Mobil** -fliken.
1. Skapa webbplatssidorna med den nya mallen.

Komponenten för mobilsidan ( `/libs/wcm/mobile/components/page`):

* Lägger till **Mobil** till dialogrutan för sidegenskaper.
* Genom `head.jsp`hämtar den den aktuella mobilenhetsgruppen från begäran och om en enhetsgrupp hittas använder gruppens `drawHead()` -metod för att inkludera enhetsgruppens associerade emulatorinit-komponent (endast i författarläge) och enhetsgruppens återgivnings-CSS.

>[!NOTE]
>
>Rotsidan för den mobila webbplatsen måste vara på nivå 1 i nodhierarkin och bör vara under noden /content.

## Skapa en mobil webbplats med Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Använd Multi Site Manager (MSM) för att skapa en mobil live kopia från en standardwebbplats. Standardwebbplatsen omvandlas automatiskt till en mobilwebbplats: den mobila webbplatsen har alla funktioner som finns på mobilsajterna (till exempel utgåva i en emulator) och kan hanteras synkroniserat med standardwebbplatsen. Se avsnittet [Skapa en Live-kopia för olika kanaler](/help/sites-administering/msm.md) på sidan Multi Site Manager.

## Mobil-API på serversidan {#server-side-mobile-api}

Java™-paketen som innehåller mobilklasserna är:

* [com.day.cq.wcm.mobile.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definierar MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - definierar Device, DeviceGroup och DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.capabilities](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definierar DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - definierar WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - definierar MobileUtil, som tillhandahåller olika verktygsmetoder som kretsar kring WCM Mobile.

### Mobilkomponenter {#mobile-components}

The **Webbplats för mobil demo inom detaljhandeln** använder följande mobila komponenter som finns nedan `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Namn</td>
   <td>Grupp</td>
   <td>Egenskaper</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>dold</td>
   <td>- sidfot</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>Mobil</td>
   <td>- baserat på bildstiftskomponenten<br /> - återger en bild om enheten är kapabel<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>Mobil</td>
   <td>- baserat på listgrundskomponenten<br /> - listitem_teaser.jsp återger en bild om enheten är kapabel<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>dold</td>
   <td>- baserat på logotypens grundkomponent<br /> - återger en bild om enheten är kapabel<br /> </td>
  </tr>
  <tr>
   <td>mobilreferens</td>
   <td>Mobil</td>
   <td><p>- som liknar komponenten för referensstiftelsen</p> <p>- mappar en textimage-komponent till en mobilextimage en och en image-komponent till en mobilbild en</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobil</td>
   <td>- baserat på komponenten textimage Foundation<br /> - återger en bild om enheten är kapabel</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>dold</td>
   <td><p>- baserat på den topnav Foundation-komponenten</p> <p>- återger bara text</p> </td>
  </tr>
 </tbody>
</table>

#### Skapa en mobilkomponent {#creating-a-mobile-component}

Med det AEM mobilramverket kan du utveckla komponenter som är känsliga för den enhet som skickar begäran. I följande kodexempel visas hur du använder det AEM Mobile API:t i en komponent-jsp och särskilt hur du gör det:

* Hämta enheten från begäran:
  `Device device = slingRequest.adaptTo(Device.class);`

* Hämta enhetsgruppen:
  `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Hämta enhetsgruppsfunktionerna:
  `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Hämta enhetsattributen (nyckel/värden för rå kapacitet från WURFL-databasen):
  `Map<String,String> deviceAttributes = device.getAttributes();`

* Hämta enhetens användaragent:
  `String userAgent = device.getUserAgent();`

* Hämta enhetsgruppslistan (enhetsgrupper som tilldelats till webbplatsen av författaren) från den aktuella sidan:
  `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Kontrollera om enhetsgruppen stöder bilder
  `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
... ELLER
  `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>I en jsp, `slingRequest` är tillgängligt via `<sling:defineObjects>` tagg och `currentPage` via `<cq:defineObjects>` -tagg.

### Emulatorer {#emulators}

Emulatorbaserad redigering ger författare möjlighet att skapa innehållssidor som är avsedda för mobila klienter. Framtagning av mobilt innehåll följer samma princip för WYSIWYG-redigering på plats. För att författare ska kunna uppfatta sidutseendet på en mobil enhet redigeras en mobilinnehållssida med en enhetsemulator.

Emulatorer för mobila enheter är baserade på det generiska emulatorramverket. Mer information finns i [Emulatorer](/help/sites-developing/emulators.md).

Enhetsemulatorn visar den mobila enheten på sidan medan den vanliga redigeringen (parsys, components) sker på enhetens skärm. Enhetsemulatorn beror på de enhetsgrupper som är konfigurerade för platsen. Flera emulatorer kan tilldelas till en enhetsgrupp. Alla emulatorer är sedan tillgängliga på innehållssidan. Som standard visas den första emulatorn som tilldelats den första enhetsgruppen som tilldelats platsen. Emulatorerna kan bytas antingen via emulatorkarusellen högst upp på sidan eller via Sidekick-redigeringsknappen.

**Skapa en emulator**

Information om hur du skapar en emulator finns i [Skapa en anpassad emulator för mobiler](/help/sites-developing/emulators.md) på den generiska Emulatorsidan.

**De viktigaste egenskaperna hos emulatorer för mobila enheter**

* En enhetsgrupp består av en av flera emulatorer: konfigurationssidan för enhetsgruppen, till exempel /etc/mobile/groups/touch, innehåller `emulators` egenskapen under `jcr:content` nod.
Obs! Även om det är möjligt att samma emulator hör till flera enhetsgrupper så är det inte särskilt klokt.

* Via enhetsgruppens konfigurationsdialogruta kan `emulators` egenskapen ställs in med sökvägen för emulatorerna. Till exempel: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Emulatorkomponenterna (till exempel `/libs/wcm/mobile/components/emulators/iPhone4`) utöka den grundläggande mobilemulatorkomponenten ( `/libs/wcm/mobile/components/emulators/base`).

* Alla komponenter som utökar basmobilemulatorn är tillgängliga för val när en enhetsgrupp konfigureras. Anpassade emulatorer kan enkelt skapas eller utökas.
* Vid begäran i redigeringsläge används emulatorimplementeringen för att återge sidan.
* När sidmallen är beroende av den mobila sidkomponenten, integreras emulatorfunktionerna automatiskt på sidan (via `head.jsp` för mobilsidkomponenten).

### Enhetsgrupper {#device-groups}

Mobila enhetsgrupper ger segmentering av mobila enheter baserat på enhetens funktioner. En enhetsgrupp innehåller den information som krävs för emulatorbaserad redigering på författarinstansen och för korrekt innehållsåtergivning på publiceringsinstansen: när författarna har lagt till innehåll på mobilsidan och publicerat det kan sidan begäras på publiceringsinstansen. I stället för emulatorns redigeringsvy återges innehållssidan med en av de konfigurerade enhetsgrupperna. Valet av enhetsgruppen görs baserat på [mobilenhetsidentifiering](#devicedetection). Den matchande enhetsgruppen tillhandahåller sedan nödvändig formatinformation.

Enhetsgrupper definieras som innehållssidor nedan `/etc/mobile/devices` och använder **Mobilenhetsgrupp** mall. Enhetens gruppmall fungerar som en konfigurationsmall för enhetsgruppsdefinitioner i form av innehållssidor. Dess huvudsakliga egenskaper är:

* Plats: `/libs/wcm/mobile/templates/devicegroup`
* Tillåten sökväg: `/etc/mobile/groups/*`
* Sidkomponent: `wcm/mobile/components/devicegroup`

#### Tilldela enhetsgrupper till din webbplats {#assigning-device-groups-to-your-site}

När du skapar en mobilwebbplats måste du tilldela enhetsgrupper till webbplatsen. AEM innehåller tre enhetsgrupper beroende på enhetens HTML och JavaScript-återgivningsfunktioner:

* **Funktion** telefoner för enheter som Sony Ericsson W800 med stöd för grundläggande HTML, men utan stöd för bilder och JavaScript.
* **Smart** telefoner, för enheter som BlackBerry® med stöd för grundläggande HTML och bilder, men utan stöd för JavaScript.

* **Touch** telefoner för enheter som iPad med fullt stöd för HTML, bilder, JavaScript och enhetsrotation.

Som emulatorer kan kopplas till en enhetsgrupp (se avsnittet [Skapa en enhetsgrupp](#creating-a-device-group)) kan författare välja mellan de emulatorer som är kopplade till enhetsgruppen när de tilldelar en enhetsgrupp till en webbplats.

Så här tilldelar du en enhetsgrupp till din plats:

1. Gå till **Webbadministratör** konsol.
1. Öppna rotsidan för din mobila webbplats nedan **Webbplatser**.
1. Öppna sidegenskaperna.
1. Välj **Mobil** tab:

   * Definiera enhetsgrupperna.
   * Klicka **OK**.

>[!NOTE]
>
>När enhetsgrupperna har definierats för en plats, ärvs de av alla sidor på platsen.

#### Enhetsgruppsfilter {#device-group-filters}

Enhetsgruppsfilter definierar funktionsbaserade villkor för att avgöra om en enhet tillhör gruppen. När du skapar en enhetsgrupp kan du välja vilka filter som ska användas för att utvärdera enheter.

Vid körning när AEM tar emot en HTTP-begäran från en enhet, jämför varje filter som är kopplat till en grupp enhetsfunktionerna med specifika kriterier. Enheten anses tillhöra gruppen när den har alla funktioner som filtren kräver. Funktioner hämtas från WURFL™-databasen.

Enhetsgrupper kan använda noll eller flera filter för funktionsidentifiering. Ett filter kan också användas med flera enhetsgrupper. AEM innehåller ett standardfilter som avgör om enheten har de funktioner som är valda för en grupp:

* CSS
* JPG och PNG-bilder
* JavaScript
* Enhetsrotation

Om enhetsgruppen inte använder ett filter är de valda funktionerna som är konfigurerade för gruppen de enda funktioner som en enhet behöver.

Mer information finns i [Skapa enhetsgruppsfilter](/help/sites-developing/groupfilters.md).

#### Skapa en enhetsgrupp {#creating-a-device-group}

Skapa en enhetsgrupp när de grupper som AEM installerar inte uppfyller dina krav.

1. Gå till **verktyg** konsol.
1. Skapa en sida nedan **verktyg** > **Mobil** > **Enhetsgrupper**. I **Skapa sida** dialog:

   * Som **Titel**, ange `Special Phones`.

   * Som **Namn**, ange `special`.

   * Välj **Mall för mobilenhetsgrupp**.
   * Klicka **Skapa**.

1. Lägg till en **static.css** filen som innehåller formaten för enhetsgruppen under `/etc/mobile/groups/special` nod.

1. Öppna **Specialtelefoner** sida.
1. Konfigurera enhetsgruppen genom att klicka på **Redigera** knapp bredvid **Inställningar**.
På **Allmänt** tab:

   * **Titel**: namnet på mobilenhetsgruppen.
   * **Beskrivning**: beskrivning av gruppen.
   * **Användaragent**: user-agent-sträng som enheterna matchas mot. Den är valfri och kan vara en regex. Exempel: `BlackBerryZ10`
   * **Funktioner**: definierar om gruppen kan hantera bilder, CSS, JavaScript eller enhetsrotation.
   * **Minsta skärmbredd** och **Höjd**
   * **Inaktivera emulatorn**: att aktivera/inaktivera emulatorn under innehållsredigering.

   På **Emulatorer** tab:

   * **Emulatorer**: välj de emulatorer som tilldelats den här enhetsgruppen.

   På **Filter** tab:

   * Om du vill lägga till ett filter klickar du på Lägg till objekt och väljer ett filter i listrutan.
   * Filter utvärderas i den ordning som de visas. När en enhet inte uppfyller filtervillkoren utvärderas inte efterföljande filter i listan.

1. Klicka på OK.

Dialogrutan för konfiguration av mobilenhetsgrupp ser ut så här:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### Anpassad CSS per enhetsgrupp {#custom-css-per-device-group}

Så som beskrivs ovan är det möjligt att koppla en anpassad CSS till en enhetsgruppssida, ungefär som CSS för en designsida. Den här CSS-koden används för att påverka enhetsgruppsspecifik återgivning av sidinnehållet vid författare och publicering. Den här CSS-koden inkluderas sedan automatiskt:

* På sidan på författarinstansen, för varje emulator som används av den här enhetsgruppen.
* Om användaragenten för begäran matchar en mobil enhet i den här enhetsgruppen på sidan i publiceringsinstansen.

## Enhetsidentifiering på serversidan {#server-side-device-detection}

Använd filter och ett bibliotek med enhetsspecifikationer för att avgöra vilka funktioner den enhet som utför HTTP-begäran har.

### Skapa enhetsgruppsfilter {#develop-device-group-filters}

Skapa ett enhetsgruppsfilter för att definiera en uppsättning krav för enhetsfunktioner. Skapa så många filter du behöver för att rikta in dig på de grupper av enhetsfunktioner som behövs.

Utforma dina filter så att du kan använda kombinationer av dem för att definiera grupper av funktioner. Vanligtvis finns det överlappande funktioner för olika enhetsgrupper. Därför kan du använda vissa filter med flera enhetsgruppsdefinitioner.

När du har skapat ett filter kan du använda det i gruppkonfigurationen.

Mer information finns på [Skapa enhetsgruppsfilter](/help/sites-developing/groupfilters.md).

### Använda WURFL™-databasen {#using-the-wurfl-database}

AEM använder en trunkerad version av [WURFL](https://wurfl.sourceforge.net/)™ -databas för att fråga efter enhetsfunktioner, som skärmupplösning eller JavaScript-stöd, baserat på enhetens User-Agent.

XML-koden för WURFL™-databasen visas som noder nedan `/var/mobile/devicespecs` genom att tolka `wurfl.xml`fil på `/libs/wcm/mobile/devicespecs/wurfl.xml.` Utökningen till noder sker första gången som `cq-mobile-core` paketet har startats.

Enhetsfunktionerna lagras som nodegenskaper och noderna representerar enhetsmodeller. Du kan använda frågor för att hämta funktionerna för en enhet eller en användaragent.

I takt med att WURFL™-databasen utvecklas kan du behöva anpassa eller ersätta den. Du kan uppdatera databasen för mobila enheter på följande sätt:

* Ersätt filen med den senaste versionen om du har en licens som tillåter den här användningen. Se Installera en annan WURFL-databas.
* Använd den version som finns i AEM och konfigurera en regexp som matchar strängarna för användaragenten och pekar på en befintlig WURFL™-enhet. Se [Lägga till en regexp-baserad användaragentmatchning](#adding-a-regexp-based-user-agent-matching).

#### Testa mappningen av en användaragent till WURFL™-funktioner {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

När en enhet kommer åt din mobila webbplats, identifierar AEM enheten, mappar den till en enhetsgrupp enligt dess funktioner och skickar en vy över sidan som motsvarar enhetsgruppen. Den matchande enhetsgruppen tillhandahåller nödvändig formatinformation. Mappningarna kan testas på testsidan för Mobile User-Agent:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installera en annan WURFL™-databas {#installing-a-different-wurfl-database}

Den trunkerade WURFL™-databasen som installeras med AEM är en release som är före den 30 augusti 2011. Om din version av WURFL släpptes efter den 30 augusti 2011 kontrollerar du att din användning är förenlig med din licens.

Installera en WURFL™-databas:

1. Skapa följande mapp i CRXDE Lite: `/apps/wcm/mobile/devicespecs`
1. Kopiera WURFL™-filen till mappen.
1. Byt namn på filen som `wurfl.xml`.

AEM tolkar automatiskt `wurfl.xml` filen och uppdaterar noderna nedan `/var/mobile/devicespecs`.

>[!NOTE]
>
>När den fullständiga WURFL™-databasen är aktiverad kan det ta några minuter att analysera och aktivera. Du kan se loggarna för förloppsinformation.

#### Lägga till en regexp-baserad användaragentmatchning {#adding-a-regexp-based-user-agent-matching}

Lägg till en användaragent som ett reguljärt uttryck nedan /apps/wcm/mobile/devicespecs/wurfl/regexp för att peka på en befintlig WURFL™-enhetstyp.

1. I **CRXDE Lite** skapar du en nod under /apps/wcm/mobile/devicespecs/regexp, till exempel `apple_ipad_ver1`.
1. Lägg till följande egenskaper i noden:

   * **regexp**: reguljärt uttryck som definierar användaragenter, till exempel .&#42;Mozilla.&#42;iPad.&#42;AppleWebKit.&#42;Safari.&#42;
   * **deviceId**: enhets-ID enligt definitionen i wurfl.xml, till exempel `apple_ipad_ver1`

Ovanstående konfiguration gör att enheter som User-Agent matchar det angivna reguljära uttrycket mappas till Apple_ipad_ver1 WURFL™-enhets-ID, om det finns.

## Enhetsidentifiering på klientsidan {#client-side-device-detection}

I det här avsnittet beskrivs hur du använder enhetsidentifiering på klientsidan för AEM för att optimera sidåtergivning eller för att ge klienten alternativa webbplatsversioner.

AEM har stöd för enhetsidentifiering på klientsidan baserat på `BrowserMap`. `BrowserMap` levereras i AEM som ett klientbibliotek under `/etc/clientlibs/browsermap`.

`BrowserMap` innehåller tre strategier som du kan använda för att tillhandahålla en alternativ webbplats till en kund, som används i följande ordning:

1. [Alternativa länkar](#providing-alternate-links)
1. [Enhetsgruppsspecifik URL](#definingdevicegroupspecificurl)
1. [Väljarbaserad URL](#defining-selector-based-urls)

>[!NOTE]
>
>Mer information om integrering av klientbibliotek finns i [Använda HTML-bibliotek på klientsidan](/help/sites-developing/clientlibs.md).

### Ange alternativa länkar {#providing-alternate-links}

The `PageVariantsProvider` OSGi-tjänsten kan generera alternativa länkar för platser som tillhör samma familj. Om du vill konfigurera webbplatser som ska beaktas av tjänsten kan du `cq:siteVariant` noden måste läggas till i `jcr:content` nod från platsens rot.

The `cq:siteVariant` noden måste ha följande egenskaper:

* `cq:childNodesMapTo` - avgör vilket attribut i länkelementet som de underordnade noderna mappas till. Vi rekommenderar att du ordnar innehållet på din webbplats på ett sådant sätt att rotnodens underordnade noder representerar roten för en språkvariant av din globala webbplats (till exempel `/content/mysite/en`, `/content/mysite/de`), i vilket fall värdet på `cq:childNodesMapTo` bör `hreflang`;
* `cq:variantDomain` - anger vad `Externalizer` Domänen används för att generera sidvarianternas absoluta URL:er. Om värdet inte anges genereras sidvarianterna med relativa länkar.
* `cq:variantFamily` - anger till vilken grupp av webbplatser denna webbplats tillhör; flera enhetsspecifika representationer av samma webbplats bör tillhöra samma familj,
* `media` - lagrar värdena för länkelementets mediaattribut; du bör använda namnet på `BrowserMap` registrerad `DeviceGroups`så att `BrowserMap` biblioteket kan automatiskt vidarebefordra klienterna till rätt variant av webbplatsen.

#### PageVariantsProvider och Externalizer {#pagevariantsprovider-and-externalizer}

När värdet för `cq:variantDomain` egenskap för en `cq:siteVariant` noden är inte tom, `PageVariantsProvider` skapar absoluta länkar med det här värdet som en konfigurerad domän för `Externalizer` service. Se till att konfigurera `Externalizer` för att återspegla din konfiguration.

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

### Definiera en enhetsgruppsspecifik URL {#defining-a-device-group-specific-url}

Om du inte vill använda alternativa länkar kan du konfigurera en global URL för varje `DeviceGroup`. Adobe rekommenderar att du skapar ett eget klientbibliotek som bäddar in `browsermap.standard` klientbiblioteket, men enhetsgrupperna definieras om.

BrowserMap är utformat på ett sådant sätt att definitioner för enhetsgrupper kan åsidosättas genom att en enhetsgrupp med samma namn skapas och läggs till i `BrowserMap` -objekt från ditt anpassade klientbibliotek.

>[!NOTE]
>
>Mer information finns i [Anpassad BrowserMap](#creatingacustomisedbrowsermap).

### Definiera väljarbaserade URL:er {#defining-selector-based-urls}

Om ingen av de tidigare funktionerna har använts för att ange en alternativ plats för `BrowserMap`och sedan väljare som ska använda namnen på `DeviceGroups` läggs till i `URL`s, och i så fall bör du tillhandahålla dina egna servrar som hanterar förfrågningarna.

En enhetssurfning till exempel `www.example.com/index.html` identifierad som `smartphone` av BrowserMap vidarebefordras till `www.example.com/index.smartphone.html.`

### Använda BrowserMap på dina sidor {#using-browsermap-on-your-pages}

Om du vill använda standardklientbiblioteket BrowserMap på en sida måste du inkludera `/libs/wcm/core/browsermap/browsermap.jsp` en fil med `cq:include`tagg på sidans `head` -avsnitt.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Förutom att lägga till `BrowserMap` klientbibliotek i din `JSP` -filer måste du också lägga till en `cq:deviceIdentificationMode` Strängegenskap inställd på `client-side` till `jcr:content` noden nedanför webbplatsens rot.

### Åsidosätta BrowserMaps standardbeteende {#overriding-browsermap-s-default-behaviour}

Om du vill anpassa `BrowserMap` - genom att åsidosätta `DeviceGroups` eller lägga till fler avsökningar - skapa ett eget klientbibliotek där du bäddar in `browsermap.standard`klientbibliotek.

Dessutom måste du manuellt anropa `BrowserMap.forwardRequest()` i `JavaScript` kod.

>[!NOTE]
>
>Mer information om integrering av klientbibliotek finns i [Använda HTML-bibliotek på klientsidan](/help/sites-developing/clientlibs.md).

När du har skapat en skräddarsydd `BrowserMap` klientbiblioteket, Adobe föreslår följande tillvägagångssätt:

1. Skapa en `browsermap.jsp` i ditt program

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. Inkludera `broswermap.jsp` i huvudsektionen.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Exkludera BrowserMap från vissa sidor {#excluding-browsermap-from-certain-pages}

Om du vill utesluta BrowserMap-biblioteket från vissa sidor där du inte behöver någon klientidentifiering kan du lägga till ett request-attribut:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

Det här kommer att göra `/libs/wcm/core/browsermap/browsermap.jsp` skript för att lägga till en meta-tagg på sidan som gör `BrowserMap` att inte utföra någon identifiering:

```xml
<meta name="browsermap.enabled" content="false">
```

### Testa en specifik version av en webbplats {#testing-a-specific-version-of-a-web-site}

Skriptet BrowserMap dirigerar normalt alltid om besökarna till den lämpligaste versionen av webbplatsen, och dirigerar vanligtvis om besökarna till skrivbordet eller till den mobila webbplatsen vid behov.

Du kan tvinga enheten i en begäran att testa en specifik version av en webbplats genom att lägga till `device` parametern till din URL. Följande URL återger mobilversionen av Geometrixx Outdoors webbplats.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>The `wcmmode` parametern är inställd på `disabled` för att simulera beteendet för en publiceringsinstans.

Det åsidosättande enhetsvärdet lagras i en cookie så att du kan bläddra på webbplatsen utan att lägga till `device` parameter till varje `URL`.

Du måste alltså ringa samma `URL` med `device` ange till `browser` för att återgå till datorversionen av webbplatsen.

>[!NOTE]
>
>BrowserMap lagrar det åsidosättande enhetsvärdet i en cookie som kallas `BMAP_device`. Om du tar bort den här cookie-filen kan du vara säker på att CQ fungerar med rätt version av webbplatsen enligt den aktuella enheten (till exempel skrivbordet eller mobilen).

## Behandling av mobilförfrågningar {#mobile-request-processing}

AEM bearbetar en begäran från en mobil enhet som tillhör gruppen med pekenheter enligt följande:

1. En iPad skickar en begäran till den AEM publiceringsinstansen, till exempel `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM avgör om webbplatsen för den begärda sidan är en mobilwebbplats (genom att kontrollera om sidan på första nivån är en sida `/content/geometrixx_mobile` utökar mobilsidkomponenten). Om ja:
1. AEM söker upp enhetsfunktionerna baserat på användaragenten i begärandehuvudet.
1. AEM mappar enhetsfunktionerna till enhetsgruppen och anger `touch` som enhetsgruppsväljare.
1. AEM dirigerar om begäran till `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM skickar svaret till iPad:

   * `products.touch.html` renderas på vanligt sätt och kan nås.
   * Återgivningskomponenterna använder väljare för att anpassa presentationen.
   * AEM lägger automatiskt till mobilväljaren till alla interna länkar på sidan.

### Statistik {#statistics}

Du kan hämta statistik om antalet förfrågningar som gjorts till AEM av mobila enheter. Antalet begäranden kan delas upp:

* per enhetsgrupp och enhet
* per år, månad och dag

Så här visar du statistiken:

1. Gå till **verktyg** konsol.
1. Öppna **Enhetsstatistik** sida nedanför **verktyg** > **Mobil**.
1. Klicka på länken om du vill visa statistik för ett visst år, en viss månad eller en viss dag.

The **Statistik** ser ut så här:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>The **Statistik** sidan skapas första gången en mobil enhet kommer åt AEM och identifieras. Den är inte tillgänglig tidigare.

Om du behöver generera en post i statistiken kan du göra så här:

1. Använd en mobil enhet eller en emulator (till exempel https://chrispederick.com/work/user-agent-switcher/ i Firefox).
1. Begär en mobilsida på författarinstansen genom att inaktivera redigeringsläget, till exempel:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

The **Statistik** sidan är nu tillgänglig.

### Cachelagring av stödsidor för länkar av typen &quot;skicka länk till en vän&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Mobilsidor kan nås på Dispatcher, eftersom sidor som återges för en enhetsgrupp särskiljs i sidans URL av enhetsgruppsväljaren, till exempel `/content/mobilepage.touch.html`. En begäran till en mobilsida utan väljare cachelagras aldrig, som i det här fallet utförs enhetsidentifieringen och dirigeras till den matchande enhetsgruppen (eller&quot;nominatch&quot; för den delen). En mobilsida som återges med en enhetsgruppsväljare bearbetas av länkomskrivaren, som skriver om alla länkar på sidan så att de även innehåller enhetsgruppsväljaren, vilket förhindrar att enhetsidentifieringen utförs på nytt för varje klick på en redan kvalificerad sida.

Därför kan du stöta på följande scenario:

Alice omdirigeras till `coolpage.feature.html`, och skickar den URL:en till en kompis Bob som kommer åt den med en annan klient som finns i `touch` enhetsgrupp.

If `coolpage.feature.html` kommer från ett klientcache-minne, AEM har inte möjlighet att analysera begäran för att ta reda på att mobilväljaren inte matchar den nya användaragenten och Bob får fel representation.

Du kan lösa det genom att ta med ett enkelt markeringsgränssnitt på sidorna, där slutanvändarna kan åsidosätta enhetsgruppen som markerats av AEM. I exemplet ovan kan slutanvändaren växla till `coolpage.touch.html` om de tycker att deras enhet är tillräckligt bra för det.
