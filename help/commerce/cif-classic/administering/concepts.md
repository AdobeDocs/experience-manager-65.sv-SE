---
title: Concepts
description: Lär dig de allmänna koncepten för e-handel med Adobe Experience Manager.
contentOwner: Guillaume Carlino
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '4439'
ht-degree: 0%

---

# Concepts{#concepts}

Integreringsramverket innehåller mekanismer och komponenter för att

* anslutning till en e-handelsmotor
* hämta in data i Adobe Experience Manager (AEM)
* visa dessa data och samla in kundens svar
* returnera transaktionsinformation
* söka efter data från båda systemen

Detta innebär att

* Köpare kan registrera sig och handla utan att vänta.
* Prisförändringar ses av kunderna utan dröjsmål.
* Produkter kan läggas till efter behov.

>[!NOTE]
>
>e-handelsramverket kan användas med:
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [SAP Commerce Cloud](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
>

>[!CAUTION]
>
>Integreringsramverket [eCommerce](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) är en AEM.
>
>Säljaren kan ge fullständig information enligt lämplig motor.

>[!CAUTION]
>
>Ramverket innehåller de grundläggande kraven för ditt eget projekt.
>
>En viss del av utvecklingsarbetet behövs alltid för att anpassa ramverket till dina specifikationer.

>[!CAUTION]
>
>Standardinstallationen AEM innehåller den allmänna AEM (JCR)-implementeringen av e-handel.
>
>Detta är avsett för demonstrationssyften, eller som en grundläggande grund för en anpassad implementering enligt dina krav.

För att optimera driften koncentrerar sig både AEM och e-handelsmotorn på sin egen expertis. Information överförs mellan de två i realtid, till exempel:

* AEM kan:

   * Begäran:

      * Produktinformation från e-handelsmotorn.

   * Ange:

      * Användarvyer för produktinformation, kundvagn och utcheckning.
      * Information om varukorgar och utcheckning till e-handelsmotorn.
      * Sökmotoroptimering (SEO).
      * Community-funktioner.
      * Ostrukturerade marknadsföringsinteraktioner.

* e-handelsmotorn kan:

   * Ange:

      * Produktinformation från databasen.
      * Hantering av produktvarianter.
      * Order Management.
      * ERP (Enterprise Resource Planning).
      * Sök i produktinformationen.

   * Process:

      * Kundvagnen.
      * Utcheckningen.
      * Beställningsvillkoren.

>[!NOTE]
>
>Exakt information beror på e-handelsmotorn och projektets implementering.

Det finns flera färdiga AEM för att använda integreringslagret. För närvarande omfattar dessa:

* Produktinformation
* Kundvagn
* Checka ut
* Mitt konto

Det finns även olika sökalternativ.

## Arkitektur {#architecture}

Integreringsramverket innehåller API:t, en rad komponenter som illustrerar funktioner och flera tillägg som ger exempel på anslutningsmetoder:

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

Ramverket ger dig tillgång till funktioner som:

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementeringar {#implementations}

AEM e-handel genomförs med en e-handelsmotor:

* Integreringsramverket för e-handel har byggts för att du enkelt ska kunna integrera en e-handelsmotor med AEM. Den specialbyggda e-handelsmotorn styr produktdata, varukorgar, utcheckning och orderhantering, medan AEM styr visningen av data och marknadsföringskampanjer.


>[!NOTE]
>
>Standardinstallationen AEM innehåller den allmänna AEM (JCR)-implementeringen av e-handel.
>
>Detta är avsett för demonstrationssyften, eller som en grundläggande grund för en anpassad implementering enligt dina krav.
>
>AEM eCommerce som genomförs inom AEM med allmän utveckling baserad på JCR är:
>
>* Ett fristående, AEM e-handelsexempel som visar hur API används. Detta kan användas för att kontrollera produktdata, varukorgar och utcheckning med befintliga dataspresentations- och marknadsföringskampanjer. I det här fallet lagras produktdatabasen i databasen som är inbyggd i AEM (Adobe-implementering av [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  Standardinstallationen AEM innehåller grunderna för den [allmänna e-handelsimplementeringen](/help/commerce/cif-classic/administering/generic.md).

### Commerce Providers {#commerce-providers}

När du importerar data från en e-handelsmotor till din AEM e-handelsplats används en e-handelsleverantör för att förse importörerna med data. En e-handelsleverantör kan stödja flera importörer.

En e-handelsleverantör är AEM kod som är anpassad till antingen:

* gränssnitt till en back-end-handelsmotor
* implementera ett handelssystem ovanpå JCR-databasen

Två exempel på e-handelsleverantörer finns för AEM:

* en för geometrixx-hybris
* en annan för geometrixx-generisk (JCR)

Vanligtvis måste ett projekt utveckla en egen, anpassad e-handelsleverantör som är specifik för PIM och produktdataschemat.

>[!NOTE]
>
>Importörerna använder CSV-filer. Det finns en beskrivning av det godkända schemat (med anpassade egenskaper tillåtna) i kommentarerna ovanför implementeringen.

[ProductServicesManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) underhåller (via [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)) en lista över implementeringar för gränssnitten [ProductImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) och [CatalogBlueImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html). Dessa listas i listrutan **Importör/Commerce-leverantör** i importguiden (med egenskapen `commerceProvider` som namn).

När en viss importör/e-handelsleverantör är tillgänglig från listrutan måste alla kompletterande uppgifter som den behöver definieras (beroende på importörens typ) i antingen

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

Mappen under rätt `importers`-mapp måste matcha importnamnet, till exempel:

* `.../importproductswizard/importers/geometrixx/.content.xml`

Formatet på källimportfilen definieras av importeraren. Eller så kan importören upprätta en anslutning (till exempel WebDAV eller http) till e-handelsmotorn.

## Roller {#roles}

Det integrerade systemet fångar upp följande roller för att underhålla data:

* PIM-användare (Product Information Management) som underhåller:

   * Produktinformation.
   * Taxonomi, kategorisering, godkännande.
   * Samverkar med digital resurshantering.
   * Priser - gäller ofta från ett ERP-system och upprätthålls inte uttryckligen i handelssystemet.

* Författare/Marknadsförare som underhåller:

   * Marknadsföringsmaterial för alla kanaler.
   * Kampanjer.
   * Vouchers.
   * Kampanjer.

* Surfer/köpare som:

   * Visar din produktinformation.
   * Placerar artiklar i kundvagnen.
   * Kolla in deras order.
   * Förväntade orderuppfyllelse.

Även om den faktiska platsen kan vara beroende av implementeringen, till exempel generisk eller med en e-handelsmotor:

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Produkter {#products}

### Produktdata kontra marknadsföringsdata {#product-data-versus-marketing-data}

#### Strukturella kontra marknadsföringskategorier {#structural-versus-marketing-categories}

Om följande två kategorier kan särskiljas kan du med den här metoden skapa tydliga URL-adresser med en meningsfull struktur (träd med `cq:Page` noder) och därför mycket nära klassisk AEM-innehållshantering):

* *Strukturella *kategorier

  Kategoriträdet som definierar *vad som är en produkt*, till exempel:

  `/products/mens/shoes/sneakers`

* *Marknadsföring* kategorier

  Alla andra kategorier som en *produkt kan tillhöra*, till exempel:

  `/special-offers/christmas/shoes`)

### Produktdata {#product-data}

Om du vill visa och hantera produkten måste du lagra en mängd information om dem.

Produktdata kan vara:

* behålls direkt i AEM (generiskt).
* i eCommerce Engine och i AEM.

  Beroende på datatypen är den [synkroniserad](#catalog-maintenance-data-synchronization) vid behov eller direkt åtkomlig. Till exempel hämtas mycket flyktiga och kritiska data som produktpriser från e-handelsmotorn på varje sidbegäran för att säkerställa att de alltid är aktuella.

Oavsett vilket kan du se produktdata från konsolen **Produkter** när produktdata har angetts/importerats till AEM. Här visas kort- och listvyerna för en produkt, t.ex.:

* bilden
* SKU-koden
* när den senast ändrades

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Produktvarianter {#product-variants}

För lämpliga produkter kan information om varianter också finnas. För klädesplagg hålls t.ex. de olika tillgängliga färgerna som varianter:

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Produktattribut {#product-attributes}

De enskilda attributen för respektive produkt kan vara beroende av vilken e-handelsmotor som används och hur AEM implementeras. Dessa är tillgängliga (om det är lämpligt) vid visning av produktsidor och/eller redigering av produktinformation och kan omfatta:

* **Bild**

  En bild av produkten.

* **Titel**

  Produktnamnet.

* **Beskrivning**

  En textbeskrivning av produkten.

* **Taggar**

  Taggar som används för att gruppera relaterade produkter.

* **Standardtillgångskategori**

  En standardkategori för resurser.

* **ERP-data**

  ERP-information (Enterprise resource planning).

   * **SKU**

     Information om lagerställeenhet.

   * **Färg**
   * **Storlek**
   * **Pris**

     Enhetspriset för produkten.

* **Sammanfattning**

  En sammanfattning av produktfunktionerna.

* **Funktioner**

  Detaljerad information om produktfunktionerna.

### Assets {#product-assets}

Ett urval av mediefiler kan sparas för enskilda produkter. Vanligtvis är det bilder och videoklipp.

## Kataloger {#catalogs}

En katalog grupperar produktdata för både enkel hantering och representation för kunden. En katalog är ofta strukturerad enligt attribut som språk, geografiskt område, varumärke, årstid, hobby, sport bland många andra.

### Katalogstruktur {#catalog-structure}

#### Kataloger på flera språk {#catalogs-in-multiple-languages}

AEM stöder produktinnehåll på flera språk. När integreringsramverket begär data hämtar det språket från det aktuella trädet (till exempel `en_US` för sidor under `/content/geometrixx-outdoors/en_US`).

För en flerspråkig butik kan du importera katalogen för varje språkträd individuellt (eller kopiera den med [MSM](/help/sites-administering/msm.md)).

#### Kataloger för flera varumärken {#catalogs-for-multiple-brands}

Liksom för språk måste stora flernationella företag ta hand om flera varumärken.

#### Kataloger efter taggar {#catalogs-by-tags}

Taggar kan också användas för att gruppera produkter i en katalog. De kan användas för mer dynamiska kataloger, till exempel säsongserbjudanden.

### Kataloginställningar (inledande import) {#catalog-setup-initial-import}

Beroende på implementeringen kan du importera produktdata som krävs för din baskatalog till AEM från:

* en CSV-fil (för allmän implementering)
* e-handelsmotorn

### Katalogunderhåll (datasynkronisering) {#catalog-maintenance-data-synchronization}

Ytterligare ändringar i produktinformationen är oundvikliga:

* för den allmänna implementeringen kan dessa hanteras med [produktredigeraren](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* när en [e-handelsmotor används måste ändringarna synkroniseras](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Datasynkronisering med en e-handelsmotor (pågående) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Efter den första importen är det oundvikligt att ändra produktinformationen.

När du använder en e-handelsmotor bevaras produktdata där och måste vara tillgängliga i AEM. Produktdata måste synkroniseras när uppdateringar görs.

Detta kan bero på datatypen:

* En [periodisk synkronisering används tillsammans med en datafeed med ändringar](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  Förutom detta kan du välja specifika uppdateringar för en snabbuppdatering.

* Mycket volatila data, till exempel prisinformation, hämtas från e-handelsmotorn för varje sidförfrågan för att säkerställa att de alltid är aktuella.

### Kataloger - prestanda och skalning {#catalogs-performance-and-scaling}

Om du importerar en stor katalog med ett stort antal produkter (fler än 100 000) från en e-handelsmotor (PIM) kan det påverka systemet på grund av det stora antalet noder. Det kan också göra redigeringsinstansen långsammare om produkterna har associerade resurser (till exempel produktbilder). Detta beror på att efterbearbetningen av dessa resurser är processor- och minneskrävande.

Det finns olika strategier som du kan använda för att lösa dessa problem:

* [Bucketing](#bucketing) - för att hantera det stora antalet noder
* [Avlasta efterbearbetning av resurser till en dedikerad instans](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importera endast produktdata](#only-import-product-data)
* [Importera begränsning och gruppspara](#import-throttling-and-batch-saves)
* [Prestandatestning](#performance-testing)
* [Prestanda - övriga](#performance-miscellaneous)

#### Bucketing {#bucketing}

Om en JCR-nod har många direkta underordnade noder (till exempel 1 000 och fler) krävs det bucket (phantom-mappar) för att säkerställa att prestandan inte påverkas. Dessa genereras enligt en algoritm vid import.

De här bucklarna har formen av fantommappar som introduceras i katalogstrukturen, men kan konfigureras så att de inte visas i offentliga URL:er.

#### Avlasta efterbearbetning av resurser till en dedikerad instans {#offload-asset-post-processing-to-a-dedicated-instance}

I det här scenariot ställs två författarinstanser in:

1. Författarinstans

   Importerar produktdata från PIM, där efterbearbetning för resurssökvägar är inaktiverat.

1. Dedikerad DAM-författarinstans

   Importerar och efterbearbetar produktresurser från PIM-filen och replikerar dem sedan tillbaka till masterförfattarinstansen för användning.

![Arkitekturdiagram](/help/sites-administering/assets/chlimage_1-8.png)

#### Importera endast produktdata {#only-import-product-data}

Om produkter inte innehåller resurser (bilder) som ska importeras kan du importera produktdata utan att påverkas av efterbearbetningen av resurser.

![Arkitekturdiagram](/help/sites-administering/assets/chlimage_1-9.png)

#### Prestandatestning {#performance-testing}

Prestandatestning måste övervägas AEM e-handelsimplementationer:

* Författarmiljö:

  Bakgrundsaktivitet (t.ex. import) kan ske samtidigt som normal användaraktivitet (t.ex. sidredigering) och även om frontendrestanda (i allmänhet) ges en högre prioritet, kan dålig prestanda som onlineförfattare ser leda till frustration som kan blockera ett beslut som går att publicera.

* Publiceringsmiljö:

  Replikering är en viktig process för att säkerställa att innehållet publiceras snabbt och tillförlitligt. Detta kan påverkas av hur författaren grupperar innehållet som ska publiceras.

* Front-end:

  Blandningen av front end- och cache-ogiltigförklaringar kan potentiellt leda till prestandaförbättringar. Testning hjälper till att undvika dessa.

Observera att den här prestandatestningen kräver kunskap om och analys av ditt mål:

* Innehållsvolymer

   * Assets
   * Lokaliserade I18end-produkter och SKU:er

* Användaraktivitet:

   * Massutgåva
   * Masspublicering
   * Intensivsökningar

* Bakgrundsprocesser

   * Importer
   * Synkroniseringsuppdateringar (till exempel priser)

* Underhållskrav (säkerhetskopia, optimering av Tjära PM, skräpinsamling för datastore osv.)

#### Prestanda - övriga {#performance-miscellaneous}

För alla implementeringar kan följande punkter beaktas:

* Eftersom det finns många olika produkter kan man försöka använda så få noder som möjligt för att modellera innehållet.

  Ju fler noder du har, desto mer flexibelt blir innehållet (till exempel parsys). Allt är dock en kompromiss och behöver du individuell flexibilitet (som standard) när du manipulerar (till exempel) 30K-produkter?

* Undvik dubbletter så mycket du kan (se lokalisering), eller när du gör det, och tänk på hur många noder dupliceringen leder till.
* Försök tagga innehållet så mycket du kan för att förbereda frågeoptimeringen.

  Till exempel:

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  ska ha en tagg per innehållsnivå (d.v.s. land, språk, kategori, varumärke, produkt). Söker efter

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  och

  `@category='shoe' and @brand='reebok' and @product='pump']`

  kommer att bli mycket snabbare än att söka efter

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* Planera en modell och tjänster för avancerad innehållsåtkomst i er tekniska hög. Detta är en allmän bästa praxis, men det är ännu viktigare här, eftersom du kan lägga till programcacher i optimeringsfaser för data som läses ofta (och som du inte vill fylla paketcachen med).

  Attributhantering är till exempel ofta en bra kandidat för cachelagring eftersom den gäller data som uppdateras via produktimport.
* Använd [proxysidor](#proxy-pages).

### Avsnittssidor för katalog {#catalog-section-pages}

I katalogavsnitten finns exempel:

* en introduktion (bild och/eller text) till kategorin; den kan också användas för banners och teasers för att marknadsföra specialerbjudanden
* länkar till de enskilda produkterna i kategorin
* länkar till andra kategorier

![ecommerce_categoryUnning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Produktsidor {#product-pages}

På produktsidorna finns omfattande information om enskilda produkter. Dynamiska uppdateringar från återspeglas också, till exempel prisändringar som registreras i eCommerce-motorn.

Produktsidor är AEM sidor som använder komponenten **Produkt**, till exempel i mallen **Commerce-produkt** :

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

Produkskomponenten innehåller:

* Allmän produktinformation, inklusive text och bilder.
* Priser - detta hämtas från e-handelsmotorn varje gång sidan visas/uppdateras.
* Produktvariantinformation, till exempel färg och storlek.

Med den här informationen kan kunden välja följande när en artikel läggs till i varukorgen:

* Färg- och storleksvarianter
* Kvantitet

#### Produktlandningssidor {#product-landing-pages}

Det här är AEM sidor som i första hand innehåller statisk information, till exempel en introduktion och en översikt med länkar till de underliggande produktsidorna.

### Produktkomponent {#product-component}

Komponenten **Produkt** kan läggas till på alla sidor med en överordnad sida som levererar de metadata som krävs (d.v.s. sökvägarna till `cartPage` och `cartObject`). På demonstrationswebbplatsen Geometrixx Outdoors tillhandahålls detta av `UserInfo.jsp`.

Komponenten **Produkt** kan också anpassas efter dina individuella krav.

### Proxysidor {#proxy-pages}

Proxysidor används för att förenkla databasens struktur och optimera lagring för stora kataloger.

När du skapar en katalog används tio noder per produkt, eftersom den innehåller enskilda komponenter för varje produkt som du kan uppdatera och anpassa i AEM. Detta stora antal noder kan bli ett problem om katalogen innehåller hundratals eller till och med tusentals produkter. Du kan undvika problem genom att skapa katalogen med hjälp av proxysidor.

Proxysidor använder en tvånodsstruktur ( `cq:Page` och `jcr:content`) som inte innehåller något av det faktiska produktinnehållet. Innehållet genereras på begäran genom att produktdata och mallsidan refereras.

Men det finns en kompromiss. Du kommer inte att kunna anpassa produktinformationen i AEM, utan en standardmall (som definierats för din webbplats) används.

>[!NOTE]
>
>Du kommer inte att få några problem om du importerar en stor katalog utan proxysidor.
>
>Du kan när som helst konvertera från en metod till en annan. Du kan också konvertera ett underavsnitt i katalogen.

## Kampanjer och kuponger {#promotions-and-vouchers}

### Vouchers {#vouchers}

Kuponger är en beprövad metod för att erbjuda rabatter som antingen lockar kunderna till att göra ett köp och/eller belönar kundens lojalitet.

* Kuponger:

   * En kupongkod (som anges i kundvagnen av kunden).
   * En verifikationsetikett (visas när kunden har skrivit in den i kundvagnen).
   * En kampanjsökväg (som definierar åtgärden som vouchern tillämpar).

* Externa handelsmotorer kan också tillhandahålla vouchers.

I AEM:

* En voucher är en sidbaserad komponent som skapas/redigeras med webbplatskonsolen.
* Komponenten **Voucher** innehåller:

   * En renderare för verifikationsadministration. Detta visar eventuella verifikationer som finns i kundvagnen.
   * Redigeringsdialogrutorna (formuläret) för att administrera (lägga till/ta bort) verifikationerna.
   * De åtgärder som krävs för att lägga till/ta bort verifikationer i/från kundvagnen.

* Vouchers har inte sina egna datum- och datumtider, utan använder dem från sina överordnade kampanjer.

>[!NOTE]
>
>AEM använder termen **Voucher**, som är synonym med termen **Kupong**.

### Erbjudanden {#promotions}

Med kampanjer och vouchers kan du förverkliga scenarier som:

* Ett företag tillhandahåller anpassade priser för anställda, vilket är en handgjord lista över användare.
* Långfristiga kunder får rabatter på alla order.
* Ett försäljningspris som erbjuds under en väldefinierad tidsperiod.
* En kund får en verifikation när den föregående ordern överstiger ett visst belopp.
* En kund som köper *product-X* får rabatt på *product-Y* (två produkter).

Kampanjer hanteras inte av produktinformationsansvariga, utan av marknadschefer:

* En kampanj är en sidbaserad komponent som skapas/redigeras med webbplatskonsolen. &quot;
* Erbjudanden:

   * En prioritet
   * En sökväg till en erbjudandehanterare

* Du kan koppla kampanjer till en kampanj för att definiera datum/tid för på/av-kampanjer.
* Du kan koppla kampanjer till en upplevelse för att definiera deras segment.
* Kampanjer som inte är kopplade till en upplevelse kommer inte att utlösas fristående, men de kan fortfarande utlösas av en Voucher.
* Komponenten Promotion innehåller:

   * renderare och dialogrutor för kampanjadministration
   * underkomponenter för återgivning och redigering av konfigurationsparametrar som är specifika för kampanjhanterarna

I AEM är kampanjerna också integrerade i [Campaign Management](/help/sites-authoring/personalization.md):

* en [kampanj](/help/sites-authoring/personalization.md) anger på-/avaktiveringstiderna
* [upplevelser](/help/sites-authoring/personalization.md) *inom* används kampanjen för att gruppera resurser (scensidor, kampanjer osv.) enligt det målgruppssegment som de motsvarar

En kampanj kan hållas antingen som en upplevelse eller direkt i kampanjen:

* Om en kampanj används i en upplevelse kan den automatiskt tillämpas på ett målgruppssegment.

  I exempelvis den externa geometrixx-exempelwebbplatsen är kampanjen:

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  har en upplevelse och aktiveras automatiskt när segmentet ( `ordervalueover100`) tolkas.

* Om en kampanj inte visas i en upplevelse (endast i kampanjen) kan den inte tillämpas automatiskt på en målgrupp. Den kan dock fortfarande utlösas om kunden anger en voucher i kundvagnen och vouchern refererar till kampanjen.

  Kampanjen:

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  ligger utanför en upplevelse och aktiveras därför aldrig automatiskt (d.v.s. baserat på segmentering). Den refereras emellertid till av vouchers som finns i flera av upplevelserna i artikelkampanjen. Om du anger dessa verifikationskoder i kundvagnen aktiveras erbjudandet.

>[!NOTE]
>
>[hybris-kampanjer](https://www.hybris.com/modules/promotion) och [hybris-vouchers](https://www.hybris.com/en/modules/voucher) täcker allt som påverkar kundvagnen och är kopplat till priset. Marknadsföringsspecifikt innehåll (t.ex. banners). ingår inte i hybris-kampanjen.

## Personalization {#personalization}

### Kundregistrering och konton {#customer-registration-and-accounts}

När en kund registrerar sig måste kontoinformationen synkroniseras mellan AEM och e-handelsmotorn. Känsliga data lagras oberoende av varandra, men profiler delas:

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

Den exakta mekanismen kan bero på scenariot:

1. Användarkonton finns i båda systemen:

   1. Ingen åtgärd krävs.

1. Användarkontot finns bara i AEM:

   1. Användaren skapas i e-handelsmotorn med samma konto-ID och ett slumpmässigt lösenord som lagras i AEM.
   1. Det slumpmässiga lösenordet är nödvändigt eftersom AEM försöker logga in på e-handelsmotorn vid den första samtalet (t.ex. när en produktsida begärs och e-handelsmotorn refereras till priset). Eftersom det här inträffar efter AEM inloggning är lösenordet inte tillgängligt.

1. Användarkontot finns bara i e-handelsmotorn:

   1. Kontot skapas i AEM med samma konto-ID och lösenord.

När du använder en e-handelsmotor lagrar AEM bara konto-ID och lösenord (eventuellt en användargrupp). All annan information lagras i e-handelsmotorn.

>[!NOTE]
>
>När du använder en e-handelsmotor måste du se till att konton som skapas för användare som loggar in i en AEM replikeras (t.ex. genom arbetsflöden) till andra AEM som kommunicerar med den motorn.
>
>I annat fall kommer dessa andra AEM att försöka skapa konton för samma användare i motorn. De här åtgärderna misslyckas med en `DuplicateUidException` som kommer från motorn.

### Kundregistrering {#customer-sign-up}

Det krävs ofta att kunden måste registrera sig för att få tillgång till kundvagnen. Detta kräver registrering (Skapa konto) så att ett kundspecifikt konto kan skapas.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>En anonym kundvagn och utcheckning stöds också.

### Kundinloggning {#customer-sign-in}

Efter registreringen kan kunden logga in med sitt konto så att deras handlingar kan spåras och deras order uppfylls.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Enkel inloggning {#single-sign-on}

enkel inloggning (SSO) tillhandahålls så att författare är kända både i AEM och e-handelssystemet utan att behöva logga in två gånger.

### myAccount {#myaccount}

Transaktionsdata från e-handelsmotorn kombineras med personuppgifter om kunden. AEM använder en del av dessa data som profildata. Ett formulärs åtgärd i AEM skriver tillbaka information till e-handelsmotorn.

Det finns en sida där du enkelt kan hantera din kontoinformation. Du kommer åt den genom att klicka på **Mitt konto** överst på en Geometrixx eller genom att gå till `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Adressbok {#address-book}

Webbplatsen måste lagra ett urval adresser, inklusive leverans, fakturering och alternativa adresser. Detta kan implementeras med formulär som baseras på ditt standardadressformat eller så kan du använda adressbokskomponenten som AEM tillhandahåller.

Med den här adressbokskomponenten kan du:

* redigera adresser i boken
* välj en adress från boken för leveransadressen
* välj en adress från boken för faktureringsadressen

Du kan välja vilken adress du vill använda som standard.

Adressbokskomponenten kan nås från sidan **Mitt konto** genom att klicka på **Adressbok** eller genom att navigera till `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

Du kan klicka på **Lägg till ny adress..** om du vill lägga till en adress i adressboken. Det öppnar ett formulär som du kan fylla i och sedan klicka på **Lägg till adress**.

>[!NOTE]
>
>Du kan ange flera adresser i adressboken.

Adressboken används när du&quot;checkar ut&quot; kundvagnen:

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Adresserna sparas under `user_home/profile/addresses`.
För Alison Parker skulle det till exempel vara under /home/users/geometrixx/aparker@geometrixx.info/profile/address

Du kan välja vilken adress du vill använda som standard. Informationen sparas i kundprofilen i stället för med adressen. Profilegenskapen `address.default` anges med sökvägen för den valda adressen för värdet.

### Kundspecifikt pris {#customer-specific-pricing}

E-handelsmotorn använder kontexten (i huvudsak kundinformationen) för att avgöra vilket pris den har, och skickar sedan rätt information tillbaka till AEM.

## Kundvagn och beställningar {#shopping-cart-and-orders}

När du handlar bläddrar du bland produktsidorna och väljer artiklar som du vill placera i kundvagnen. När de går vidare till kassan kan de lägga en order.

### Anonyma köpare {#anonymous-shoppers}

En anonym kund kan

* Visa produkter
* Lägg produkter i kundvagnen
* Utför utcheckning för att placera beställningen

>[!NOTE]
>
>Beroende på konfigurationen av din instansadressinformation, eller kundregistrering, kan behövas före utcheckning.

### Registrerade köpare {#registered-shoppers}

En registrerad kund kan

* Logga in på deras konto
* Visa produkter
* Lägg produkter i kundvagnen
* Utför utcheckning för att placera beställningen
* Visa och spåra tidigare order

### Översikt över kundvagnsinnehåll {#shopping-cart-content-overview}

Kundvagnen innehåller följande:

* en översikt över markerade objekt
* länkar till produktsidorna för de valda objekten
* möjlighet att

   * uppdatera antalet/kvantiteten för de enskilda artiklarna
   * ta bort enskilda objekt

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

Kundvagnen sparas enligt den motor som används:

* AEM lagrar vagnen i en cookie.
* Vissa e-handelsmotorer kan lagra vagnen i en session.

I båda fallen behålls objekten i vagnen (och kan återställas) mellan inloggning/utloggning (men endast på samma dator/webbläsare). Till exempel:

* bläddra som `anonymous` och lägg till produkter i kundvagnen
* logga in som `Allison Parker` - Allison&#39;s cart är tom
* lägg till produkter i Allisons kundvagn
* logga ut - i kundvagnen visas produkterna för `anonymous`

* logga in igen som `Allison Parker` - Allison&#39;s products are restored

>[!NOTE]
>
>En anonym vagn kan bara återställas på samma dator/webbläsare.

>[!NOTE]
>
>Vi rekommenderar inte att du testar att kundvagnens innehåll återställs med kontot `admin` eftersom detta kan skapa en konflikt med eCommerce-motorns `admin`-konto (till exempel hybris).

>[!NOTE]
>
>hybris kan konfigureras för att ta bort väntande varukorgar efter en angiven tidsperiod.

Innan du går till kassan återspeglas prisförändringarna (i båda systemen) när de inträffar.

### Beställningsinformation {#order-information}

Beroende på din implementeringsinformation om en beställning finns antingen i eCommerce-motorn eller AEM återges den här informationen av AEM.

Olika typer av information lagras, t.ex.:

* **Beställnings-ID**

  Orderns referensnummer.

* **Placerad**

  Datumet då ordern lades.

* **Status**

  Orderns status, t.ex. Skickad.

* **Valuta**

  Orderns valuta.

* **Innehållsobjekt**

  En lista med artiklar ordnade.

* **Delsumma**

  Den totala kostnaden för beställda artiklar.

* **Skatt**

  Beloppet för eventuella skatter som ska betalas på ordern.

* **Leverans**

  Fraktkostnader.

* **Totalt**

  Orderns totala värde: beställda artiklar, skatter och frakt.

* **Faktureringsadress**

  Den adress som fakturan ska skickas till.

* **Betalningstoken**

  Betalningsmetoden.

* **Betalningsstatus**

  Status för betalningen.

* **Leveransadress**

  Den adress dit varorna ska skickas.

* **Leveranssätt**

  Leveranssätt, till exempel land, hav eller luft.

* **Spårningsnummer**

  Spårningsnummer som används av rederiet.

* **Spårningslänk**

  Länken som används för att spåra ordern medan den skickas.

>[!NOTE]
>
>Fälten som används i guiden Skapa order är beroende av att det finns en beröringsoptimerad ställningar för platsen. I det generiska exemplet finns det här:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

När beställningen hålls i AEM visar orderkonsolen följande för varje beställning:

* antalet artiklar i kundvagnen
* orderns totala värde
* när ordern lades
* status

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### Orderspårning {#order-tracking}

Efter att ha lagt en order kommer kunderna ofta tillbaka till:

* Kontrollera orderstatus
* Ta bort produkter från beställningen
* Lägg till produkter i ordern

Efter att ha tagit emot beställningsleveransen kanske kunderna också vill se historiken över beställningar som gjorts under en tidsperiod.

Beställningsleveranser och -spårning hanteras av e-handelsmotorn. Information kan visas genom AEM med komponenten Orderhistorik, som visar all relevant information, inklusive kuponger och erbjudanden som används. Till exempel:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Utcheckning {#checkout}

Utcheckning implementeras med AEM. På så sätt kan marknadschefen anpassa upplevelsen av marknadsföringsmaterialet.

E-handeln hanterar sedan utcheckningsprocessen med indata från AEM.

### Betalningssäkerhet {#payment-security}

Betalningsinformation, inklusive kreditkortsinformation, hanteras ofta av e-handelsmotorn. AEM vidarebefordrar sådan transaktionsinformation till motorn (varifrån den sedan vidarebefordras till en betalningstjänst).

Kompatibilitet med betalkortsbranschen (PCI) kan uppnås.

### Bekräftelse av beställning {#confirmation-of-order}

Ordningen bekräftas på skärmen och kan spåras med [orderspårning](#order-tracking).

## Sök {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

Eftersom AEM använder standardsidor för produkter kan du använda standardsökkomponenten för att skapa en söksida.

Om du behöver en mer detaljerad implementering kan du antingen:

* Utöka standardsökkomponenten med de funktioner du behöver.
* Implementera sökmetoden i `CommerceService` och använd sedan sökkomponenten för eCommerce på söksidan.

När du använder en eCommerce-motor kan e-handelssöknings-API:t implementeras helt i eCommerce-motorlösningen, så att du kan använda eCommerce-sökkomponenten som medföljer. Med den fasetterade sökningen kan du söka i antingen JCR och/eller motorn:
