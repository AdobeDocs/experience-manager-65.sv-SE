---
title: Skapa platser för mobila enheter
seo-title: Skapa platser för mobila enheter
description: Att skapa en mobilwebbplats liknar att skapa en standardwebbplats, eftersom det även handlar om att skapa mallar och komponenter
seo-description: Att skapa en mobilwebbplats liknar att skapa en standardwebbplats, eftersom det även handlar om att skapa mallar och komponenter
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Skapa platser för mobila enheter{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Att skapa en mobilwebbplats liknar att skapa en standardwebbplats, eftersom det även handlar om att skapa mallar och komponenter. Mer information om hur du skapar mallar och komponenter finns på följande sidor: [Mallar](/help/sites-developing/templates.md), [komponenter](/help/sites-developing/components.md) och [Komma igång med att utveckla AEM-platser](/help/sites-developing/getting-started.md). Den största skillnaden är att aktivera de inbyggda mobilfunktionerna i AEM på webbplatsen. Detta uppnås genom att skapa en mall som är beroende av mobilsidkomponenten.

Du bör också överväga att använda [responsiv design](/help/sites-developing/responsive.md), så att du kan skapa en enda plats som kan hantera flera skärmstorlekar.

Du kan komma igång genom att titta på **vår demowebbplats** för återförsäljning som är tillgänglig i AEM.

Så här skapar du en mobilwebbplats:

1. Skapa sidkomponenten:

   * Ange `sling:resourceSuperType` egenskapen på `wcm/mobile/components/page`det här sättet som komponenten är beroende av den mobila sidkomponenten.

   * Skapa `body.jsp` med projektspecifik logik.

1. Skapa sidmallen:

   * Ställ in egenskapen på den `sling:resourceType` nya sidkomponenten.
   * Ange `allowedPaths` egenskapen.

1. Skapa designsidan för webbplatsen.
1. Skapa platsrotsidan under `/content` noden:

   * Ange `cq:allowedTemplates` egenskapen.
   * Ange `cq:designPath` egenskapen.

1. Ange enhetsgrupperna på fliken **Mobil** i sidegenskaperna för webbplatsens rotsida.
1. Skapa webbplatssidorna med den nya mallen.

Komponenten för mobilsidan ( `/libs/wcm/mobile/components/page`):

* Lägger till fliken **Mobil** i dialogrutan för sidegenskaper.
* Genom `head.jsp``drawHead()` den hämtas den aktuella mobilenhetsgruppen från begäran och om en enhetsgrupp hittas använder gruppens metod för att inkludera den tillhörande emulatorinit-komponenten för enhetsgruppen (endast i redigeringsläge) och enhetsgruppens återgivnings-CSS.

>[!NOTE]
>
>Rotsidan för den mobila webbplatsen måste vara på nivå 1 i nodhierarkin och bör vara under noden /content.

## Skapa en mobil webbplats med Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Använd Multi Site Manager (MSM) för att skapa en mobil live kopia från en standardwebbplats. Standardwebbplatsen omvandlas automatiskt till en mobil webbplats: mobilsajten har alla funktioner som finns på mobilsajterna (t.ex. utgåva i en emulator) och kan hanteras synkroniserat med standardsajten. Se avsnittet [Skapa en Live-kopia för olika kanaler](/help/sites-administering/msm.md) på sidan Multi Site Manager.

## Mobile API för serversidan {#server-side-mobile-api}

Java-paketen som innehåller de mobila klasserna är:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definierar MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - definierar Device, DeviceGroup och DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.capabilities](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definierar DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - definierar WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - definierar MobileUtil, som tillhandahåller olika verktygsmetoder som kretsar kring WCM Mobile.

### Mobilkomponenter {#mobile-components}

Demonstrationswebbplatsen **för** webb.butik använder följande mobila komponenter som finns nedan `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Namn</td>
   <td>Grupp</td>
   <td>Egenskaper</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>hidden</td>
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
   <td>- baserat på listgrundskomponenten<br /> - listitem_teaser.jsp återger en bild om enheten kan<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>hidden</td>
   <td>- baserat på komponenten<br /> som utgör grunden för logotypen - återger en bild om enheten är kapabel<br /> </td>
  </tr>
  <tr>
   <td>mobilreferens</td>
   <td>Mobil</td>
   <td><p>- som liknar komponenten för referensgrunden</p> <p>- mappar en textimage-komponent till en mobilextimage en och en image-komponent till en mobilbild en</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobil</td>
   <td>- baserat på komponenten<br /> textimage Foundation - återger en bild om enheten är kapabel</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>hidden</td>
   <td><p>- baserat på den topnav Foundation-komponenten</p> <p>- återger bara text</p> </td>
  </tr>
 </tbody>
</table>

#### Skapa en mobilkomponent {#creating-a-mobile-component}

Med AEM Mobile-ramverket kan du utveckla komponenter som är känsliga för den enhet som skickar begäran. I följande kodexempel visas hur du använder AEM Mobile API i en komponent-jsp och särskilt hur du gör:

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
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`...ELLER
   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>I ett jsp `slingRequest` är tillgängligt via `<sling:defineObjects>` -taggen och `currentPage` via `<cq:defineObjects>` -taggen.

### Emulatorer {#emulators}

Emulatorbaserad redigering ger författare möjlighet att skapa innehållssidor som är avsedda för mobila klienter. Framtagning av mobilt innehåll följer samma princip för WYSIWYG-redigering på plats. För att författare ska kunna uppfatta sidutseendet på en mobil enhet redigeras en mobilinnehållssida med en enhetsemulator.

Emulatorer för mobila enheter är baserade på det generiska emulatorramverket. Mer information finns på sidan [Emulatorer](/help/sites-developing/emulators.md) .

Enhetsemulatorn visar den mobila enheten på sidan medan den vanliga redigeringen (parsys, components) sker på enhetens skärm. Enhetsemulatorn beror på de enhetsgrupper som är konfigurerade för platsen. Flera emulatorer kan tilldelas till en enhetsgrupp. Alla emulatorer är sedan tillgängliga på innehållssidan. Som standard visas den första emulatorn som tilldelats den första enhetsgruppen som tilldelats platsen. Emulatorerna kan bytas antingen via emulatorkarusellen högst upp på sidan eller via Sidekes redigeringsknapp.

**Skapa en emulator**

Mer information om hur du skapar en emulator finns i avsnittet [Skapa en anpassad mobilemulator](/help/sites-developing/emulators.md) på den generiska emulatorsidan.

**De viktigaste egenskaperna hos emulatorer för mobila enheter**

* En enhetsgrupp består av en av flera emulatorer: konfigurationssidan för enhetsgruppen, t.ex. /etc/mobile/groups/touch, innehåller egenskapen `emulators` under `jcr:content` noden.
Obs! Även om det är möjligt att samma emulator tillhör flera enhetsgrupper så är det inte särskilt klokt.

* Via enhetsgruppens konfigurationsdialogruta ställs egenskapen in med sökvägen till önskad(a) emulator(er). `emulators` Exempel: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Emulatorkomponenter (t.ex. `/libs/wcm/mobile/components/emulators/iPhone4`) utöka den grundläggande mobilemulatorkomponenten ( `/libs/wcm/mobile/components/emulators/base`).

* Alla komponenter som utökar basmobilemulatorn är tillgängliga för val när en enhetsgrupp konfigureras. Anpassade emulatorer kan enkelt skapas eller utökas.
* Vid begäran i redigeringsläge används emulatorimplementeringen för att återge sidan.
* När sidmallen är beroende av den mobila sidkomponenten, integreras emulatorfunktionerna automatiskt på sidan (via `head.jsp` den mobila sidkomponenten).

### Enhetsgrupper {#device-groups}

Mobila enhetsgrupper ger segmentering av mobila enheter baserat på enhetens funktioner. En enhetsgrupp innehåller den information som krävs för emulatorbaserad redigering på författarinstansen och för korrekt innehållsåtergivning på publiceringsinstansen: När författarna har lagt till innehåll på mobilsidan och publicerat det kan sidan begäras på publiceringsinstansen. I stället för emulatorns redigeringsvy återges innehållssidan med en av de konfigurerade enhetsgrupperna. Valet av enhetsgruppen görs baserat på identifiering [av](#devicedetection)mobila enheter. Den matchande enhetsgruppen tillhandahåller sedan nödvändig formatinformation.

Enhetsgrupper definieras som innehållssidor nedan `/etc/mobile/devices` och använder mallen **Mobile Device Group** . Enhetens gruppmall fungerar som en konfigurationsmall för enhetsgruppsdefinitioner i form av innehållssidor. Dess huvudsakliga egenskaper är:

* Plats: `/libs/wcm/mobile/templates/devicegroup`
* Tillåten sökväg: `/etc/mobile/groups/*`
* Sidkomponent: `wcm/mobile/components/devicegroup`

#### Tilldela enhetsgrupper till din webbplats {#assigning-device-groups-to-your-site}

När du skapar en mobilwebbplats måste du tilldela enhetsgrupper till webbplatsen. AEM har tre enhetsgrupper beroende på enhetens HTML- och JavaScript-återgivningsfunktioner:

* **Funktionstelefoner** för enheter som Sony Ericsson W800 med stöd för grundläggande HTML, men utan stöd för bilder och JavaScript.
* **Smarta** telefoner, för enheter som Blackberry med stöd för grundläggande HTML och bilder, men inget stöd för JavaScript.

* **Pektelefoner** , för enheter som iPad med fullt stöd för HTML, bilder, JavaScript och enhetsrotation.

När emulatorer kan kopplas till en enhetsgrupp (se avsnittet [Skapa en enhetsgrupp](#creating-a-device-group)) kan författare som tilldelar en enhetsgrupp till en plats välja mellan de emulatorer som är kopplade till enhetsgruppen för att redigera sidan.

Så här tilldelar du en enhetsgrupp till din plats:

1. Gå till **SiteAdmin** Console i webbläsaren.
1. Öppna rotsidan för den mobila webbplatsen under **Webbplatser**.
1. Öppna sidegenskaperna.
1. Välj fliken **Mobil** :

   * Definiera enhetsgrupperna.
   * Click **OK**.

>[!NOTE]
>
>När enhetsgrupperna har definierats för en plats, ärvs de av alla sidor på platsen.

#### Enhetsgruppsfilter {#device-group-filters}

Enhetsgruppsfilter definierar funktionsbaserade villkor för att avgöra om en enhet tillhör gruppen. När du skapar en enhetsgrupp kan du välja vilka filter som ska användas för att utvärdera enheter.

Vid körning när AEM tar emot en HTTP-begäran från en enhet, jämför varje filter som är kopplat till en grupp enhetens funktioner med specifika kriterier. Enheten anses tillhöra gruppen när den har alla funktioner som filtren kräver. Funktioner hämtas från WURFL™-databasen.

Enhetsgrupper kan använda noll eller flera filter för funktionsidentifiering. Ett filter kan också användas med flera enhetsgrupper. AEM tillhandahåller ett standardfilter som avgör om enheten har de funktioner som är valda för en grupp:

* CSS
* JPG- och PNG-bilder
* JavaScript
* Enhetsrotation

Om enhetsgruppen inte använder ett filter är de valda funktionerna som är konfigurerade för gruppen de enda funktioner som en enhet behöver.

Mer information finns i [Skapa enhetsgruppsfilter](/help/sites-developing/groupfilters.md).

#### Skapa en enhetsgrupp {#creating-a-device-group}

Skapa en enhetsgrupp när grupperna som AEM installerar inte uppfyller dina krav.

1. Gå till **verktygskonsolen** i webbläsaren.
1. Skapa en ny sida under **Verktyg** > **Mobil** > **Enhetsgrupper**. I dialogrutan **Skapa sida** :

   * Som **titel** anger du `Special Phones`.

   * Som **namn** anger du `special`.

   * Välj **gruppmallen** för mobila enheter.
   * Klicka på **Skapa**.

1. I CRXDE lägger du till en **static.css** -fil som innehåller stilarna för enhetsgruppen under `/etc/mobile/groups/special` noden.

1. Öppna sidan **Specialtelefoner** .
1. Om du vill konfigurera enhetsgruppen klickar du på knappen **Redigera** bredvid **Inställningar**.
På fliken **Allmänt** :

   * **Titel**: namnet på mobilenhetsgruppen.
   * **Beskrivning**: beskrivning av gruppen.
   * **Användaragent**: användaragentsträng som enheterna matchas mot. Den är valfri och kan vara en regex. Exempel: `BlackBerryZ10`
   * **Funktioner**: definierar om gruppen kan hantera bilder, CSS, JavaScript eller enhetsrotation.
   * **Minsta skärmbredd** och **-höjd**
   * **Inaktivera emulatorn**: för att aktivera/inaktivera emulatorn under innehållsredigering.
   På fliken **Emulatorer** :

   * **Emulatorer**: Välj emulatorerna som är tilldelade den här enhetsgruppen.
   På fliken **Filter** :

   * Om du vill lägga till ett filter klickar du på Lägg till objekt och väljer ett filter i listrutan.
   * Filter utvärderas i den ordning som de visas. När en enhet inte uppfyller filtervillkoren utvärderas inte efterföljande filter i listan.



1. Klicka på OK.

Dialogrutan för konfiguration av mobilenhetsgrupp ser ut så här:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### Anpassad CSS per enhetsgrupp {#custom-css-per-device-group}

Så som beskrivs ovan är det möjligt att koppla en anpassad CSS till en enhetsgruppssida, ungefär som CSS för en designsida. Den här CSS används för att påverka den enhetsgruppsspecifika återgivningen av sidinnehållet vid författaren och vid publiceringen. Den här CSS-koden inkluderas sedan automatiskt:

* På sidan för författarinstansen för varje emulator som används av den här enhetsgruppen.
* På sidan i publiceringsinstansen om användaragenten för begäran matchar en mobil enhet i den här enhetsgruppen.

## Enhetsidentifiering på serversidan {#server-side-device-detection}

Använd filter och ett bibliotek med enhetsspecifikationer för att avgöra vilka funktioner den enhet som utför HTTP-begäran har.

### Skapa enhetsgruppsfilter {#develop-device-group-filters}

Skapa ett enhetsgruppsfilter för att definiera en uppsättning krav för enhetsfunktioner. Skapa så många filter du behöver för att rikta in dig på de grupper av enhetsfunktioner som behövs.

Utforma dina filter så att du kan använda kombinationer av dem för att definiera grupper av funktioner. Vanligtvis finns det överlappande funktioner för olika enhetsgrupper. Därför kan du använda vissa filter med flera enhetsgruppsdefinitioner.

När du har skapat ett filter kan du använda det i gruppkonfigurationen.

Mer information finns i [Skapa enhetsgruppsfilter](/help/sites-developing/groupfilters.md).

### Använda WURFL™-databasen {#using-the-wurfl-database}

AEM använder en trunkerad version av [WURFL](https://wurfl.sourceforge.net/)™-databasen för att fråga efter enhetsfunktioner, som skärmupplösning eller stöd för javascript, baserat på enhetens användaragent.

XML-koden för WURFL™-databasen representeras som noder nedan `/var/mobile/devicespecs` genom att `wurfl.xml`filen analyseras vid `/libs/wcm/mobile/devicespecs/wurfl.xml.` Utökningen till noder första gången som `cq-mobile-core` paketet startas.

Enhetsfunktionerna lagras som nodegenskaper och noderna representerar enhetsmodeller. Du kan använda frågor för att hämta funktionerna för en enhet eller en användaragent.

I takt med att WURFL™-databasen utvecklas kan du behöva anpassa eller ersätta den. Du kan uppdatera databasen för mobila enheter på följande sätt:

* Ersätt filen med den senaste versionen om du har en licens som tillåter den här användningen. Se Installera en annan WURFL-databas.
* Använd den version som finns i AEM och konfigurera en regexp som matchar strängarna för användaragenten och pekar på en befintlig WURFL™-enhet. Se [Lägga till en regexpbaserad matchning](#adding-a-regexp-based-user-agent-matching)av användaragent.

#### Testa mappningen av en användaragent till WURFL™-funktioner {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

När en enhet kommer åt din mobila webbplats känner AEM av enheten, mappar den till en enhetsgrupp enligt dess funktioner och skickar en vy över sidan som motsvarar enhetsgruppen. Den matchande enhetsgruppen tillhandahåller nödvändig formatinformation. Mappningarna kan testas på testsidan för Mobile User-Agent:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installera en annan WURFL™-databas {#installing-a-different-wurfl-database}

Den trunkerade WURFL™-databasen som installeras med AEM är en release som är före den 30 augusti 2011. Om din version av WURFL släpptes efter den 30 augusti 2011 kontrollerar du att din användning överensstämmer med din licens.

Så här installerar du en WURFL™-databas:

1. Skapa följande mapp i CRXDE Lite: `/apps/wcm/mobile/devicespecs`
1. Kopiera WURFL™-filen till mappen.
1. Byt namn på filen som `wurfl.xml`.

AEM tolkar automatiskt `wurfl.xml` filen och uppdaterar noderna nedan `/var/mobile/devicespecs`.

>[!NOTE]
>
>När den fullständiga WURFL™-databasen är aktiverad kan det ta några minuter att analysera och aktivera. Du kan se loggarna för förloppsinformation.

#### Lägga till en regexp-baserad användaragentmatchning {#adding-a-regexp-based-user-agent-matching}

Lägg till en användaragent som ett reguljärt uttryck nedan /apps/wcm/mobile/devicespecs/wurfl/regexp för att peka på en befintlig WURFL™-enhetstyp.

1. I **CRXDE Lite** skapar du en nod under /apps/wcm/mobile/devicespecs/regexp, t.ex. apple_ipad_ver1.
1. Lägg till följande egenskaper i noden:

   * **regexp**: reguljära uttryck som definierar användaragenter, t.ex.: .*Mozilla.*iPad.*AppleWebKit.*Safari.*
   * **deviceId**: det enhets-ID som definieras i wurfl.xml, t.ex.: apple_ipad_ver1

Ovanstående konfiguration gör att enheter som User-Agent matchar det angivna reguljära uttrycket mappas till Apple_ipad_ver1 WURFL™-enhets-ID, om det finns.

## Identifiering av klientenhet {#client-side-device-detection}

I det här avsnittet beskrivs hur du använder enhetsidentifieringen av AEM på klientsidan för att optimera sidåtergivningen eller för att förse klienten med alternativa webbplatsversioner.

AEM har stöd för identifiering på klientsidan baserat på `BrowserMap`. `BrowserMap` levereras i AEM som ett klientbibliotek under `/etc/clientlibs/browsermap`.

`BrowserMap` innehåller tre strategier som du kan använda för att tillhandahålla en alternativ webbplats till en kund, som används i följande ordning:

1. [Alternativa länkar](#providing-alternate-links)
1. [Enhetsgruppspecifik URL](#definingdevicegroupspecificurl)
1. [Väljarbaserad URL](#defining-selector-based-urls)

>[!NOTE]
>
>Mer information om integrering av klientbibliotek finns i avsnittet [Använda HTML-bibliotek](/help/sites-developing/clientlibs.md) på klientsidan.

### Ange alternativa länkar {#providing-alternate-links}

OSGi- `PageVariantsProvider` tjänsten kan generera alternativa länkar för platser som tillhör samma familj. Om du vill konfigurera platser som ska beaktas av tjänsten måste en nod läggas till i `cq:siteVariant` `jcr:content` noden från platsens rot.

Noden måste `cq:siteVariant` ha följande egenskaper:

* `cq:childNodesMapTo` - bestämmer vilket attribut för länkelementet som de underordnade noderna ska mappas till, Vi rekommenderar att du ordnar innehållet på din webbplats på ett sådant sätt att rotnodens underordnade objekt representerar roten för en språkvariant av din globala webbplats (t.ex. `/content/mysite/en`, `/content/mysite/de`), i vilket fall värdet på `cq:childNodesMapTo` den ska vara `hreflang`.
* `cq:variantDomain` - anger vilken `Externalizer` domän som kommer att användas för att generera sidvarianternas absoluta URL:er, Om detta värde inte anges genereras sidvarianterna med relativa länkar.
* `cq:variantFamily` - anger vilken typ av webbplatser denna webbplats tillhör, Flera enhetsspecifika representationer av samma webbplats bör tillhöra samma familj.
* `media` - lagrar värdena för länkelementets medieattribut, Vi rekommenderar att du använder namnet på den `BrowserMap` registrerade `DeviceGroups`så att `BrowserMap` biblioteket automatiskt kan vidarebefordra klienterna till rätt variant av webbplatsen.

#### PageVariantsProvider och Externalizer {#pagevariantsprovider-and-externalizer}

När värdet för `cq:variantDomain` egenskapen för en `cq:siteVariant` nod inte är tomt genereras absoluta länkar med det här värdet som en konfigurerad domän för `PageVariantsProvider` `Externalizer` tjänsten. Se till att konfigurera `Externalizer` tjänsten så att den återspeglar din konfiguration.

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommendationer finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

### Definiera en enhetsgruppsspecifik URL {#defining-a-device-group-specific-url}

Om du inte vill använda alternativa länkar kan du konfigurera en global URL för varje `DeviceGroup`. Vi rekommenderar att du skapar ett eget klientbibliotek som bäddar in `browsermap.standard` klientbiblioteket men definierar om enhetsgrupperna.

BrowserMap är utformat på ett sådant sätt att definitioner för enhetsgrupper kan åsidosättas genom att en ny enhetsgrupp med samma namn skapas och läggs till i `BrowserMap` objektet från ditt anpassade klientbibliotek.

>[!NOTE]
>
>Mer information finns i avsnittet [Customized BrowserMap](#creatingacustomisedbrowsermap) .

### Definiera väljarbaserade URL:er {#defining-selector-based-urls}

Om ingen av de tidigare funktionerna har använts för att ange en alternativ plats för `BrowserMap`kommer väljare som använder namnen på `DeviceGroups` att läggas till i `URL`grupperna. I så fall bör du ange egna servrar som hanterar förfrågningarna.

En enhetssurfning `www.example.com/index.html` som identifieras `smartphone` av BrowserMap vidarebefordras till exempel till `www.example.com/index.smartphone.html.`

### Använda BrowserMap på dina sidor {#using-browsermap-on-your-pages}

Om du vill använda standardklientbiblioteket BrowserMap på en sida måste du inkludera `/libs/wcm/core/browsermap/browsermap.jsp` filen med en `cq:include`tagg i sidans `head` avsnitt.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Förutom att lägga till `BrowserMap` klientbiblioteket i dina `JSP` filer måste du också lägga till en `cq:deviceIdentificationMode` String-egenskap som anges `client-side` till `jcr:content` noden nedanför webbplatsens rot.

### Åsidosätta BrowserMaps standardbeteende {#overriding-browsermap-s-default-behaviour}

Om du vill anpassa `BrowserMap` - genom att åsidosätta `DeviceGroups` eller lägga till fler avsökningar - bör du skapa ett eget klientbibliotek där du bäddar in `browsermap.standard`klientbiblioteket.

Dessutom måste du manuellt anropa metoden `BrowserMap.forwardRequest()` i din `JavaScript` kod.

>[!NOTE]
>
>Mer information om integrering av klientbibliotek finns i avsnittet [Använda HTML-bibliotek](/help/sites-developing/clientlibs.md) på klientsidan.

När du har skapat ett anpassat `BrowserMap` klientbibliotek föreslår vi följande tillvägagångssätt:

1. Skapa en `browsermap.jsp` fil i programmet

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

1. Inkludera `broswermap.jsp` filen i huvudsektionen.

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

Detta gör att `/libs/wcm/core/browsermap/browsermap.jsp` skriptet lägger till en meta-tagg på sidan som gör `BrowserMap` att ingen identifiering utförs:

```xml
<meta name="browsermap.enabled" content="false">
```

### Testa en specifik version av en webbplats {#testing-a-specific-version-of-a-web-site}

Skriptet BrowserMap dirigerar normalt alltid om besökarna till den lämpligaste versionen av webbplatsen, och dirigerar vanligtvis om besökarna till skrivbordet eller till den mobila webbplatsen vid behov.

Du kan tvinga fram en enhet för en begäran för att testa en specifik version av en webbplats genom att lägga till parametern `device` i URL:en. Följande URL återger den mobila versionen av webbplatsen Geometrixx Outdoor.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>Parametern `wcmmode` ställs in på `disabled` för att simulera beteendet för en publiceringsinstans.

Det åsidosatta enhetsvärdet lagras i en cookie så att du kan bläddra på webbplatsen utan att lägga till `device` parametern för varje `URL`.

Därför måste du ringa samma sak `URL` med den `device` inställda inställningen `browser` för att komma tillbaka till datorversionen av webbplatsen.

>[!NOTE]
>
>BrowserMap lagrar det åsidosatta enhetsvärdet i en cookie som kallas `BMAP_device`. Om du tar bort den här cookien kommer CQ att fungera som den version av webbplatsen som passar din aktuella enhet (t.ex. dator eller mobil).

## Behandling av mobilförfrågningar {#mobile-request-processing}

AEM bearbetar en begäran som skickas av en mobil enhet som tillhör gruppen med pekenheter enligt följande:

1. En iPad skickar en begäran till AEM-publiceringsinstansen, t.ex. `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM avgör om den begärda sidans webbplats är en mobilwebbplats (genom att kontrollera om den första sidan `/content/geometrixx_mobile` utökar den mobila sidkomponenten). Om ja:
1. AEM söker upp enhetsfunktionerna baserat på användaragenten i begärandehuvudet.
1. AEM mappar enhetsfunktionerna till enhetsgruppen och anger dem `touch` som enhetsgruppsväljare.
1. AEM dirigerar om begäran till `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM skickar svaret till iPad:

   * `products.touch.html` renderas på vanligt sätt och kan nås.
   * Återgivningskomponenterna använder väljare för att anpassa presentationen.
   * AEM lägger automatiskt till mobilväljaren till alla interna länkar på sidan.

### Statistik {#statistics}

Du kan hämta statistik om antalet förfrågningar som gjorts till AEM-servern via mobila enheter. Antalet begäranden kan delas upp:

* per enhetsgrupp och enhet
* per år, månad och dag

Så här visar du statistiken:

1. Gå till **verktygskonsolen** .
1. Öppna sidan **Enhetsstatistik** under **Verktyg** > **Mobil**.
1. Klicka på länken om du vill visa statistik för ett visst år, en viss månad eller en viss dag.

Sidan **Statistik** ser ut så här:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>Sidan **Statistik** skapas första gången en mobilenhet öppnar AEM och identifieras. Den är inte tillgänglig tidigare.

Om du behöver generera en post i statistiken kan du göra så här:

1. Använd en mobil enhet eller en emulator (till exempel https://chrispederick.com/work/user-agent-switcher/ i Firefox).
1. Begär en mobilsida på författarinstansen genom att inaktivera redigeringsläget, t.ex.:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

Sidan **Statistik** är nu tillgänglig.

### Cachelagring av stödsidor för länkar av typen &quot;skicka länk till en vän&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Mobilsidor kan oftast nås via Dispatcher, eftersom sidor som återges för en enhetsgrupp urskiljs i sidans URL av enhetsgruppsväljaren, till exempel `/content/mobilepage.touch.html`. En begäran till en mobilsida utan väljare cachelagras aldrig, som i det här fallet utförs enhetsidentifieringen och dirigeras till den matchande enhetsgruppen (eller&quot;nominatch&quot; för den delen). En mobilsida som återges med en enhetsgruppsväljare bearbetas av länkomskrivaren, som skriver om alla länkar på sidan så att de även innehåller enhetsgruppsväljaren, vilket förhindrar att enhetsidentifiering utförs på nytt varje gång du klickar på en redan kvalificerad sida.

Därför kan du stöta på följande scenario:

Användare Alice omdirigeras till `coolpage.feature.html`och skickar den URL:en till en vän Bob som kommer åt den med en annan klient som ingår i `touch` enhetsgruppen.

Om `coolpage.feature.html` betjänas från ett klientcache-minne får AEM ingen chans att analysera begäran för att ta reda på att mobilväljaren inte matchar den nya användaragenten och Bob får fel representation.

För att lösa problemet kan du inkludera ett enkelt markeringsgränssnitt på sidorna, där slutanvändarna kan åsidosätta enhetsgruppen som valts av AEM. I exemplet ovan kan slutanvändaren växla till en länk (eller en ikon) på sidan `coolpage.touch.html` om han anser att enheten är tillräckligt bra för det.
