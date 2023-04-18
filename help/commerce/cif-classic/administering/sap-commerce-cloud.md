---
title: Använd AEM med SAP Commerce Cloud
description: Lär dig använda AEM med SAP Commerce Cloud.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 1%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

Efter installationen kan du konfigurera instansen:

1. [Konfigurera den motsatta sökningen efter Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Konfigurera katalogversionen](#configure-the-catalog-version).
1. [Konfigurera importstrukturen](#configure-the-import-structure).
1. [Konfigurera de produktattribut som ska läsas in](#configure-the-product-attributes-to-load).
1. [Importera produktdata](#importing-the-product-data).
1. [Konfigurera katalogimporteraren](#configure-the-catalog-importer).
1. Använd [importör för att importera katalogen](#catalog-import) till en specifik plats i AEM.

## Konfigurera den motsatta sökningen efter Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Detta behövs inte för hybris 5.3.0.1 och senare.

1. I webbläsaren går du till **Hanteringskonsol för hybris** vid:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Välj **System** sedan **Fasettsökning** sedan **Konfiguration för sökning efter ansikten**.
1. **Öppna redigeraren** för **Exempel på Solr-konfiguration för katalog**.

1. Under **Katalogversioner** use **Lägg till katalogversion** lägga till `outdoors-Staged` och `outdoors-Online` till listan.
1. **Spara konfigurationen.**
1. Öppna **SOLR-objekttyper** lägga till **SOLR Sorts** till `ClothesVariantProduct`:

   * relevans (&quot;Relevans&quot;, poäng)
   * name-asc (&quot;Name (stigande)&quot;, name)
   * name-desc (&quot;Name (fallande)&quot;, name)
   * price-asc (&quot;Price (stigande)&quot;, priceValue)
   * price-desc (&quot;Price (fallending)&quot;, priceValue)

   >[!NOTE]
   >
   >Använd snabbmenyn (oftast högerklickning) för att markera `Create Solr sort`.
   >
   >För Hybris 5.0.0 öppnar du `Indexed Types` flik, dubbelklicka på `ClothesVariantProduct`och sedan fliken `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. I **Indexerade typer** tabbuppsättningen **Sammansatt typ** till:

   `Product - Product`

1. I **Indexerade typer** tabbjustera **Indexerfrågor** for `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. I **Indexerade typer** tabbjustera **Indexerfrågor** for `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. I **Indexerade typer** tabbjustera `category` facet. Dubbelklicka på den sista posten i kategorilistan för att öppna **Indexerad egenskap** tab:

   >[!NOTE]
   >
   >För hybris 5.2 ska du se till att `Facet` i egenskapstabellen väljs enligt skärmbilden nedan:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Öppna **Fasettinställningar** och justera fältvärdena:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Spara ändringarna.**
1. Igen från **SOLR-objekttyper**, justera `price` ansiktet enligt följande skärmbilder. Som med `category`, dubbelklicka på `price` för att öppna **Indexerad egenskap** tab:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Öppna **Fasettinställningar** och justera fältvärdena:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Spara ändringarna.**
1. Öppna **System**, **Fasettsökning** sedan **Åtgärdsguiden för indexering**. Starta ett cronjob:

   * **Indexeringsåtgärd**: `full`
   * **Solr-konfiguration**: `Sample Solr Config for Clothes`

## Konfigurera katalogversionen {#configure-the-catalog-version}

The **Katalogversion** ( `hybris.catalog.version`) som importeras kan konfigureras för OSGi-tjänsten:

**Dag CQ Commerce Hybris Configuration**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Katalogversion** är vanligtvis inställd på antingen `Online` eller `Staged` (standard).

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för fullständig information. Se även konsolen för en fullständig lista över konfigurerbara parametrar och deras standardvärden.

Loggutdata ger återkoppling om skapade sidor och komponenter och rapporterar potentiella fel.

## Konfigurera importstrukturen {#configure-the-import-structure}

I följande lista visas en exempelstruktur (med resurser, sidor och komponenter) som skapas som standard:

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

En sådan struktur skapas av OSGi-tjänsten `DefaultImportHandler` som implementerar `ImportHandler` gränssnitt. Den faktiska importören anropar en importhanterare för att skapa produkter, produktvariationer, kategorier, tillgångar osv.

>[!NOTE]
>
>Du kan [anpassa den här processen genom att implementera en egen importhanterare](#configure-the-import-structure).

Strukturen som ska skapas vid import kan konfigureras för:

&quot;**Standardimporthanterare för handelshybris för dagskvot**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för fullständig information. Se även konsolen för en fullständig lista över konfigurerbara parametrar och deras standardvärden.

## Konfigurera de produktattribut som ska läsas in {#configure-the-product-attributes-to-load}

Svarsparsern kan konfigureras för att definiera egenskaper och attribut som ska läsas in för (variant) produkter:

1. Konfigurera OSGi-paketet:

   **Standardsvarsparser för handelshybris i CQ**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Här kan du definiera olika alternativ och attribut som behövs för inläsning och mappning.

   >[!NOTE]
   >
   >När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för fullständig information. Se även konsolen för en fullständig lista över konfigurerbara parametrar och deras standardvärden.

## Importera produktdata {#importing-the-product-data}

Det finns flera olika sätt att importera produktdata. Produktdata kan importeras när miljön först konfigureras eller efter att hybris-data har ändrats:

* [Fullständig import](#full-import)
* [Inkrementell import](#incremental-import)
* [Express Update](#express-update)

Faktisk produktinformation som importerats från hybris lagras i databasen enligt följande:

`/etc/commerce/products`

Följande egenskaper anger länken till hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris-implementeringen (dvs. `geometrixx-outdoors/en_US`) lagrar endast produkt-ID:n och annan grundläggande information under `/etc/commerce`.
>
>Det hänvisas till hybris-servern varje gång information om en produkt begärs.

### Fullständig import {#full-import}

1. Om det behövs tar du bort alla befintliga produktdata med CRXDE Lite.

   1. Navigera till det underträd som innehåller produktdata:

      `/etc/commerce/products`

      Till exempel:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Ta bort noden som innehåller produktdata, till exempel `outdoors`.
   1. **Spara alla** för att behålla ändringen.

1. Öppna hybris-importören i AEM:

   `/etc/importers/hybris.html`

   Till exempel:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Konfigurera de parametrar som krävs, till exempel:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Klicka **Importera katalog** för att starta importen.

   När du är klar kan du verifiera de data som importerats på:

   ```
       /etc/commerce/products/outdoors
   ```

   Du kan öppna den här i CRXDE Lite; till exempel:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Inkrementell import {#incremental-import}

1. Kontrollera uppgifterna i AEM för den eller de berörda produkterna i respektive underträd under

   `/etc/commerce/products`

   Du kan öppna den här i CRXDE Lite; till exempel:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. I hybris ska informationen om relevanta produkter uppdateras.

1. Öppna hybris-importören i AEM:

   `/etc/importers/hybris.html`

   Till exempel:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Markera kryssrutan **Inkrementell import**.
1. Klicka **Importera katalog** för att starta importen.

   När det är klart kan du verifiera de data som har uppdaterats i AEM under:

   ```
       /etc/commerce/products
   ```


### Express Update {#express-update}

Importprocessen kan ta lång tid, så som ett tillägg till produktsynkroniseringen kan du välja specifika områden i katalogen för en snabb uppdatering som aktiveras manuellt. Detta använder exportflödet tillsammans med standardattributskonfigurationen.

1. Kontrollera uppgifterna i AEM för den eller de berörda produkterna i respektive underträd under

   `/etc/commerce/products`

   Du kan öppna den här i CRXDE Lite; till exempel:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. I hybris ska informationen om relevanta produkter uppdateras.

1. I hybris lägger du till produkten/produkterna i Express-kön. till exempel:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Öppna hybris-importören i AEM:

   `/etc/importers/hybris.html`

   Till exempel:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Markera kryssrutan **Express Update**.
1. Klicka **Importera katalog** för att starta importen.

   När det är klart kan du verifiera de data som har uppdaterats i AEM under:

   ```
       /etc/commerce/products
   ```

## Konfigurera katalogimporteraren {#configure-the-catalog-importer}

hybriskatalogen kan importeras till AEM med hjälp av satsimportör för hybris-kataloger, kategorier och produkter.

De parametrar som används av importeraren kan konfigureras för:

**Dag CQ Commerce Hybris Catalog Import**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för fullständig information. Se även konsolen för en fullständig lista över konfigurerbara parametrar och deras standardvärden.

## Katalogimport {#catalog-import}

hybris-paketet levereras med en katalogimportör för att skapa den inledande sidstrukturen.

Det här är tillgängligt från:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Följande uppgifter måste lämnas:

* **Bas**
Identifieraren för basbutiken som konfigurerats i hybris.

* **Katalog**
Identifieraren för den katalog som ska importeras.

* **Rotsökväg**
Sökvägen dit katalogen ska importeras.

## Ta bort en produkt från katalogen {#removing-a-product-from-the-catalog}

Så här tar du bort en eller flera produkter från katalogen:

1. [Konfigurera tjänsten för OSGi](/help/sites-deploying/configuring-osgi.md) **Dag CQ Commerce Hybris Catalog Import**; se även [Konfigurera katalogimporteraren](#configure-the-catalog-importer).

   Aktivera följande egenskaper:

   * **Aktivera produktborttagning**
   * **Aktivera borttagning av produktresurser**

   >[!NOTE]
   >
   >När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) för fullständig information. Se även konsolen för en fullständig lista över konfigurerbara parametrar och deras standardvärden.

1. Initiera importören genom att utföra två stegvisa uppdateringar (se [Katalogimport](#catalog-import)):

   * Första körningen resulterar i en uppsättning ändrade produkter som anges i logglistan.
   * För andra gången ska inga produkter uppdateras.

   >[!NOTE]
   >
   >Den första importen är att initiera produktinformationen. Den andra importen verifierar att allt fungerade och att dess produktuppsättning är klar.

1. Kontrollera kategorisidan som innehåller den produkt du vill ta bort. Produktinformationen ska vara synlig.

   I följande kategori visas information om Cajamara-produkten:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Ta bort produkten i hybris-konsolen. Använd alternativet **Ändra godkännandestatus** för att ställa in status på `unapproved`. Produkten tas bort från liveflödet.

   Till exempel:

   * Öppna sidan [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Markera katalogen `Outdoors Staged`
   * Sök efter `Cajamara`
   * Välj den här produkten och ändra godkännandestatusen till `unapproved`

1. Utför en annan stegvis uppdatering (se [Katalogimport](#catalog-import)). Loggen visar den borttagna produkten.
1. [Utrullning](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) lämplig katalog. Produkt- och produktsidan har tagits bort från AEM.

   Till exempel:

   * Öppna:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Gör `Hybris Base` katalog
   * Öppna:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * The `Cajamara` produkten kommer att ha tagits bort från `Bike` kategori

1. Så här återinstallerar du produkten:

   1. I hybris ska godkännandestatusen återställas till **godkänd**
   1. I AEM:

      1. utföra en stegvis uppdatering
      1. lansera lämplig katalog igen
      1. uppdatera lämplig kategorisida

## Lägg till orderhistorikspår i klientkontexten {#add-order-history-trait-to-the-client-context}

Lägga till orderhistorik i [klientkontext](/help/sites-developing/client-context.md):

1. Öppna [designsida för klientkontext](/help/sites-administering/client-context.md), antingen

   * Öppna en sida för redigering och öppna sedan klientkontexten med **Ctrl-Alt-c** (fönster) eller **control-option-c** (Mac). Använd pennikonen i klientkontextens övre vänstra hörn för att **Öppna designsidan för ClientContext**.
   * Navigera direkt till [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Lägg till **Orderhistorik** komponent](/help/sites-administering/client-context.md#adding-a-property-component) till **Kundvagn** t-komponenten i klientkontexten.
1. Du kan bekräfta att klientkontexten visar information om din orderhistorik. Till exempel:

   1. Öppna [klientkontext](/help/sites-administering/client-context.md).
   1. Lägg en artikel i kundvagnen.
   1. Slutför utcheckningen.
   1. Kontrollera klientkontexten.
   1. Lägg till ytterligare en artikel i kundvagnen.
   1. Navigera till utcheckningssidan:

      * Klientkontexten visar en sammanfattning av orderhistoriken.
      * Meddelandet&quot;Du är en återkommande kund&quot; visas.

   >[!NOTE]
   >
   >Meddelandet realiseras av:
   >
   >* Navigera till [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  Kampanjen består av en upplevelse.
   >
   >* Klicka på segmentet ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* Segmentet byggs med **Egenskap för orderhistorik** egenskap.

